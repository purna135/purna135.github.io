# Week 1-2 into GSoC

Finally, the coding period has started!

Me and my mentor, [Sayam Kumar](https://github.com/Sayam753) have settled for Weekly Progress calls about discussing the progress of the project and what next we should be looking into it. The Week starts with this call itself. We decided to divide the complete project into two parts since it involves two libraries

1. Aesara
2. PyMC

The first step was to collect the `Op` of `Aesara` which is being used in Multivariate Distributions.

Before moving forward, Let me introduce you to Aesara and its `Op`. Though I am still learning it, I have some idea about Op which I learned by the end of community bonding.

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
At First, to keep track of our progress, me and my mentor created a list of Action Items, which can be found [here](https://hackmd.io/SGiqe31gRGusiVdQT_PPFg?view). 
We decided to start with `cholesky decomposition` since it has been used in lot of distributions. At this time I have no Idea on how to start implementing a `Op` in aesara since It was very new to me. But many thanks to my Mentor and [Luciano Paz](https://github.com/lucianopaz) for helping me a lot. [Luciano Paz](https://github.com/lucianopaz) has already started working on this Op and he gave me his implementation for reference. By looking his code I got a clear Idea on how to write a new Op in Aesara. 

Also to verify my understanding on Op I created a new Op and write some test, which is given bellow.
<script src="https://gist.github.com/purna135/22768555c4eb0846ab9a5ad205bd4624.js"></script>

After testing all the Ops with batched Data we listed the below Ops to work on:

1. solve
2. cholesky
3. det
4. eigh
5. matrix_inverse

So by the end of phase-1 of GSoC, I am hoping to get these Ops done.

I am thankful to my mentor for his constant guidance and pymc-devs for being such a supportive community.
> Thank you for reading!