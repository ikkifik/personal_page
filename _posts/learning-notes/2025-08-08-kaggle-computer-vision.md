---
layout: posts
title: "Kaggle: Computer Vision"
date: 2025-08-08
category: Learning-notes
---

- ***Convolution** is the mathematical operation that gives the layers of a CNN their unique structure.*
- *A CNN used for image classification consists of two parts: a **convolutional base** and a **dense head***
- The goal of the network during training is to learn two things:
	1. which features to extract from an image (base),
	2. which class goes with what features (head).

**Preparing Conv. Base part**
- CNN are rarely trained from scratch, instead we use what is called pre-trained model. Reusing pre-trained model is a technique we called transfer learning, we reuse the part of a network that has already learned (trained).
- ImageNet is a common dataset used for training computer vision model. Then we use a model that pre-trained on ImageNet, called VGG16.
- Base part uses for feature extraction
- We can use `.trainable` attribute on loaded pre-trained model to turn off its function to retrain the base (pre-trained).

**Preparing Dense Head part, or the DNN part**
- Similar with what we've done in previous classifier, we use Dense (hidden) layer to perform prediction.
- We apply Flatten layer to transforms 2-D outputs of the base (pre-trained) into 1-D inputs needed by the head.

- We can actually use the pre-trained model without fine tuning needed, we use it *off-the-shelf* along with the head (DNN) part.
- Fine-tuning is a term of we re-train a pre-trained model with new data

---
- There are 2 common yet important layers we typically find in convolutional image classifier, they're **convolutional layer with ReLU activation**, and **maximum pooling layer.**
- *The **feature extraction** performed by the base consists of **three basic operations**:*
	1. ***Filter** an image for a particular feature (convolution)*
	2. ***Detect** that feature within the filtered image (ReLU)*
	3. ***Condense** the image to enhance the features (maximum pooling)*

**Kernels**
- The **weights** primarily contained in convolutional layers, it's called **kernels**.
- Kernels == weights
- *a kernel will act sort of like a polarized lens*, the value forms as a matrix.
![Kernel: Edges](/assets/images/posts/learning-notes/kaggle-computer-vision/kernel-edges.png "Kernel Edges Illustration"){: .post-figure }

- The kernel set up how convolutional layer connect to the layer that follows.
![Sliding window kernel](/assets/images/posts/learning-notes/kaggle-computer-vision/sliding-window-kernel.png "Sliding Window Kernel Illustration"){: .post-figure style="width: 300px"}

- *The kernel above will connect each neuron in the output to nine neurons in the input.*
- To form connection with nine neurons, we set the dimension using `kernel_size`.

**Feature maps**
- The **activations** in the network we call **feature maps**.
- we use `filters` parameter to define how many feature maps we want to create as an output.

Conclusion so far: to do feature extraction, in the convolution and ReLU course we learned 2 steps of methods a CNN uses: filter with convolution (defining kernels(weights) with tensor constant, then creating feature maps (activation)), and detect with _rectified linear unit_ or ReLU is an effort to *(ChatGPT) suppress unimportant values in a feature map by setting negative values to zero.*

**ReLU** = `f(x) = max(0, x)`

- It **removes negative values**, which the network may interpret as **less important or irrelevant**.
- Positive values (which can represent detected features) are **kept**.
- ReLU acts like a **filter that says “only keep what’s useful”**    
- Negative values → **zeroed out**    
- Positive values → **passed through unchanged**

 - There are several other kernels constant already served for us to use, just kindly search it on internet or google it.
 - *In general, a kernel can have any number of rows and columns.* It doesn't always 3x3 kernel.

---

- **Condense** == memadatkan
- Condense, meaning to make the detected features more appears by upscaling to maximize value of a group of pixels. *To retain only the most useful part -- the feature itself.*
- ***Max pooling** takes a patch of activations in the original feature map and replaces them with the **maximum activation** in that patch.*
- There is also a term **average pooling**, which averages patches of the feature map.

![Max Pooling](/assets/images/posts/learning-notes/kaggle-computer-vision/max-pooling.png "Max Pooling Illustration"){: .post-figure style="width: 500px"}

- `tf.nn.pool` == `MaxPool2D`
- Oversimplify, max pooling does condense similar to up-scaling pixels, make the pixels bigger by using the maximum value of map(?).
- Invariance? created by max pooling?
- **translation invariance**, how many pixels in a map shifted, 4x4 is larger than 64x64, as we may notice on above figure.

---
- **Flatten layer, used to make the multidimensional input one-dimensional,** commonly used in the transition from the convolution layer to the full connected layer. (TensorSpace)
- (ChatGPT) **"Reduced parameter size"** means **fewer trainable weights** in convolutional networks compared to dense networks. This is one reason why convolutional networks are more **efficient*, especially for image data. 

ChatGPT answers:
- **Dense layers** connect **every input node to every output node**, which creates **a lot of parameters**.
- **Convolutional layers** use **filters (kernels)** that slide over the input with **shared weights**.
- This **weight sharing** drastically reduces how many parameters are needed.

---
### The Sliding window
- `strides` = steps, how far the window moves at each step
- `padding` = how we handle the pixels at the edges 
- *Whenever the stride in either direction is > 1, the sliding window will skip over some of the pixels in the input at each step.* Therefore, in convolutional layers it's often to use `strides=(1,1)`. In contrast with pooling layers, it's usually use stride value > 1, such as (2, 2) or (3, 3), but not larger than the window itself.
- Having a large stride on convolutional layers, better be coupled with a larger kernel. For instance, in ResNet50 model, it uses 7x7 kernel and stride = 2 in its first layer.

---
### Data augmentation
- is a way we expand our dataset in order to improve our model to learn by creating 'fakes' data, which in this course is images. 
- When we create different 'condition' of a data: rotating, skewing, contrast, brightness, etc; we basically expanding our image from one image to more based on what transformations we applied.
- But keep in mind that we cannot do this for every cases, for example like digit recognizer, we cannot apply rotation as number '6' and '9' would mix up.
- There is a new terms in layering, that's **preprocessing layers**. Where we able to apply several things to transform our dataset right before we do the convolutional activation layer.