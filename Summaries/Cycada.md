# CyCADA: Cycle-Consistent Adversarial Domain Adaptation
## Paper Details

* Authors: Judy Hoffman, Eric Tzeng, Taesung Park, Jun-Yan Zhu, Phillip Isola, K Saenko, A Efros, T Darrell
* Link: [Arxiv](http://proceedings.mlr.press/v80/hoffman18a/hoffman18a.pdf)
* Tags: Domain Adaptation, Unsupervised Learning
* Year: 2017
* Conference: ICML 2018
* Implementation [Official in PyTorch](https://github.com/jhoffman/cycada_release)

## Summary

While Cycle GAN got a lot of attention from all parts, their extension Cycala got *relatively* unnoticed even after being a very interesting read in itself.

### Problem
Domain Adaptation is the problem where we want to adapt a model trained on task to perform well for another related task as well. In this space most of the recent works have been feature space alignment models where some measure of discrepancy between the source and target features is minimized, this paper proposed a new model that reduces pixel level discrepancy while preserving the semantic meaning. Note that the classes must remain the same in both datasets so its essentially an adaptation over datasets than tasks.

### How it is solved
The model consists of multiple steps and losses as explained in the following points but the general idea is to transform the data from source dataset to target dataset and then train a model on this augmented data set. Then use this learned model for testing on samples from target dataset. This leads to significant improvement over a model that was trained on the source dataset only.

* Train a model f_s on the source dataset. This is represented in Eq 1 (in the paper)
* Pixel-level Adaptation:
  * The aim here is to make a generator <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a>
 that can transform an image from source dataset to target dataset while learning a classifier in the opposite direction as well.
  * **Loss 1** GAN loss of <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a>. This means that a discriminator <a href="https://www.codecogs.com/eqnedit.php?latex=$D_T$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$D_T$" title="$D_T$" /></a> is trained along with the generator. The discriminator has to detect points from target dataset as real and ones transformed from source by generator as fake. Similarly a symmetric GAN loss for <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{T\rightarrow&space;S}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{T\rightarrow&space;S}$" title="$G_{T\rightarrow S}$" /></a> as well. Eq 2

  * **Loss 2** The cycle GAN loss. This is same as the cycle loss used in the Cycle GAN paper [1]. It is essentially the reconstrution loss of a data point that is first transformed from source to target via <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a> and then back with <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{T\rightarrow&space;S}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{T\rightarrow&space;S}$" title="$G_{T\rightarrow S}$" /></a>. Again symmetric loss for a target data point. This is the reason <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{T\rightarrow&space;S}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{T\rightarrow&space;S}$" title="$G_{T\rightarrow S}$" /></a> is trained even though its not needed for the end goal. Eq 3

  * **Loss 3** Semantic Consistency Loss: This is an additional loss that is necessary to mainain the semantic meaning og the original image with respect to the classifier f_s. This essentially means that the class predicted by f_s for a data point before and after transformation with <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a> is as close as possible. Eq 4

* Feature-Level Adaptation:
  * the authors additionally add a feature level adaptation loss as well in the same vein as the previous loss which is along the lines of traditional domain adaptation works.
  * **Loss 4** This is a GAN loss, here a discriminator has to distinguish between features extracted from target images and a source image that has been transformed with <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a>. This enforces that at feature level as well the images are similar to each other after transformation. Eq 5

**Loss 5** Finally there is a task loss that actually trains a model to for the given task. This model is trained on source images transformed with <a href="https://www.codecogs.com/eqnedit.php?latex=$G_{S\rightarrow&space;T}$" target="_blank"><img src="https://latex.codecogs.com/gif.latex?$G_{S\rightarrow&space;T}$" title="$G_{S\rightarrow T}$" /></a>

All these losses are then clubbed together to train the *several* involved models!

[1] Unpaired Image-to-Image Translation using Cycle-Consistent Adversarial Networks ([link](https://arxiv.org/abs/1703.10593)])
