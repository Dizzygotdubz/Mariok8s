🏆 Deploying Super Mario on Kubernetes 🎮
Hey folks! Remember the thrill of '90s gaming? Let’s step back in time and relive those exciting moments! With the game deployed on Kubernetes, it’s time to dive into the nostalgic world of Mario. Grab your controllers—it’s game time!

🏗 Overview
This guide walks you through deploying the Super Mario game on Amazon Elastic Kubernetes Service (EKS). By leveraging Kubernetes, we can ensure scalability, reliability, and seamless management of the game on AWS.

📌 Prerequisites
An Ubuntu Instance
IAM Role (with necessary permissions)
Terraform installed on your instance
AWS CLI and Kubectl installed on your instance

🚀 Deployment Steps

🔹 Step 1: Launch an Ubuntu Instance
Navigate to the EC2 Dashboard and click Launch Instance.
Select an AMI → Choose an Ubuntu image.
Choose Instance Type → Select t2.micro.
Configure Instance Details → Set storage to at least 8GB.
Configure Security Group → Ensure necessary inbound/outbound rules are set.
Launch the Instance and connect using SSH.

🔹 Step 2: Create an IAM Role
In the AWS Console, search for IAM and click Roles.
Click Create Role → Choose AWS Service → Select EC2.
Assign Administrator Access (for learning purposes).
Provide a Role Name and click Create Role.
Attach the Role to the EC2 instance:
Go to EC2 Dashboard → Select instance → Click Actions > Security > Modify IAM Role.
Select the created IAM Role and click Update IAM Role.

🔹 Step 3: Provision the Kubernetes Cluster
Clone the repository:
bash
Copy
Edit
git clone https://github.com/Aj7Ay/k8s-mario.git
cd k8s-mario
Make the script executable and run it:
bash
Copy
Edit
sudo chmod +x script.sh
./script.sh
This installs Terraform, AWS CLI, Kubectl, and Docker.
Verify installations:
bash
Copy
Edit
docker --version
aws --version
kubectl version --client
terraform --version
Initialize Terraform:
bash
Copy
Edit
cd EKS-TF
terraform init
⚠️ NOTE: Edit the backend.tf file to update the S3 bucket name before proceeding.
Validate & plan Terraform deployment:
bash
Copy
Edit
terraform validate
terraform plan
Deploy the cluster:
bash
Copy
Edit
terraform apply --auto-approve


🔹 Step 4: Update Kubernetes Configuration
Set up your kubeconfig:
bash
Copy
Edit
aws eks update-kubeconfig --name EKS_CLOUD --region us-east-2
Navigate back to the k8s-mario directory:
bash
Copy
Edit
cd ..

🔹 Step 5: Deploy the Mario Game
Deploy the application:
bash
Copy
Edit
kubectl apply -f deployment.yaml
✅ Check the deployment status:
bash
Copy
Edit
kubectl get all
Apply the service:
bash
Copy
Edit
kubectl apply -f service.yaml
kubectl get all
Get the LoadBalancer Ingress URL:
bash
Copy
Edit
kubectl describe service mario-service
Access the game!
Copy the Ingress URL and paste it into your browser.
🎉 Enjoy playing Super Mario on Kubernetes!
