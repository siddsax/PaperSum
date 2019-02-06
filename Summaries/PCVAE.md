# Lagging inference networks and posterior collapse in variational auto-encoders

## Details:

Code: [Official Code in PyTorch](https://github.com/jxhe/vae-lagging-encoder)

## Summary 

### Problem

Variational Auto-Encoders suffer from the problem of posterior-collapse where the posterior learned through VI collapeses 
into the prior of the model. This can further be categorized into two cases:-
* Model Collapse: p(z|x) collapeses into the prior
* Inference Collapse: q(z|x) collapses into the prior 
 and model collapse. These occur when p(z|x) collapses into the prior.

Both of these distribution are tracked with the means of the gaussian, which if tends to zero indicates posterior collapse 
( as the prior is N(0, 1) )
