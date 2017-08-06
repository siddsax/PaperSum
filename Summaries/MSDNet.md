#Multi-Scale Dense Network for Resource Efficient Image Classification
## Paper Details
* Authors: Gao Huang, Danlu Chen, Tianhong Li, Felix Wu, Laurens van der Maaten, Kilian Q. Weinberger
* Link: [Arxiv](https://arxiv.org/pdf/1703.09844.pdf)
* Tags: Image Classification, Low Resource Deep Learning
* Year: 2017
* Conference: ICML 2018
* Implementation: [Official in Torch(Lua)](https://github.com/gaohuang/MSDNet), [Reproduced in PyTorch](https://github.com/avirambh/MSDNet-GCN)

## Summary

### Problem

Most deep learning frameworks take enormous amount of recources even at test time, in terms of memory and time. In this work the authors 
propose a new perspective to look at this problem as *a) anytime classification* *b) budgeted batch classification*. Further 
they propose an image classifier called MSD-Net that gives good accuracies when placed in restrictions posed by these conditions.


  
