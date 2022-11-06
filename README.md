# Classifying-MNIST-digits-with-a-spiking-neural-network-Nengo
This repo mainly focus on how to build a spiking neural network to classfy the digits from 0-9 on MNIST dataset on Nengo platform. The code and related explanation will be stated and the idea is mainly from the literature (Training Spiking Deep Networks for Neuromorphic Hardware) and examples on Nengo website (Optimizing a spiking neural network). The wish is to instruct the reader can fully understand the code and knowledge behind. 

Knowledge behind:

1. ReLU ANN:
The original ReLU ANN network stucture is based on the work on literature(ImageNet classification with deep convolutional neural networks) and figure shows below.  
![image](https://user-images.githubusercontent.com/60885586/200172935-5707b8a6-3d65-4e5f-8093-d62a4a8cd4ef.png) 

To make the ANN transferable to spiking neurons, a number of modifications are necessary. 

  First, we remove the local response normalization layers. Response-normalization layers follow the first and second convolutional layers. This computation would likely require some sort of lateral connections between neurons, which are difficult to add in the current framework since the resulting network would not be feedforward and we are using methods focused on training feedforward networks.
  
  Second, we changed the pooling layers from max pooling to average pooling. Again, computing max pooling would likely require lateral connections between neurons, making it difficult to implement without significant changes to the training methodology. Average pooling, on the other hand, is very easy to compute in spiking neurons, since it is simply a weighted sum.
  
Therefore, only three convolutional layer left and related average pooling layer. 

2. LIF model 

3. LIF ANN

4. LIF SNN

Finally, we convert the trained ANN to a SNN. The parameters in the spiking network (i.e. weights and biases) are all identical to that of the ANN. The convolution operation also remains the same, since convolution can be rewritten as simple connection weights (synapses) wij between presynaptic neuron i and post-synaptic neuron j. (How the brain might learn connection weight patterns, i.e. filters, that are repeated at various points in space, is a much more difficult problem that
we will not address here.) Similarly, the average pooling operation can be written as a simple connection weight matrix, and this matrix can be multiplied by the convolutional weight matrix of the following layer to get direct connection weights between neurons.

The only component of the network that changes when moving from the ANN to the SNN is the neurons themselves. The most significant change is that we replace the soft LIF rate model (Equation 2) with the LIF spiking model (Equation 1). We remove the additive Gaussian noise used in training. We also add post-synaptic filters to the neurons, which removes a significant portion of the high-frequency variation produced by spikes.



