# Composing graphical models with neural networks for structured representations and fast inference

## Paper Details
* Authors
* Link: [Arxiv](https://arxiv.org/pdf/1603.06277.pdf)
* Tags: Graphical Models, VAE, probailistic models
* Year: 2016
* Conference: NIPS 2017
* Implementation: [Official in TensorFlow](https://github.com/mattjj/svae)

## Summary
* In the first half of the paper, the authors argue that neural networks and graphical models have complementary strengths. The latter makes rigid assumptions about the data opposed to flexibility of neural networks while giving structured representations which is generally tough to obtain for neural networks. They give examples where this can be seen as bellow.
    * Gaussian Mixture Models + Neural Nets: (Fig 1) Here they show a simple neural network can not encode the clustered structure of the data, while GMM by itself doesn't leed to very good partitions
    *  VAE + Linear Dynamic System: Here by making the output at time step n, depend on output at time step n-1. It can encode time dependence in the outputs that is important to model videos.
    * VAE + Switching LDS: Going a step further. Latent LDS can be combined with GMM to create a model that has another latent discrete layer. Hence making ot possible for the model to evolve over time.

But all these model are tough to do inference upon. This is the problem that the authors address in this paper with a new class of AEVB inference methods.

  
