# Week 5-6 into GSoC

This week I spent a lot of time experimenting with the performance of Numpy and Scipy. I have created two notebooks one is for small batches of data and the other is for large amounts of data. I noted the time taken by both Numpy and Scipy to compute the Cholesky decomposition and got the below result:

## Experiment - 1 (for small data)
<script src="https://gist.github.com/purna135/1c217a521cf5f31a87c783cf49c4101d.js"></script>

## Experiment - 2 (for large data)
<script src="https://gist.github.com/purna135/6da4f68b784f29af33156bf8f2c7d381.js"></script>

To summarize I got the bellow 2 graphs:

1. Numpy vs Scipy for Small Dataset
![](/images/cholesky-1.png){ align=center }

2. Numpy vs Scipy for Large Dataset
![](/images/cholesky-2.png){ align=center }

As we can see from these two graphs the Numpy is performing better with the reasonable dataset, so we decided to go with the Numpy implementation.

With the help of my mentor, I have implemented the `Solve` and `Cholesky` in Aesara and now we are fixing some issues with calculating `grad`.

I owe my mentor a huge debt of gratitude. He is really amiable and helpful. He is always willing to assist and has clarified all of my doubts for me, even when I ask him dumb things in Slack. He spent a lot of time debugging the code and came up with an easy fix; in fact, he taught me how to debug. He's the one who first showed me how to use the Python Debugger (PDB).

Without my Mentor, I can't image how my GSoC experience would be, [Sayam Kumar](https://github.com/Sayam753).

> I am grateful to my mentor for his ongoing advice and to the pymc-devs community for being so encouraging.