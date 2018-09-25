# Hierarchical Long-term Video Prediction without Supervision

## Paper Details

* Authors: Nevan Wichers, Ruben Villegas, Dumitru Erhan, Honglak Lee
* Link: [Arxiv](https://arxiv.org/pdf/1806.04768.pdf)
* Tags: Video Prediction, Adverserial Learning
* Year: 2018
* Conference: ICML 2018
* Implementation: [Official in TensorFlow](https://github.com/brain-research/long-term-video-prediction-without-supervision)

## Summary

### Problem 

The paper looks at the problem of predicting long term future image frames given some starting frames, without using ground truth
skeletal features i.e. joints coordinates.

## How it is solved?

* The paper tackles the problem by doing prediction of video frames at in high level feature spacesimilar to [1]. The difference
here is that there is no direct supervision in learning these features opposed to [2] where ground truth Mo-Cap features are
needed.
* The model is composes of multple networks as follows ( See Fig 1 in paper ):
    * Image Encoder: This is a CNN that encodes the frame at time step *t* to the high level feature **(HL-F)** space. It is only used till time
step *C* i.e. the point till when we have ground truth image frames and after which prediction starts.
    * Predictior LSTM: Eq (1). This is the main predictor of the model. It takes as input the hidden layer of the LSTM 
and HL-F at the previous time step. The output is the HL-F at the next time. The input HL-F here comes from the Image encoder
till step *C* and after that is taken from the output of the LSTM at previous time step only. 
    * VAN: The VAN is in turn compised of several networks. It takes as input the predicted HL-F, say at time step *t* 
from the LSTM and then using the image and HL-F from the *first* image frame generates the image frame at the time step *t*.
The main idea is that it takes the HL-F at a time step *t* and then using the analogy from the first image of how HL-F
and the image are related, procudes the image at that time step. The details of these networks are in Eq 2 and its subsequent paragraph.
   * Finally a gating mechanism is used so that  frames that are not changing /predicted to change can directly be copied from the input image in Eq 3. The output from this is the final predicted image.





[1] Learning to generate long-term future via hierarchical prediction

