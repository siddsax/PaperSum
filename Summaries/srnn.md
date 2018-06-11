# Structural-RNN: Deep Learning on Spatio-Temporal Graphs

## Details:
* Authors: Ashesh Jain, Amir R. Zamir, Silvio Savarese, Ashutosh Saxena
* Link: [cs.stanford](https://cs.stanford.edu/people/asaxena/papers/structural-rnn-cvpr16-jain-saxena.pdf)
* Tags: RNNs, Motion Prediction, Structured ML
* Year: 2015
* Conference CVPR 2016 (Best Paper Award)
* Implementation [Official in Theano](https://github.com/asheshjain399/RNNexp)

## Summary

### Problem

Spatiotemporal graphs are a popular tool for imposing high-level intuitions in the formulation of several real world problems. But modeling them through simple RNNs doesn't work as well in practice. In this work, the authors propose structured RNNs that can encode the spatial features of objects onto the model. This has consequences to a wide variety of tasks like human motion prediction, Human activity detection as well as real life problems such as driver manouver prediction that can be used to reduce accidents.

### How they solve it.

The authors propose **Structued RNNs** that can model spatio-temoral graphs. 
* **Spatio-temoral graphs**: Defined in figure 2. A spatio-temporal graph is defined as (V, E_t, E_s) where V are the vertices/nodes, E_t and E_s being temporal and spatial edge. The graphs capture the prior knowledge of a situation and in turn design the architecture of the network. 
* The nodes need to be designed with care depending on the situation. The authors have described the process for human activity detection in section 3.1 second half. After that, each node has a temporal edge with itself, passing its information from one time-step to the next. The spatial connections can be treated as hyper-paramters ( as well can be nodes but then the hyper-parameter space becomes very large ). The authors fixed the connections by experimentation only. 
* If nodes are semantically similar, they have the same edge-factor (an RNN in the model). As explained in human activity detection task (Fig 3). If we model objects separately then there will be 2 RNN wrt human( think of them as just weights ) but by considering them same, they have same edgeRNN wrt to human.

* Converting from ST-graph to S-RNN: First we should understand types of RNNs in S-RNN:
    * Temporal EdgeRNN: These are the RNNs that represent temporal edges in ST-Graph.
    * Spatial EdgeRNN: Represent the spatial edges in graph.
    * NodeRNN: They model the nodes/vertices in the graphs.
* The edges among them are defined as:
    * Temporal EdgeRNN has only one edge, to its corresponding NodeRNN.
    * Spatial EdgeRNN can have one or two edges depending if its connecting semantically similar nodes or not respectively.
    * There is no edge among EdgeRNNs and among NodeRNNs themselves. Hence this creates a bi-partite graph.

* This defines the over-arching model as described in the paper. Though another important aspect is the input and output of these component RNNs. Explaining this with the example of human motion forecasting as in Fig 5. Each node is a body part at time step *t*. The model is fed the node positions at time steps 1, 2, ... *t*, the model has to predict the position at time step *t+1*. Note as each constitutent is an RNN, the model involves similar unfolding.
    * NodeRNN is fed the *concatenation* of all the outputs of its connected EgdeRNNs (both temporal and spatial) and the node feature ( i.e. position of that body part) at that time step.
    * Both EdgeRNNs are fed the summation of the features, f_{o1o2} of the nodes that are in the same semantic groups. Further, these features f_{o1o2} for each constituent of the semantic group are defined as follows.
         * For Temporal Edges they are concatenation of that body part's co-ordinates at that point and the difference between the co-ordinates at that time step and previous time step. 
         * For Spatial Edges, its just the concatenation of both body part's co-ordinates.
