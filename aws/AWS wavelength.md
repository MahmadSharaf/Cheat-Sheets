# AWS Wavelength

- [AWS Wavelength](#aws-wavelength)
  - [What cloud continuum is](#what-cloud-continuum-is)
  - [What AWS Wavelength is](#what-aws-wavelength-is)
  - [AWS Wavelength Benefits](#aws-wavelength-benefits)
    - [How to get started](#how-to-get-started)
  - [Resources and services supported](#resources-and-services-supported)
  - [How to test](#how-to-test)

## What cloud continuum is

- It is bringing bringing the cloud where the customers need it.  
![Continuum](Wavelength%20Materials/Continuum.png)

## What AWS Wavelength is

- It is a new type of AWS infrastructure designed to run workloads that require ultra-low latency over mobile networks.
- It is a form of AWS services running close to the edge of the network.
- It helps to build applications that requires ultra-low latency wth 5G connection.

## AWS Wavelength Benefits

- 5G connectivity have a huge increase in bandwidth capacity, in comparison to 4G connectivity. But some applications requires ultra-low latency (the total time of the packets journey from and back to the device), for example 30ms time to travel from the device to an AWS region and 40ms of application processing and 30ms to travel back to the device, with total of 100ms. This considered a high latency connection, which is not suitable for realtime applications.
- As shown in the below image, there is multiple middle points between an AWS region and the mobile network.
![E2E Region and Carrier](Wavelength%20Materials/Region%20and%20Carrier%20Mobile%20Network.png)
- AWS Wavelength solves this issue by installing a zone inside or close to the carrier network, which allows a direct connection with the carrier network. And also, there is a direct link between this Wavelength Zone and AWS region, through AWS service link, that removes the middle points illustrated above.
![Wavelength and Carrier](Wavelength%20Materials/Wavelength%20and%20Carrier%20Mobile%20Network.png)
- This allows to deploy the portion of the application that requires the low latency closest to the edge network.
- So here below the full picture.
![E2E Wavelength network](Wavelength%20Materials/Putting%20altogether.png)

### How to get started

1. Create a VPC.
2. Create a subnet in Wavelength zone.
3. Use the carrier gateway to route traffic in and out of Wavelength zone to the end-user in the mobile network.
4. Create a route table to connect services in the region with Wavelength zone.
5. It is not allowed to access Wavelength directly from public internet. It is only allowed from the regions and mobile network.

## Resources and services supported

- Compute and Storage: Amazon EC2 instances, and EBS volumes.
  - The supported EC2 instances:
    - G4 (2XL): For machine learning inference and graphics workstations.
    - R5 (2XL): For memory intensive applications (databases, in-memory caches, real time data analytics)
    - T3 (Medium, XL): For general purpose applications with burst computing requirements.
- Networking: Amazon VPC, Security groups, Network ACL
- Containers: Amazon Elastic Containers Service (ECS) and Amazon Elastic Kubernetes Service (EKS).
- All managed services like Rekognition, Kinesis, KVS, ..etc are not supported.

## How to test

1. Have a 4G or 5G-connected Verizon device? Use your existing device to connect to AWS Wavelength endpoints via the Carrier IPs you've attached to your infrastructure. To learn more about Carrier IP, visit the [developer guide](https://docs.aws.amazon.com/wavelength/latest/developerguide/how-wavelengths-work.html).
2. Don't have access to a Verizon-connected device? Reach out to our 5G Labs team to learn more about Nova, our remote device testing tool.
3. Want to use your own mobile device? Create an additional subnet in your VPC in the parent region (i.e., non-Wavelength Zone infrastructure) and test your application in the parent region.
For more [information](https://devpost-public.s3.amazonaws.com/Wavelengths/5GEdgeTestingOptions.pdf).