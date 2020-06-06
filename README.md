# Udacity_DevOpsDegree_Capstone
Final project for the Udacity DevOps Nanodegree. 

## Infrastructure setup
Deploy an EKS cluster (based on AWS quickstart template available [here](https://aws.amazon.com/de/quickstart/architecture/amazon-eks/)):

Follow this guide to install eksctl:
https://docs.aws.amazon.com/eks/latest/userguide/getting-started-eksctl.html

### Install Jenkins on Bastion Host
The Quickstart Template provisions one EC2 instance as bastion host to the EKS cluster. Install Jenkins on this instance:
- Update OS, install JDK, get the repo for latest Jenkins version, install and verify service is running.
- `sudo yum update`
- `sudo yum upgrade`
- `sudo amazon-linux-extras install java-openjdk11`
- `sudo wget -O /etc/yum.repos.d/jenkins.repo http://pkg.jenkins.io/redhat/jenkins.repo`
- `sudo rpm --import http://pkg.jenkins.io/redhat/jenkins.io.key`
- `sudo yum install jenkins`
- `sudo service jenkins start`

### Configure Jenkins
- Navigate to port 8080 on EC2 instance
- Use `sudo cat /var/lib/jenkins/secrets/initialAdminPassword` to retrieve install pwd, create new admin
- Install suggested plugins, then manually add Blue Ocean Aggregator and pipeline-aws

### Link github project in Jenkins, add credentials
- Connect git to jenkins (preferably using github access token) to build pipeline. Change pipeline to check repo for changes every 2 minutes.
- In Jenkins credentials menu select global, aws from dropdown and use key generated in AWS IAM

## Install hadolint
- `wget https://github.com/hadolint/hadolint/releases/download/v1.18.0/hadolint-Linux-x86_64`
- `chmod +x hadolint`
- `export hadolint`


## Install docker CE on bastion host
sudo yum install -y yum-utils

sudo yum-config-manager \
    --add-repo \
    https://download.docker.com/linux/centos/docker-ce.repo

sudo yum install docker-ce docker-ce-cli containerd.io


- ``
- ``
- ``

## test eksctl 
- `eksctl`
 


## Docker image manual 
Use bastion host to test manual building and deployment of image

### Set up a conda environment and build the docker image:

- `conda create --name py37a python=3.7.2` 
- `activate py37a`
- `pip install pylint`
- `docker build -t jansdockerhub/streamlit .`

### Testing docker container locally:
`docker run -d --name streamlit -p 127.0.0.1:8080:8501 jansdockerhub/streamlit`


### Upload docker image:
- `dockerpath=jansdockerhub/streamlit`
- `echo "Docker ID and Image: $dockerpath"`
- `docker login &&\ docker image tag streamlit $dockerpath`
- `docker push $dockerpath`

### Deploy image manually to EKS
Test deployment from bastion host of dockerhub image to EKS.
- ``

## Use jenkins pipeline to deploy
Jenkinsfile contains a pipeline that:
- performs a linting step
    - todo: screenshot failed linting
    - todo: screenshot succesful linting
- builds a docker container
- pushes container to dockerhub
- uploads the docker image to the eks cluster
    - screenshot succesful pipeline run





dockerpath=jansdockerhub/mlapp

# Step 2
# Run the Docker Hub container with kubernetes
#minikubectl run mlapp --image=$dockerpath --port=80 
kubectl create deployment mlapp --image=$dockerpath
kubectl expose deployment mlapp --type=LoadBalancer --port=80
# Step 3:
# List kubernetes pods
kubectl get pods

# Step 4:
# Forward the container port to a host
kubectl port-forward deployment/mlapp 8000:80

