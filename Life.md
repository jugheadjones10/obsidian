
- [ ] "Beasts of a Little Land" reading
- [ ] Math for Machine Learning
- [ ] Exercise
- [ ] Obsidian review

# 2025-12-18
- [x] Obsidian review

- [x] Exercise

- [x] Walk in the park
- [x] Write Eujin appeal letter

# 2025-12-19
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Generate target schedule for m4ml

- [x] Continue notes for PLR
- [x] Start reading PLR code in JaxUED

- [x] Exercise
- [x] Obsidian review

## ideas
- Obsidian plugin that, when prompted, fills in the "answer" part of my flashcard (to be used together with the Spaced Repetition plugin). This is to speed up flashcard-making for cards where writing the answer on my own doesn't necessarily help in my learning.

# 2025-12-20
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning

- [ ] Continue notes for PLR
- [ ] Continue reading PLR code in JaxUED
- [ ] Start writing "The Intelligence Manifesto"
- [ ] Clear tabs

- [x] Obsidian review

- [ ] Trex test answer key cropping using Gemini 3 Flash


# 2025-12-21
- [ ] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [ ] Continue notes for PLR
- [x] Continue reading PLR code in JaxUED
- [x] Exercise
- [ ] Obsidian review
- [ ] Trex test answer key cropping using Gemini 3 Flash

# 2025-12-22
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning

- [ ] Start "RL for dummies"
- [ ] Start "RL perf for dummies"
- [ ] Start "The Intelligence Manifesto"

- [x] Continue implementing in-training video and perf logging like in Kinetix
- [x] Exercise
- [x] Obsidian review

- [ ] Trex test answer key cropping using Gemini 3 Flash

# 2025-12-23
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Obsidian review
- [ ] Write about experience yesterday getting distracted while doing hard Jax stuff. The need to interleave fun stuff with not-so-fun stuff.
- [ ] Expand on the idea on neuro-evolution and RL life simulator you had while waiting in line at OCBC.

- [x] Continue implementing in-training video and perf logging like in Kinetix

- [ ] Exercise

## ideas
- Extend Karpathy's "reading books with LLMs" project and actually productise it: https://github.com/karpathy/reader3.
- For your Telegram tracker, maybe add a daily "digest" to help you clear everything bit by bit.

## project neumann
What if I feed an LLM every single flashcard I made for a chapter and the original chapter text, and then ask it to think hard to generate hard variants of my flashcards that really drill into my conceptual understanding of the topics? Make it go section by section of the chapter. That might be a good way to add good cards for a chatper.

# 2025-12-24
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [ ] Exercise
- [x] Obsidian review

- [ ] Continue using the debugger to understand JaxUED

- [ ] Move Notion todos to here
- [ ] Message Titin about new arrangement
- [ ] Write about experience yesterday getting distracted while doing hard Jax stuff. The need to interleave fun stuff with not-so-fun stuff.
- [ ] Expand on the idea on neuro-evolution and RL life simulator you had while waiting in line at OCBC.

## PushWorld ideas
- Thinking back to the "Interpreting Emergent Planning in Model-Free Reinforcement Learning" paper, can we say that emergent planning also implies that world models also emerged? Maybe the "General agents need world models" paper can help make the connection?

## PushWorld engineering
I was trying to understand a particularly gnarly network in JaxUED. I was confused about the shapes, I didn't know what the intermediate values looked like, etc. I asked Claude in Cursor to "create a notebook that initialises some fake values that are in the same shape as what the network will receive as actual input during real execution, and then walk me through the network line by line, allowing me to execute each important part one at a time so that i can look at the outputs and inspect the shapes, etc.?"

This worked really really well. This got me thinking, maybe I should do mini Jax projects whose outputs are similar notebooks interspersed with commentary and explanations, to publish on my blog. Maybe I should use this approach for my upcoming "RL for Dummies" series.

I mean just look at this magnificent output in one of the cells:
```python
# STEP 1: Convolution on image
# Original code:
#   img_embed = nn.Conv(16, kernel_size=(3, 3), strides=(1, 1), padding="VALID")(obs.image)

print("STEP 1: Convolution")
print("=" * 50)
print(f"Input: obs.image shape = {fake_obs.image.shape}")
print()

# Create and initialize the Conv layer
conv_layer = nn.Conv(16, kernel_size=(3, 3), strides=(1, 1), padding="VALID")
rng, key = jax.random.split(rng)
conv_params = conv_layer.init(key, fake_obs.image)

# Apply convolution
img_embed = conv_layer.apply(conv_params, fake_obs.image)

print(f"Output: img_embed shape = {img_embed.shape}")
print()
print("Explanation:")
print(f"  • 3x3 kernel with VALID padding reduces spatial dims by 2")
print(f"  • H: {IMAGE_H} → {IMAGE_H - 2},  W: {IMAGE_W} → {IMAGE_W - 2}")
print(f"  • Output channels: 16")
```

We can even use this approach to create "notes" for codebases that we read, such as
- https://jax-js.com/
- https://tinygrad.org/
- https://github.com/adam-maj/tiny-gpu

# 2025-12-25
- [ ] Trex test answer key cropping using Gemini 3 Flash

# 2025-12-26


# money
Tweets and ideas for earning money:

- [ ] Migrate writings from old Obsidian vault and maybe expand on them, especially the intelligence writings.
- [ ] Start "RL for dummies"
- [ ] Start "RL perf for dummies"
- [ ] Start "The Intelligence Manifesto"