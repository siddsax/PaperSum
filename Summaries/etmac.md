# Emergent translation in multi-agent communication

## Details:

* Authors: J. Lee, K. Cho, J. Weston and D. Kiela
* Link: [Arxiv](https://arxiv.org/pdf/1710.06922.pdf)
* Tags: Neural Machine Translation, 
* Year: 2017
* Conference: ICLR 2018
* Implementation: [Official in PyTorch](https://github.com/facebookresearch/translagent)

## Summary

### Problem

Achieve tranlations between 2 languages from un-alignmed a set of image captioning datasets in the required languages. Hence 
broadly in an unsupervision fashion with respect to translation.

### How they solve it?

* The authors propose a 2-agent game that as a side product leads to a model that can translate between the given languages 
without using a parallel corpora. To achieve this, the agents are equiped with 3 modules each. An image encoder, a native
speaker module, a foreign language encoder. 
    * **Native Speaker Module** (NSM): This is basically an image captioning model, that is tasked with describing an image as well as 
        possible. It is a GRU that is fed the image as its first input, via, producing a hidden state that is then used to 
        produce text via a fully connected layer and ST-Gumbel softmax sampling. Further unfolding produces the full discripton.
    * **Foreign Langage Encoder** (FLE): This is also a RNN, that can generate features of dimension D from a given text in 
        the foreign language to the agent. This text is actually the discription of the image as done by the other agent in its 
        language.
    * **Image Encoder** (IE): This is a CNN that encodes the image into features of the same dimension D that FLE does. The aim
        is that these encodings and the ones that an agent gets with FLE are as close as possible.

* The overall process is then as below. (_1 and _2 represent the agents)
    * Image --> NSM_1 --> FLE_2 --> Feature <-- IE_2 <-- (Set of images, one of them being the original image )
* From this translation can be done as follows:
    * Text in Language 1 --> FLE_1 --> NSM_2 --> Text in Language 2
* The different loss functions used are as follows:   
