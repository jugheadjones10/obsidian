---
generated-by: life-tag-aggregator
source: "[[Life]]"
tag: pushworld-engineering
do-not-edit: true
---

# Pushworld Engineering

## 2025-12-24 [[Life#2025-12-24#Pushworld Engineering|↩]]

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
