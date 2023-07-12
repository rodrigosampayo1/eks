### En la VM

curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"

unzip awscliv2.zip

which aws # It should be /usr/bin/aws.

sudo ./aws/install --bin-dir /usr/bin --install-dir /usr/bin/aws-cli --update

aws --version

### Config AWS account
aws configure

### Install Kubectl
curl -o kubectl https://amazon-eks.s3.us-west-2.amazonaws.com/1.16.8/2020-04-16/bin/linux/amd64/kubectl

- Apply execute permissions to the binary:
chmod +x ./kubectl

- Copy the binary to a directory in your path:
mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin

- Ensure kubectl is installed:
kubectl version --short --client

- Move the extracted binary to /usr/bin:
sudo mv /tmp/eksctl /usr/bin

- Get the version of eksctl:
eksctl version

### Provision an EKS Cluster
- Provision an EKS cluster with three worker nodes in us-east-1:
eksctl create cluster --name dev --region us-east-1 --nodegroup-name standard-workers --node-type t3.medium --nodes 3 --nodes-min 1 --nodes-max 4 --managed



- In the CLI, check the cluster:
eksctl get cluster

- Enable it to connect to our cluster:
aws eks update-kubeconfig --name dev --region us-east-1


### Create a Deployment on Your EKS Cluster
    Install Git:
    sudo yum install -y git

    Download the course files:
    git clone https://github.com/ACloudGuru-Resources/Course_EKS-Basics

    Change directory:
    cd Course_EKS-Basics

    Take a look at the deployment file:
    cat nginx-deployment.yaml

    Take a look at the service file:
    cat nginx-svc.yaml

    Create the service:
    kubectl apply -f ./nginx-svc.yaml

    Check its status:
    kubectl get service

    Copy the external DNS hostname of the load balancer, and paste it into a text file, as we'll need it in a minute.

    Create the deployment:
    kubectl apply -f ./nginx-deployment.yaml

    Check its status:
    kubectl get deployment

    View the pods:
    kubectl get pod

    View the ReplicaSets:
    kubectl get rs

