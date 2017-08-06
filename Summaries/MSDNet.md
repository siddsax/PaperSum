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

### How is it Solved

* Some Definations:
  * Anytime classification: Fixed time for prediction of each data point.
  * Budgeted batch classification: Fixed time for prediction of a *batch* of points, hence sharing of total time among all points. 
  * Block: A group of layers that opperate at separate scales (in this paper 3 different scales). Each block having a classifier at end.
* Some Related Recent Models:
  * Adaptive Neural Networks ( Bolukbasi *et al.* [1] ): Train multiple models of increasing capacity and sequentially evalute them at 
    test time. This is undesirable as there is no sharing between networks.
  * Classifiers after features of intermediate layers: Here classifiers are fitted after multiple layers of a network like ResNet or           DenseNet. The authors show classifiers after layers producing fine featues suffer in terms of accuracies.
* Approach: 
  * **Problem 1** They note that coarse-level features are necessary for good classification, hence they create a multi-scale network with one **block** consisting of multiple layers that operate at different features.
  * Feature maps of a particular layer are made up of a) Regular convolution of previous layer with same scale features b) Doing Strided Convolutions (i.e. stride = 2) over a layer with finer-scale feature maps. 
  * This facilitates transfer of information from one *block* to another. After the coarse-level features of each block is the classifier corresponding to that block.
  * **Problem 2** The authors observed that adding classifiers in between layers of a network, compromised the accuracy of the layers after that. But this was not the case for DenseNet where each layer was connected with its subsequent layers. 
  * Hence they used Dense Connections. This means that a layer can by-pass a previous layer that is optimized for short-term gain for imporoving the accuracy of an intermediate classifier.

* Minor Points on Architecture:
  * First layer consists of lateral connections within the block.
  * Featues at scale 's' are made up of concatenation of features of previous layers made at scale 's' and 's-1'
    
  



[1] Adaptive Neural Networks for Efficient Inference ([link](https://arxiv.org/pdf/1702.07811.pdf))
  
