# AWS AI services Cheat sheet

- [AWS AI services Cheat sheet](#aws-ai-services-cheat-sheet)
  - [AI services](#ai-services)
    - [Amazon Rekognition](#amazon-rekognition)
    - [Amazon Polly](#amazon-polly)
    - [Amazon Transcribe](#amazon-transcribe)
    - [Amazon Translate](#amazon-translate)
    - [Amazon Comprehend](#amazon-comprehend)
    - [Amazon Lex](#amazon-lex)
    - [Amazon Forecast](#amazon-forecast)
    - [Amazon Personalize](#amazon-personalize)
  - [ML services (SageMaker)](#ml-services-sagemaker)
    - [Amazon SageMaker Ground Truth](#amazon-sagemaker-ground-truth)
    - [Amazon SageMaker Notebooks](#amazon-sagemaker-notebooks)
    - [Algorithms](#algorithms)
    - [Amazon SageMaker Model Training Jobs](#amazon-sagemaker-model-training-jobs)
    - [Amazon SageMaker Automatic Model Tuner](#amazon-sagemaker-automatic-model-tuner)
    - [Amazon SageMaker Neo](#amazon-sagemaker-neo)
    - [Amazon SageMaker Endpoint](#amazon-sagemaker-endpoint)
    - [Amazon Elastic Inference](#amazon-elastic-inference)
  - [ML Frameworks & Infrastructure services](#ml-frameworks--infrastructure-services)
    - [Frameworks](#frameworks)
    - [Infrastructure](#infrastructure)
  - [Amazon Rekognition capabilities](#amazon-rekognition-capabilities)
  - [Deep Learning Amazon Machine Images (DLAMI)](#deep-learning-amazon-machine-images-dlami)
  - [Deep Learning Containers](#deep-learning-containers)
    - [Container images](#container-images)
    - [Amazon ECR](#amazon-ecr)
    - [Amazon ECS](#amazon-ecs)
    - [AWS Deep learning containers](#aws-deep-learning-containers)

- AWS provides instant access to fast and high quality AI tools that are based on the same technology used to power Amazon's own businesses.
- You can choose from pre-trained AI services for computer vision, speech, language, time series, and recommendations.
- These services can be used stand alone or together to create sophisticated and human-like functionality

## AI services

- AI services that are suited to application developers.

### Amazon Rekognition

- It is used to identify objects, scenes, and activities in both images and the videos, as well as detect inappropriate content.

### Amazon Polly

- It can turn text into lifelike speech allowing you to create applications that talk. It offers one of the most natural and human-like text-to-speech voices on the market, and it's made possible with deep neural networks.

### Amazon Transcribe

- It works in the opposite direction than Amazon Polly. It's an automatic speech recognition service that enables speech to text capabilities on audio that's pre-recorded or from a live stream.

### Amazon Translate

- It can deliver fast, high-quality, and affordable language translations.
- Amazon Translate allows to localize content such as websites and applications for international users.

### Amazon Comprehend

- It is a natural language processing service that uses machine learning to find insights and relationships in text.
- It is used to extract important entities, key phrases, and topics in the text, as well as to classify documents and determine sentiment.
- It supports general and industry-specific texts such as medical notes and allows you to train on your own data too.

### Amazon Lex

- It can be used this to create a conversational interface for your application, which is sometimes referred to the chatbot, is powered by the same technologies as Amazon Alexa, and provides a highly engaging user experience through intent detection.

### Amazon Forecast

- It is an accurate time series forecasting service.
- Unlike traditional forecasting methods, this service combines time series sources with additional variables to build more accurate forecasts.
- All forecasts are unique to your data, and tools are provided to schedule update to these models as new data becomes available.

### Amazon Personalize

- It is an AI service that makes it easy for developers to create individualized recommendations for their customers.
- It provides an activity stream from your application, clicks, page views, sign-ups, purchases, and so forth, as well as any inventory of the items you want to recommend, such as articles, products, videos, or music.
- You can also choose to provide Amazon personalized with additional demographic information from your users, such as age or geographic locations.
- Amazon Personalize will process and examine the data, identify what is meaningful, select the right algorithms, and train and optimize a personalization model that is customized for your data.

## ML services (SageMaker)

- ML services are suited to data scientists and developers who want to get more
hands-on with the machine learning workflow.
- All services in this category are managed by **Amazon SageMaker**.
- Amazon SageMaker enables developers and data scientists to quickly and easily build, train, and deploy machine learning models at any scale.
- With the services across all stages of the machine learning workflow, Amazon SageMaker removes the blockers that get in the way of a successful machine learning implementation.
- It's a fully managed service that covers the entire machine learning workflow. All the steps from data labeling to model development are covered, and many features are provided for model development, training, and optimization.

### Amazon SageMaker Ground Truth

- It can help when a dataset that needs to be annotated by a human.
- Amazon SageMaker Ground Truth handles the whole process, from retraining the active learning model, to routine the annotation requests, to human labelers.
- It supplements the labeling process with a technique called active learning,
which reduces costs and speeds up the labeling process.

### Amazon SageMaker Notebooks

- It is a fully managed Jupyter server.
- It can be used to explore datasets through a visual interface or orchestrate the machine learning workflow.
- As an alternative to writing custom models and algorithms on Amazon SageMaker notebooks, you can use built-in algorithms to solve a wide variety of tasks, such as fraud detection, forecasting, and image classification.
- Amazon SageMaker Notebooks come pre-installed with optimized versions of Apache MXNet, TensorFlow, PyTorch, and Chainer, as well as other non-deep learning frameworks, such as Scikit-learn and Spark ML. These frameworks are managed through pre-configured CONDA environments.
- Although SageMaker Notebooks can be used directly for model training, it's common to use notebooks with the Amazon SageMaker SDK to coordinate other components.

### Algorithms

- There are algorithms for computer vision, natural language processing, time series forecasting, to name a few.
- Supervised Learning:
  - Linear:
    - Linear Learner: Linear + Logistic Regression
  - Non-Linear:
    - XGBoost
    - Factorization Machines
      - Good for high dimensional sparse datasets
      - e.g. click prediction & item recommendation
- Unsupervised Learning
  - Clustering
    - K-means Clustering
  - Anomaly Detection
    - Random Cut Forest
    - It is available in Kinesis Data Analytics
  - Topic Modeling
    - Latent Dirichlet Allocation (LDA)
    - It is available on Amazon Comprehend
  - Principle Component Analysis (PCA)
    - Reduces dataset dimensionality
- Deep Learning
  - Image Classification
    - CNN (ResNet)
  - Sequence to Sequence (seq2seq)
    - RNN for text summarization, transition, TTS
  - Neural Topic Modeling (NTM)
  - DeepAR Forecasting
    - Time Series Prediction

### Amazon SageMaker Model Training Jobs

- After selecting an algorithm or developing your own, Amazon SageMaker provides a variety of services for training and tuning your algorithm.
- When you start a training job, Amazon SageMaker provisions instances that are dedicated to training, downloading the data sets onto the instances, and running the models in a containerized environment.
- When the training is complete, Amazon SageMaker will automatically stop the instances, so you will only pay for what you need.
- Compared to Amazon SageMaker Notebooks that might sit idle for long periods of time during model development, this can be more cost effective.
- You could use a small instance type for development on the notebook, and then use large instance types for model training jobs.

### Amazon SageMaker Automatic Model Tuner

- It is to avoid manual trial and error when tweaking algorithms settings.
- Using efficient search strategies, it will help find the best settings for the algorithm.
- You can specify optimization hyperparameters such as the learning rate and you can specify data related hyperparameters such as the amount of random color augmentations added to your training images.
- The recommended search strategy for the best model hyperparameters in Amazon Sage Maker Model Tuning is Bayesian search. Using a technique called Gaussian Processes, this strategy selects combinations more intelligently than random sampling values.

### Amazon SageMaker Neo

- It is  to optimize the speed and memory consumption of your model for specific hardware devices.
- It makes them run up to twice as fast with less than one tenth of the memory footprint, with no loss in accuracy.
- For compilation, you start with a machine learning model, built with MXNet, TensorFlow, PyTorch or XGBoost and then choose your target hardware platform. Some options include Intel, Nvidia, Arm and Qualcomm.
- Amazon SageMaker Neo then compiles the train model into an executable program.
- Under the hood, a neural network is used to discover the specific performance optimizations that will make your model run most efficiently.

### Amazon SageMaker Endpoint

- You can host models with a single click and generate predictions in real-time using HTTP requests.
- You can also auto-scale endpoints and spread them across multiple availability zones to deliver both high performance and high availability.

### Amazon Elastic Inference

- Accelerated compute service for Amazon SageMaker and Amazon EC2.
- Choose the instance type that suits the ML needs and independently specify the amount of inference accelerators.
- Respond to change in demand
- Reduce inference costs by up to 75%
- TensorFlow, ONNX, mxnet model support
- How it works:
  - Instances communicate with accelerators
  - Model serving platforms for these frameworks automatically use EI accelerators
  - Models loaded
  - Inference calls
- Amazon EI accelerator available in medium, large, and xlarge sizes

## ML Frameworks & Infrastructure services

- Advanced data scientists and developers can get full control over
the machine learning workflow with these services.

### Frameworks

- Amazon SageMaker supports optimized versions of these frameworks out-of-the-box.
- You can create models using TensorFlow, Apache MXNet, PyTorch, Chainer,
Keras, and many other non-deep learning frameworks such as scikit-learn and Spark ML.

### Infrastructure

- You can take control and manage your own Amazon Elastic Compute Cloud
or Amazon EC2 instances.
- You can choose from a wide variety of instance types, everything from compute-optimized C5 instances to GPU-accelerated P3 instances.
- You can scale up to 256 gigabytes of GPU memory on a single instance with a p3dn 24xlarge.
- You can also find instances with field-programmable gate arrays, often abbreviated to FPGAs.
- They can be specialized to neural network training.
- You don't need to worry about setting up the frameworks or the optimized libraries such as Nvidia CUDA.
- You can start your instance with the Deep Learning Amazon Machine Image, often abbreviated to DLAMI.
- Other infrastructure options include Deep Learning Containers on Amazon Elastic Container Service
- And Edge deployments through AWS IoT Greengrass.

## Amazon Rekognition capabilities

- Amazon Rekognition is a simple API for image and video analysis that continuously learns and integrates with AWS services.
- It doesn't need computer vision or deep learning expertise to use the high-quality Amazon Rekognition predictions.
- Amazon Rekognition removes the complexity of building your own visual recognition capabilities by making powerful and accurate analysis available with easy-to-use APIs.
- Amazon Rekognition also provides consistent response times regardless
of the volume of requests you make.
- Amazon Rekognition works with videos, understanding motion between video frames. It can accurately identify complex activities such as blowing out a candle or extinguishing a fire. You can apply this type of analysis in real-time to video streams at low latency or in batches for high-throughput.
- Amazon Rekognition is continually trained on new data to expand its ability to recognize objects, scene, and activities.
- Amazon Rekognition works seamlessly with other AWS services too. It integrates directly with Amazon S3 and AWS Lambda.
- Amazon Rekognition you only pay for the number of images or minutes of video that you analyze, and the face data you store for facial recognition.
- With Amazon Rekognition, you can identify thousands of objects such as bikes, telephones, and buildings; and scenes such as parking lot, beach, and cities. When analyzing video, you can also identify specific activities in the frame such as delivering a package or playing soccer. You can retrieve object locations in an image and a confidence score for every prediction.
- Using the compare faces feature, you could implement a face-based user verification system for your application or company. You could compare a reference image from an employee badge to a live image from a camera and use Amazon Rekognition to return a similarity score.
- Amazon Rekognition can estimate emotions and age ranges, alongside other features such as glasses and facial hair. With video, you can see these changes overtime.
- Amazon Rekognition can recognize thousands of celebrities in a wide range of categories such as entertainment and media, sports, business, and politics.
- You can capture the path taken by people in the scene. It can be used to track the movement of athletes during a game to identify plays in post-game analysis.
- Amazon Rekognition also helps you identify potentially unsafe or inappropriate content in images and videos, and provides you with a detailed label that shows how to accurately control what you want to allow based on your needs.
- Amazon Rekognition can detect and recognize texts from images such as street names, captions, product names, and license plates. It's built to work with real-world images, not just perfectly scanned documents.

## Deep Learning Amazon Machine Images (DLAMI)

- AMI stands for Amazon Machine Image.
- An AMI is a template that's used to create an instance with Amazon Elastic Compute Cloud, also known as Amazon EC2.
- An AMI includes what operating system the instance will run, as well as the necessary software dependencies.
- The level of customization, which software dependencies are pre installed on the instance depends on the task or application.
- The DLAMI allows you to quickly launch Amazon EC2 instances pre-installed with popular deep learning frameworks.
- DLAMI comes in two variants:
  - Conda DLAMI
    - It is available for Ubuntu, Amazon Linux, and Windows. And it comes with frameworks like MXNet, TensorFlow and PyTorch that are installed in separate Conda environments. This ensures that all the dependencies for each framework exist in separate environments, and any framework can be used on the instance.
  - The base DLAMI
    - It is available only for Ubuntu and Amazon Linux. It doesn't have the deep learning frameworks pre-installed. Instead, it comes pre-installed with the foundational building blocks for deep learning, such GPU drivers and Nvidia CUDA libraries. It provides a clean slate to build custom versions of deep learning frameworks.
- The list of supported frameworks pre-installed on the DLAMI covers all major popular deep learning frameworks.

## Deep Learning Containers

- It provides another way for you to set up deep learning environments on AWS with optimized, prepackaged container images.

### Container images

- A container is a standardized unit of software developed by Docker, which lets you package software applications for development, shipment, and deployment. You can package up code and its related dependencies into what's known as a container image.
- This container image is an abstraction that includes everything you need to run an application in a container. Using containers enables OS-level virtualization, which allows developers to isolate software from complex dependencies on the environment and platform it was built on, which enables portability.
- Container images are created by combining and modifying standard images from container repositories.
- One such container repository is Amazon Elastic Container Registry, or Amazon ECR.

### Amazon ECR

- Amazon ECR is a fully managed Docker container registry by AWS.
- It can store Docker images in the cloud, inside AWS account.
- It allows access to pre-built container images from public repositories in ECR.
- ECR also provides tools for you to use these container images and deploy them as Docker containers on a Amazon Elastic Container Service, or Amazon ECS.

### Amazon ECS

- Amazon ECS is a container orchestration service on AWS.
- ECS supports Docker containers and allows you to easily run and scale containerized applications on AWS.
- ECS is a highly scalable service that eliminates the need for you to install and operate your own container orchestration software.
- With simple, secure API calls, it can launch and stop Docker-enabled
applications, as well as query the complete state of your application.
- You can run containers with ECS on Amazon EC2 Spot instances and get access to heavily discounted prices compared to on-demand instances.
- ECS is a high performance service built on technology developed from many years of experience, running highly scalable services.
- It is also used by AWS Fargate, so you can deploy and manage containers without having to provision or manage servers. This means you no longer have to select Amazon EC2 instance types and scale clusters of instances.
- To assist in deploying custom machine learning environments using ECS, AWS introduced deep learning containers.

### AWS Deep learning containers

- These are Docker container images pre-installed with deep learning frameworks, allowing you to skip the complicated process of building and optimizing your environment from scratch.
- These container images are available from Amazon ECR and the AWS marketplace. And they are available and no additional cost because you only pay for the resources that you use, just like instances.
- AWS Deep Learning Containers support Apache MXNet and TensorFlow, and other deep learning frameworks are coming soon.