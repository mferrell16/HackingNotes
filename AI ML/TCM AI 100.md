Neural networks/deep learning can be used for classification and regression.
Deep learning is a popular variant of neural networks that utilizes multiple “hidden” (or middle) layers of nodes containing weights and biases.
Regression is predicting a continuous numeric value (a decimal) such as temperature or inches of rainfall.
Classification is predicting a label (e.g. dog/cat/bird, true/false) based on numeric inputs.
Neural networks are a computational model that learn from data 
Input layer -> hidden layers -> output layer 
The input and output layers are observed, the hidden layers are very complex and often not understood. 
The layers consist of neurons 
A neuron is a unit in a neural network 
A value of a neuron is calculated using an activation function, that uses both linear and non-linearity to compute the value. 
Activation of a neuron is dependent on the activation of all neurons in the preceding layer and their weights. 
At the start of training a neural network the weights and biases are randomized 
When the training data is not fully representative of the real world data, the model can be less accurate and could lead to unexpected behaviors 
back propagation uses the error to go back through the model and retrain the weights.  
forward propagation, which is passing an input through a neural network or deep learning model to get a prediction.
The epoch number and batch number decide how many test cases to train the model on and how often to update the weights/biases during training. 
![[Screenshot 2025-12-31 at 5.49.33 PM.png]]


N-grams model local word patterns, embeddings capture semantic meaning.
RNNs process sequences by updating a hidden state using the current input and past context, though they suffer from vanishing gradients over long sequences. 

In Maximum Likelihood Estimation (greedy) bigram model the proabability of a word is based on only the previous word. 
In feed-forward neural network bigram model, the output layer represents the probability distribution over possible next words. 
In a RNN, the hidden state is mainly responsible for keeping track of past information from previous steps and providing context. 
Feed-forward bigram networks are less powerful than RNNs for NLP because they do not maintain sequential context beyond one word. 
In word2vec embeddings, words iwth similar meaning appear close together in vector space. 

