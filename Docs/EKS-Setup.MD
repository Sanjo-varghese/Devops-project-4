# Setup Kubernetes on Amazon EKS

You can follow same procedure in the official  AWS document [Getting started with Amazon EKS – eksctl](https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html)   

#### Pre-requisites: 
  - an EC2 Instance (Kubernetes Management Host) -> Amazon linux Ami -> t2.micro


# 1. Install and setup kubectl on Management host
   a. Download kubectl version 1.28.1 

   b. Grant execution permissions to kubectl executable   

   c. Move kubectl onto /usr/local/bin   

   d. Test that your kubectl installation was successful 


   ```sh 
  curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.28.1/2023-09-14/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mv ./kubectl /usr/local/bin 
   kubectl version --short --client
```


Install or update the AWS CLI

```sh
curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
unzip awscliv2.zip
sudo ./aws/install
```

2. Install and setup eksctl on Management Host   
   a. Download and extract the latest release   
   b. Move the extracted binary to /usr/local/bin   
   c. Test that your eksclt installation was successful   
   ```sh
   curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_amd64.tar.gz" | tar xz -C /tmp
   sudo mv /tmp/eksctl /usr/local/bin
   eksctl version
   ```
  
3. Create an IAM Role and attache it to EC2 instance Management Host  
   `Note: create IAM user with programmatic access if your bootstrap system is outside of AWS`   
   IAM user should have access to   
   IAM   
   EC2   
   VPC    
   CloudFormation

4. Create EKS cluster and nodes from EC2 Management Host
   ```sh
   eksctl create cluster --name cluster-name  \
   --region region-name \
   --node-type instance-type \
   --nodes-min 2 \
   --nodes-max 2 \ 
   --zones <AZ-1>,<AZ-2>
```





example:
```sh
eksctl create cluster --name Sanjo-cluster --region us-west-2 --node-type t2.medium --zones us-west-2a,us-west-2b
```




5. To delete the EKS clsuter 
   ```sh 
   eksctl delete cluster sanjo-cluster --region us-west-2
   ```



   
6. Validate your cluster using by creating by checking nodes and by creating a pod 
   ```sh 
   kubectl get nodes
   kubectl run pod tomcat --image=tomcat 
   ```
