# Week 3-4 into GSoC

Following up on the work done in weeks 1 & 2, I started working on `Cholesky` decomposition with the help of my mentor and [Luciano Paz](https://github.com/lucianopaz). But since the Cholesky op depends on some same small op `tril` and `triu` which are not supporting batched data so we decided to fix these op first.

After spending 3-4 days understanding the code and a lot of debugging I finally came up with a solution and this week I created my first PR [#1026](https://github.com/aesara-devs/aesara/pull/1026)


## Work done in this PR:
- After doing a lot of experiments with `tril` and `triu` I got to know that in order to work with batched data we have - to use the last 2 dimensions of the batched data.
- Now I am so happy that after this small fix `tril` and `triu` can work with batched data.
- I finally clean up the code added some examples and corrected the docstring.
- After writing the test cases for the new feature, I am done with my first PR to be merged : )
- This PR gives me so much confidence for future work, now I have a strong understanding of Aesara and its Op.


## What next ?
So the next thing is to complete the implementation of Cholesky Op.
But here we have 2 choices here whether we can use Scipy for computing Cholesky decomposition but Scipy is restricted to 2d data only but we can use vectorization in order to work with batched data. And the second option we have is to use Numpy to compute the Cholesky decomposition which supports the batched data but is a little bit slower than the Scipy one.

So we have to experiment with these two methods and have to find the best one to implement in the Aesara library.

So by the next week, I will come up with an approach to implement the Cholesky in Apsara.

I am thankful to my mentor for his constant guidance and pymc-devs for being such a supportive community.

> Thank you for reading!
