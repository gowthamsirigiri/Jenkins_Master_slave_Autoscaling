# Jenkins_Master_slave_Autoscaling
## Overview
This repository outlines a blueprint for a Jenkins master-agent setup using Docker and AWS EC2 auto-scaling. The master coordinates jobs, while agent nodes spin up on-demand in an auto-scaling group.

## Architecture
- **Master Node**: Runs Jenkins on a dedicated EC2 instance.
- **Agents**: Dynamically provisioned EC2 instances via auto-scaling, connected to the master as Jenkins agents.

## Steps

### 1. Set up the Jenkins Master
- Launch an EC2 instance (e.g., t2.micro etc).
- Install Docker and pull the official Jenkins image:

#Expose the Ports 8080 for runing the Jenkins , 5000 for agent connectivity

docker run -d -p 8080:8080 -p 50000:50000 --name jenkins-master jenkins/jenkins:lts

#Below is the model Url 
Access Jenkins UI on http://<your-ec2-public-ip>:8080

Configure security, plugins, and the "Docker" plugin.

2. Set up Auto-Scaling Agents

Create a launch configuration or template with a base AMI (with Docker installed).

In the user data script, include:

#Need to add the curl herw ill do

***Configure an auto-scaling group (min: 1, max: 10) with the user data script.***


3. Jenkins Configuration

Add the agent nodes in Jenkins: "Manage Nodes" → "New Node".

Assign each agent as per your scaling logic.

User Data Script: Include the EC2

Here I have created 10 nodes in jenkins UI and added the naming as predictable agent-1,agent-2......


We can even Have the jenkins api included here and do this when evey things are required.
