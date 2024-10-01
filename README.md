# Setting up a GPU Instance for Machine Learning on AWS

This guide will walk you through the process of setting up a GPU instance on Amazon Web Services (AWS) for machine learning tasks.

![AWS GPU Instance Setup Overview](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/EC2_GetStarted.html)

## Table of Contents
1. [Introduction](#introduction)
2. [Prerequisites](#prerequisites)
3. [Setting up an EC2 Instance](#setting-up-an-ec2-instance)
4. [Connecting to Your Instance](#connecting-to-your-instance)
5. [Using Anaconda Environments and Jupyter Notebooks](#using-anaconda-environments-and-jupyter-notebooks)
6. [Conclusion](#conclusion)

## Introduction

Training large deep learning models on conventional machines can be computationally expensive and time-consuming. Using a GPU instance on AWS can significantly speed up your machine learning tasks.

![GPU vs CPU Performance](https://miro.medium.com/v2/resize:fit:828/format:webp/1*OkFROmRr8j08mKLurTQ3NA.png)

## Prerequisites

Before you begin, make sure you have:

- An AWS account
- Basic familiarity with AWS EC2
- SSH client installed on your local machine

![AWS Console](https://miro.medium.com/v2/resize:fit:828/format:webp/1*zbD9-Xtv1K3J9-89oSnFzQ.png)

## Setting up an EC2 Instance

### 1. Choose an AMI

1. Sign in to the AWS Console and navigate to EC2.
2. Click on "Launch Instance".
3. In the AWS Marketplace, search for "machine learning".
4. Select the "AWS Deep Learning AMI (Ubuntu 18.04)" or a similar AMI that suits your needs.

![Choosing AMI](https://miro.medium.com/v2/resize:fit:828/format:webp/1*lWKkAZUz6TrVWXeI8o3yCw.png)

### 2. Choose an Instance Type

1. Filter by GPU instances.
2. Choose `g3s.xlarge` or a similar instance type based on your requirements and budget.

![Choosing Instance Type](https://miro.medium.com/v2/resize:fit:828/format:webp/1*qY73H_bRB6cUCIzgLuwnDw.png)

### 3. Configure the Instance

You can use the default configuration for most settings.

![Configure Instance](https://miro.medium.com/v2/resize:fit:828/format:webp/1*uyvMmQ8m0Ivw3FN5A7pVMw.png)

### 4. Add Storage

Allocate storage as needed. 90GB is a good starting point.

![Add Storage](https://miro.medium.com/v2/resize:fit:828/format:webp/1*hfWVfg3oPrC5Pu3uv3Qq5A.png)

You can now click Next: Add Tags (no need to add any tags for now) and then Next: Configure Security Group.

### 5. Configure Security Group

1. Create a new security group or select an existing one.
2. Add a rule to allow SSH access (port 22).
3. Add a custom TCP rule for port 8888 (for Jupyter Notebook access).

![Configure Security Group](https://miro.medium.com/v2/resize:fit:828/format:webp/1*XkSaXrMd3MRopxnR4k9aKg.png) 
### . Review

Once you’re set, click on the Review and Launch button to review your instance’s details and then Launch your instance.


## Connecting to Your Instance

1. From the EC2 Dashboard, select your instance and click "Connect".
2. Follow the provided SSH instructions to connect to your instance.

![Connect to Instance](https://miro.medium.com/v2/resize:fit:828/format:webp/1*4Go9TqcuVeWRRzbw0GE-ZQ.png)

## Using Anaconda Environments and Jupyter Notebooks

1. Once connected, activate the desired Anaconda environment:
   ```
   source activate pytorch_p36
   ```

2. Launch Jupyter Notebook:
   ```
   jupyter notebook --no-browser --port=8888
   ```

3. Note the token provided in the output.

4. In a new terminal window, set up port forwarding:
   ```
   ssh -i your-key-pair.pem -L 5511:127.0.0.1:8888 ubuntu@your-instance-public-dns
   ```

5. Open a web browser and go to `http://127.0.0.1:5511`.

6. Enter the token when prompted.
