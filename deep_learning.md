# Deep learning Interviews
- [Deep learning Interviews](#deep-learning-interviews)
  - [interview questions](#interview-questions)
    - [why non-linearities in NN](#why-non-linearities-in-nn)
    - [Gradient vanish and explotion](#gradient-vanish-and-explotion)
    - [DNN and CNN](#dnn-and-cnn)
    - [Ways to visualize features](#ways-to-visualize-features)
    - [optimizers & learning rate](#optimizers--learning-rate)
    - [Data augumentation](#data-augumentation)
    - [Classical Networks](#classical-networks)
    - [end-to-end learning](#end-to-end-learning)
    - [activate function, Non-linear](#activate-function-non-linear)
    - [Transfer learning](#transfer-learning)
    - [Overfitting problem](#overfitting-problem)
    - [weights and bias](#weights-and-bias)
    - [Supervised and unsupervised learning](#supervised-and-unsupervised-learning)
    - [Transfer learning](#transfer-learning-1)

## interview questions
Here lists some web-page of deep learning interview questions.  
[25 Deep Learning Interview Questions](https://towardsdatascience.com/50-deep-learning-interview-questions-part-1-2-8bbc8a00ec61)  



### why non-linearities in NN
A composition of Linear functions is still a linear function. Which is a linear model. A linear model has much smaller number of parameters so that the complexity of this model is limited. 


### Gradient vanish and explotion
**Differentiation** in **Chain rule**  
The reason behind this phonomenon is model uses differentiation of activation function to update the weight. And after numbers of layers of differentiation by chain rule. It could result in:  
- big number, exploation
- near 0, vanishing.  

Solution:  
- gradient clipping, set the gradient to a fixed range, when the gradient exceed a threshold, cut it into the threshold.
- ReLU as the activate function, instead of sigmoid
- BN Batch normalization. See [BN](https://blog.csdn.net/qq_25737169/article/details/79048516) for detail. BN accerlerates the training process and has a regularization effect.  
- Residual structure, because of Idendity mapping. Check this [resNet](https://zhuanlan.zhihu.com/p/31852747) for detail.


### DNN and CNN
Dense neural network and Convolutional neural network are models both capture the relationship among close pixels.  

**Difference**:
- CNN is transition invariant, exact location of pixels are irrelevent for the filter.
- CNN is less likely to overfit. The parameters of CNN is much less than those of DNN.
- Hierarchical nature, learn the patterns by describing complex patterns from simple ones.

### Ways to visualize features
- input occlusion
- MAP
- Activation maximization

### optimizers & learning rate
Adam: adaptive momentum, combines two ideas to converge. Pre-parameter which give fast convergence, and momentum which helps to avoid getting stuck in saddle point.

BGD， SGD， MBGD: Batch gradient decent, Stochastic Gradient Descent, mini batch grident decent. 
- BGD: calculate the grident of whole batch, slow, and maybe get to local mini point. **No need to shuffle**, then.
- SGD: choose one example to calculate. Fast and possible to get the global mini point. Can be stuck in the saddle point. Has a big variance of cost function and sensitive to noise.
- MBGD: take a mini batch from batch. A compromise method of SGD and BGD. Both SGD and MBGD need to **shuffle**.

**LR**: it's recommended to try a logarithmic scale to optimize the LR. 

### Data augumentation
A technique to increase the input data by ferforming some process on the original data. Like Flipping, rotation, crop, Blur, add noise. 


### Classical Networks
- GANS: Generative adversial networks, generator generate objects, like image and discriminator make the judge that whether a input image is an authentic image or a generated image. These two modules are competing each other. Same idea here in LSTM. But LSTM has a internel pipeline for storing informations after a long pass. 

- RNN, Recurrent Neural Networks (RNN): Addition of a loop at each node. This brings recurrence in RNNs. For a sequential input, model process current input is influenced by previous output and this output will also be one of input for the next sequential input. It will capture the relationship between sequential inputs.


### end-to-end learning
a model takes raw data as input and output the desired outcome.


### activate function, Non-linear

**why we need activation**: without activation, it's just linear functions, and linear model cannot find out the complex pattern inside data.


- ReLU: output non-negative results, 
  - Advantage: solve gradient vanish/explotion problems, easy to calculate
  - Disadvantage: negative gets 0, cannot activate some neurons.

- Sigmoid: [0, 1]二分类， probability produced by *sigmoid* is independent, results can be multiple labels.
- softmax: [0, 1]多分类, the sum of produced probabilities is 1. It's the chance of each class. Results can only be one class.
- tanh: [-1, 1],similar to sigmoid but more symmetric. 

detail of *sigmoid* and *softmax*, check [The Differences between Sigmoid and Softmax Activation Functions](https://medium.com/arteos-ai/the-differences-between-sigmoid-and-softmax-activation-function-12adee8cf322), [sigmoid and softmax](https://www.cnblogs.com/jins-note/p/12528412.html).

### Transfer learning
Continue to train, or start training based on a pretrained model.

Need to think, how many layers to keep, to add, and to freeze.

### Overfitting problem
- Drop out: 
A trick of regularization for **avoid over-fitting**. Randomly stop some neurons in the hidden layers.

    The regularization inside is we will turn off a part of the model. And finally get an average model.

- L1/ L2 regularization

- data augumentation

- early stop


### weights and bias
- same initial weights: same value after every propagation. No learning at all. Underfitting.


### Supervised and unsupervised learning
Unsupervised learning: Word embedding, Bag of words.


### Transfer learning
Using pretrained model has become the norm in research and industry. We don't need to retrain the whole model but using it to fit our special tasks.
Used pretrained model in internship.


