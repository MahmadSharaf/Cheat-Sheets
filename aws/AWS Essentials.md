# AWS Essential Services Cheat Sheet

- [AWS Essential Services Cheat Sheet](#aws-essential-services-cheat-sheet)
  - [Basics](#basics)
  - [Compute in the Cloud](#compute-in-the-cloud)
    - [EC2](#ec2)
      - [EC2 Auto Scaling](#ec2-auto-scaling)
    - [ELB](#elb)
    - [Messaging and Queueing](#messaging-and-queueing)
      - [SNS](#sns)
      - [SQS](#sqs)
    - [Containerized services](#containerized-services)
      - [ECS](#ecs)
      - [EKS](#eks)
    - [Serverless computing](#serverless-computing)
      - [Fargate](#fargate)
      - [Lambda](#lambda)
    - [Cloud Compute additional resources](#cloud-compute-additional-resources)
  - [Analytics](#analytics)
    - [Streaming (data-ingestion) services](#streaming-data-ingestion-services)
      - [Amazon MSK](#amazon-msk)
      - [AWS Kinesis](#aws-kinesis)
      - [MSK vs Kinesis](#msk-vs-kinesis)
      - [Reference](#reference)
    - [Query services](#query-services)
      - [Amazon Athena](#amazon-athena)
    - [Data Transformation](#data-transformation)
      - [AWS Data Pipeline](#aws-data-pipeline)
      - [Amazon EMR](#amazon-emr)
  - [Global Infrastructure and Reliability](#global-infrastructure-and-reliability)
    - [Region](#region)
    - [Availability Zone](#availability-zone)
    - [Edge Locations](#edge-locations)
      - [Amazon CloudFront](#amazon-cloudfront)
    - [AWS Outposts / Local Zone](#aws-outposts--local-zone)
    - [Global Infrastructure additional resources](#global-infrastructure-additional-resources)
  - [Provision AWS resources](#provision-aws-resources)
    - [AWS Management Console](#aws-management-console)
    - [AWS Command Line Interface](#aws-command-line-interface)
    - [Software Development Kit](#software-development-kit)
    - [AWS Elastic Beanstalk](#aws-elastic-beanstalk)
    - [AWS CloudFormation](#aws-cloudformation)
  - [Networking](#networking)
    - [VPC](#vpc)
      - [Subnets](#subnets)
      - [Network traffic in a VPC](#network-traffic-in-a-vpc)
      - [Network access control lists (NACLs)](#network-access-control-lists-nacls)
      - [Security Group](#security-group)
      - [Network Address Translation (NAT) Gateway](#network-address-translation-nat-gateway)
      - [Elastic IP (EIP)](#elastic-ip-eip)
      - [PrivateLink](#privatelink)
      - [VPC Endpoint](#vpc-endpoint)
    - [AWS Direct Connect](#aws-direct-connect)
    - [Amazon Route 53](#amazon-route-53)
    - [Networking additional resources](#networking-additional-resources)
  - [Storage Services](#storage-services)
    - [Block Storage](#block-storage)
      - [Instance Store](#instance-store)
      - [EBS](#ebs)
    - [Object Storage](#object-storage)
      - [S3](#s3)
    - [File Storage](#file-storage)
      - [EFS](#efs)
      - [FSx](#fsx)
      - [Storage types speed comparison](#storage-types-speed-comparison)
    - [Storage additional resources](#storage-additional-resources)
  - [Databases](#databases)
    - [RDS](#rds)
    - [Amazon Aurora](#amazon-aurora)
    - [Amazon DynamoDB](#amazon-dynamodb)
    - [Amazon RedShift](#amazon-redshift)
    - [AWS DMS](#aws-dms)
    - [Amazon DocumentDB](#amazon-documentdb)
    - [Amazon Neptune](#amazon-neptune)
    - [Amazon QLDB](#amazon-qldb)
    - [Amazon Managed Blockchain](#amazon-managed-blockchain)
    - [Amazon ElastiCache](#amazon-elasticache)
    - [Amazon DAX](#amazon-dax)
    - [Databases additional resources](#databases-additional-resources)
  - [Security](#security)
    - [AWS Shared Security Model](#aws-shared-security-model)
    - [IAM](#iam)
    - [AWS Multi-Tier (Defense In-depth) Security Groups](#aws-multi-tier-defense-in-depth-security-groups)
    - [VPC: Network Control](#vpc-network-control)
    - [AWS Organizations](#aws-organizations)
    - [Compliance](#compliance)
      - [AWS Artifact](#aws-artifact)
      - [Customer Compliance Center](#customer-compliance-center)
    - [DDoS](#ddos)
      - [AWS Shield](#aws-shield)
    - [AWS KMS](#aws-kms)
    - [AWS WAF](#aws-waf)
    - [Amazon Inspector](#amazon-inspector)
    - [Amazon GuardDuty](#amazon-guardduty)
    - [Security additional resources](#security-additional-resources)
  - [Monitoring and Analytics](#monitoring-and-analytics)
    - [Amazon CloudWatch](#amazon-cloudwatch)
    - [AWS CloudTrail](#aws-cloudtrail)
    - [AWS Trusted Advisor](#aws-trusted-advisor)
    - [Monitoring and Analytics additional resources](#monitoring-and-analytics-additional-resources)
  - [Pricing and Support](#pricing-and-support)
    - [AWS Free Tier](#aws-free-tier)
    - [AWS Pricing Concepts](#aws-pricing-concepts)
    - [AWS Pricing Calculator](#aws-pricing-calculator)
    - [Billing dashboard](#billing-dashboard)
    - [Consolidated billing](#consolidated-billing)
    - [AWS Budget](#aws-budget)
    - [AWS Cost Explorer](#aws-cost-explorer)
    - [AWS Support plans](#aws-support-plans)
    - [AWS Marketplace](#aws-marketplace)
    - [Pricing and Support additional resources](#pricing-and-support-additional-resources)
  - [Migration and Innovation](#migration-and-innovation)
    - [AWS CAF](#aws-caf)
    - [Migration strategies](#migration-strategies)
    - [AWS Snow Family](#aws-snow-family)
  - [Innovate with AWS Services](#innovate-with-aws-services)
    - [Migration and Innovation additional resources](#migration-and-innovation-additional-resources)
  - [The Cloud Journey](#the-cloud-journey)
    - [The AWS Well-Architected Framework](#the-aws-well-architected-framework)
    - [Advantages of cloud computing](#advantages-of-cloud-computing)
    - [Cloud Journey additional resources](#cloud-journey-additional-resources)

## Basics

What is a client-server model?

- Almost all of modern computing uses a basic client-server model.
- In computing, a client can be a web browser or desktop application that a person interacts with to make requests to computer servers. A server can be services such as Amazon Elastic Compute Cloud (Amazon EC2), a type of virtual server.

## Compute in the Cloud

- [Cloud Computing](https://aws.amazon.com/products/compute) is the on-demand delivery of IT resources over the internet with pay-as-you-go pricing

### EC2

- Amazon Elastic Compute Cloud (EC2) is a virtual machine.
- Resizable compute capacity
- Complete control of computing resources
- Reduced time required to obtain and boot new server instances
- Scale capacity as your computing requirements change
- Pay only for capacity that you actually use
- Choose Linux, Windows, or Mac
- Deploy across AWS Regions and Availability Zones for reliability
- Use tags to help manage your Amazon EC2 resources

EC2 instance created by Amazon Machine Image (AMI), select an AMI based on:

- Region
- Operating system
- Architecture (32-bit or 64-bit)
- Launch permissions
- Storage for the root device

[Instance Type Families](https://aws.amazon.com/ec2/instance-types/):

- General purpose (T2, M5, M4):
  - Low-traffic websites and web applications
  - Small databases and mid-size databases
- Compute-optimized (C5, C4):
  - High performance web servers
  - Video-encoding
  - Batch processing
- Memory-optimized (X1e, X1, R4):
  - High performance databases
  - Distributed memory caches
- Storage-optimized (H1, I3, D2)
  - Data warehousing
  - Log or data-processing applications
- Accelerated Computing (P3, P2, G3, F1)
  - 3D visualizations
  - Machine learning

Instance User Data:

- Runs scripts after the instance starts.
- Can be passed to the instance at launch.
- Can be used to perform common automated configuration tasks.

Amazon [EC2 Pricing](https://aws.amazon.com/ec2/pricing/) Options:

- On-Demand Instances:
  - Pay by the hour
  - Pay by the second for Linux instances
- Savings Plans:
  - Enables you to reduce your compute costs by committing to a consistent amount of compute usage for a 1-year or 3-year term. This term commitment results in savings of up to 72% over On-Demand costs.
  - Any usage up to the commitment is charged at the discounted Savings Plan rate (for example, $10 an hour). Any usage beyond the commitment is charged at regular On-Demand rates.
  - It is applied to EC2, Lambda, and Fargate.
- [Reserved Instances](https://aws.amazon.com/ec2/pricing/reserved-instances/)
  - Purchase, at a significant discount, instances that are always available.
  - 1-year to 3-year terms
- Scheduled Instances
  - Purchase instances that are always available on the specified recurring schedule, for a **one-year** term.
- Spot Instances
  - Bid on unused instances, which can run as long as they are available and your bid is above the Spot price.
- Dedicated Instances
  - Pay, by the hour, for instances that run on singletenant hardware.
  - Dedicated underlying host but without any control on Hyper Visor or hardware configurations
  - There is no affinity
- Dedicated Hosts
  - Pay for a physical host that is fully dedicated to run your instances.
  - Dedicated underlying host with no control on Hyper Visor, but has full hardware configurations control
  - There is affinity which enables to set EC2 instances on specific hosts.
- I3.Metal
  - It is a dedicated hardware that provide full control for customers to use their own Hyper Visor, Hardware configurations.

#### EC2 Auto Scaling

- Scalability involves beginning with only the resources you need and designing your architecture to automatically respond to changing demand by scaling out or in.
- [Amazon EC2 Auto Scaling](https://aws.amazon.com/ec2/autoscaling) is the AWS service that provides this functionality for Amazon EC2 instances.
- Amazon EC2 Auto Scaling enables you to automatically add or remove Amazon EC2 instances in response to changing application demand.
- Within Amazon EC2 Auto Scaling, you can use two approaches: dynamic scaling and predictive scaling.
  - Dynamic scaling responds to changing demand.
  - Predictive scaling automatically schedules the right number of Amazon EC2 instances based on predicted demand.
- To scale faster, you can use dynamic scaling and predictive scaling together.

Auto Scaling group:

- When an Auto Scaling group is created ,the minimum number of Amazon EC2 instances can be set. The **minimum capacity** is the number of Amazon EC2 instances that launch immediately after creating the Auto Scaling group. For example, the Auto Scaling group has a minimum capacity of one Amazon EC2 instance.
- Then, the **desired capacity** at two Amazon EC2 instances even though the application needs a minimum of a single Amazon EC2 instance to run.
  - If you do not specify the desired number of Amazon EC2 instances in an Auto Scaling group, the desired capacity defaults to your minimum capacity.
- The third configuration is the maximum capacity. For example, you might configure the Auto Scaling group to scale out in response to increased demand, but only to a maximum of four Amazon EC2 instances.

### ELB

- [Amazon Elastic Load Balancing](https://aws.amazon.com/elasticloadbalancing) (Amazon ELB) is the AWS service that automatically distributes incoming application traffic across multiple resources, such as Amazon EC2 instances.
- A load balancer acts as a single point of contact for all incoming web traffic to the Auto Scaling group.
- For example, if you have multiple Amazon EC2 instances, Elastic Load Balancing distributes the workload across the multiple instances so that no single instance has to carry the bulk of it.
- Although Elastic Load Balancing and Amazon EC2 Auto Scaling are separate services, they work together to help ensure that applications running in Amazon EC2 can provide high performance and availability.

### Messaging and Queueing

#### SNS

- [Amazon Simple Notification Service (Amazon SNS)](https://aws.amazon.com/sns) is a publish/subscribe service. Using Amazon SNS topics, a publisher publishes messages to subscribers.
- In Amazon SNS, subscribers can be web servers, email addresses, AWS Lambda functions, or several other options.

#### SQS

- Using Amazon Simple Queue Service (Amazon SQS), you can send, store, and receive messages between software components, without losing messages or requiring other services to be available.
- In Amazon SQS, an application sends messages into a queue. A user or service retrieves a message from the queue, processes it, and then deletes it from the queue.

### Containerized services

Containers:

- Containers provides a standard way to package application code and dependencies into a single object.
- Containers are used for processes and workflows in which there are essential requirements for security, reliability, and scalability.
- Container orchestration services helps to deploy, manage, and scale containerized applications.

#### ECS

- [Amazon Elastic Container Service (Amazon ECS)](https://aws.amazon.com/ecs/) is a highly scalable, high-performance container management system that enables you to run and scale containerized applications on AWS.
- Amazon ECS supports Docker containers. [Docker](https://www.docker.com/) is a software platform that enables you to build, test, and deploy applications quickly.
- AWS supports the use of open-source Docker Community Edition and subscription-based Docker Enterprise Edition.
- With Amazon ECS, API calls can be used to launch and stop Docker-enabled applications.

#### EKS

- [Amazon Elastic Kubernetes Service (Amazon EKS)](https://aws.amazon.com/eks/) is a fully managed service that you can use to run Kubernetes on AWS.
- [Kubernetes](https://kubernetes.io/) is open-source software that enables you to deploy and manage containerized applications at scale.
- EKS always updated with new features and functionalities release for Kubernetes applications, you can easily apply these updates to your applications managed by Amazon EKS.

### Serverless computing

- The term “serverless” means that your code runs on servers, but you do not need to provision or manage these servers.
- With serverless computing, you can focus more on innovating new products and features instead of maintaining servers.
- Another benefit of serverless computing is the flexibility to scale serverless applications automatically.

#### Fargate

- [AWS Fargate](https://aws.amazon.com/fargate/) is a serverless compute engine for containers. It works with both Amazon ECS and Amazon EKS.
- When using AWS Fargate, you do not need to provision or manage servers. AWS Fargate manages the server infrastructure, and charges only for the resources that are required to run the containers.

#### Lambda

- [AWS Lambda](https://aws.amazon.com/lambda) is a service that lets you run code without needing to provision or manage servers.
- Code can be run for virtually any type of application or backend service, all with zero administration.

[Pricing](https://aws.amazon.com/lambda/pricing/)

- Charging is based on the number of requests and the time that it takes for them to run.
- AWS Lambda allows 1 million free requests and up to 3.2 million seconds of compute time per month.
- A Compute Savings Plan offers lower compute costs in exchange for committing to a consistent amount of usage over a 1-year or 3-year term.

### Cloud Compute additional resources

- [Compute on AWS](https://aws.amazon.com/products/compute)
- [AWS Compute Blog](https://aws.amazon.com/blogs/compute/)
- [AWS Compute Services](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/compute-services.html)
- [Hands-On Tutorials: Compute](https://aws.amazon.com/getting-started/hands-on/?awsf.getting-started-category=category%23compute&awsf.getting-started-content-type=content-type%23hands-on)
- [Category Deep Dive: Serverless](https://aws.amazon.com/getting-started/deep-dive-serverless/)
- [AWS Customer Stories: Serverless](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23serverless)

## Analytics

### Streaming (data-ingestion) services

#### Amazon MSK

- [Apache Kafka](https://kafka.apache.org/intro) is an open-source stream-processing software platform developed by LinkedIn, donated to Apache Software Foundation, and written in Scala and Java.
- [Amazon Managed Streaming Service for Kafka (Amazon MSK)](https://aws.amazon.com/msk/) takes away the operational burden of managing an Apache Kafka cluster.
- APIs allow producers to publish data streams to topics. A topic is a partitioned log of records with each partition being ordered and immutable.Consumers can subscribe to topics.
- Kafka can run on a cluster of brokers with partitions split across cluster nodes.
- Kafka has five core APIs:
  - The **Producer** API allows applications to send streams of data to topics in the Kafka cluster.
  - The **Consumer** API allows applications to read streams of data from topics in the Kafka cluster.
  - The **Streams** API allows transforming streams of data from input topics to output topics.
  - The **Connect** API allows implementing connectors that continually pull from some source system or application into Kafka or push from Kafka into some sink system or application.
  - The **AdminClient** API allows managing and inspecting topics, brokers, and other Kafka objects.
- Kafka has the following feature for real-time streams of data collection and big data real-time analytics:
  - **Performance**: Works with the huge volume of real-time data streams. Handles high throughput for both publishing and subscribing
  - **Scalability**: Highly scales distributed systems with no downtime in all four dimensions: producers, processors, consumers, and connectors
  - **Fault tolerance**: Handles failures with the masters and databases with zero downtime and zero data loss
  - **Data Transformation**: Offers provisions for deriving new data streams using the data streams from producers
  - **Durability**: Uses Distributed commit logs to support messages persisting on disk
  - **Replication**: Replicates the messages across the clusters to support multiple subscribers

#### AWS Kinesis

- [Amazon Kinesis](https://aws.amazon.com/kinesis) is a platform for streaming data on AWS.
- It can be used for ingesting and processing stream of data.
- AWS Kinesis offers key capabilities to cost-effectively process streaming data at any scale, along with the flexibility to choose the tools that best suit the requirements of your application.
- Amazon Kinesis software is modeled after an existing Open Source system, Apache Kafka.
- Amazon Kinesis has four capabilities:
  1. **Kinesis Video Streams**:
     - Securely stream video from connected devices to AWS for analytics, machine learning, playback, and other processing.
  2. **Kinesis Data Streams** (KDS):
     - Collect and process large streams of data records in real time as same as Apache Kafka.
  3. **Kinesis Data Firehose**:
     - Batch and compress the data to generate incremental views
  4. **Kinesis Data Analytics**:
     - Process the data that is streaming through Kinesis Data Streams or Kinesis Data Firehose using SQL
- Other capabilities:
  1. **Amazon Kinesis Client Library** (KCL):
     - Reads the data from Amazon Kinesis
  2. **Amazon Kinesis Producer Library** (KPL):
     - Writes the data to other services

The high-level architecture on Kinesis Data Streams:

- The producers put records (data ingestion) into KDS. AWS provides Kinesis Producer Library (KPL) to simplify producer application development and to achieve high write throughput to a Kinesis data stream.
- A Kinesis data Stream a set of shards. Each shard has a sequence of data records. Data records are composed of a sequence number, a partition key, and a data blob (up to 1 MB), which is an immutable sequence of bytes.
- The consumers get records from Kinesis Data Streams and process them. You can build your applications using either Kinesis Data Analytics, Kinesis API or Kinesis Client Library (KCL).

Kinesis Data Streams has the following benefits:

- **Fully managed**: Kinesis is fully managed and runs your streaming applications without requiring you to manage any infrastructure
- **Scalability**: Handle any amount of streaming data and process data from hundreds of thousands of sources with very low latencies
- **Durability**: Kinesis Data Streams application can start consuming the data from the stream almost immediately after the data is added.
- **Elasticity**: Scale the stream up or down, so the data records never lose before they expire
- **Fault tolerance**: The Kinesis Client Library enables fault-tolerant consumption of data from streams and provides scaling support for Kinesis Data Streams applications
- **Security**: Data can be secured at-rest by using server-side encryption and AWS KMS master keys on sensitive data within Kinesis Data Streams. Access data privately via your Amazon Virtual Private Cloud (VPC)

[Pricing](https://aws.amazon.com/kinesis/data-streams/pricing/)

- KDS has no upfront cost, and you only pay for the resources you use (e.g., $0.015 per Shard Hour.)

#### MSK vs Kinesis

- Both Apache Kafka and AWS Kinesis Data Streams are good choices for real-time data streaming platforms. If you need to keep messages for more than 7 days with no limitation on message size per blob, Apache Kafka should be your choice. However, Apache Kafka requires extra effort to set up, manage, and support. If your organization lacks Apache Kafka experts and/or human support, then choosing a fully-managed AWS Kinesis service will let you focus on the development. AWS Kinesis is catching up in terms of overall performance regarding throughput and events processing.
- Both services are publish-subscribe (pub-sub) systems, which means producers publish messages to Kinesis/MSK and consumers subscribe to Kinesis/MSK to read those messages. An inherent benefit of adopting pub-sub systems is the decoupling of message producers from message consumers.
- Availability, Scalability, and Ease of Management:
  - Kinesis:
    - It synchronously replicates data across three availability zones.
    - One shard provides an ingest capacity of 1MB/sec or 1000 records/sec.
    - Provides auto-scaling capabilities using APIs that can trigger scaling actions based on usage metrics, or to auto-scale based on record throughput.
    - The Kinesis streams remain fully functional during the scaling process and producers & consumers can continue to read/write to the streams during these operations.
  - MSK:
    - It requires a cluster-sizing exercise prior to resource provisioning.
    - When an MSK cluster is configured , the brokers are spread across three availability zones by default.
    - Using MSK APIs you can scale out your MSK cluster by adding more brokers.
  - With low volumes of data, Kinesis is a preferred service because of its ease of use and minimal operational management. However, if you currently operate a Kafka cluster on-premise or have high volume workloads and are evaluating your options in AWS, MSK may be the correct choice.
- Integration with other AWS Services
  - Kinesis:
    - **Kinesis Firehose**: To load data into S3/Redshift/Amazon ElasticSearch/Splunk.
    - **Kinesis Data Analytics**: To build and deploy SQL or Flink applications.
    - **AWS Lambda**: Serverless compute-to-perform custom stream processing.
    - **AWS EMR**: To process big data leveraging the Spark or Flink framework.
    - **EC2 / Fargate / EKS**: To build custom streaming applications.
  - MSK:
    - **Kinesis Data Analytics**: To build and deploy SQL or Flink applications.
    - **Amazon EMR**: To process big data leveraging the Spark or Flink framework.
    - **EC2 / Fargate / EKS**: To build custom streaming applications. There are some very powerful, easy to use, open source streaming frameworks specific to Kafka, like KSQL and the Streams API that expedite pipeline development. However, these do require operational expertise to be deployed in a scalable manner.
- Price and Cost:
  - [Kinesis](https://aws.amazon.com/kinesis/data-streams/pricing/):
    - Uses a pay-as-you-go pricing model.
    - Pricing is based on Shard-Hour and per 25KB payload.
    - One shard provides ingest capacity of 1MB/sec or 1000 records/sec.
    - A Shard Hour is the number of shards used by your stream, charged at an hourly rate.
  - [MSK](https://aws.amazon.com/msk/pricing/):
    - You pay for the number of instances in your cluster and the storage volumes attached to them.
- Message Delivery:
  - Message delivery semantics are critical to building fault-tolerant streaming data pipelines.
  - There are three message delivery semantics:
    - **At-least-once delivery** - In the event a system fails or a network issue occurs, a message producer may continue to retry a message until it receives a successful acknowledgement. This can cause message duplication in the streaming platform. Hence, consumer applications must handle these scenarios by explicitly de-duplicating messages.
    - **At-most-once delivery** — If message producers are configured to not retry messages, it can lead to data loss if the streaming platform fails to commit and acknowledge the message. Consumers are only guaranteed messages that were successfully written to the streaming platform. Data loss is a serious problem for most businesses but its significance can vary based on your use case, specially if the original message can be recovered or reproduced easily
    - **Exactly-once delivery** — The perfect world where a producer sends a message, it is written exactly once to the streaming platform and no duplication of messages or data loss occurs when a consumer reads that message.
  - Kinesis provides at-least-once message delivery, to anticipate and handle Kinesis duplicate records, refer to the [guidance provided](https://docs.aws.amazon.com/streams/latest/dev/kinesis-record-processor-duplicates.html). while MSK (Kafka) provides exactly-once delivery, to utilize usage of its transactions API, refer to this [article](https://www.confluent.io/blog/transactions-apache-kafka/).
- [Another comparison](https://cloudonaut.io/versus/messaging/kinesis-data-streams-vs-msk/)

#### Reference

- [Medium article](https://medium.com/faun/apache-kafka-vs-apache-kinesis-57a3d585ef78)
- [Another Medium article](https://medium.com/slalom-build/a-guide-to-choosing-the-right-streaming-solution-for-you-on-aws-57089f03e034)

### Query services

#### Amazon Athena

- [Amazon Athena](https://docs.aws.amazon.com/athena/latest/ug/what-is.html) is an interactive query service that makes it easy to analyze data directly in Amazon Simple Storage Service (Amazon S3) using standard [SQL](https://docs.aws.amazon.com/athena/latest/ug/ddl-sql-reference.html).
- Athena is serverless and scales automatically.
- Athena helps you analyze unstructured, semi-structured, and structured data stored in Amazon S3. Examples include CSV, JSON, or columnar data formats such as Apache Parquet and Apache ORC.
- You can use Athena to run ad-hoc queries using ANSI SQL, without the need to aggregate or load the data into Athena.
- Athena integrates with Amazon QuickSight for easy data visualization.
- You can use Athena to generate reports or to explore data with business intelligence tools or SQL clients connected with a JDBC or an ODBC driver.
- Athena integrates with the AWS Glue Data Catalog. This allows you to create tables and query data in Athena based on a central metadata store available throughout your AWS account and integrated with the ETL and data discovery features of AWS Glue.
- You can access Athena using the AWS Management Console, a JDBC or ODBC connection, the Athena API, the Athena CLI, the AWS SDK, or AWS Tools for Windows PowerShell.
- In Athena, tables and databases are containers for the metadata definitions that define a schema for underlying source data. For each dataset, a table needs to exist in Athena. The metadata in the table tells Athena where the data is located in Amazon S3, and specifies the structure of the data, for example, column names, data types, and the name of the table. Databases are a logical grouping of tables, and also hold only metadata and schema information for a dataset.
- When you query an existing table, under the hood, Amazon Athena uses Presto, a distributed SQL engine.
- In regions where AWS Glue is supported, Athena uses the AWS Glue Data Catalog as a central location to store and retrieve table metadata throughout an AWS account.

### Data Transformation

#### AWS Data Pipeline

- [AWS Data Pipeline](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/what-is-datapipeline.html) is a web service that you can use to automate the movement and transformation of data.
- With AWS Data Pipeline, you can define data-driven workflows, so that tasks can be dependent on the successful completion of previous tasks.
- You define the parameters of your data transformations and AWS Data Pipeline enforces the logic that you've set up.
- AWS Data Pipeline workflow:
  - A [**pipeline definition**](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-writing-pipeline-definition.html) specifies the business logic of your data management.
  - A **pipeline** schedules and runs tasks by creating Amazon EC2 instances to perform the defined work activities.
  - [**Task Runner**](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/dp-how-remote-taskrunner-client.html) polls for tasks and then performs those tasks. For example, Task Runner could copy log files to Amazon S3 and launch Amazon EMR clusters.
- You can create, access, and manage your pipelines using: AWS Management Console, AWS CLI, AWS SDKs, and Query API
- AWS Data Pipeline works with the following services to store data:
  - Amazon DynamoDB
  - Amazon RDS
  - Amazon Redshift
  - Amazon S3
- AWS Data Pipeline works with the following compute services to transform data:
  - Amazon EC2
  - Amazon EMR
- [Pricing](https://aws.amazon.com/datapipeline/pricing/)

![Data Pipeline example](https://docs.aws.amazon.com/datapipeline/latest/DeveloperGuide/images/dp-how-dp-works-v2.png)

#### Amazon EMR

- [Amazon EMR](https://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-what-is-emr.html) is a managed cluster platform that simplifies running big data frameworks, such as Apache Hadoop and Apache Spark, on AWS to process and analyze vast amounts of data.
- By using these frameworks and related open-source projects, such as Apache Hive and Apache Pig, you can process data for analytics purposes and business intelligence workloads.
- Additionally, you can use Amazon EMR to transform and move large amounts of data into and out of other AWS data stores and databases, such as Amazon Simple Storage Service (Amazon S3) and Amazon DynamoDB.

## Global Infrastructure and Reliability

### Region

- Region: It is a Geographic location that consists of at least two Availability Zones, and each AZ is physically distant from each other.
- When determining the right Region for your services, data, and applications, consider the following four business factors.
  1. Compliance:
     - Compliance with data governance and legal requirements.
     - Depending on your company and location, you might need to run your data out of specific areas. For example, if your company requires all of its data to reside within the boundaries of the UK, you would choose the London Region.
  2. Proximity:
     - Selecting a Region that is close to your customers will help you to get content to them faster.
  3. Features Availability:
     - Sometimes, the closest Region might not have all the features.
     - AWS is frequently innovating by creating new services and expanding on features within existing services. However, making new services available around the world sometimes requires AWS to build out physical hardware one Region at a time.
  4. Pricing:
     - Cost of services can vary from Region to Region.
     - Suppose that you are considering running applications in both the United States and Brazil. The way Brazil’s tax structure is set up, it might cost 50% more to run the same workload out of the São Paulo Region compared to the Oregon Region.

### Availability Zone

- An Availability Zone is a single data center or a group of data centers within a Region.
- An Availability Zone is a fully isolated portion of the AWS global infrastructure.
- Availability Zones are located tens of miles apart from each other. This is close enough to have low latency (the time between when content requested and received) between Availability Zones. However, if a disaster occurs in one part of the Region, they are distant enough to reduce the chance that multiple Availability Zones are affected.
- Planning for failure and deploying applications across multiple Availability Zones is an important part of building a resilient and highly available architecture.

### Edge Locations

- An edge location is a site that [Amazon CloudFront](https://aws.amazon.com/cloudfront) uses to store cached copies of your content closer to your customers for faster delivery.

#### Amazon CloudFront

Amazon CloudFront is a content delivery service. It uses a network of edge locations to cache content and deliver content to customers all over the world. When content is cached, it is stored locally as a copy. This content might be video files, photos, webpages, and so on.

### AWS Outposts / Local Zone

- [AWS Outposts](https://aws.amazon.com/outposts/) is a service that enables you to run infrastructure in a hybrid cloud approach. Extend AWS infrastructure and services to your on-premises data center.
- Local Zone is dedicated servers for companies that exists in the company premises but owned and managed by AWS.

### Global Infrastructure additional resources

- [Global Infrastructure](https://aws.amazon.com/about-aws/global-infrastructure/)
- [Regions and AZ](https://aws.amazon.com/about-aws/global-infrastructure/regions_az)
- [Interactive map of the AWS Global Infrastructure](https://infrastructure.aws/)
- [Choosing Regions and Availability Zones](https://docs.aws.amazon.com/AmazonElastiCache/latest/mem-ug/RegionsAndAZs.html)
- [AWS Networking and Content Delivery Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/)
- [Tools to Build on AWS](https://aws.amazon.com/tools/)
- [AWS Customer Stories: Content Delivery](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23content-delivery)

## Provision AWS resources

### AWS Management Console

- It is a web-based interface for accessing and managing AWS services.
- There is AWS Console mobile application to perform tasks such as monitoring resources, viewing alarms, and accessing billing information. Multiple identities can stay logged into the AWS Console mobile app at the same time.

### AWS Command Line Interface

- AWS CLI enables you to control multiple AWS services directly from the command line within one tool. AWS CLI is available for users on Windows, macOS, and Linux.
- By using AWS CLI, you can automate the actions that your services and applications perform through scripts. For example, you can use commands to launch an Amazon EC2 instance, connect an Amazon EC2 instance to a specific Auto Scaling group, and more.

### Software Development Kit

- SDKs make it easier for you to use AWS services through an API designed for your programming language or platform.
- SDKs enable you to use AWS services with your existing applications or create entirely new applications that will run on AWS.

### AWS Elastic Beanstalk

With AWS Elastic Beanstalk, you provide code and configuration settings, and Elastic Beanstalk deploys the resources necessary to perform the following tasks:

- Adjust capacity
- Load balancing
- Automatic scaling
- Application health monitoring

AWS Elastic Beanstalk can save environment configurations, so they can be deployed again easily.

### AWS CloudFormation

- AWS CloudFormation is an infrastructure as code tool that allows you to define a wide variety of AWS resources in a declarative way using JSON or YAML text-based documents called CloudFormation templates. This means that you can build an environment by writing lines of code,  instead of using the AWS Management Console to individually provision resources, and CloudFormation engine will call APIs to get everything built out.
- AWS CloudFormation provisions your resources in a safe, repeatable manner, enabling you to frequently build your infrastructure and applications without having to perform manual actions or write custom scripts. It determines the right operations to perform when managing your stack and rolls back changes automatically if it detects errors.
- CloudFormation supports many different AWS resources from storage, databases, analytics, machine learning, and more.

## Networking

Slash notation:

- In AWS, IP addresses ranges from 192.168.0.0/16 to 192.168.0.0/28
- 192.168.0.0/16 means that there are 16 bits for the network and 16 bits for the host with $2^{16}=65,536$ possible IP addresses
- 192.168.0.0/17 means that there are 17 bits for the network and 15 bits for the host with $2^{15}=32,768$ possible IP addresses
- 192.168.0.0/28 means that there are 28 bits for the network and 4 bits for the host with $2^4=16$ possible IP addresses
- 192.168.0.0/n means that there are n bits for the network and 32-n bits for the host with $2^{32-n}$ possible IP addresses
- There are no range 192.168.0.0/29 because it has 8 possible IP addresses and AWS takes 5 IPs from any configured network. 4 from the beginning and the last IP address.

### VPC

- [Amazon Virtual Private Cloud (VPC)](https://aws.amazon.com/vpc/) is a networking service that you can use to establish boundaries around your AWS resources
- Provision a private, isolated virtual network on the AWS cloud.
- Have a complete control over your virtual networking environment.
- A virtual network over a physical network.
- VPC is created inside a region and can stretch across Availability Zones (AZs) inside this region.

#### Subnets

- A subnet is a section of a VPC in which can group resources,such as Amazon EC2 instances, based on security or operational needs.
- Subnets can be public or private.
- Subnets consists of Route Tables. Route Tables are used for communication between the subnets inside the VPC and outside.
- All subnets have Local route by default that allows communication with each other.

Public Subnet:

- If a subnet has [IGW (Internet Gateway)](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Internet_Gateway.html) route, then it considered as Public subnet.
- An internet gateway is a connection between a VPC and the internet.

Private Subnet

- If a subnet has VPG (Virtual Private Gateway) route, then it is considered as VPN only subnet.
- The virtual private gateway is the component that allows protected internet traffic to enter into the VPC.
- A virtual private gateway enables you to establish a virtual private network (VPN) connection between your VPC and a private network, such as an on-premises data center or internal corporate network.
- A virtual private gateway allows traffic into the VPC only if it is coming from an approved network. This connection is through the public internet but with end-to-end encryption.

#### Network traffic in a VPC

- When a customer requests data from an application hosted in the AWS Cloud, this request is sent as a packet. A packet is a unit of data sent over the internet or a network.
- It enters into a VPC through an internet gateway. Before a packet can enter into a subnet or exit from a subnet, it checks for permissions. These permissions indicate who sent the packet and how the packet is trying to communicate with the resources in a subnet.
- The VPC component that checks packet permissions for subnets is a network [access control list (ACL)](https://docs.aws.amazon.com/vpc/latest/userguide/vpc-network-acls.html).

#### Network access control lists (NACLs)

- A network access control list (ACL) is a virtual firewall that controls inbound and outbound traffic at the subnet level.
- Each AWS account includes a default network ACL.
- The default ACL allows all inbound and outbound traffic.
- For custom network ACLs, all inbound and outbound traffic is denied until you add rules to specify which traffic to allow.
- Additionally, all network ACLs have an explicit deny rule. This rule ensures that if a packet doesn’t match any of the other rules on the list, the packet is denied.
- Stateless packet filtering
  - Network ACLs perform stateless packet filtering. They remember nothing and check packets that cross the subnet border each way: inbound and outbound.
  - When a packet response for that request comes back to the subnet, the network ACL does not remember your previous request. The network ACL checks the packet response against its list of rules to determine whether to allow or deny.
- After a packet has entered a subnet, it must have its permissions evaluated for resources within the subnet, such as Amazon EC2 instances.
- The VPC component that checks packet permissions for an Amazon EC2 instance is a [security group](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_SecurityGroups.html).

#### Security Group

- A security group is a virtual firewall that controls inbound and outbound traffic for an Amazon EC2 instance.
- By default, a security group denies all inbound traffic and allows all outbound traffic.
- Same security group can be associated to multiple EC2 instances.
- Stateful packet filtering
  - Security groups perform stateful packet filtering. They remember previous decisions made for incoming packets.
  - When a packet response for that request returns to the instance, the security group remembers your previous request. The security group allows the response to proceed, regardless of inbound security group rules.

#### Network Address Translation (NAT) Gateway

- A managed NAT gateway
- Allow instances in Private Subnets to access the Internet, to download software, access public services, etc., but not the other way around
- Charges hourly + traffic

#### Elastic IP (EIP)

- An AWS-owned public IP address that can be allocated and associated to instances
- Once allocated, an EIP is dedicated to the user until it is released
- Instances with EIP associated do not change their public IP addresses after rebooting

#### PrivateLink

- A term used to describe the internal networking mechanism that allows user to access AWS services without going through public Internet

#### VPC Endpoint

- A private endpoint powered by PrivateLink that allows private access to S3, DynamoDB, etc.

### AWS Direct Connect

- [AWS Direct Connect](https://aws.amazon.com/directconnect/) is a service that enables you to establish a dedicated private connection between your data center and a VPC.

### Amazon Route 53

- [Amazon Route 53](https://aws.amazon.com/route53) is a DNS web service. It gives developers and businesses a reliable way to route end users to internet applications hosted in AWS.
- Amazon Route 53 connects user requests to infrastructure running in AWS (such as Amazon EC2 instances and load balancers). It can route users to infrastructure outside of AWS.
- Other features of Route 53:
  - Manage the DNS records for domain names.
  - Register new domain names directly in Route 53.
  - Transfer DNS records for existing domain names managed by other domain registrars.

![VPC Overview](https://theawsdotblog.files.wordpress.com/2020/05/image-14.png)

### Networking additional resources

- [Networking and Content Delivery on AWS](https://aws.amazon.com/products/networking)
- [AWS Networking & Content Delivery Blog](https://aws.amazon.com/blogs/networking-and-content-delivery/)
- [Amazon Virtual Private Cloud](https://aws.amazon.com/vpc)
- [What is Amazon VPC?](https://docs.aws.amazon.com/vpc/latest/userguide/what-is-amazon-vpc.html)
- [How Amazon VPC works](https://docs.aws.amazon.com/vpc/latest/userguide/how-it-works.html)
- [VPC and Subnets](https://docs.aws.amazon.com/vpc/latest/userguide/VPC_Subnets.html)

## Storage Services

### Block Storage

#### Instance Store

- Block-level storage volumes behave like physical hard drives.
- An [instance store](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/InstanceStorage.html) provides temporary block-level storage for an Amazon EC2 instance.
- An instance store is physically attached to the host computer for an EC2 instance, and therefore has the same lifespan as the instance.
- A lighting speed volumes, up to 365,000 IOPs
- Volatile storage, can't be retrieved

#### EBS

- [Amazon Elastic Block Store (Amazon EBS)](https://aws.amazon.com/ebs) is a service that provides block-level storage volumes used Amazon EC2 instances. If you stop or terminate an Amazon EC2 instance, all the data on the attached EBS volume remains available.
- Persistent block level storage volumes offer consistent and low-latency performance.
- Stored data is automatically replicated within its Availability Zone.
- Snapshots are stored durably in Amazon S3.

EBS Facts:

- Availability Zone level resource. It needs to be in the same AZ to attach EC2 instances.
- EBS is recommended when data must be quickly accessible and requires long-term persistence
- Volumes do not automatically scale
- You can launch your EBS volumes as encrypted volumes. Data stored at rest on the volume, disk I/O, and snapshots created from the volume are all encrypted.
- To create an EBS volume, you define the configuration (such as volume size and type) and provision it. After you create an EBS volume, it can attach to an Amazon EC2 instance.
- You can create point-in-time [snapshots of EBS volumes](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EBSSnapshots.html), which are persisted to Amazon S3.
  - An EBS snapshot is an incremental backup. This means that the first backup taken of a volume copies all the data. For subsequent backups, only the blocks of data that have changed since the most recent snapshot are saved.
- Can be attached to only one EC2 instance.

It has two main volume types

- SSD:
  - General Purpose SSD (gp2):
    - Balanced price and performance for a wide variety of transactional loads.
    - It size can range from 1GiB - 16 TiB
    - Each 1GB of storage gives 3 IOPs. Purchased together.
  - Provisioned IOPs SSD (io1):
    - Highest-performance SSD volume designed for mission-critical applications.
    - It size ranges from 4 GiB - 16 TiB
    - Size and speed are configured separately. Purchased individually.
- HDD:
  - Throughput Optimized:
    - Low-cost HDD designed for frequently accessed, throughput-intensive workloads.
    - It size ranges from 500 GiB - 16 TiB
  - Cold:
    - Lowest cost HDD designed for less frequent accessed workloads.
    - It size ranges from 500 GiB - 16 TiB

Use Cases:

- **OS:** Use for boot/root volume, secondary volumes
- **Databases:** Scales with your performance needs
- **Enterprise applications:** Provides reliable block storage to run mission-critical applications
- **Business continuity:** Minimize data loss and recovery time by regularly backing up using EBS Snapshots
- **Applications:** Install and persist any application

Pricing:

- Pay for what you provision
- Pricing based on region
- Review pricing calculator online
- Pricing available as:
  - Storage
  - IOPs

### Object Storage

[What is object cloud storage?](https://aws.amazon.com/what-is-cloud-object-storage/)

#### S3

- [Amazon Simple Storage Service (Amazon S3)](https://aws.amazon.com/s3/) is a service that provides object-level storage.
- Amazon S3 stores data as objects in buckets.
- Storage for the Internet
- Natively online, HTTP access
- Storage that allows you to store and retrieve any amount of data, any time, from anywhere on the web.
- Highly scalable, reliable, fast and durable.

Some Facts:

- Can set permissions to control visibility and access to it.
- Objects created are replicated in 3 different AZs within same region
- Can store an unlimited number of objects in a bucket
- Objects can be up to 5 TB; no bucket size limit
- Designed for 99.999999999% durability and 99.99% availability of objects over a given year
- Can use HTTP/S endpoints to store and retrieve any amount of data, at any time, from anywhere on the web
- Highly scalable, reliable, fast, and inexpensive
- Can use optional server-side encryption using AWS or customer-managed provided client-side encryption
- Auditing is provided by access logs
- Provides standards-based REST and SOAP interfaces

[Storage Classes](https://aws.amazon.com/s3/storage-classes):

- S3 Standard
  - Designed for frequently accessed data
  - Stores data in a minimum of three Availability Zones
  - High availability for objects
  - Common Use Scenarios
    - Websites
    - Storage and backup
    - Application file hosting
    - Media Hosting
    - Software delivery
    - Storage AMIs and snapshots
  - S3 Standard has a higher cost than other storage classes intended for infrequently accessed data and archival storage.

- S3 Standard-Infrequent Access (S3 Standard-IA)
  - Ideal for infrequently accessed data
  - Similar to S3 Standard but has a lower storage price and higher retrieval price

- S3 One Zone-Infrequent Access (S3 One Zone-IA)
  - Stores data in a single Availability Zone
  - Has a lower storage price than S3 Standard-IA
  - Good choice if:
    - You want to save costs on storage.
    - You can easily reproduce your data in the event of an Availability Zone failure.

- S3 Intelligent-Tiering
  - Ideal for data with unknown or changing access patterns
  - Requires a small monthly monitoring and automation fee per object
  - Moves objects to S3 Standard-IA, if object not accessed for 30 consecutive days. And if the object is accessed, it will be moved to S3 Standard

- S3 Glacier
  - Low-cost storage designed for data archiving
  - Able to retrieve objects within a few minutes to hours
  - Long term low-cost archiving service
  - Optimal for infrequently accessed data
  - Designed for 99.999999999% durability
  - Three to five hours' standard retrieval time
  - Less than $0.01 per GB/month (depending on region)

- S3 Glacier Deep Archive
  - Lowest-cost object storage class ideal for archiving
  - Able to retrieve objects within 12 hours

Versioning

- Protects from accidental overwrites and deletes with no performance penalty.
- Generates a new version with every upload.
- Allows easily retrieval of deleted objects or roll back to previous versions.
- Three states of an Amazon S3 bucket
  - Un-versioned (default)
  - Versioning-enabled
  - Versioning-suspended

Pricing

- Pay only for what you use
- No minimum fee
- Prices based on location of your Amazon S3 bucket
- Estimate monthly bill using the AWS Simple Monthly Calculator
- Pricing is available as:
  - Storage Pricing
  - Request Pricing
  - Data Transfer Pricing: data transferred out of Amazon S3

### File Storage

- In file storage, multiple clients (such as users, applications, servers, and so on) can access data that is stored in shared file folders.
- In this approach, a storage server uses block storage with a local file system to organize files.
- File storage is ideal for use cases in which a large number of services and resources need to access the same data at the same time.

#### EFS

- [Amazon Elastic File System (Amazon EFS)](https://aws.amazon.com/efs/) is a scalable file system used with AWS Cloud services and on-premises resources.
- On-premises servers can access Amazon EFS using AWS Direct Connect.
- Multiple instances reading and writing simultaneously.
- Linux file system
- Regional resource
- Automatically scales
- [How it works](https://docs.aws.amazon.com/efs/latest/ug/how-it-works.html)

#### FSx

- Microsoft Windows files system
- The highest storage throughput

#### Storage types speed comparison

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

### Storage additional resources

- [Cloud Storage on AWS](https://aws.amazon.com/products/storage)
- [AWS Storage Blog](https://aws.amazon.com/blogs/storage/)
- [Hands-On Tutorials: Storage](https://aws.amazon.com/getting-started/hands-on/?awsf.getting-started-category=category%23storage&awsf.getting-started-content-type=content-type%23hands-on)
- [AWS Customer Stories: Storage](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23storage)

## Databases

|              | SQL              | NoSQL                              |
| ------------ | ---------------- | ---------------------------------- |
| Data Storage | Rows and Columns | Key-Value                          |
| Schemas      | Fixed            | Dynamic                            |
| Querying     | Using SQL        | Focused on collection of documents |
| Scalability  | Vertical         | Horizontal                         |

### RDS

- [Amazon Relational Database Service (Amazon RDS)](https://aws.amazon.com/rds/) is a service that enables you to run relational databases in the AWS Cloud.
- It is a managed service that automates tasks such as:
  - hardware provisioning
  - database setup
  - patching
  - backups
- Cost-efficient and resizable capacity
- Simple and fast to deploy and scale
- Manages time-consuming database administration tasks
- Fast, predictable performance
- Secure. Many Amazon RDS database engines offer encryption at rest (protecting data while it is stored) and encryption in transit (protecting data while it is being sent and received).
- Compatible with your applications
- Amazon RDS is available on six database engines, which optimize for memory, performance, or input/output (I/O). Supported database engines include:
  - Amazon Aurora
  - MySQL
  - MariaDB
  - Microsoft SQL Server
  - Oracle
  - PostgreSQL

DB Instances:

- DB Instances are the basic building blocks of Amazon RDS.
- They are an isolated database environment in the cloud.
- They can contain multiple user-created databases

How Backups Work:

- Automatic Backups
  - Restore your database to a point in time.
  - Are enabled by default.
  - Let you choose a retention period up to 35 days.
- Manual Snapshots
  - Let you build a new database instance from a snapshot.
  - Are initiated by the user.
  - Persist until the user deletes them.
  - Are stored in Amazon S3.
- Cross-Region Snapshots
  - Are a copy of a database snapshot stored in a different AWS region.
  - Provide a backup for disaster recovery.
  - Can be used as a base for migration to a different region.

### Amazon Aurora

- [Amazon Aurora](https://aws.amazon.com/rds/aurora/) is an enterprise-class relational database.
- It is compatible with MySQL and PostgreSQL relational databases.
- 5x faster than MySQL, and 3x faster than PostgreSQL.
- It replicates six copies of data across three Availability Zones and continuously backs up data to Amazon S3.
- It helps to reduce database costs by reducing unnecessary I/O operations

### Amazon DynamoDB

- [Amazon DynamoDB](https://aws.amazon.com/dynamodb/) is a key-value (NoSQL) database service.
- It delivers single-digit millisecond performance at any scale.
- Scaling up to 10 trillion requests per day
- Store any amount of data with no limits up to PetaBytes. But item size can not exceed 400k
- Provides fast, predictable performance using SSDs.
- Allows you to easily provision and change the request capacity needed for each table.
- Is a fully managed, NoSQL database service.
- It is serverless, no need for provision, patch, manage servers, install, maintain, or operate software.

Supported Operations

- Query:
  - Query a table using the partition key and an optional sort key filter.
  - If the table has a secondary index, query using its key.
  - It is the most efficient way to retrieve items from a table or secondary index.
- Scan:
  - You can scan a table or secondary index.
  - Scan reads every item - slower than querying.
- You can use conditional expressions in both Query and Scan operations.

### Amazon RedShift

- [Amazon Redshift](https://aws.amazon.com/redshift) is a data warehousing service.
- Used for big data analytics.
- Collect data from many sources.
- Help to understand relationships and trends across the data.

### AWS DMS

- [AWS Database Migration Service (AWS DMS)](https://aws.amazon.com/dms/) enables you to migrate relational databases, nonrelational databases, and other types of data stores.
- [The source and target databases](https://aws.amazon.com/dms/resources) can be of the same type or different types.
- During the migration, the source database remains operational.
- Development and test database migrations
- Database consolidation. Combining several databases into a single database.
- continuous replication by sending ongoing copies of your data to other target sources instead of doing a one-time migration

### Amazon DocumentDB

[Amazon DocumentDB](https://aws.amazon.com/documentdb) is a document database service that supports MongoDB workloads. (MongoDB is a document database program.)

### Amazon Neptune

[Amazon Neptune](https://aws.amazon.com/neptune) is a graph database service.

You can use Amazon Neptune to build and run applications that work with highly connected datasets, such as recommendation engines, fraud detection, and knowledge graphs.

### Amazon QLDB

[Amazon Quantum Ledger Database (Amazon QLDB)](https://aws.amazon.com/qldb) is a ledger database service.

You can use Amazon QLDB to review a complete history of all the changes that have been made to your application data.

### Amazon Managed Blockchain

[Amazon Managed Blockchain](https://aws.amazon.com/managed-blockchain) is a service that you can use to create and manage blockchain networks with open-source frameworks.

Blockchain is a distributed ledger system that lets multiple parties run transactions and share data without a central authority.

### Amazon ElastiCache

[Amazon ElastiCache](https://aws.amazon.com/elasticache) is a service that adds caching layers on top of your databases to help improve the read times of common requests.

It supports two types of data stores: Redis and Memcached.

### Amazon DAX

[Amazon DynamoDB Accelerator (DAX)](https://aws.amazon.com/dynamodb/dax/) is an in-memory cache for DynamoDB.

It helps improve response times from single-digit milliseconds to microseconds.

### Databases additional resources

- [AWS Database Migration Service](https://aws.amazon.com/dms/)
- [Databases on AWS](https://aws.amazon.com/products/databases)
- [Category Deep Dive: Databases](https://aws.amazon.com/getting-started/deep-dive-databases/)
- [AWS Database Blog](https://aws.amazon.com/blogs/database/)
- [AWS Customer Stories: Databases](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23databases)

## Security

### AWS [Shared Security Model](https://aws.amazon.com/compliance/shared-responsibility-model/)

1. AWS: is responsible for security OF the cloud
   - AWS services:
     - Compute
     - Storage
     - Database
     - Networking
   - AWS Global Infrastructure
     - Regions
     - Availability Zones
     - Edge Locations
2. Customers: are responsible for security IN the cloud
   - Customer Applications and Content
   - Platform, Applications, Identity, and Access Management
   - Operating System, Network, and Firewall Configuration
   - Client-side Data Encryption
   - Server-side Data Encryption
   - Network Traffic Protection

### IAM

[AWS Identity and Access Management (IAM)](https://aws.amazon.com/iam/) enables you to manage access to AWS services and resources securely.

- [Root user](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_root-user.html):
  - The root user is accessed by signing in with the email address and password that used to create the AWS account.
  - It has complete access to all the AWS services and resources in the account.
- User:
  - It is an identity that you create in AWS
    - Access Key ID and Security Access Key, to have programmatic access (SDK, CLI)
    - User name and password, to have console management access.
  - By default, it has no permissions associated with it.
- Policy:
  - It is a document that allows or denies permissions to AWS services and resources
  - These permissions set, can be linked to a User, a Group, or a Role
- [Group](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_groups.html):
  - A collection of IAM users
  - Assigned to users (ex: IT Group). All users in the group are granted permissions specified by the policy.
  - It is easier to adjust permissions when an employee transfers to a different job.
- [Role](https://docs.aws.amazon.com/IAM/latest/UserGuide/id_roles.html):
  - Permissions set that can be linked to a User or a Resource (EC2, Lambda).
  - It is beneficial when a temporary access is required.
- [MFA](https://aws.amazon.com/iam/features/mfa/)
  - In IAM, multi-factor authentication (MFA) provides an extra layer of security for your AWS account.

[Best Practices](https://docs.aws.amazon.com/IAM/latest/UserGuide/best-practices.html):

- Delete AWS account (root) access keys.
- Create individual IAM users.
- Use groups to assign permissions to IAM users.
- Grant least privilege.
- Configure a strong password policy.
- Enable MFA (Multi-Factor Authentication) for privileged users.
- Use roles for applications that run on Amazon EC2 instances.
- Delegate by using roles instead of by sharing credentials.
- Rotate credentials regularly.
- Remove unnecessary users and credentials.
- Use policy conditions for extra security.
- Monitor activity in your AWS account. Using AWS Cloud Trail

AWS CloudTrail:

- Records AWS API calls for accounts.
- Delivers log files with information to an Amazon 53 bucket.
- Make calls using the AWS Management Console, AWS SDKs, AWS CLI
and higher-level AWS services.

### AWS Multi-Tier (Defense In-depth) Security Groups

Instance Firewall: Use security groups to configure firewall rules for instances.

- Web tier:
  - It is a security group that gives access to public internet (HTTP/s) and corporate network (ssh, rdp).
  - It communicates with Application tier with APIs.
- Application tier:
  - It is a security group that gives only access to Corporate network (ssh, rdp).
  - It can communicate with Web tier and Database tier with APIs.
- Database tier:
  - It is a security group that gives only access to Corporate network (ssh, rdp).
  - It can communicate with Application tier with APIs.

### VPC: Network Control

- Use public and private subnets, NAT, and VPN support in your virtual private cloud to create low-level networking constraints for resource access.

### AWS Organizations

- [AWS Organizations](https://aws.amazon.com/organizations) used to consolidate and manage multiple AWS accounts within a central location.
- AWS Organizations automatically creates a root, which is the parent container for all the accounts in your organization.

[Service control policies (SCPs)](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps.html)

- SCP centrally control permissions for the accounts in the organization.
- SCPs place restrictions on the AWS services, resources, and individual API actions that users and roles in each account can access.
- SCPs are [attached](https://docs.aws.amazon.com/organizations/latest/userguide/orgs_manage_policies_scps_attach.html) to the organization root, an individual member account, or an OU

Organizational units

- Hierarchical groupings of accounts.
- Accounts are grouped into organizational units (OUs)
- All the accounts in the OU automatically inherit the permissions specified in the policy.

Consolidated billing

### Compliance

#### AWS Artifact

- [AWS Artifact](https://aws.amazon.com/artifact) is a service that provides on-demand access to AWS security and compliance reports and select online agreements.
- AWS Artifact consists of two main sections:
  - AWS Artifact Agreements
    - In AWS Artifact Agreements, you can review, accept, and manage agreements for an individual account and for all your accounts in AWS Organizations.
  - AWS Artifact Reports
    - AWS Artifact Reports provide compliance reports from third-party auditors.
    - These auditors have tested and verified that AWS is compliant with a variety of global, regional, and industry-specific security standards and regulations.
    - AWS Artifact Reports remains up to date with the latest reports released.

#### Customer Compliance Center

- The [Customer Compliance Center](https://aws.amazon.com/compliance/customer-center/) contains resources to help you learn more about AWS compliance.
- In the Customer Compliance Center, you can read customer compliance stories to discover how companies in regulated industries have solved various compliance, governance, and audit challenges.

### DDoS

- A denial-of-service (DoS) attack is a deliberate attempt to make a website or application unavailable to users.
- In a distributed denial-of-service (DDoS) attack, multiple sources are used to start an attack that aims to make a website or application unavailable.

#### AWS Shield

- AWS Shield is a service that protects applications against DDoS attacks. AWS Shield provides two levels of protection
  - Standard
    - AWS Shield Standard automatically protects all AWS customers at no cost. It protects your AWS resources from the most common, frequently occurring types of DDoS attacks.
    - As network traffic comes into your applications, AWS Shield Standard uses a variety of analysis techniques to detect malicious traffic in real time and automatically mitigates it.
  - Advanced
    - AWS Shield Advanced is a paid service that provides detailed attack diagnostics and the ability to detect and mitigate sophisticated DDoS attacks.
    - It also integrates with other services such as Amazon CloudFront, Amazon Route 53, and Elastic Load Balancing. Additionally, you can integrate AWS Shield with AWS WAF by writing custom rules to mitigate complex DDoS attacks.

### AWS KMS

- [AWS Key Management Service (AWS KMS)](https://aws.amazon.com/kms) enables you to perform encryption operations through the use of cryptographic keys.
- AWS KMS used to create, manage, and use cryptographic keys.
- You can control the use of keys across a wide range of services and in your applications.
- With AWS KMS, you can choose the specific levels of access control that you need for your keys.

### AWS WAF

- [AWS WAF](https://aws.amazon.com/waf) is a web application firewall that lets you monitor network requests that come into your web applications.
- AWS WAF works together with Amazon CloudFront and an Application Load Balancer.
- AWS WAF block or allow traffic using a [web access control list (ACL)](https://docs.aws.amazon.com/waf/latest/developerguide/web-acl.html)

### Amazon Inspector

- [Amazon Inspector](https://aws.amazon.com/inspector/) runs automated security assessments.
- It checks applications for security vulnerabilities and deviations from security best practices, such as open access to Amazon EC2 instances and installations of vulnerable software versions.
- After assessment, it provides a list of security findings. The list prioritizes by severity level, including a detailed description of each security issue and a recommendation for how to fix it.
- However, AWS does not guarantee that following the provided recommendations resolves every potential security issue.

### Amazon GuardDuty

- [Amazon GuardDuty](https://aws.amazon.com/guardduty) is a service that provides intelligent threat detection for your AWS infrastructure and resources.
- It identifies threats by continuously monitoring the network activity and account behavior within your AWS environment.
- GuardDuty begins monitoring your network and account activity after being enabled. No need to deploy or manage any additional security software
- GuardDuty then continuously analyzes data from multiple AWS sources, including VPC Flow Logs and DNS logs.
- Detailed findings can reviewed, including recommended steps for remediation.
- AWS Lambda functions can be created to take remediation steps automatically in response to GuardDuty’s security findings.

### Security additional resources

- [Security, Identity, and Compliance on AWS](https://aws.amazon.com/products/security)
- [AWS IAM: Policies and permissions](https://docs.aws.amazon.com/IAM/latest/UserGuide/access_policies.html)
- [Whitepaper: Introduction to AWS Security](https://docs.aws.amazon.com/whitepapers/latest/introduction-aws-security/welcome.html)
- [Whitepaper: Amazon Web Services - Overview of Security Processes](https://docs.aws.amazon.com/whitepapers/latest/aws-overview-security-processes/aws-overview-security-processes.pdf)
- [AWS Security Blog](https://aws.amazon.com/blogs/security/)
- [AWS Compliance](https://aws.amazon.com/compliance)
- [AWS Customer Stories: Security, Identity, and Compliance](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23security-identity-compliance)

## Monitoring and Analytics

### Amazon CloudWatch

- [Amazon CloudWatch](https://aws.amazon.com/cloudwatch/) is a web service that enables you to monitor and manage various metrics and configure alarm actions based on data from those metrics.
- CloudWatch uses [metrics](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/working_with_metrics.html) to represent the data points for your resources.
- CloudWatch then uses these metrics to create graphs automatically that show how performance has changed over time.

CloudWatch Alarms

- Alarms created, automatically perform actions if the value of your metric has gone above or below a predefined threshold.
- When configuring the alarm, you can specify to receive a notification whenever this alarm is triggered.

CloudWatch Dashboard

- The CloudWatch [dashboard](https://docs.aws.amazon.com/AmazonCloudWatch/latest/monitoring/CloudWatch_Dashboards.html) feature enables you to access all the metrics for your resources from a single location.

### AWS CloudTrail

- [AWS CloudTrail](https://aws.amazon.com/cloudtrail/) records API calls. The recorded information includes the identity of the API caller, the time of the API call, the source IP address of the API caller, and more.
- It shows a complete history of user activity and API calls for your applications and resources.
- Events are typically updated in CloudTrail within 15 minutes after an API call.
- Events can be filtered by specifying the time and date that an API call occurred, the user who requested the action, the type of resource that was involved in the API call, and more.

[CloudTrail Insights](https://docs.aws.amazon.com/awscloudtrail/latest/userguide/logging-insights-events-with-cloudtrail.html)

- This optional feature allows CloudTrail to automatically detect unusual API activities in your AWS account.

### AWS Trusted Advisor

- [AWS Trusted Advisor](https://aws.amazon.com/premiumsupport/technology/trusted-advisor/) is a web service that inspects your AWS environment and provides real-time recommendations in accordance with AWS best practices.
- Trusted Advisor compares its findings to AWS best practices in five categories: cost optimization, performance, security, fault tolerance, and service limits.
- Trusted Advisor offers a list of recommended actions and additional resources to learn more about AWS best practices. 
- For each category:
  - The green check indicates the number of items for which it detected no problems.
  - The orange triangle represents the number of recommended investigations.
  - The red circle represents the number of recommended actions.

### Monitoring and Analytics additional resources

- [Management and Governance on AWS](https://aws.amazon.com/products/management-tools)
- [Monitoring and Observability](https://aws.amazon.com/products/management-tools/use-cases/monitoring-and-observability/)
- [Configuration, Compliance, and Auditing](https://aws.amazon.com/products/management-tools/use-cases/configuration-compliance-and-auditing/)
- [AWS Management & Governance Blog](https://aws.amazon.com/blogs/mt/)
- [Whitepaper: AWS Governance at Scale](https://docs.aws.amazon.com/whitepapers/latest/aws-governance-at-scale/introduction.html)

## Pricing and Support

### AWS Free Tier

- The [AWS Free Tier](https://aws.amazon.com/free/) enables you to begin using certain services without having to worry about incurring costs for the specified period.
- Three types of offers are available:
  - Always Free
  - 12 Months Free
  - Trials

### AWS Pricing Concepts

- Pay for what you use:
  - For each service, you pay for exactly the amount of resources that you actually use, without requiring long-term contracts or complex licensing.
- Pay less when you reserve:
  - Some services offer reservation options that provide a significant discount compared to On-Demand Instance pricing.
- Pay less with volume-based discounts when you use more:
  - Some services offer tiered pricing, so the per-unit cost is incrementally lower with increased usage.

### AWS Pricing Calculator

- The [AWS Pricing Calculator](https://calculator.aws/#/) is for exploring AWS services and creating an estimate for the cost.
- Estimates can be grouped.
- Estimates can be saved and shared via links.

### Billing dashboard

[AWS Billing & Cost Management dashboard](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/billing-what-is.html) used to pay your AWS bill, monitor your usage, and analyze and control your costs.

- Compare your current month-to-date balance with the previous month, and get a forecast of the next month based on current usage.
- View month-to-date spend by service.
- View Free Tier usage by service.
- Access Cost Explorer and create budgets.
- Purchase and manage Savings Plans.
- Publish [AWS Cost and Usage Reports](https://docs.aws.amazon.com/cur/latest/userguide/what-is-cur.html).

### Consolidated billing

- AWS Organizations also provides the option for [consolidated billing](https://docs.aws.amazon.com/awsaccountbilling/latest/aboutv2/consolidated-billing.html).
- It enables to receive a single bill for all AWS accounts in your organization.
- Easily track the combined costs of all the linked accounts in the organization.
- The default maximum number of accounts allowed for an organization is 4, but AWS Support can increase your quota, if required.
- On the monthly bill, itemized charges incurred by each account can be reviewed.
- Another benefit of consolidated billing is the ability to share bulk discount pricing, Savings Plans, and Reserved Instances across the accounts in your organization.

### AWS Budget

- In [AWS Budgets](https://aws.amazon.com/aws-cost-management/aws-budgets), you can create budgets to plan your service usage, service costs, and instance reservations.
- The information in AWS Budgets updates three times a day.
- Custom alerts can be set for when usage exceeds (or is forecasted to exceed) the budgeted amount.

### AWS Cost Explorer

- [AWS Cost Explorer](https://aws.amazon.com/aws-cost-management/aws-cost-explorer/) is a tool  to visualize, understand, and manage AWS costs and usage over time.
- AWS Cost Explorer includes a default report of the costs and usage for the top five cost-accruing AWS services.
- Apply custom filters and groups to analyze the data.

### AWS Support plans

- AWS offers four different [Support plans](https://aws.amazon.com/premiumsupport/plans/) to help you troubleshoot issues, lower costs, and efficiently use AWS services.
- Basic
  - Basic Support is free for all AWS customers.
  - It includes access to whitepapers, documentation, and support communities.
  - Contact AWS for billing questions and service limit increases.
  - Limited selection of AWS Trusted Advisor checks.
  - AWS Personal Health Dashboard, a tool that provides alerts and remediation guidance when AWS is experiencing events that may affect you.
- Developer
  - Basic Plan
  - Best practice guidance
  - Client-side diagnostic tools
  - Building-block architecture support, which consists of guidance for how to use AWS offerings, features, and services together
- Business
  - Basic + Developer Plans
  - Use-case guidance to identify AWS offerings, features, and services that can best support your specific needs
  - All AWS Trusted Advisor checks
  - Limited support for third-party software, such as common operating systems and application stack components
- Enterprise
  - Basic, Developer and Business plans
  - Application architecture guidance, which is a consultative relationship to support your company’s specific use cases and applications
  - Infrastructure event management: A short-term engagement with AWS Support that helps your company gain a better understanding of your use cases. This also provides your company with architectural and scaling guidance.
  - A Technical Account Manager

### AWS Marketplace

[AWS Marketplace](https://aws.amazon.com/marketplace) is a digital catalog that includes thousands of software listings from independent software vendors.

AWS Marketplace categories:

- Business Applications
- Data & Analytics
- DevOps
- Infrastructure Software
- Internet of Things
- Machine Learning
- Migration
- Security

### Pricing and Support additional resources

- [AWS Pricing](https://aws.amazon.com/pricing)
- [AWS Free Tier](https://aws.amazon.com/free)
- [AWS Cost Management](https://aws.amazon.com/aws-cost-management/)
- [Whitepaper: How AWS Pricing Works](https://d1.awsstatic.com/whitepapers/aws_pricing_overview.pdf)
- [Whitepaper: Introduction to AWS Economics](https://d1.awsstatic.com/whitepapers/introduction-to-aws-cloud-economics-final.pdf)
- [AWS Support](https://aws.amazon.com/premiumsupport)
- [AWS Knowledge Center](https://aws.amazon.com/premiumsupport/knowledge-center/)

## Migration and Innovation

### AWS CAF

- [AWS Cloud Adoption Framework (AWS CAF)](https://d1.awsstatic.com/whitepapers/aws_cloud_adoption_framework.pdf) organizes guidance into six areas of focus, called Perspectives.
- In general, the Business, People, and Governance Perspectives focus on business capabilities, whereas the Platform, Security, and Operations Perspectives focus on technical capabilities.
- Business Perspective:
  - The Business Perspective ensures that IT aligns with business needs and that IT investments link to key business results.
  - Common roles in the Business Perspective include:
    - Business managers
    - Finance managers
    - Budget owners
    - Strategy stakeholders
- People Perspective:
  - The People Perspective supports development of an organization-wide change management strategy for successful cloud adoption.
  - Common roles in the People Perspective include:
    - Human resources
    - Staffing
    - People managers
- Governance Perspective:
  - The Governance Perspective focuses on the skills and processes to align IT strategy with business strategy. This ensures that you maximize the business value and minimize risks.
  - Common roles in the Governance Perspective include:
    - Chief Information Officer (CIO)
    - Program managers
    - Enterprise architects
    - Business analysts
    - Portfolio managers
- Platform Perspective:
  - The Platform Perspective includes principles and patterns for implementing new solutions on the cloud, and migrating on-premises workloads to the cloud.
  - Common roles in the Platform Perspective include:
    - Chief Technology Officer (CTO)
    - IT managers
    - Solutions architects
- Security Perspective
  - The Security Perspective ensures that the organization meets security objectives for visibility, auditability, control, and agility.
  - Common roles in the Security Perspective include:
    - Chief Information Security Officer (CISO)
    - IT security managers
    - IT security analysts
- Operations Perspective:
  - The Operations Perspective helps you to enable, run, use, operate, and recover IT workloads to the level agreed upon with your business stakeholders.
  - Common roles in the Operations Perspective include:
    - IT operations managers
    - IT support managers

[Whitepaper: An Overview of the AWS Cloud Adoption Framework](https://d1.awsstatic.com/whitepapers/aws_cloud_adoption_framework.pdf)

### Migration strategies

When migrating applications to the cloud, six of the most common [migration strategies](https://aws.amazon.com/blogs/enterprise-strategy/6-strategies-for-migrating-applications-to-the-cloud/) that you can implement are:

1. Rehosting:
   - Rehosting also known as “lift-and-shift” involves moving applications without changes.
2. Replatforming:
   - Replatforming, also known as “lift, tinker, and shift,” involves making a few cloud optimizations to realize a tangible benefit. Optimization is achieved without changing the core architecture of the application.
3. Refactoring/re-architecting:
   - Refactoring (also known as re-architecting) involves reimagining how an application is architected and developed by using cloud-native features. Refactoring is driven by a strong business need to add features, scale, or performance that would otherwise be difficult to achieve in the application’s existing environment.
4. Repurchasing:
   - Repurchasing involves moving from a traditional license to a software-as-a-service model.
5. Retaining:
   - Retaining consists of keeping applications that are critical for the business in the source environment. This might include applications that require major refactoring before they can be migrated, or, work that can be postponed until a later time.
6. Retiring:
   - Retiring is the process of removing applications that are no longer needed.

### AWS Snow Family

- The [AWS Snow Family](https://aws.amazon.com/snow) is a collection of physical devices that help to physically transport up to exabytes of data into and out of AWS.
- AWS Snow Family is composed of AWS Snowcone, AWS Snowball, and AWS Snowmobile.
  - AWS Snowcone:
    - [AWS Snowcone](https://aws.amazon.com/snowcone) is a small, rugged, and secure edge computing and data transfer device.
    - It features 2 CPUs, 4 GB of memory, and 8 TB of usable storage.
  - [AWS Snowball](https://aws.amazon.com/snowball/) offers two types of devices:
    - Snowball Edge Storage Optimized
      - Devices that are well suited for large-scale data migrations and recurring transfer workflows, in addition to local computing with higher capacity needs.
      - Storage: 80 TB of hard disk drive (HDD) capacity for block volumes and Amazon S3 compatible object storage, and 1 TB of SATA solid state drive (SSD) for block volumes.
      - Compute: 40 vCPUs, and 80 GiB of memory to support Amazon EC2 sbe1 instances (equivalent to C5)
    - Snowball Edge Compute Optimized
      - Devices that provides powerful computing resources for use cases such as machine learning, full motion video analysis, analytics, and local computing stacks.
      - Storage: 42-TB usable HDD capacity for Amazon S3 compatible object storage or Amazon EBS compatible block volumes and 7.68 TB of usable NVMe SSD capacity for Amazon EBS compatible block volumes.
      - Compute: 52 vCPUs, 208 GiB of memory, and an optional NVIDIA Tesla V100 GPU. Devices run Amazon EC2 sbe-c and sbe-g instances, which are equivalent to C5, M5a, G3, and P3 instances.
  - [AWS Snowmobile](https://aws.amazon.com/snowmobile):
    - It is an exabyte-scale data transfer service used to move large amounts of data to AWS.
    - Can transfer up to 100 petabytes of data per Snowmobile, a 45-foot long ruggedized shipping container, pulled by a semi trailer truck.

## Innovate with AWS Services

You are properly equipped to drive innovation in the cloud if you can clearly articulate the following conditions:

- The current state
- The desired state
- The problems you are trying to solve

Some Paths that worth exploring:

- Serverless applications:
  - Serverless refers to applications that don’t require provision, maintain, or administer servers.
  - Building an architecture with serverless applications enables the developers to focus on their core product instead of managing and operating servers.
- Artificial Intelligence:
  - AWS offers a variety of services powered by artificial intelligence (AI).
    - Convert speech to text with Amazon Transcribe.
    - Discover patterns in text with Amazon Comprehend.
    - Identify potentially fraudulent online activities with Amazon Fraud Detector.
    - Build voice and text chatbots with [Amazon Lex](https://aws.amazon.com/lex).
- Machine Learning:
  - AWS offers [Amazon SageMaker](https://aws.amazon.com/sagemaker) to remove the difficult work from the process and empower you to build, train, and deploy ML models quickly.

### Migration and Innovation additional resources

- [Migration & Transfer on AWS](https://aws.amazon.com/products/migration-and-transfer)
- [A Process for Mass Migrations to the Cloud](https://aws.amazon.com/blogs/enterprise-strategy/214-2/)
- [6 Strategies for Migrating Applications to the Cloud](https://aws.amazon.com/blogs/enterprise-strategy/6-strategies-for-migrating-applications-to-the-cloud/)
- [AWS Cloud Adoption Framework](https://aws.amazon.com/professional-services/CAF/)
- [AWS Fundamentals: Core Concepts](https://aws.amazon.com/getting-started/fundamentals-core-concepts/)
- [AWS Cloud Enterprise Strategy Blog](https://aws.amazon.com/blogs/enterprise-strategy/)
- [Modernizing with AWS Blog](https://aws.amazon.com/blogs/modernizing-with-aws/)
- [AWS Customer Stories: Data Center Migration](https://aws.amazon.com/solutions/case-studies/?customer-references-cards.sort-by=item.additionalFields.publishedDate&customer-references-cards.sort-order=desc&awsf.customer-references-location=*all&awsf.customer-references-segment=*all&awsf.customer-references-product=product%23vpc%7Cproduct%23api-gateway%7Cproduct%23cloudfront%7Cproduct%23route53%7Cproduct%23directconnect%7Cproduct%23elb&awsf.customer-references-category=category%23datacenter-migration)

## The Cloud Journey

### The AWS Well-Architected Framework

The [AWS Well-Architected](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf) Framework helps you understand how to design and operate reliable, secure, efficient, and cost-effective systems in the AWS Cloud. It provides a way for you to consistently measure your architecture against best practices and design principles and identify areas for improvement.

The Well-Architected Framework is based on five pillars:

- Operational excellence
  - Operational excellence is the ability to run and monitor systems to deliver business value and to continually improve supporting processes and procedures.
  - Design principles for operational excellence in the cloud include performing operations as code, annotating documentation, anticipating failure, and frequently making small, reversible changes.
- Security
  - The Security pillar is the ability to protect information, systems, and assets while delivering business value through risk assessments and mitigation strategies.
  - When considering the security of your architecture, apply these best practices:
    - Automate security best practices when possible.
    - Apply security at all layers.
    - Protect data in transit and at rest.
- Reliability
  - Reliability is the ability of a system to do the following:
    - Recover from infrastructure or service disruptions
    - Dynamically acquire computing resources to meet demand
    - Mitigate disruptions such as misconfigurations or transient network issues
  - Reliability includes testing recovery procedures, scaling horizontally to increase aggregate system availability, and automatically recovering from failure.
- Performance efficiency
  - Performance efficiency is the ability to use computing resources efficiently to meet system requirements and to maintain that efficiency as demand changes and technologies evolve.
  - Evaluating the performance efficiency of your architecture includes experimenting more often, using serverless architectures, and designing systems to be able to go global in minutes.
- Cost optimization
  - Cost optimization is the ability to run systems to deliver business value at the lowest price point.
  - Cost optimization includes adopting a consumption model, analyzing and attributing expenditure, and using managed services to reduce the cost of ownership.

[Whitepaper: AWS Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)

### Advantages of cloud computing

Operating in the AWS Cloud offers many benefits over computing in on-premises or hybrid environments.

- [Six advantages of cloud computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)
  - Trade upfront expense for variable expense.
  - Benefit from massive economies of scale.
  - Stop guessing capacity.
  - Increase speed and agility.
  - Stop spending money running and maintaining data centers.
  - Go global in minutes.

### Cloud Journey additional resources

- [AWS Well-Architected](https://aws.amazon.com/architecture/well-architected/)
- [Whitepaper: AWS Well-Architected Framework](https://d1.awsstatic.com/whitepapers/architecture/AWS_Well-Architected_Framework.pdf)
- [AWS Architecture Center](https://aws.amazon.com/architecture)
- [Six Advantages of Cloud Computing](https://docs.aws.amazon.com/whitepapers/latest/aws-overview/six-advantages-of-cloud-computing.html)
- [AWS Architecture Blog](https://aws.amazon.com/blogs/architecture)