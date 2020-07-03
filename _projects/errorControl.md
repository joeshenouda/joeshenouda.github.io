---
title: "Error Control Coding Saves Distributed Gradient Descent"
description: Using coding theory to speed up distributed gradient descent
layout: post
---
In most machine learning tasks our goal is to minimize the empirical risk leaving us with an optimization problem of the following form in an attempt to find the best parameter $$\beta$$ for our model based on the data.

$$\min_{\beta} \sum_{i=1}^{D}\ell(\beta; x_{i}, y_{i})$$

This unconstrained optimization problem is most commonly solved using the famous gradient descent or some variation of it. Thus in each iteration we wish to evaluate the gradient of our objective function in order to take a "step" in the direction of steepest descent. Computing this gradient at each iteration can become very computationally expensive especially with large datasets used in real world problems. Thankfully, our objective functions are often additively separable meaning we can express the gradient at each iteration as:

$$\nabla  \sum_{i=1}^{D}\ell(\beta_{k}; x_{i}, y_{i}) = \nabla \sum_{i=1}^{D_{1}}\ell(\beta_{k}; x_{i}, y_{i})+... $$

$$+\nabla \sum_{i=1}^{D_{n}}\ell(\beta_{k}; x_{i}, y_{i})$$

Where we have now split our dataset into $$n$$ partitions. The full gradient can be computed using a distributed architecture by taking the gradient of our objective function evaluated only at the specific data partition assigned to each node.

<img src="/assets/distributedGradDescent.JPG" alt="distributed pic"
	title="Distributed Gradient Descent" width="70%" height="70%"/>

Here each partial gradient is denoted $$g_{j}$$ depending on which data points are being used. While this solution seems to have solved our problem the team is only as strong as its weakest member. Notice that in order to recover the full gradient back to the fusion center we must wait for all the nodes to finish computing their partial gradients thus, the computation is only as fast as the slowest nodes, which we refer to as the "stragglers". 

It turns out that in the same way redundancy is introduced in digital communications to correct erasures or errors redundancy can also be introduced in computation at each node which allows for robustness against the straggler nodes. [Gradient Coding](https://arxiv.org/abs/1612.03301) by R. Tandon present a framework to solve this problem and present an algorithm describing how to most effectively add redundancy to each node such that we can recover the full gradient from the first $$k$$ nodes that finish first. [Gradient Coding from Cyclic MDS Codes and Expander Graphs](https://arxiv.org/abs/1707.03858) by N. Raviv expand upon this work further and provide a connection to classical cyclic MDS codes.

For my course on error control coding I did my final project on this problem based on these two papers. My full write up on these topics can be found [here](/assets/Error_Control_Final_Project_Report.pdf) where I explain the main results and proofs.
