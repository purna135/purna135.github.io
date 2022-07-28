# Week 3-4 into GSoC

Following up on my work from weeks 1 and 2, I began working on `Cholesky` decomposition with the assistance of my mentor and [Luciano Paz](https://github.com/lucianopaz). However, because the Cholesky op is dependent on some small op `tril` and `triu`, which do not support batched data, we decided to fix these op first.

After 3-4 days of debugging and understanding the code, I finally came up with a solution, and this week I created my first PR [#1026](https://github.com/aesara-devs/aesara/pull/1026).

## Work done in this PR:
- After conducting numerous experiments with `tril` and `triu`, I discovered that in order to work with batched data, we must use the last two dimensions of the batched data.
- Now that this minor issue has been resolved, `tril` and `triu` can work with batch data.
- Finally, I cleaned up the code, added some examples, and fixed the docstring.
- I finished my first PR to be merged after writing the test cases for the new feature:)
- This PR boosts my confidence for future work; I now have a solid understanding of Aesara and its Op.

## What next ?
So the next step is to finish implementing Cholesky Op. However, we have two options here: we can use Scipy to compute Cholesky decomposition, but Scipy is limited to 2d data only, or we can use vectorization to work with batched data. The second option is to use Numpy to compute the Cholesky decomposition, which supports batched data but is slightly slower than Scipy.

So we must experiment with these two methods to determine which is the best to implement in the Aesara library.

So, within the next week, I will devise a strategy for implementing the Cholesky in Apsara.

I am thankful to my mentor for his constant guidance and pymc-devs for being such a supportive community.

> Thank you for reading!
