# Best Practices in AWS services

## Data

- The amount of data required for any machine learning and deep learning predictive modeling application, is directly proportional to the complexity of the problem and algorithm.
- To determine whether the dataset size is sufficient, many data scientists implement learning curves, k-fold cross validation resampling methods on smaller datasets, and assessing confidence intervals of final results.
- **Plotting** is helpful to **analyze** the data. It helps to **visualize trends** that might inform about data preprocessing and modeling choices. Visualizations can help identify **accidental correlations**, **sampling biases**, or **non-response biases** that are indicative of whether the dataset is representative enough, and will generalize well to new, unseen data.
- Data quality can be quantified by assessing frequency of errors or missing values, noise-to-signal ratio, and heterogeneity of data distribution.
- AWS data visualization services:
  - **Amazon QuickSight** to build plots in an **interactive** dashboard using data stored in **Amazon S3**.
  - **Amazon SageMaker** offers managed **Jupyter Notebooks** that you can connect to data in your Amazon S3 bucket, for visualization tasks, and to run **Amazon Athena** and **AWS Glue jobs**.
- ML applications requires high computing power (GPU instances). However, the I/O storage access might be slower than that of the GPU instances. So, the suitable storage type must be considered according to the GPU instance type. For P2 instances, Amazon S3 is sufficient to maintain desirable concurrency on I/O processing. For P3 instances that need high throughput, you can select a massively parallel file system, such as Amazon Elastic File System (Amazon EFS) or Amazon FSx for Lustre (Amazon FSx), to elastically scale to demand.
- Moving a large dataset from one location to another can be an expensive process. So, it is only required if training speed can be essential to meeting your business needs
- Comparison of the relative (to Amazon EFS) images per second that each file system can load

    | File System | Relative Speed |
    | ----------- | -------------- |
    | Amazon S3   | <1.00          |
    | Amazon EFS  | 1              |
    | Amazon EBS  | 1.29           |
    | NVMe        | 1.4            |
    | RAMDisk     | 1.44           |
    | BeeGFS      | 1.6            |
    | Amazon FSx  | >1.60          |

## Data Warehousing

- ETL processing services (Amazon Athena, AWS Glue, Amazon Redshift Spectrum) are functionally complementary and can be architected to preprocess datasets stored in or targeted to Amazon S3.
- The choice of ETL processing tool is largely dictated by the type of data you have. For example, tabular data processing with Amazon Athena gives you the ability to manipulate your data files in Amazon S3 using SQL.If your datasets or computations are not optimally compatible with SQL, you can use Amazon Glue to seamlessly run Spark Jobs (Scala and Python support) on data stored in your Amazon S3 buckets.

## ML Model deployment

- **After a model is trained**, the process of evaluating the model is often **not as data dependent as the training step**.
- For **deployment**, the **data needs** are highly **dependent on the problem**.
- If the model is used for a batch transform, then data can be prepared in advance and be given to the model using either Amazon S3 or one of the other previously mentioned file systems.
  - Currently, Amazon S3 single object uploads are capped at 5GB and file sizes are set at up to 5TB.
  - If data is in Amazon S3, this enables to leverage tools such as Amazon SageMaker Batch Transform to evaluate a model in a serverless environment.
- Real-time prediction systems are more complex because they are only considered real-time for a short duration.
  - For real-time inference on AWS, you can use an Amazon SageMaker Deployment with a server placed behind a load balancer that is auto-scaled to meet the API requests,which are sent to the model endpoint.
  - Another option is to use Amazon Elastic Inference set to the correct amount of GPU-acceleration at reduced cost to provide scaled inference, without needing an oversized instance.
  - Similarly, you can deploy popular deep learning framework models in SageMaker Neo to optimize the trained model for the targeted hardware platform.
- In extreme cases, a SageMaker deployment might have too much latency. In these situations, to find the bottlenecks, you must perform an extensive audit of where the data for inference is coming from, its path to the model, the hardware running the model, and the response pathway.
  - In some cases,getting the data you need from the disparate data sources can be limiting and you must rearchitect your data access patterns to enable real-time inference.
  - In other cases, you need to bring the model closer to the data sources. In these cases, you deploy the model at the edge to interact directly with data generators.

## Distributed Computation Frameworks

- In principle, distributed computation frameworks provide a protocol of data processing and node task distribution and management.
- Frameworks such as MapReduce and Apache Spark also provide algorithms to split datasets into subsets and distribute them across nodes in a compute cluster.

### Amazon EMR

- Apache Spark cluster can run on Amazon EMR, provides a managed framework that can process massive quantities of data.
- Amazon EMR supports many instance types.
- Amazon SageMaker notebook instances can connect to a Spark EMR cluster.

### Amazon Glue

### Amazon SageMaker pipes

### Best Practices

- If Dataset is too large to fit into memory:
  - Split the data into a small number of files with a uniform number of partitions, as a pre-process step.
  - Pack the data in parallel, distributed across multiple machines.

- Ideally, all data processing should be run on the CPU side and GPUs for training the DL models to make sure that no consumer or producer overlap occurs between the CPU (producer) and the GPU (consumer).
  - In some situations, such as image manipulation, data preparation can be compute intensive. In these situations, you can use an AWS Batch job, which provides access to GPU-enabled instances, to manipulate large datasets.

- In loading process, data is shuffled randomly.
  - To make sure that shuffling happens without negative impacts on performance, run this on small, partitioned files.

- Most frameworks, such as Tensorflow, PyTorch, and MxNet, offer a data loading class. These functions call a data loader function each time the next chunk of data is needed, which allows you to process Big Data in batches.
  - Many frameworks also include a data pipelines feature that you can use to write a custom pipeline in python code and library helper functions. Because there is more than one option for a single framework and there are no universal formats available.
  - There are also several open source libraries that enable parallel computing with task scheduling for analytics, such as Dask, Ray, PyToolz, and ipyparallel.

- Because model training is compute intensive, we suggest you complete vertical scaling before horizontal scaling.
  - It is not recommended training complex ML models on traditional CPUs.
  - Try a more powerful GPU before moving to multiple GPUs.
  - Leverage multiple GPUs on a single node before you move to a multi-node solution.
  - This approach generally provides the best performance and limits the complexity of the system until that complexity is necessary.

- Step-by-step analysis process is recommended before moving from a single GPU instance to more complex training infrastructures.
  - Evaluate GPU utilization.
    - If the data cannot be prepared for the GPU faster than the GPU is consuming the data, then there is a data preparation bottleneck, and a faster GPU will not significantly increase the model training speed.
    - To help make sure that data preparation is not a bottleneck, prepare the datasets using CPUs and store them in memory for GPU consumption.
    - When the CPUs cannot handle more processes, it becomes important to determine if the data preparation processes are IO limited or compute limited.
      - If IO limits the data preparation, you can consider moving the data to a different data store.
      - If the compute process limits the data preparation, first make sure that only necessary processes are running. In extreme cases, when you cannot reduce preprocessing, you might have to use a data preparation cluster to generate batches of data to feed the model.
  - If single GPU is fully saturated and the training time is still not sufficient, try a more powerful GPU, if one is available.
    - After switching to a more powerful GPU, repeat the process above to make sure that the new GPU has not moved the bottleneck from the GPU to the data preparation.
  - If the GPU is still limiting and the training times are insufficient, then the next step is moving to a node with more GPUs.
    - A single node with multiple GPUs has some advantages over the same number of GPUs spread over many nodes.
      - First, the communication between GPUs on a single node is often over NVLink and is substantially faster than traveling across the network to another node.
      - Secondly, the movement of information between the GPU memory and system memory is faster than communication across the network.
  - If the largest single node GPU system is not sufficiently fast and data preparation is not a bottleneck, a cluster of GPU compute nodes is a possible solution.
    - Deep learning frameworks have different methods of enabling multi-node model training, so the ideal cluster setup depends on the framework.

## Build Compute Clusters to Fit the Workload

- A good default architecture for deep learning training should include the Amazon S3, Amazon EC2, Amazon Virtual Private Cloud (Amazon VPC), Amazon EC2 Auto Scaling, Amazon Elastic Container Service for Kubernetes (Amazon EKS), and AWS Identity and Access Management (IAM) services.
- AWS CloudFormation templates, such as the deep learning CFN cluster, increases flexibility, reliability, and low-level transparency. AWS CloudFormation can help to identify potential bottlenecks and areas of improvement quickly.
- Amazon EC2 Auto Scaling enables the application to scale dynamically from a few nodes to over a hundred, with the added benefit of providing multi-region coverage for resources in replica sets.
- When you put them in containers and control them with Kubernetes on Amazon EKS you create dependency isolation with a unified monitoring and logging framework. In addition, it gives you the benefit of separating the OS and device-driver layer dependencies.

## Modeling Using Hybrid Infrastructures

- Hybrid infrastructure architectures refer to the use of on-premises servers or edge computing device endpoints (off-cloud) together with in-the-cloud resources.
- Hybrid network architectures often use VPN services and AWS Direct Connect (DX) for connectivity to an AWS Region.
- In a hybrid network architecture, data transfer to Amazon S3 can take place over a private connection instead of using the default secure protocol (HTTPS) over the public internet.
- For both ML and DL applications, training jobs in the cloud, can leverage the infinitely scalable resources of the cloud. After a model is trained, it can be transferred to an on-premises server or edge device to run inference workloads.
- Hybrid architectures are also useful in cases where data privacy is a concern.
- For workload optimization:
  - AWS Storage Gateway combine multi-protocol storage capabilities with high network connectivity.
  - Selecting job scheduling methods that leverage the compute capacity that is closest to the data source.
  - When you deploy AI and deep learning to millions of connected edge devices, it is recommended that you create, train, and optimize your models in the AWS Cloud, and then deploy them for inference to NVIDIA Jetson-powered edge devices (for example) using AWS IoT Greengrass. This architecture enables edge devices to act locally on real-time data while leveraging the cloud for model management.
- Data returned to the cloud and targeted to an Amazon S3 bucket can be used as a trigger in an automated CI/CD workflow by integrating additional AWS services such as AWS CodeBuild, AWS CodePipeline, Amazon CloudWatch, and AWS Lambda.

---

- If you plan to use GPU devices for model training, make sure that your containers are nvidia-docker compatible. Only the CUDA toolkit should be included on containers; don't bundle NVIDIA drivers with the image.
- Secure SageMaker from internet access by creating a SM notebook, connect it to a VPC and private subnet, disable Direct internet access option.
- Horovod distributed framework supported by Amazon SageMaker. Parallelize the training to as many machines as needed to achieve the business goals.
- RecordIO protobuf format, is the best format for training on SageMaker