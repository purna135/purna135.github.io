# GSoC'22 with PyMC
![](/images/gsoc-pymc.jpg){ align=center }

I'm happy to share that my [Google Summer of Code](https://summerofcode.withgoogle.com/) proposal has been accepted by [PyMC](https://github.com/pymc-devs/pymc) under the [NumFOCUS](https://numfocus.org/) umbrella. I'd like to express my gratitude to my mentors [Sayam Kumar](https://github.com/Sayam753) and [Ricardo Vieira](https://github.com/ricardoV94), as well as the entire PyMC community, for providing this opportunity.

This summer, I'm looking forward to expanding my skills and contributing to the PyMC library. I'd like to thank all the PyMC members for their assistance, from merging my first PR to reviewing my proposal.

The Dashboard for my GSoC project can be viewed [here](https://summerofcode.withgoogle.com/programs/2022/projects/1wz8q5wi)


## About the Project

My project is to `Increase Support for Batched Multivariate Distributions`, several multivariate distributions in [PyMC](https://www.pymc.io/projects/docs/en/stable/api/distributions/multivariate.html), such as [MvNormal](https://www.pymc.io/projects/docs/en/stable/api/distributions/generated/pymc.MvNormal.html), [MvStudentT](https://www.pymc.io/projects/docs/en/stable/api/distributions/generated/pymc.MvStudentT.html), and others, are constrained to working with 2D inputs and do not function with arbitrarily batched dimensions. The project's goal is to improve multivariate distribution support, making it possible to work with batched data (> 2D) in a vectorized manner.


## My First Task

My initial goal for this project is to

1. Investigate how Random Variables are implemented in v4.
2. Collect all Aesara Ops that are utilised in multivariate distribution implementations.
3. Expand the Ops to operate with more than 2D inputs.
4. Update any/all test cases relating to these Ops and multivariate distributions.


## What’s next?
I will be posting about my GSoC experiences on a weekly basis.

Thank you. 😊

With 💖 Purna.