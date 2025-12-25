#flashcards/software/jax


# jnp

## jnp.where
What are the arguments to jnp.where (for the 3 arguments version), and what does it return?
?
For the 3-argument version, the signature is:
`jnp.where(condition, x, y)`
- `condition`: boolean array (broadcastable with `x` and `y`)
- `x`: arraylike, values used where `condition` is `True`
- `y`: arraylike, values used where `condition` is `False`
Returns an array with values drawn from `x` where condition is True, and from `y` where condition is False.
<!--SR:!2026-01-04,11,286--> 

# jax.random
## jax.random.choice
What are the commonly used positional arguments of `jax.random.choice`, and in what order?::The usual signature is `jax.random.choice(key, a, shape=(), replace=True, p=None, ...)`.

In  `jax.random.choice(key, a, shape=(), replace=True, p=None, ...)`, what is `shape`?:: An optional tuple of ints, which determines the output shape of the returned samples. If the given shape is, e.g., `(m, n)`, then `m * n` samples are drawn. Default is (), in which case a single value is returned.

You need to randomly sample one or more items from a set of candidates (optionally with a probability distribution, and optionally with the results in some arbitrary shape). What JAX function do you use?::`jax.random.choice(key, a, shape=() replace=True, p=None, ...)`.

# jax.lax
## jax.lax.scan
What are the commonly used positional arguments of `jax.lax.scan`, and in what order?::The usual signature is  `jax.lax.scan(f, init, xs=None, length=None, ...)`.
<!--SR:!2026-01-01,9,261-->

In `jax.lax.scan(f, init, xs=None, length=None, ...)`, what is `f`?::It is a Python function to be scanned of type `(c, a) -> (c, b)`, meaning that `f` accepts two arguments where the first is a value of the loop carry and the second is a slice of `xs` along its leading axis, and that `f` returns a pair where the first element represents a new value for the loop carry and the second represents a slice of the output.
<!--SR:!2025-12-28,4,295-->

In `jax.lax.scan(f, init, xs=None, length=None, ...)`, what is `init`?::It is an initial loop carry value which can be a scalar, array, or any pytree (nested Python tuple/list/dict) thereof. This value must have the same structure as the first element of the pair returned by `f`.
<!--SR:!2026-01-02,10,270-->

In `jax.lax.scan(f, init, xs=None, length=None, ...)`, what is `xs`?::It is the value of type `[a]` over which to scan along the leading axis, where `[a]` can be an array or any pytree (nested Python tuple/list/dict) thereof with consistent leading axis sizes.
<!--SR:!2026-01-07,15,290-->

In `jax.lax.scan(f, init, xs=None, length=None, ...)`, what is `length`?::It is an optional integer specifying the number of loop iterations, which must agree with the sizes of leading axes of the arrays in `xs` (but can be used to perform scans where no input `xs` are needed).
<!--SR:!2026-01-06,13,288-->

Should we combine scan with `jit()`?::No, because `scan()` already compiles `f`.
<!--SR:!2026-01-08,16,301-->

## jax.lax.switch
What are the commonly used positional arguments of `jax.lax.switch`, and in what order?::The usual signature is `jax.lax.switch(index, branches, *operands, ...)`.
<!--SR:!2026-01-03,10,287-->

In `jax.lax.switch(index, branches, *operands, ...)`, what is `index`?::Integer scalar type, indicating which branch function to apply.
<!--SR:!2026-01-08,16,304-->

In `jax.lax.switch(index, branches, *operands, ...)`, what is `branches`?::Sequence of functions (A -> B) to be applied based on `index`. All branches must return the same output structure.
<!--SR:!2026-01-08,16,301-->

In `jax.lax.switch(index, branches, *operands, ...)`, what are `operands`?::Operands are passed as inputs to whichever branch is applied.
<!--SR:!2026-01-08,16,296-->

What does `jax.lax.switch` do if the `index` passed to it is out of bounds?::If `index` is out of bounds, it is clamped into the valid range.
<!--SR:!2026-01-07,15,290-->

What does `jax.lax.switch` return?::The value (B) of `branch(*operands)` for the branch that was selected based on `index`.
<!--SR:!2026-01-07,15,296-->

## jax.lax.dynamic_slice
What are the commonly used positional arguments of `jax.lax.dynamic_slice`, and in what order?::The usual signature is `jax.lax.dynamic_slice(operand, start_indices, slice_sizes, ...)`.
<!--SR:!2026-01-08,15,296-->

In `jax.lax.dynamic_slice(operand, start_indices, slice_sizes, ...)`, what is `operand`?::It is the array to slice.
<!--SR:!2026-01-02,10,284-->

In `jax.lax.dynamic_slice(operand, start_indices, slice_sizes, ...)`, what is `start_indices`?::It is a list/sequence of scalar indices, one per dimension, giving the starting index of the slice along each dimension of the input array; these values may be dynamic.
<!--SR:!2026-01-05,12,276-->

In `jax.lax.dynamic_slice(operand, start_indices, slice_sizes, ...)`, what is `slice_sizes`?::It is the size of the slice: a sequence of non-negative integers with length equal to `ndim(operand)` that specifies how many elements to take along each dimension.
<!--SR:!2026-01-03,11,281-->

# Code golf



# Conceptual
**Why do we even need these lax functions in the first place?**




# Tricks
