# Computer Vision Cheat sheet

- [Computer Vision Cheat sheet](#computer-vision-cheat-sheet)
  - [What Computer Vision is](#what-computer-vision-is)
  - [Computer Vision Model](#computer-vision-model)
  - [Computer Vision History](#computer-vision-history)
  - [Neural Networks](#neural-networks)
    - [Neural Network Types](#neural-network-types)
      - [Convolutional Neural Network](#convolutional-neural-network)
    - [Neural Networks Training](#neural-networks-training)
      - [Three steps of training](#three-steps-of-training)
      - [Backward pass](#backward-pass)
        - [Gradient Descent and its importance](#gradient-descent-and-its-importance)
        - [Gradient Descent computation](#gradient-descent-computation)
        - [Backpropagation](#backpropagation)
      - [Optimizer](#optimizer)
  - [Computer Vision Tasks](#computer-vision-tasks)
    - [Image Classification](#image-classification)
      - [Image Classification Data sets](#image-classification-data-sets)
      - [Image Classification Neural Network Models](#image-classification-neural-network-models)
    - [Object Detection](#object-detection)
    - [Image Segmentation](#image-segmentation)
      - [Semantic Segmentation](#semantic-segmentation)
        - [Semantic Segmentation Data sets](#semantic-segmentation-data-sets)
        - [Semantic Segmentation Neural Network Models](#semantic-segmentation-neural-network-models)
      - [Instance Segmentation](#instance-segmentation)
  - [Frameworks](#frameworks)
    - [Apache MXNet](#apache-mxnet)
      - [Imperative vs Symbolic Programming](#imperative-vs-symbolic-programming)
  - [Toolkits](#toolkits)
    - [GluonCV](#gluoncv)
      - [GluonCV model types (Model Zoo)](#gluoncv-model-types-model-zoo)

## What Computer Vision is

- Computer vision is a technological field concerned with extracting high level understanding from digital images or videos for various applications.
- The concept of computer vision is creating software systems that can process, analyze and make inferences from digital images.
- The goal is to extract the numerical or symbolic information from image inputs.
- Computer vision is often considered a sub field of artificial intelligence.

## Computer Vision Model

- A model refers to a function takes in an input and returns an output. The output of a function depends on the parameters that constitute the function and how they interact with the input.
- In computer vision, a model is a function that takes in an image and generates certain predictions.
- The class of functions that work well in computer vision tasks are neuron networks. Specifically, convolutional neural networks.
- Different tasks generally require different predictions. So you need different models for different tasks. However, even for the same tasks such as image classification, you might still need different model architectures. That's usually the trade off between each model's prediction accuracy, and computational resource consumption. A more complex model might perform better in terms of higher accuracy. But you'll also most likely require larger memory and longer computational time.

## Computer Vision History

- The field of computer vision emerged in the 1960s. It originated in universities that were building on the early success of AI which began a decade earlier.
- The Nobel-Prize-winning jewel David Hubel and Torsten Wiesel, conducted key research in mammalian neurobiology. They established that processing in the visual cortex of the brain starts with neurons that respond to simple structures like edges before those that respond to complex patterns. A few years later, this inspired Kunihiko Fukushima, a Japanese scientist to build an artificial network of self-organizing cells that could hierarchically recognize patterns in digital images.
- This is called artificial framework, the neurocognition. This networks are now called convolutional neural networks or CNN's.
- A few years after the neurocognitive was developed, Yann LeCun a friend's scientists applied machine learning techniques to train a neural network architecture called LeNet. LeNet was successful and it was deployed to recognize zip codes and process bank checks.
- After LeNet, computer vision progress stalled for awhile because more expressive network architectures were difficult to train.
- In 2012, there was a resurgence due to the availability of more powerful computer resources, hardware accelerators like GPUs and large datasets thanks to the Internet.
- The subfield of deep learning grew and dominated accuracy benchmarks for computer vision tasks.
- Now, all the state of the art resulting computer vision are achieved using deep learning.

## Neural Networks

![Neural Network](CV%20images/Neural-Network.png)

- Many forms of neural networks exist, but one of the fundamental networks is called the Fully Connected Network. It's called fully connected, because all layer inputs are connected to all layer outputs.
- The input image is represented and past the network as composition of pixels, and each pixel of an RGB image will have three values that encode the intensity of the red, green, and blue colors.
- With fully connected networks, all of the pixels are flattened for the first fully connected layer. As a result, all of the spatial information of the pixels is lost, and the network will have to relearn the spatial relationships between pixels during the network training. Small horizontal and vertical shifts in the input can be a real challenge for this type of network.
- Our first fully connected layer has four input units, corresponding in four input pixels in this example, and three output units. And the connections between the units are weighted.
- The weights of the connection can be positive or negative. This weighted connections are called Network parameters that can be tuned to achieve the best results.
- We'll compute the intermediate values and use them as inputs to the second fully connected layer with two output units.
- Our last layer has three output units because we have three classes. And we make a final prediction from the values of these output units.
- We can break the learning process into three stages. Forward Pass, Backward Pass, and Update Step.
  - Forward Step is applied to all units in the network, and it consists of two steps:
    - Step one is by summing up the contributions of each of the input units. Contributions consists of the value of the input multiplied by the weight of the connection.
    - Step two is applying activation function.
      - It is a critically important step.
      - A non-linear function is applied.
      - It is called activation because it controls how active the unit is, given the total input contributions.
      - One simple choice of activation function is Sigmoid function. With large contributions from the input, the Sigmoid function return a value close to 1, and it can be said that the unit is activated.
      - Using an activation function gives the network ability to learn nonlinear patterns in the data. As non-linear relationships can be modeled.
    - The final activation can depend on multiple factors. It depends on the activations from the previous layer, and the connection weights between units. But the activations from the previous layer depend on the layer before that.
  - Backward Step is to improve the network's performance:
    - When learning parameters from scratch, you begin by randomly initializing the parameters and then improve them slightly one small step at a time.
    - It can be improved by the loss function, that measures the performance of our network. It takes the network predictions and compare them to the ground truth labels. Returning a score that's often called the loss.
    - When the predictions are similar to the labels, the loss will be small. So during training we try to minimize the loss.
    - A loss function is always chosen to be differentiable so that we can calculate the gradient of the loss with respect to every parameter of the network.
    - We start by calculating the gradients of the parameters in the last layer. Once we know the gradient for each parameter, we know how to change each parameter to slightly reduce the overall loss.
    - Before updating these parameters, we need to calculate the gradient for all other parameters of the network. We work backwards through the network as part of a process called Back Propagation.

$$\begin{bmatrix}
  -1 & 0 & 1 \\
  -1 & 0 & 1 \\
  -1 & 0 & 1
\end{bmatrix}$$

### Neural Network Types

#### Convolutional Neural Network

- It is much more common in practice than Fully connected Neural Network, due to its limitations. One of the limitations is fully connected layer treats every pixel independently of its original spatial position and another one is the large number of parameters that need to be learned which takes large memory and slows the computation speed.
- Convolutional neural networks learn local patterns from small neighborhoods of pixels, unlike fully connected networks that learned patterns across all pixels of the image. It's possible to learn large-scale spatial relationships by stacking convolutional layers and learning a hierarchy of features.
- The first convolutional layer might learn to extract edges. The second might combine these edges to learn to extract textures. The final convolutional layer might combine these textures and learn to extract body parts.
- It consists of two operations, convolution operation and the max-pooling operation.
  - Convolutional layer just applies the **Convolutional operation**.
    - A first component of the convolution operation is the **kernel** or filter.
      - It's usually a small, square matrix, and its size and shape define the neighborhood of pixels that will be considered when learning patterns or features to extract.
      - These parameters are randomly initialized at the start of training, and will be optimized during training.
      - The kernel is used many times over as part of the convolution operation, and it's applied in a sliding window fashion. Starting in the top-left corner of the input, we can calculate the value in the top-left of the output. We take each value from the input and multiply it by the corresponding value in the kernel.
    - Our second step in the process is to add up all of these intermediate values and obtain a final output value.
    - Computation for each window doesn't have to be sequential though. One advantage of the convolution operation is computational efficiency because each window can be processed in parallel.
    - We can lose outputs around the edge because the kernel is smaller than the input. We compensate for this effect by padding the input to obtain an output with the same size as the input. Zero is a common choice for padding value. But all of this is handled for you with MXNet operators and blocks.
    - Just like with fully connected parameters, we randomly initialize the parameters,and then optimize their values using stochastic gradient descent. We calculate the gradients and then shift the parameter slightly, one small step at a time.
    - In practice, you'll need to use multiple kernels to extract multiple image features, and kernels are typically multichannel, not just single channel.
  - One key component for creating hierarchical feature extractors is the **max-pooling** operation.
  - When combined with stride, it's an effective way to reduce the spatial dimensions of the input.
  - When the spatial dimensions are reduced, the memory footprint of the model is also reduced, which means more features can be extracted.
  - Another advantage of max-pooling is that it can introduce a certain amount of invarianced rotation, which is a useful characteristic for most real-world computer vision tasks.
  - So, how max pooling works. We find the maximum value from the values in this window and use this for the output. It's common to apply max-pooling with stride. So instead of moving the window one pixel at a time, we move the window two pixels at a time in each direction. As a result, we half the amount of output values in each dimension. When adding this after our convolution, we can reduce the spatial dimensions by half.

### Neural Networks Training

- The general procedure to train neural networks involves an algorithmic technique called backpropagation.

#### Three steps of training

- Neural network training consists of repeating three simple steps over and over until the parameters of the model converge to a good solution.

  1. First step is know as Forward step:
     - It involves passing the data through the model to obtain the output, also called the model prediction.
     - The model prediction is then compared to the ground truth label via a loss function which gives an estimate of how well our model is performing at the current task. The model loss is what we want to minimize during neural network training.
  2. The next step is the backward step:
     - This involves computing the gradient of the loss function with respect to the parameters of the network. Typically, this is done in reverse.
     - The gradient of the loss with respect to the last layer parameters are computed first and then the upstream gradients are computed recursively using the chain rule.
     - Computing the gradients this way is efficient and is what makes training deep neural networks computationally tractable.
  3. The final step is the optimize or optimization step:
     - In this step, we use the gradients computed from the backward step to update the model parameters in a way that improves the model and minimizes the loss.
     - Repeating these steps several times causes the model parameters to evolve towards a good solution during model training.

#### Backward pass

##### Gradient Descent and its importance

- The gradient of a function at a given point is the value of the first derivative of the function at the point.
- Visually, you can think of the gradient as the slope of a tangent line to the function at that point.
- For a function that depends on more than one parameter, you can express the gradient of the function with respect to each parameter as a vector.
- The gradient of the function at the point gives the direction of steepest increase, this means that the negative gradient gives the direction of steepest decline. Therefore, by following the direction of the negative gradient, you eventually arrive at a local minimum for that function.
- This procedure is what is known as gradient descent, and was introduced by French mathematician, Augustin Louis Cauchy in the middle of the 19th century.

##### Gradient Descent computation

- For simple functions, you can compute gradients analytically by taking advantage of the product rule or the quotient rule from differential calculus. However, for complex functions like the last functions of deep convolutional neural networks, that are the results of complex chained operations, computing the gradients analytically in one go is not feasible so we turned to automatic differentiation.
- Automatic differentiation is a way to numerically compute the derivatives of a function at a point. It takes advantage of the fact that any function that can be expressed as a computer program will execute a sequence of arithmetic operations and simple functions with known derivatives.
- Typically automatic differentiation proceeds by recording the operations to build a computational graph of the function. Then, it repeatedly apply the chain rule to the operations in the computational graph to compute the derivatives.

##### Backpropagation

- Backpropagation is an efficient algorithm for training neural networks that uses automatic differentiation and dynamic programming to update the network parameters.
- The three-step iterative process to train neural networks that was introduced earlier is informed by the backpropagation algorithm.
- For backpropagation to be effective, we store in the forward pass the intermediate outputs of the hidden layers of the neural network, and then the value of the loss function as well.
- In the backward pass, we use the chain rule to compute the gradients of the lastly first, working backwards from the loss to the input layer.
- During the backward pass, we use the stored intermediate outputs and gradients of later layers to compute the gradient of earlier layers. Once we obtain the gradient for all parameters, the gradients are then used to improve the parameter values.

#### Optimizer

- It is an implementation of a gradient descent algorithm that is responsible for performing a updates step to the model parameters.
- An optimizer updates the model parameters to minimize the loss and improve the model. It does this by nudging the parameter step by step towards values that minimize the loss function. This improves the model accuracy or the performance metric.
- Optimizers used in deep learning are almost always implementations of a variant of the gradient descent algorithm. However, it is possible to have optimizers that are not directly based on gradient descent.
- Optimizer use the gradient to an approximation of the gradient. The gradient here is that of the loss with respect to the current parameter values. But sometimes optimizers also use previously recorded historical parameters or gradients.
- Different optimizers have different rates of convergence for the same learning task.
- One simple example of an optimizer is stochastic gradient descent.
  - Stochastic Gradient Descent is a variant of the gradient descent algorithm. A general purpose function minimizer.
  - In Stochastic Gradient Descent, only a subset of the data, called the minibatch is used during the forward pass and backward pass. And that every iteration, the model parameters are updated using only the error signals from the current subset of the data. This means that the lost is computed using the outputs of the model on one minibatch of data.
  - This minibatch last gradient provide an approximation of the full batch last gradient that is less computationally intensive but still guarantees convergence to a minimum.
  - Once the minibatch last gradients are computed the parameters of the model updated according to the same update rule as gradient descent, by going in the direction of the negative gradient.
- The LR term is what is known as the learning rate.
  - Learning rate is a hyper parameter that controls how big of a step the optimizer takes to update current parameters in the direction of the negative gradient.
  - A hyper parameter, is a parameter that is not strictly part of the model, or learned during model training but still affects overall model performance.
  - The learning rate can be tweaked as necessary to fit different stages of the training process according to predefined schedule. One popular technique is to the learning rate by a little bit as training progresses. Based on the intuition that at later stages of training the model, parameters are close to the optimal values and only need to change ever so slightly.
  - In addition, some optimizers use an adaptive learning rate technique where each parameter gets its own learning rate.

## Computer Vision Tasks

### Image Classification

  ![Image Classification Example](CV%20images/Image-Classification.png)

- A model solve this task by providing a level output that corresponds to the class dog when fed the image input.
- Image classification models are trained using images annotated with pre-specified classes and they learn to associate those class labels to the images.
- A severe limitation of image classification is made apparent in image with multiple objects because no matter what class the model assigns this image to, the results will be unsatisfactory.

#### Image Classification Data sets

- CIFAR-10:
  - It was released by the Canadian Institute for Advanced Research known as CIFAR in 2009.
  - It has 10 basic classes including cars, cats and dogs, and current state of the art models obtain around 98 percent accuracy.
  - it's unlikely you'll want to use models pre-trained on CIFAR-10 for practical applications.
  - Another characteristic of this dataset is the low resolution of the input images. At 32 pixels by 32 pixels, there's a limited amount of information being passed to the network.
- ImageNet:
  - t was released by researchers at Princeton University in 2009, and it currently has around 14 million images, and 22,000 classes that are organized in wordnet hierarchy.
  - Models are usually pre-trained on a more manageable subset of the data though.
  - The full dataset is referred to as ImageNet22k, and the subset as ImageNet1k.
  - Instead of 22,000 classes, the subset has 1,000 classes and flattens the hierarchy. Instead of 14 million images, it contains one million images.
  - Most references to ImageNet refer to the ImageNet1k dataset because this was used for the popular large-scale visual recognition challenge from 2010-2014.

#### Image Classification Neural Network Models

- One of the most popular architectures is ResNet.
- MobileNet is unsurprisingly a good choice for mobile phone deployments.

### Object Detection

  ![Object Detection Example](CV%20images/Object-Detection.png)

- Unlike image classification, with object detection, we can have multiple objects from different classes in the same image.
- The task localizes the objects with boxes on the input image and for each localization it classifies the object in the box. Also, the model assigns a name to each box.
- However, the box is not accurate enough, because objects are usually not shaped like rectangular boxes.
- It's got a wide range of practical applications. Everything from medical image analysis to collision avoidance systems, and self-driving cars.
- Some models work well for images with a large number of objects. Other models work well for images with objects of different sizes.
- GluonCV has a comprehensive selection of neural network models in a GluonCV Model Zoo, and they've been pre-trained on publicly available data sets with over 100,000 images and over 800,000 labeled objects across 80 pluses.
- There are specific datasets that can be used for pre-training object detection models.
  - Pascal VOC:
    - It was created for the visual object classes challenge, around from 2005-2012.
    - A first iteration of the dataset was released in 2005 with few images and labels. Over the following years, more images and object classes were added.
    - GluonCV object detection models are pre-trained on the union of the 2007 and 2012 versions of the data set, which in total gives around 20,000 images and 50,000 labeled objects.
    - Models that have been pre-trained on Pascal VOC can only detect and classify objects from this set.
  - COCO stands for Common Objects in Context:
    - It has six times as many images as Pascal VOC and 18 times more labeled objects in the images.
    - GluonCV pre-trained models used the 2017 version of the object detection dataset.
    - COCO has 80 object classes covering a wide range of categories.
    - All of the Pascal VOC classes are included in COCO, but there's better coverage on sports, foods, and other common household objects, such as beds, refrigerators, and books.
- Neural network models that can be used for object detection. There are three main options for model architecture Faster R-CNN, SSD and YOLO.
  - The model is not the only choice, the architecture used to extracting the image features is important as well.
  - Using Faster R-CNN with ResNet as an example, this architecture is an extension of ResNet with additional components that are specific to object detection. ResNet is called the base network or backbone in this context.
  - Model accuracy is an important consideration. A model will never predict the bounding box of an object exactly. You define a threshold in terms of the overlap required for a successful object detection. All of this goes into a metric called Mean Average Precision or MAP.
  - Higher MAP is better but this comes at a cost in terms of reduced speed of the network and increase consumption.
  - You can find the latest statistics for models in the GluonCV Model Zoo on a GluonCV website. You can select detection from the Model Zoo dropdown, and then use the interactive plot to evaluate different models.

### Image Segmentation

- Image segmentation is a parent term for two sub-tasks semantic segmentation, and instance segmentation.
- Image segmentation techniques can be useful when trying to understand the details of an image. Unlike image classification that makes a high level prediction about the whole image, image segmentation make low level predictions.
- The objective of semantic segmentation is to classify every pixel of the image.
- A model will take a pixel and classify the particular pixel assigning probabilities to every one of the classes.
- Good segmentation models will look at the full context of the image before making pixel level predictions.

#### Semantic Segmentation

- Semantic segmentation generates a mask on objects so that every object has a boundary and is separated from the background. This requires predicting a class for every pixel in the image.
- Semantic segmentation can tell objects from the background and it can also tell objects in one class from objects in a different class.
- For objects in the same class like the two dogs, it cannot tell the difference.

    ![Semantic Segmentation Example](CV%20images/Semantic-Segmentation.png)

##### Semantic Segmentation Data sets

- Pascal VOC:
  - It was created for the visual object classes challenge. Although the challenge run from 2005 to 2012, segmentation wasn't added as a standard challenge until 2009.
  - GluonCV semantic segmentation models a pretrained on the 2012 version of the data set that has 2,900 images and 6,000 segmented objects.
- COCO:
  - Compared to Pascal VOC, it's a much larger and much more comprehensive data set with 123,000 images.
  - This data set is used for both semantic segmentation and instance segmentation pretraining.
  - One difference when using COCO for object detection, semantic segmentation, and instance segmentation is the number of classes used for pretraining.
  - Although 80 classes are labeled, semantic segmentation models only use 20 classes, specifically the same classes that are used for the pascal VOC data set. On the other hand, object detection and instance segmentation models use all 80 classes.
- ADE20K:
  - It was released in 2016 by researchers from MIT.
  - Models pretrained on ADE20K users 140 classes in total. Many types of objects are included as well as many things that could be classed as background in other data sets such as sky, floor, and sidewalk.

##### Semantic Segmentation Neural Network Models

- There are three options for model architecture: FCN, PSP, and DeepLab.
- These architectures use base networks such as ResNet to extract useful image features. Some modifications to the ResNet architecture are required for improved performance on semantic segmentation tasks. After feature extraction, there are a number of different approaches to segmentation.
- DeepLab model with a ResNet 101C backbone:
  - After been trained on the ADE20K data set, the modal obtains a pixel accuracy of 81.1 percent. It can process 15 images per second with an NVIDIA V100 GPU, and it consumes 1.7 gigabytes of memory.
- FCN model with a ResNet 50C backbone:
  - It's not as precise with a pixel accuracy of 79 percent. But it's about twice as quick processing around 30 images per second on the same GPU.
Memory usage between these is very similar.

#### Instance Segmentation

- Instance segmentation generates masks for segments or objects in the image as well as separate different instances even if they are in the same class.
- That approach has multiple drawbacks.
  - First, each object in one image must be labeled manually to get a mask to learn from. Creating a pixel mask is much more expensive than assigning the name.
    ![Instance Segmentation Example](CV%20images/Instance-Segmentation-Labeling.png)
  - Simple algorithms run faster. If you don't need fine level information, you should not choose an overly-complex model.  

    ![Instance Segmentation Example](CV%20images/Instance-Segmentation.png)

## Frameworks

### Apache MXNet

- MXNet is a deep learning framework that provides the software tool for building and training neural network models for computer vision and other applications.
- It has multiple features that make it a desirable deep learning framework.
  - It is scalable,
  - debuggable,
  - and flexible.
- MXNet originated as a project by the Distributed Machine Learning community known as DMLC.
- A group of students and researchers at various institutions in machine learning field formed the DMLC. The goal was to create open-source software tools for machine learning applications.
- Projects on the DMLC include XGBoost, TVM, and MXNet.
  - XGBoost is an optimized distributed library that implements gradient boosted decision tree models.
  - TVM is a deep learning compiler.
  - MXNet is a deep learning framework.
- In November 2016, Amazon announced MXNet as the company's deep learning framework of choice.
- Then in January 2017, MXNet was donated to the Apache Open-Source Software Foundation and accepted into the Apache Incubator.
- One of the main features of Apache MXNet is that it supports multiple programming language interfaces.
  - Python, R, Perl Java, Julia, Scala, Clojure and C++ as front end languages.
  - To ensure reliable performance, its back end, the asynchronous MXNet engine is implemented in C++.
- MXNet has a rich collection of pre-trained models in its models zoo.
  - **GluonCV** is a toolkit for computer vision applications, that makes it easy to use state of the art pre-trained models for specific computer vision tasks.
  - **GluonNLP** is similar to GluonCV, and it's the toolkit counterpart for natural language processing. It has translation models, a variety of pre-trained language models, embeddings, and general utility tools for language data.
  - **Keras** is a well-known front end deep learning interface. Now, you can choose to use MXNet as its back end with Keras MXNet.
  - **MXBoard** helps users visualize the training process, and diagnose possible issues and bugs at an early stage.
  - The **model server** is an open-source tool developed by AWS, for seven models exported from MXNet, or the Open Neural Network Exchange format known as ONNX.
  - **TensorRT** is a deep learning inference optimizer by NVIDIA, for high-throughput inference on deep neural networks. It is tightly integrated with MXNet library, and can be used by MXNet models.
  - **TVM** mentioned earlier, is an open-source tool that helps model deployment on various hardware environments, while achieving impressive acceleration during inference.
  - **ONNX** is an ecosystem for interchangeable AI models. MXNet has significant support for converting MXNet models from and to the ONNX open format.

#### Imperative vs Symbolic Programming

- These concepts are central to deep learning framework design.
- Imperative and symbolic represents two styles or paradigms of deep learning programming interface.

Imperative Programming

```py
from mxnet import nd
a = nd.ones(10)
b = nd.ones(10) * 2
c = b * a
print(c)
d = c + 1
```

- Advantages:
  - Straightforward and flexible
  - Uses language natively
- Disadvantages:
  - Hard to optimize

Symbolic Programming

```py
A = Variable('A')
B = Variable('B')
C = B * A
D = C + 1
f = compile(D)
d = f(A=np.ones(10),B=np.ones(10)*2)
```

- Advantages:
  - Opportunities for optimization
  - Easy to serialize models
  - More portable across languages
- Disadvantages:
  - Hard to debug
  - Unsuitable for dynamic models

Hybrid Programming

- It is an approach pioneered by MXNet.
- The idea of the hybrid interface is to ask users to build models with imperative program interface, which means they can use native language support to implement the deep learning model and to debug whatever errors they might see. Once development is finalized, they can convert and optimize the model with the symbolic engine.
- The hybrid programming interface provided by MXNet is enabled by the Gluon API.
- The hybrid programming interface provided by MXNet is enabled by the Gluon API. Once you finished, you can run the command net that `hybridize` to switch to symbolic mode. At this point, the model runs as a symbolic graph with the backend MXNet executor and can be easily exported and loaded elsewhere for inference.
- This is why the Gluon API is the preferred way to use MXNet

## Toolkits

- Many open source tools have a few common issues.
  1. First, the tool might not have the models you need for your specific task.
     - It only contain models for a single task,such as image classification or object detection.
     - If you have a complex process that requires different models for different steps, you might have to cobble together models from different sources and toolkits. This requires work overhead, non-trivial differences in installation and configuration, data pre-processing, model performance, or programming languages. In the worst case, this might conflict across tools.
  2. some open source implementations are incorrect.
     - For instance, the research paper might only vaguely describe the model specification or the tools model implementation might be at an early stage and has not been rigorously tested.
  3. Individual developers often give up on the maintenance of their open source implementations.
     - Repository sometimes attract attention and significant use early on,but over time, they fail to receive followup maintenance or incremental improvements. As a result, users incur the cost of maintaining an entire project themselves just to use the tools or they must expand efforts to find workable alternatives.
  4. Model deployment is not considered.
     - For an industrial or commercial applications, model are expected to work on various hardware configurations like GPUs, CPUs or Edge devices. In many vision toolkits, the gap exists between model experimentation and applicable model deployment.

### [GluonCV](https://gluon-cv.mxnet.io)

- GluonCV is built on MxNet Amazon's Framework.
- GluonCV is an open source, flexible, easy to use computer vision toolkit.
- GluonCV provides models for different tasks, including image classification, object deduction, semantic segmentation, instance segmentation, and pose estimation. You can learn to use a trend model for one task and easily transfer the knowledge to other tasks.
- In addition, GluonCV provides vetted implementations for state-of-the-art computer vision models, sometimes a better accuracy than the original paper or other open source implementations.
- AWS scientists maintain GluonCV, which includes official maintenance and development support.
- GluonCV provides easy-to-use APIs that researchers and developers can use for experimentation.
- GluonCV also provides multiple deployment options for various hardware configurations. It bridges the gap between development and deployment
with support from AWS and open source community.

#### GluonCV model types (Model Zoo)

- Various models are available for the same task with different accuracies and resource demand. This is Gluon CV's classification [model zoo page](https://gluon-cv.mxnet.io/model_zoo/index.html).
- For convenience, Gluon CV provides a chart to help in understanding the  tradeoffs and choose the best model for the case. In the chart, each bubble represents a model. The Y axis is the prediction accuracy. And the X axis is the speed. The size of each bubble is the memory consumption. You can see an advanced frontier on all models.
- Usually, you have a restriction on either accuracy or speed, and then you pick the best qualified model with regards to the other dimension.
