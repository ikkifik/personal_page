---
layout: posts
title: "Kaggle: Intro to Deep learning"
date: 2025-08-05
category: Learning-notes
---

- Deep learning is an advancement of Machine Learning, it doesn't differs in terms of usage. DL can also be used for regression and classification problems.
- _**Deep learning** is an approach to machine learning characterized by deep stacks of computations._
- **Neural networks** (NN) are composed of **neurons**, each neurons performs a simple computation. So the power of NN comes from the complexity of the neurons connection forms.
- Neuron == Unit
- As previously mentioned, the power of NN is the **connection** of neurons. The connector contains **weight**, where each time there is an input it multiplied with the weight. Therefore, *a neural network "learns" by modifying its weights.*

![Linear Unit](/assets/images/posts/learning-notes/kaggle-intro-to-dl/linear-unit.png "Linear Unit Illustration"){: .post-figure }

- *For the input `x`, what reaches the neuron is `w * x`.*
- **Bias** is a special kind of weight, it doesn't have any input data, so we just put it 1. The purpose is so that the neuron can modify the output independently of its input.
- To get the output, neurons using what is called *neuron's activation*, that is a formula `y = w * x + b`, or as a formula `y = wx + b`. We know it on math, it's a linear equation, where *w* is the slope and *b* is the y-intercept.
	- `y` = output
	- `x` = input
	- `w` = weight
	- `b` = bias
- *Single neuron models are linear models.*

**Multiple inputs**
![Multiple input linear unit](/assets/images/posts/learning-notes/kaggle-intro-to-dl/linear-unit-multi.png "Multiple input linear unit Illustration"){: .post-figure }


- *We can just add more input connections to the neuron, one for each additional feature.*
- The formula for this neuron would be `y= w0x0 + w1x1 + w2x2 + b`.
- `(ChatGPT) The bias is not counted as an input. It’s a separate term.`
- `(ChatGPT The **bias** is not counted as an input (it's a constant) but shifts the hyperplane.`
- A linear unit with two inputs (input x1 and x2) will fit a plane (formula: y = w₁·x₁ + w₂·x₂ + b).
- A unit with more inputs (input x1, x2, x3,... xn) than that will fit a hyperplane (formula: **y = w₁·x₁ + w₂·x₂ + w₃·x₃ + ... + wₙ·xₙ + b**) or (formula: y = Σ wᵢ·xᵢ + b).
- This defines a **hyperplane** in n-dimensional input space.
- A **hyperplane** is the higher-dimensional generalization of a line (in 2D) or a plane (in 3D).

Code example for analogy of measuring calories (output) with combination of sugars, fiber, and protein (input):
```
from tensorflow import keras
from tensorflow.keras import layers

# Create a network with 1 linear unit
model = keras.Sequential([
    layers.Dense(units=1, input_shape=[3])
])
```
Becomes
```
calories = keras.Sequential([
	// units=1, means there is only one neuron
	// input_shape=3, for the model accept sugar, fiber, and protein as input
    layers.Dense(units=1, input_shape=[3])
])
```

> **Why is `input_shape` a Python list?**  
> The data we'll use in this course will be tabular data, like in a Pandas dataframe. We'll have one input for each feature in the dataset. The features are arranged by column, so we'll always have `input_shape=[num_columns]`. The reason Keras uses a list here is to permit use of more complex datasets. Image data, for instance, might need three dimensions: `[height, width, channels]`.

---
- In Keras, weights of a neural network represented as tensors
	- `(ChatGPT) All **weights** are stored in **tensors**, but Not all **tensors** are weights (they could be inputs, outputs, gradients, etc.) Think of a **weight** as a **role**, and a **tensor** as a **container**.`
- *Tensors are basically TensorFlow's version of a Numpy array with a few differences that make them better suited to deep learning*
- *Before the model is trained, the weights are set to random numbers (and the bias to 0.0). A neural network learns by finding better values for its weights.*
- Tensors are data structure!
- `(ChatGPT) Tensors are data structures that store numbers in 0D, 1D, 2D, or more dimensions. They are the fundamental building blocks of data in deep learning.`
	- Scalar (0D) -> ()
	- Vector (1D) -> (3,)
	- Matrix (2D) -> (2, 3)
	- 3D Tensor -> (2, 3, 4)
	- n-D Tensor (n, ...)

---
- Building Deep Neural Networks, is based on the idea of _modularity_, *building up a complex network from simpler functional units.*
- Combine and modify the linear units (single) to model complex relationship
- **Layers** is an organized neurons.
- **Dense layer** is a collection of linear units having a common set of inputs.
- *In Keras, a layer can be, essentially, any kind of data transformation*
- Layers such as **Convolutional** and **Recurrent**, basically *transform data through use of neurons and differ primarily in the pattern of connections they form*
- The activation function == nonlinear approach to add in-between each layers, otherwise NN can only learn linear relationships
- *An **activation function** is simply some function we apply to each of a layer's outputs (its _activations_).*
- *The rectifier function has a graph that's a line with the negative part "rectified" (diperbaiki) to zero.*
- ![A graph of the rectifier function. The line y=x when x>0 and y=0 when x<0, making a 'hinge' shape like '_/'.](https://storage.googleapis.com/kaggle-media/learn/images/aeIyAlF.png){: .post-figure }

- Applying Rectified to a linear unit becomes **rectified linear unit** or **ReLU**. Hence, the formula becomes `max(0, w * x + b)` or `max(0, wx + b)`
![Linear unit with relu](/assets/images/posts/learning-notes/kaggle-intro-to-dl/linear-unit-relu.png "Linear unit with ReLU Illustration"){: .post-figure }



- *The layers before the output layer are sometimes called **hidden** (layer) since we never see their outputs directly.*
- The final output layer is a linear unit (meaning, no activation function), that makes it's appropriate for regression task, where we're trying to predict some arbitrary numeric value. *Other tasks (like classification) might require an activation function on the output.*

Code example:
```
from tensorflow import keras
from tensorflow.keras import layers

model = keras.Sequential([
    # the hidden ReLU layers
    layers.Dense(units=4, activation='relu', input_shape=[2]),
    layers.Dense(units=3, activation='relu'),
    
    # the linear output layer 
    layers.Dense(units=1),
])
```
- the first layer gets the input, the last layer produces the output
- To add an activation function to a layer, just give its name in the `activation` argument.
- complex == non-linear

---
- *A "loss function," measures how good the network's predictions are (disparity between the the target's true value and the value the model predicts.).*
- *An "optimizer," to tell the network how to change its weights.*
- A common loss function for regression task is **Mean Absolute Error (MAE).** The model use loss function *as a guide for finding the correct values of its weights (lower loss is better).*
- *The optimizer is an algorithm that **adjusts the weights to minimize the loss.***
- Essentially all of the optimization algorithm in deep learning is based on stochastic gradient descent. It's an iterative algorithms that train a network in **steps**.
- *One **step** of training goes like this, loop until the loss as small as needed or until it won't decrease any further:*
	1. *Sample some training data and run it through the network to make predictions.*
	2. *Measure the loss between the predictions and the true values.*
	3. *Finally, adjust the weights in a direction that makes the loss smaller.*

- (ChatGPT) Understanding the differences between step, batch, and epoch; :
	- **10,000 samples ÷ 100 samples/batch** = **100 batches**
	- **1 batch** = 100 samples
	- **1 step** = processes **1 batch**
	- So you’ll have **100 steps per epoch**
	- After completing those 100 steps → that’s **1 epoch**
- **Explanation**: imagine there's 10,000 of data or samples, we set for each process 100 samples, we called it 1 batch. Let say we apply division (10,000 / 100 samples), then to process the entire data, we need 100 batch. Each batch is going through 1 step (above 3 process in 1 round). Because we have 100 batch (or chunk/split of data), we absolutely have 100 steps to go. Lastly, the entire of process we obtain 1 epoch.
- The size of a small shift in the direction of each batch is determined by the **learning rate**.
- ***Adam Optimizer** is an SGD algorithm that has an adaptive learning rate that makes it suitable for most problems without any parameter tuning (it is "self tuning", in a sense). Adam is a great general-purpose optimizer.*


---
- **Signal**, is the part that generalizes, the part that can help our model make predictions from new data. The Part that we need.
- Noise, is that part that is _only_ true of the training data; it's a pattern that just added randomly that comes from dataset during training. The part we don't need.
- During training model which produces training loss, both signal and noise are mixed, yields a curve that goes down. In contrast, when it applies to validation loss, it only goes down when it learns signal, when it comes to gap, the curve will make a gap between training loss and validation loss.
- To prevent a large gap between training loss and validation loss, we can apply early stopping method, where we interrupt the training process once it *seems the validation loss isn't decreasing anymore.*
- Set the epoch more than we need, to prevent **overfitting** where the model learns too long, and to prevent **underfitting** where the model hasn't learned long enough. So, let the Keras do the work with early stopping.

- **Underfitting**, is when the model isn't learn enough data, resulted bad score even in training set 
- **Overfitting**, is when the model got a good score in training evaluation, but cannot predict new data.

---
- Dropout, shuting off neurons
- Batch normalization, performs a kind of coordinated rescaling of its inputs. Can be used for increasing optimization process as it tend to *need fewer epoch*.
- Batch normalization *adaptively scaling the data as it passes through the network, batch normalization can let you train models on difficult datasets.*

---
- Using cross-entropy to obtain probability before applying it into loss function, in classification task.