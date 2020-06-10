# CloudDevopsCapstone
Repo for final capstone project of Cloud Devops Nanodegree from Udacity
Implementation of blue/green deveolpment of "Hello World" website in AWS EC2 Instance by means of Jenkins.

Prerequsities:
- EC2 instance with proper IAM roles
- Jenkins installed (also Blue Ocean plugin used)
- Docker installed 
- eksctl installed (aws cli v2 used)

Cluster created by EKSCTL commend which creates cloud formation:

eksctl create cluster \
--name capstonecluster \
--version 1.16 \
--region us-west-2 \
--nodegroup-name standard-workers \
--node-type t2.small \
--nodes 2 \
--nodes-min 1 \
--nodes-max 3 

Project created based on guidance from:
https://medium.com/@andresaaap/jenkins-pipeline-for-blue-green-deployment-using-aws-eks-kubernetes-docker-7e5d6a401021
