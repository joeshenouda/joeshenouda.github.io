---
title: Coding Theory meets distributed optimization
description: Using coding theory to speed up distributed gradient descent
layout: post
feature_text: |
    ## Error correcting codes meet distributed optimization
---

For my course on error control coding I did my final project on two very interesting papers that took ideas from classical coding theory and applied them in a very clever way to distributed gradient descent.

The first paper [Gradient Coding](https://arxiv.org/abs/1612.03301) explains the problems that arise when performing distributed gradient descent specifically the effect of stragglers. They then present a clever framework that introduces redundancy into the computation in order to recover the full gradient from any surviving workers.

The second paper [Gradient Coding from Cyclic MDS Codes and Expander Graphs](https://arxiv.org/abs/1707.03858) expands upon the initial framework setup in [Gradient Coding](https://arxiv.org/abs/1612.03301) to show its relation to cyclic MDS code.

My full write up on these topics can be found in [here](/assets/Error_Control_Final_Project_Report.pdf).