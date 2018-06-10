# Dynamic Graph CNN for Learning on Point Clouds

## Details

* Authors: Yue Wang, Yongbin Sun, Ziwei Liu, Sanjay E. Sarma, Michael M. Bronstein, Justin M. Solomon
* Link: [Arxiv](https://arxiv.org/pdf/1803.04189.pdf)
* Tags: Point Cloud, Graph CNN
* Year: 2018
* Implementation: [Official in tensorflow](https://github.com/WangYueFt/dgcnn)

## Summary

### Problem

The problem is simple enough. Given a point-cloud perform segmentation and classification and imporving the state-of-art by incorporating local information of each point.

### How is it Solved

The authors propose an incremental extension of the popular Graph CNN model [read here](https://tkipf.github.io/graph-convolutional-networks/) named as Edge Convolution that is tailored for their task. Further due to the fact that point-clouds inherently is not a graph. Hence the lack of an adjacency matrix needed for graph-convolutions. They propose Dynamic Graph CNN i.e. dynamic connections between points.

* **Edge Convolution**: A Graph-CNN layer consists of finding the features of a node ( a point in the point cloud here ) at the next time step as a function of that point and its neighbours. Its defined as a simple summation of weights multiplied into the features in Graph-CNN while here it is defined as <a href="https://www.codecogs.com/eqnedit.php?latex=x_i'&space;=&space;Aggregation\limits_{j:(i,&space;j)&space;\subset&space;\mathcal{E})}&space;h(x_i,&space;x_j&space;-&space;x_i)" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i'&space;=&space;Aggregation\limits_{j:(i,&space;j)&space;\subset&space;\mathcal{E})}&space;h(x_i,&space;x_j&space;-&space;x_i)" title="x_i' = Aggregation\limits_{j:(i, j) \subset \mathcal{E})} h(x_i, x_j - x_i)" /></a>. 
    * Here the function h() is modelled using a neural network. The reason for using a function of <a href="https://www.codecogs.com/eqnedit.php?latex=x_i,&space;x_j&space;-&space;x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i,&space;x_j&space;-&space;x_i" title="x_i, x_j - x_i" /></a> is that <a href="https://www.codecogs.com/eqnedit.php?latex=x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_i" title="x_i" /></a> contributes towards the globalposition of the point and <a href="https://www.codecogs.com/eqnedit.php?latex=x_j&space;-&space;x_i" target="_blank"><img src="https://latex.codecogs.com/gif.latex?x_j&space;-&space;x_i" title="x_j - x_i" /></a> towards its relation with other points.
    * The aggregation function used here is the max operation.
 
* **Dynamic GraphCNNs**: Point Cloud even though has some geometric properties is not a graph inherently. Hence in this work, the neighbors of a node are defined at each pass using K-nearest neighbors. This means that the connections between nodes can change from one iteration to another leading to the name Dynamic GraphCNN.
