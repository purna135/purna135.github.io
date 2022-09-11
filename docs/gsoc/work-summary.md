# Google Summer of Code'22 Highlights with PyMC
![](/images/gsoc-pymc.jpg){ align=center }

This post is intended to summarise the work completed during the GSoC coding period.

## About the project 🚩
Several multivariate distributions in PyMC, such as MvNormal, MvStudentT, and others, are constrained to working with 2D inputs and do not function with arbitrarily batched dimensions. The project's goal was to improve multivariate distribution support, making it possible to work with batched data (>2D) in a vectorized manner.


## Community Bounding Period 🤝
- This was a super interesting period. I got to know about many PyMC core developers through slack.
- Due to my university exam I was quite occupied but I managed to spent some time learning about the basics of Bayesian statistics, RandomVariable, Aesara.
- I took part in PyMC Developer Hackathon which gave me opprtunity of meet with PyMC core developer in video call and learned a lot of things about PyMC.
- I started working on some good first issue and by the help of PyMC team I was able to merger the PR[#5806](https://github.com/pymc-devs/pymc/pull/5806)  
- The most difficult part for me was understanding the Aesara, how the symbolic variale works and how to implement a new Ops.

## Month - 1️⃣:
The coding period began on June 13, and my goal for this period was to list all of the Ops used by the PyMC distributions that I want to generalize. Before beginning work on the actual issue, I began exploring Aesara, reading a lot about it from Aesara documentation and attempting to create a custom Op, which can be found [here](https://github.com/purna135/GSoC-Learnings/blob/main/Creating%20new%20Ops%20-%20Python%20implementation.ipynb).

- I began to investigate various PyMC distributions, and I am grateful to my Mentor, who has always assisted and guided me at every step of the way.

- With the help of my Mentor, I discovered that the Cholesky decomposition is something I should tackle first because it affects many distributions, including MvNormal, MvStudentT, MatrixNormal... etc.

- Because there are a lot of things going on in the Cholesky decomposition (for example making node, infering shape, calculating grad...etc), my mentor suggested that I start by solving a simple Op, such as `tril`, `triu`.

- After learning a little bit about these Ops, I was able to create my first PR[#1026](https://github.com/aesara-devs/aesara/pull/1026), which was merged into the main branch. Hooray 🙌🥳🎉, my first 1️⃣ PR has been merged, and I am super excited and energised to solve other Ops.

- I began testing all other Ops with batched data and listed all of the Ops that do not support >2D data. The Ops used by the distributions are listed below, and detailed testing of these Ops can be found in this Jupyter notebook [Notebook 1](https://github.com/purna135/GSoC-Learnings/blob/main/Testing%20Ops%20with%20Nd%20data.ipynb), [Notebook 2](https://github.com/purna135/GSoC-Learnings/blob/main/Testing%20Ops%20with%20Nd%20data-2.ipynb).

#### Below are the lists of Ops used by PyMC distributions
1. MvNormal
    - matrix_inverse
    - solve (L_Op is left to be implemented)
    - cholesky (dependent on solve)
2. MvStudentT
    - at.broadcast_arrays
    - at.concatenate
    - at.full
    - at.diag
    - at.all
    - at.switch
    - at.sum
    - at.log
    - at.dot
    - solve_upper_triangular
    - solve_lower_triangular
    - aesara.tensor.gammaln
    - at.log1p
3. KroneckerNormal
    - at.transpose
    - at.sqrt
    - at.batched_dot
4. MatrixNormal
    - at.full_like
    - at.nlinalg.matrix_dot
    - at.nlinalg.trace
5. LKJCorr
    - at.zeros_like
    - at.take
    - at.fill_diagonal
    - at.arange
    - at.linalg.det
6. LKJCholeskyCov
    - at.cumsum
    - at.zeros
    - at.sqrt
7. StickBreakingWeights
    - at.or_
    - at.any
    - at.and_
    - at.le
    - at. ge
    - at.allclose
    - at.neq
    - at.linalg.eigh
    - at.linalg.trace

After testing all of the operations with batch data,I identified the following operations to work on:

1. solve
2. cholesky
3. det
4. eigh
5. matrix_inverse

### Achived this month: 

- Got a thorough understanding of Aesara Ops 
- Generalized `tril` and `triu` beyond 2D arrays PR[#1026](https://github.com/aesara-devs/aesara/pull/1026) 
- Listed out all the Ops to work on



## Month - 2️⃣:
This month's goal is to complete the Cholesky decomposition and the Solve method.

- I spent a lot of time experimenting with the performance of Numpy and Scipy. I created two notebooks, one for small batches of data and the other for large amounts of data. I timed Numpy and Scipy as they computed the Cholesky decomposition.

- We decided to use Numpy Cholesky decomposition method in Aesara after seeing the results from experimets. The detailed code implementation and tests of `solve` methodcan be found in PR[#1060](https://github.com/aesara-devs/aesara/pull/1060).

- After submitting a PR for `solve` method, we received feedback from the Aesara developers and decided to use Scipy `solve` method and `Cholesky` decomposition instead of NumPy because SciPy supports many more parameters.

- So I spent all of my time generalising all of the Scipy methods using the NumPy vectorization technique.

### Work completed this month:

- Tested Numpy vs Scipy performance to solve cholesky decomposition - [Notebook - 1](https://github.com/purna135/GSoC-Learnings/blob/main/Cholesky%20-%20Numpy%20vs%20Scipy%20for%20Small%20Array.ipynb), [Notebook - 2](https://github.com/purna135/GSoC-Learnings/blob/main/Cholesky%20-%20Numpy%20vs%20Scipy%20for%20Large%20Array.ipynb)
- Implemented the Numpy Solve method in Aesara, [Code](https://github.com/aesara-devs/aesara/pull/1060).
- Implemented the NumPy Cholesky method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:numpy_cholesky)
- Implemented NumPy determinant method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_det)
- implemented NumPy eigh method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_eigh)
- Used NumPy vectorization to generalise Scipy's solve, Cholesky, determinant, and eigh method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_Aesara_Ops)
- Create tests for all new features and improve existing tests to test Ops with batched data.



## Month - 3️⃣:
We planned to work on generalising the PyMC distribution beyond 2D data this month in the GSoC proposal.

- Though our project requires the resolution of a few Ops in order to function, there are numerous other Ops that must be generalised in order to work with batched data in Apsara. As a result, we decide to work on issue[#695](https://github.com/aesara-devs/aesara/issues/695). This new Op allows Aesara to support batched data for all Ops, which not only solves our problem but also adds a new feature to Apsara.

- [@brandonwillard](https://github.com/brandonwillard) has already outlined a PR[#757](https://github.com/aesara-devs/aesara/pull/757) for Blockwise Op, and my task is to add the `grad` method to this Op and get it to merge to the main branch after all of the implementation is complete.

- Aside from Aesara-related tasks, I was able to devote some time to PyMC distribution development.

- `StickBreakingWeights` was the first distribution I chose because it does not require any Aesara Ops to function.

- Thank you to my mentor for explaining how PyMC works in detail. After observing the current implementation, I was able to devise a solution, and this was my first merged PR[#6042](https://github.com/pymc-devs/pymc/pull/6042) to PyMC that allow for batched alpha in StickBreakingWeights.


### Work done this month:

- Started working on Blockwise Op
- Got the PR[#6042](https://github.com/pymc-devs/pymc/pull/6042) that allow for batched alpha in `StickBreakingWeights`.


## Contributions ⚒
During this GSoC period, I worked on some issues and submitted Pull Requests; some of them were merged, while others are still open and I am working on them. A summary of them is provided below.

- Generalize tril and triu beyond 2D arrays PR[#1026](https://github.com/aesara-devs/aesara/pull/1026)
- Add Op to solve batched linear matrix equation PR[#1060](https://github.com/aesara-devs/aesara/pull/1060)
- Generalize aesara.tensor.linalg.cholesky beyond 2D arrays PR[#1012](https://github.com/aesara-devs/aesara/pull/1012)
- allow for batched alpha in StickBreakingWeights PR[#6042](https://github.com/pymc-devs/pymc/pull/6042)

- Implemented the Numpy Solve method in Aesara, [Code](https://github.com/aesara-devs/aesara/pull/1060).
- Implemented the NumPy Cholesky method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:numpy_cholesky)
- Implemented NumPy determinant method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_det)
- implemented NumPy eigh method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_eigh)
- Used NumPy vectorization to generalise Scipy's solve, Cholesky, determinant, and eigh method, [Code](https://github.com/aesara-devs/aesara/compare/main...purna135:aesara:generalize_Aesara_Ops)



## Notebook/Gists Created 📝
Whatever experiments I conduct to help my learning, I polish them and share them using Jupyter Notebook. Here are all of the experiments I conducted this summer.

- Cholesky - Numpy vs Scipy for Large Array, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Cholesky%20-%20Numpy%20vs%20Scipy%20for%20Large%20Array.ipynb)
- Cholesky - Numpy vs Scipy for Small Array, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Cholesky%20-%20Numpy%20vs%20Scipy%20for%20Small%20Array.ipynb)
- Creating a new Op in Aesara, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Creating%20new%20Op.ipynb)
- Creating new Ops - Python implementation, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Creating%20new%20Ops%20-%20Python%20implementation.ipynb)
- Experimenting with numpy solve, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Experimenting%20with%20numpy%20solve.ipynb)
- Performance Comparison for Solve method - Numpy vs Scipy, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Performance%20Comparison%20for%20Solve%20method%20-%20Numpy%20vs%20Scipy.ipynb)
- StickBreakingWeights - Experiment, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/StickBreakingWeights%20-%20Experiment.ipynb)
- Testing Cholesky Vectorization, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Testing%20Cholesky%20Vectorization.ipynb)
- Testing Ops with Nd data, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Testing%20Ops%20with%20Nd%20data-2.ipynb)
- Testing Tril and Triu for batch data, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Testing%20Tril%20and%20Triu%20for%20batch%20data.ipynb)
- Working Tril for 3D Data, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Working%20Tril%20for%203D%20Data.ipynb)
- Numpy Solve Example, [Source](https://github.com/purna135/GSoC-Learnings/blob/main/Numpy%20Solve%20Example.ipynb)


## Future Goals 📌
Some future tasks I would like to work upon

- Complete implementation Blockwise Op
- Generalize below PyMC distributions:

    1. MvNormal
    2. MvStudentT
    3. KroneckerNormal
    4. MatrixNormal



## Conclusion 💌
It was a fantastic experience to contribute to open source. I learned a lot of new things. I made some wonderful friends, including [@larryshamalama](https://github.com/larryshamalama), [@danhphan](https://github.com/danhphan), [@kunalghosh](http://github.com/kunalghosh), [@hassanconor](https://twitter.com/HassanConor), [@5hv5hvnk](http://github.com/5hv5hvnk) and [@nicospinu](https://twitter.com/nicospinu). Volunteered in building the [PyMCon 2022 website](https://purna135.github.io/pymcon-hugo/). 

I'd like to thank my mentors [Sayam Kumar](https://github.com/Sayam753) and [Ricardo Vieira](https://github.com/ricardoV94) for their unwavering support throughout this journey. I'm having a great time with the PyMC community. Next, I'd like to thank the [@numfocus](https://github.com/numfocus) community for making this opportunity available through Google Summer of Code.

Thank you for being a part of this wonderful summer.

With 💗, Purna Chandra Mansingh