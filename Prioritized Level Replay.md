---
type: paper
---
#flashcards/papers/prioritized-level-replay

What is the title of Jiang, 2021?::"Prioritized Level Replay"
<!--SR:!2026-01-02,14,290-->

Which citation has the title "Prioritized Level Replay"?::Jiang, 2021
<!--SR:!2026-01-05,17,299-->

# 2 Background
What is a PCG environment?::It is an environment where, given a level identifier such as an index or a random seed, a *level* is generated, where the level is an environment instance exhibiting a unique configuration of its underlying factors of variation, such as layout, asset appearances, or specific environment dynamics.
<!--SR:!2025-12-31,11,270-->

# 3 Prioritized Level Replay
What are the two metrics that PLR tracks for each visited level?::First, the level score $S_i$ for the visited training level $l_i$ where $S_i$ is based on the latest episode trajectory on $l_i$. Second, the episode count $C_i$ at which the level $l_i$ was last sampled.
<!--SR:!2026-01-05,17,299-->

In PLR, when is the replay distribution $P_{\text{replay}}$ updated?::After each terminated episode.
<!--SR:!2026-01-03,15,290-->

In PLR, what formula is used to update the replay distribution $P_{\text{replay}}$ (in terms of $P_S$ and $P_C$)?
?
The replay distribution is computed by taking the mixture of two distributions, $P_S$, based on the level scores, and $P_C$ , based on how long ago each level was last sampled:
$$
P_{\text{replay}} = (1 - \rho)\, P_S + \rho\, P_C
$$
where the staleness coefficient $\rho \in [0, 1]$ is a hyperparameter.
<!--SR:!2026-01-03,14,296-->

How does PLR decide which level to train on at the start of every training episode?::PLR decides between sampling a level from the replay distribution $P_{\text{replay}}$ and sampling a new, unseen level from $\Lambda_{\text{train}}$ according to some distribution $P_{\text{new}}(l \mid \Lambda_{\text{train}} \setminus \Lambda_{\text{seen}})$. This decision is made by sampling a replay-decision from a Bernoulli distribution $P_D(d)$.
<!--SR:!2026-01-04,16,299-->

In practice, how is the new-level distribution $P_{\text{new}}$​ implemented when the training set is finite?::As a uniform distribution over the remaining unseen levels.
<!--SR:!2026-01-04,16,299-->

How is the new-level distribution $P_{\text{new}}$​ implemented if the training set is countably infinite?::We simulate $P_{\text{new}}$ by sampling levels from $P_{\text{train}}$  until encountering an unseen level.
<!--SR:!2026-01-04,15,290-->

In the finite training-level setting, what is a suitable way to schedule how the replay probability $P_D(d = 1)$ changes over time?::We can naturally anneal it as $|\Lambda_{\text{seen}}| / |\Lambda_{\text{train}}|$.
<!--SR:!2026-01-02,14,296-->

Why does it make sense to anneal the replay probability $P_D(d = 1)$ as $|\Lambda_{\text{seen}}| / |\Lambda_{\text{train}}|$?::As training proceeds, the proportion of seen levels increases, causing the fraction $|\Lambda_{\text{seen}}| / |\Lambda_{\text{train}}|$ to increase. The replay probability will therefore increase as training proceeds, which makes sense because the higher the fraction of training levels we have seen, the more we want to replay them.
<!--SR:!2026-01-05,16,296-->

Add the diagram thing!

## 3.1 Scoring Levels for Learning Potential
What is the formula for the TD-error at timestep $t$, $\delta_t$?::$\delta_t = r_t + \gamma V(s_{t+1}) - V(s_t)$.
<!--SR:!2026-01-02,14,290-->

Why is $\delta_t$ a useful measure of the learning potential of a particular state transition?::Because a larger $\delta_t$ indicates a greater mismatch between $V(s_t)$ and the one-step TD target $r_t + \gamma V(s_{t+1})$, signaling higher learning potential.
<!--SR:!2025-12-26,8,256-->

How do we use $\delta_t$, which is for single state transitions, to calculate a proxy for the learning potential of a whole episode trajectory?::We calculate the average magnitude of the GAE over each of the T time steps in the latest episode trajectory $\tau$ from that level: $\frac{1}{T}\sum_{t=0}^{T}\left|\sum_{k=t}^{T}(\gamma\lambda)^{k-t}\,\delta_k\right|$.
<!--SR:!2025-12-31,7,250-->

In PLR, what is the formula for the level score $S_i$ of level $i$ that gives a measure of the learning potential of replaying that level in the future?:$S_i = \mathrm{score}(\tau,\pi) = \frac{1}{T}\sum_{t=0}^{T}\left|\sum_{k=t}^{T}(\gamma\lambda)^{k-t}\delta_k\right|.$

In PLR, what is the formula for calculating the score-prioritized distribution $P_S(\Lambda_{\text{train}})$ over the training levels?::$P_S\!\left(l_i \mid \Lambda_{\text{seen}}, S\right) = \frac{h(S_i)^{1/\beta}}{\sum_j h(S_j)^{1/\beta}}$, where the function $h$ defines how differences in level scores translate to differences in level prioritization, and the the temperature parameter $\beta$ tunes how much $h(S)$ ultimately determines the resulting distribution.
<!--SR:!2026-01-09,16,307-->

In the formula for score-prioritized distribution over the training levels $P_S(\Lambda_{\text{train}})$, what role does the temperature term $\beta$ play? Why is it able to play that role?::In $P_S\!\left(l_i \mid \Lambda_{\text{seen}}, S\right) = \frac{h(S_i)^{1/\beta}}{\sum_j h(S_j)^{1/\beta}}$, $\beta$ tunes how much $h(S)$ ultimately determines the resulting distribution. Imagine that four levels have $h(S)$ values \[1, 2, 4, 8\]. If $\beta$ is something like 0.5, we will get \[1, 4, 16, 64\] for our $h(S)$ values, causing much more probability mass to go to scores with higher $h(S)$. On the other hand, if $\beta$ is something like 2, the distribution will be much flatter. Try picturing the graphs for $x^2$ and $\sqrt{x}$ to get an intuition.
<!--SR:!2026-01-04,12,293-->

In the formula for score-prioritized distribution over the training levels $P_S(\Lambda_{\text{train}})$, how can we tune the temperature parameter $\beta$ to get an almost uniform distribution?::In $P_S\!\left(l_i \mid \Lambda_{\text{seen}}, S\right) = \frac{h(S_i)^{1/\beta}}{\sum_j h(S_j)^{1/\beta}}$, as $\beta$ tends to $\infty$, each $h(S)$ tends to 1, resulting in a uniform distribution.
<!--SR:!2025-12-27,4,296-->

In the formula for the score-prioritized distribution over the training levels $P_S(\Lambda_{\text{train}})$, what function did PLR decide to use for $h$? Why?::It decided to go with $h(S_i) = 1 / \operatorname{rank}(S_i)$. They chose this simply because it performed better compared to other functions such as proportional prioritization ($h(S_i) = S_i$) as well as greedy prioritization (the level with the highest score receives probability $1$).
<!--SR:!2026-01-09,17,304-->

## 3.2 Staleness-Aware Prioritization
Why do we need to mix the score-prioritized sampling distribution over training levels $P_S$ with a staleness-prioritized distribution $P_C$?::This is because the scores used to parameterise $P_S$ are a function of the state of the policy at the time the associated level was last played. Therefore, as training proceeds and the policy is improved, the scores become a more off-policy measure, and we need a way to push those levels with "stale" scores to be replayed.
<!--SR:!2026-01-07,15,304-->

In PLR, what is the formula for calculating the staleness-prioritized distribution $P_C(\Lambda_{\text{train}})$ over the training levels?::$P_C(l_i \mid \Lambda_{\text{seen}}, C, c) = \frac{c - C_i}{\sum_{C_j \in C} (c - C_j)}$, which assigns probability mass to each level $l_i$ in proportion to the level’s staleness $c - C_i$. Here, $c$ is the count of total episodes sampled so far in training and $C_i$ (referred to as the level’s timestamp) is the episode count at which $l_i$ was last sampled. By pushing support to levels with staler scores, $P_C$ ensures no score drifts too far off-policy.
<!--SR:!2026-01-09,17,307-->

In PLR, what formula is used to update the replay distribution $P_{\text{replay}}$ (where we expand the $P_S$ and $P_C$ into their more detailed conditional probability forms)?::$P_{\text{replay}}(l_i) = (1 - \rho)P_S(l_i \mid \Lambda_{\text{seen}}, S) + \rho P_C(l_i \mid \Lambda_{\text{seen}}, C, c).$
<!--SR:!2026-01-03,11,287-->





**Skipped some paragraphs in Section 3.1 because I haven't studied GAE properly yet.** Come back afterwards.

