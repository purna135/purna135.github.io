# Week 1-2 into GSoC

The coding period has finally begun!

My mentor, [Sayam Kumar](https://github.com/Sayam753), and I have agreed to hold weekly progress calls to discuss the project's progress and what steps we should take next. The Week begins with this phone call. We decided to split the project into two parts because it involves two libraries.

1. Aesara
2. PyMC

The first step was to collect Aesara's `Op`, which is used in Multivariate Distributions.

Before we continue, allow me to introduce you to `Aesara` and its `Op`. Though I am still learning, I have some knowledge of Op from the end of community bonding.


## Aesara
The best description is the one taken straight from the GitHub repository and Read the Docs: Aesara is a Python library that lets you define, optimize, and evaluate mathematical expressions, especially ones involving multi-dimensional arrays (e.g. numpy.ndarrays). Using Aesara it is possible to attain speeds rivaling hand-crafted C implementations for problems involving large amounts of data.

Aesara’s compiler applies many optimizations of varying complexity to these symbolic expressions.


### Working with Aesara
Here is an example of how to use Aesara. It doesn’t show off many of its features, but it illustrates concretely what Aesara is.

```python
import aesara
from aesara import tensor as at

# declare two symbolic floating-point scalars
a = at.dscalar()
b = at.dscalar()

# create a simple expression
c = a + b

# convert the expression into a callable object that takes `(a, b)`
# values as input and computes a value for `c`
f = aesara.function([a, b], c)

# bind 1.5 to 'a', 2.5 to 'b', and evaluate 'c'
assert 4.0 == f(1.5, 2.5)
```

The example above was taken straight from the frontpage of Aesara. Here, `a`, `b` and `c` are tensor variables of type TensorVariable which do not have a value associated. 

Aesara is not a programming language in the normal sense because you write a program in Python that builds expressions for Aesara. Still it is like a programming language in the sense that you have to

- declare variables `a` and `b` and give their types,
- build expressions graphs using those variables,
- compile the expression graphs into functions that can be used for computation.

It is good to think of `aesara.function()` as the interface to a compiler which builds a callable object from a purely symbolic graph. One of Aesara’s most important features is that `aesara.function()` can optimize a graph and even compile some or all of it into native machine instructions.

## Getting started with Project

To begin, in order to keep track of our progress, my mentor and I created a list of Action Items, which can be found [here](https://hackmd.io/SGiqe31gRGusiVdQT_PPFg?view). We chose to begin with `cholesky decomposition` because it has been used in many distributions. I had no idea how to begin implementing an `Op` in Aesara because it was all new to me. However, I would like to express my gratitude to my Mentor and [Luciano Paz](https://github.com/lucianopaz) for their invaluable assistance. [Luciano Paz](https://github.com/lucianopaz) has already begun work on this Op, and he has provided me with his implementation for reference. Looking at his code gave me a good idea of how to write a new Op in Aesara.

In order to validate my understanding of Op, I created a new Op and wrote some tests, which are listed below.
<script src="https://gist.github.com/purna135/22768555c4eb0846ab9a5ad205bd4624.js"></script>

After testing all of the operations with batch data, we identified the following operations to work on:

1. solve
2. cholesky
3. det
4. eigh
5. matrix_inverse

So I'm hoping to complete these Ops by the end of phase 1 of GSoC.

I am grateful to my mentor for his constant guidance and to the pymc-devs community for its encouragement.

> Thank you for reading!