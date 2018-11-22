# Noise2Noise: Learning Image Restoration without Clean Data

## Details

* Authors: Jaakko Lehtinen, Jacob Munkberg, Jon Hasselgren, Samuli Laine, Tero Karras, Miika Aittala, Timo Aila
* Link: [Arxiv](https://arxiv.org/pdf/1801.07829.pdf)
* Tags: Image DeNoising, Learning with less clean data
* Year: 2018
* Conference ICML 2018
* Implementation: [Official in tensorflow](https://github.com/NVlabs/noise2noise), [Port in PyTorch](https://github.com/joeylitalien/noise2noise-pytorch)

## Summary

### Problem
Can we learn to denoise images with noisy images only?

### How they solve it?

* The authors motivate their work with a temperature predictor example. If we are given the temperature of last few days then using a L2 loss predictor will lead to a model that predicts the mean of given samples as the temperature on the next day. In a similar fashion if a model is given noisy images as targets ( where input is also a noisy image that has to be denoised ) then the model will learn to predict the mean as its impossible to predict random noise. They then go on experiementing with different noises.

* For the experiments, they use a recent State-of-art model RED30 [1]. They then explain how this model is trained with noisy images in a slightly odd manner. Though what they broadly mean is that there are 3 training cases. 
    * *Case I* The traditional case. Say the dataset has 100 clean images and 19 noisy ones for each. Now we have 100 * (19+1) * 1 training pairs ( input = noisy or clean; output = clean ).
    * *Case II* Here the model is trained with target also being possibly noisy. Hence we have 100 * (19+1) * (19) choices. This is because, same image can't be both input and output. 
    * *Case III* Noise2Noise case. Here the input and output both are noisy images only while having only 2 noisy images for each image and 1000 image samples. This means there are 1000* 2 training samples.
    
* Hence in effect, in cases II and III, training for one image is done, by using multiple noisy samples of that scene. For example if one brain's MRI scans were to be used for training the model, several MRI scan images will be taken corresponding to the same brain at the same position. As the noise here is random, it will be different always which makes it impossible for the model to learn the noise itself. The only constant thing being the denoised image MRI scan hence in this way a model can be trained to denoise the image even without the used of clean samples.

* Coming back to the 3 cases  as described above, the authors report that Case III which is the noise2noise scenario performs the best, then case II, case I at 3rd. The reason is that, in case 3 there are more real images on the same budget of 2000 images. While case 2 has much more training samples than any of them. 

They then go on to experiment with different noise types showing that it is possible to denoise images with only noisy samples. 


[1] Image restoration using convolutional auto-encoders with symmetric skip connections
