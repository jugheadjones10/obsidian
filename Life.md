
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


# 2025-12-21
- [ ] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [ ] Continue notes for PLR
- [x] Continue reading PLR code in JaxUED
- [x] Exercise
- [ ] Obsidian review

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

- [x] Continue using the debugger to understand JaxUED

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
- [ ] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Exercise
- [x] Obsidian review
## project neumann
- Maybe I need to memorise content pages as well? So that I can list out every topic and sub-topic learned from a textbook, and create a map of concepts in my mind that I can traverse at will.
- I want to try experimenting how well different models are at converting content into flashcards. Not for math, but for the kind of content that involves more memory than conceptual understanding, like Linux commands, or Operating System facts.

# 2025-12-26
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Exercise
- [x] Obsidian review

- [x] Continue using the debugger to understand JaxUED
- [ ] Continue reading and ankifying "Assessing Adaptive World Models in Machines with Novel Games"

- [ ] Move Notion todos to here
- [ ] Expand on the idea on neuro-evolution and RL life simulator you had while waiting in line at OCBC.

- [ ] Take care of Titin payment
- [ ] Message Titin about new arrangement
- [x] Take care of Dong Jin stuff
- [ ] Trex test answer key cropping using Gemini 3 Flash
- [ ] teebloc-trex: for some reason, in ak.py, y2 returned null, which caused the script to error out. Fix it.
	- [ ] Hmm, why not just train a YOLO model on answer key boxes, and then use Gemini 3.0 flash to label them or stitch them together?

## PushWorld engineering
- I'm at a crossroad right now. I have my existing `train_single_task_pushworld_all.py` implementation that I modified from the implementation in `xland-minigrid` to fit PushWorld's case. I have also just finished studying the plr/accel implementation in `jaxued`. Originally I thought I could just copy over some of the stuff in `jaxued` to my original code, but the structure of the code in `jaxued` is different enough that I'm wondering if it's worth it to painstaking update my original implementation. The `jaxued` version has support for a lot more things, like real-time logging and video output, ability to configure evaluation to be done every x updates, etc. It also already has support for accel, meaning if we modify the `jaxued` for the PushWorld case we get to run accel experiments for "free". Should I just use this opportunity to start a whole new PushWorld repository? And move away from `xland-minigrid`?
- What if I try passing a whole repo to an LLM and ask it to generate atomic Jax puzzles that will help me master all the small Jax concepts used? And then paste it into my Obsidian spaced repetition system.

# 2025-12-27
- [x] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Exercise
- [x] Obsidian review

## life as an experiment
- I find that on days that I cannot fall asleep easily, I turn to Youtube, which inevitably leads to like a 4am bedtime and a late wakeup the next day. Instead, read a novel or something, which can help you fall asleep more easily.
- If you need to do something you dread doing...do something more fun instead, and once you are in your flow you can do the harder thing. Like a gateway drug.

# 2025-12-28
- [ ] "Beasts of a Little Land" reading
- [x] Math for Machine Learning
- [x] Exercise
- [x] Obsidian review

- [ ] Continue porting JaxUED to PushWorld
- [ ] Continue reading and ankifying "Assessing Adaptive World Models in Machines with Novel Games"

- [ ] Finish Dong Jin Payment Slip
- [x] Take care of Titin payment
- [x] Message Titin about new arrangement
- [ ] Trex test answer key cropping using Gemini 3 Flash
- [ ] teebloc-trex: for some reason, in ak.py, y2 returned null, which caused the script to error out. Fix it.
	- [ ] Hmm, why not just train a YOLO model on answer key boxes, and then use Gemini 3.0 flash to label them or stitch them together?

# 2025-12-29
- [ ] "Beasts of a Little Land" reading
- [ ] Math for Machine Learning
- [ ] Exercise
- [ ] Obsidian review

- [ ] Finish Dong Jin Payment Slip
- [ ] Trex test answer key cropping using Gemini 3 Flash
- [ ] teebloc-trex: for some reason, in ak.py, y2 returned null, which caused the script to error out. Fix it.
	- [ ] Hmm, why not just train a YOLO model on answer key boxes, and then use Gemini 3.0 flash to label them or stitch them together?
- [ ] Run on P6

 - [ ] Continue porting JaxUED to PushWorld
- [ ] Continue reading and ankifying "Assessing Adaptive World Models in Machines with Novel Games"

- [ ] Move Notion todos to here
- [ ] Expand on the idea on neuro-evolution and RL life simulator you had while waiting in line at OCBC.

## Teebloc
### Answer key cropping
We know that there are many different types of answer keys. Here are the categories encountered so far:
- Grid view, with one column.
	- For this, what if we train a YOLO model to identify all rows, and then we use a light Gemini model to label the question number of rows as well as decide whether each row is a continuation of an existing question or now.
- Grid view, with two columns.
	- Similar approach to one column, except we might need to train a different YOLO model?
- Similar to questions, except with the answers filled in.



# money
Tweets and ideas for earning money:

- [ ] Migrate writings from old Obsidian vault and maybe expand on them, especially the intelligence writings.
- [ ] Start "RL for dummies"
- [ ] Start "RL perf for dummies"
- [ ] Start "The Intelligence Manifesto"

# 2025-12-28

## journal

