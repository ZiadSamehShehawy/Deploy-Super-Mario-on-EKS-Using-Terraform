# Deploying Super Mario on Amazon EKS with Terraform

## Technologies Used:
- **Terraform:** Infrastructure as Code (IaC) for configuration.
- **Amazon EKS:** Managing cluster elements and automatic scaling.
- **GitHub:** Version control and collaboration.

## Key Highlights:
- Achieved a smooth deployment of Super Mario on a scalable and managed Kubernetes cluster.
- Leveraged Terraform to streamline the infrastructure setup, ensuring an efficient and reproducible process.

## Project Repository
🔗 [GitHub Repo Link](https://github.com/ZiadSamehShehawy/Deploy-Super-Mario-on-EKS-Using-Terraform.git)

## Prerequisites
Ensure the following dependencies are installed:

1. **AWS CLI:**
   ```bash
   curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
   unzip awscliv2.zip
   sudo ./aws/install
   aws --version
   ```

2. **Docker:**
   ```bash
   sudo apt update
   sudo apt install -y ca-certificates curl gnupg lsb-release
   curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /usr/share/keyrings/docker-archive-keyring.gpg
   echo "deb [arch=$(dpkg --print-architecture) signed-by=/usr/share/keyrings/docker-archive-keyring.gpg] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
   sudo apt-get update
   sudo apt install docker-ce docker-ce-cli containerd.io -y
   sudo usermod -aG docker $USER
   newgrp docker
   ```

3. **Kubectl:**
   ```bash
   curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.25.6/2023-01-30/bin/linux/amd64/kubectl
   chmod +x ./kubectl
   mkdir -p $HOME/bin && cp ./kubectl $HOME/bin/kubectl && export PATH=$PATH:$HOME/bin
   kubectl version
   ```

4. **Terraform:**
   ```bash
   # Install Terraform
   wget -O- https://apt.releases.hashicorp.com/gpg | sudo gpg --dearmor -o /usr/share/keyrings/hashicorp-archive-keyring.gpg
   echo "deb [signed-by=/usr/share/keyrings/hashicorp-archive-keyring.gpg] https://apt.releases.hashicorp.com $(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/hashicorp.list > /dev/null
   sudo apt update
   sudo apt install terraform -y
   ```

## Deployment Steps:
1. **Clone the repository:**
   ```bash
   mkdir super_mario
   cd super_mario
   git clone https://github.com/ZiadSamehShehawy/Deploy-Super-Mario-on-EKS-Using-Terraform.git
   cd Deploy-Super-Mario-on-EKS-Using-Terraform/EKS-TF
   ```

2. **Initialize and validate Terraform:**
   ```bash
   terraform init
   terraform validate
   ```

3. **Plan and apply Terraform changes:**
   ```bash
   terraform plan
   terraform apply --auto-approve
   ```

4. **Configure kubectl with EKS cluster details:**
   ```bash
   aws eks update-kubeconfig --name EKS_CLOUD --region us-east-2
   ```

5. **Apply Kubernetes deployment and service configurations:**
   ```bash
   kubectl apply -f deployment.yaml
   kubectl apply -f service.yaml
   ```

6. **Verify the deployment:**
   ```bash
   kubectl get all
   kubectl describe service mario-service
   ```

## Cleanup (Destroy Infrastructure):
To destroy all the infrastructure created:
   ```bash
   kubectl delete service mario-service
   kubectl delete deployment mario-deployment
   cd EKS-TF
   terraform destroy --auto-approve
   ```
🌟 #Terraform #AmazonEKS #Kubernetes #CloudNative #DevOps
