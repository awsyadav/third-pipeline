# AWS Elastic Container Service (ECS) - EC2-Launch Type
# What is ECS
* ECS stands for EC2 Container Service and is the AWS platform for running Docker containers. The full documentation about ECS can be found here, the development guide can be found here.

# EC2 Launch Type
* The EC2 launch type allows you to run your containerized applications on a cluster of Amazon EC2 instances that you manage.

# ECS infra
* ECS needs EC2 nodes that are being used as slaves to run Docker containers on. To do so you need infrastructure for this. Here is an ECS infrastructure diagram (EC2-type).

# What are we creating:
*	VPC with a /16 ip address range and an internet gateway
*	We are choosing a region and a number of availability zones we want to use.
*	Public subnet convention is 10.x.0.x and 10.x.1.x etc..
*	Private subnet convention is 10.x.10.x and 10.x.11.x etc..
*	In the public subnet we place either NAT instances or a Nat Gateway. Nat instances are the default as they are cheaper for high throughput applications.
*	We create an EC2 instance in private subnet with installing a ECS agent and connecting node to ECS cluster.
*	In Order to access the EC2 container we would need to be in same vpc network, if your AWS VPC network is not connected to deera network then connect Bastion host and access the EC2 container.

# Task definition in Json formate:-  Creating task definition in json format.
*	Task definition contain name of container 
*	Aws image repository path 
*	Used Memory and cpu
*	Define AWS cloudwatch log group
*	Application running on port no

# Project structure

    ├──  ecs-ec2-cluster                 
    ├──  ├── terraform
    |        └── backend.tf               # Storing tfstate in s3 bucket
    |        └── main.tf                  # ECS, EC2, ALB, cloudwatch
    |        └── user_data.tpl            # Script for installing the ECS agent
    |        └── variable.tf              # Contain values
    |        └── task_defination.json     # task_defination- contain container image and resources
    ├── Dockerfile                        # swagger container image creation file
    ├── Jenkinsfile                       # pipeline for swagger-app deployment
    ├── docker-compose.yml                # docker building
    ├── lab-env.var                       # OIDC client id, secret, redirect url
    ├── entrypoint.sh                     # Entrypoint script
    ├── httpd.conf                        # web-server configuration
    └── README.md
            
    
    
 
