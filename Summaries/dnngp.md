# Deep Neural Networks as Gaussian Process

## Details:

* Authors: Jaehoon Lee, Yasaman Bahri, Roman Novak, Samuel S. Schoenholz, Jeffrey Pennington, Jascha Sohl-Dickstein
* Link: [Arxiv](https://arxiv.org/pdf/1711.00165.pdf)
* Tags: Bayesian ML, Gaussain Processes, Neural Networks
* Year: 2017
* Conference: ICLR 2018
* Implementation: [Official in TensorFlow](https://github.com/brain-research/nngp)

## Summary:

### Problem
How can we frame deep/multi-layered neural networks as GPs hence deriving a corresponding GP mean and variance for a neural network.  

### How they solve it?

* Gaussian Process Defination: A gaussian process defines a *distribution over functions* with <a href="https://www.codecogs.com/eqnedit.php?latex=\mu" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu" title="\mu" /></a> as the *average* function and <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> as variance over it. Hence they can be treated as flexible prior over functions. Practically a GP is defined by value of functions at some finite number of points. Hence for a sample from a GP ( which is a function ), its value at those finite points form a gaussian distribution with the <a href="https://www.codecogs.com/eqnedit.php?latex=\mu" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\mu" title="\mu" /></a> and <a href="https://www.codecogs.com/eqnedit.php?latex=\Sigma" target="_blank"><img src="https://latex.codecogs.com/gif.latex?\Sigma" title="\Sigma" /></a> being the mean and covariance matrix respectively. 
* Correspondence between 1 layer neural network and GPs [1]. From Eq 1 <a href="https://www.codecogs.com/eqnedit.php?latex=z_i^l" target="_blank"><img src="https://latex.codecogs.com/gif.latex?z_i^l" title="z_i^l" /></a> can be seen as a summation of variables from i.i.d distribution. Hence <a href="https://www.codecogs.com/eqnedit.php?latex=z_i^l" target="_blank"><img src="https://latex.codecogs.com/gif.latex?z_i^l" title="z_i^l" /></a> comes from a gaussian distribution. * This by extension means that <a href="https://www.codecogs.com/eqnedit.php?latex=z_i^l(x^{\alpha=1}),&space;z_i^l(x^{\alpha=2}),&space;...&space;,&space;z_i^l(x^{\alpha=N})" target="_blank"><img src="https://latex.codecogs.com/gif.latex?z_i^l(x^{\alpha=1}),&space;z_i^l(x^{\alpha=2}),&space;...&space;,&space;z_i^l(x^{\alpha=N})" title="z_i^l(x^{\alpha=1}), z_i^l(x^{\alpha=2}), ... , z_i^l(x^{\alpha=N})" /></a>, which is the set of outputs for different inputs forming a multi-variate gaussian distribution. This basically defines a gaussian process as we have that a sample from this neural network ( that has a gaussian prior over its parameters with zero mean) follows a gaussian distribution. They then find the mean and co-variance matrix of this distribution which leads to a GP that is a distribution over *all* single layer neural networks with infinite width. The infinite width is needed because only then the central limit theorm is valid.

 we have described in the previous point.





[1] Bayesian Learning for Neural Networks
