# GCP Flask Backend Deployment with Terraform and Cloud Build

## Project Overview
This project demonstrates the deployment of a Flask backend application on GCP using Terraform for Infrastructure as Code (IaC) and Cloud Build for automation. The architecture includes a containerized Flask app, deployed on a Compute Engine instance within a custom VPC.

## Architecture Details
- **VPC:** Custom VPC with public and private subnets
- **Compute Engine Instance:** Hosts the Flask application
- **Docker Image:** Flask app containerized and stored in Google Artifact Registry
- **Firewall Rules:** Allow access to the application port
- **Cloud Build:** Automates container build and deployment to GCP

## Technologies Used
- Google Cloud Platform (GCP)
- Terraform
- Docker
- Flask
- Cloud Build

## Deployment Steps

### Pre-Deployment
1. **Create Docker Image:**
   - Build a Docker image for the Flask backend application and test it locally.
   - Push the Docker image to Google Artifact Registry.

2. **Docker Commands:**
   ```bash
   docker build -t dobhalapp:latest .
   docker tag dobhalapp:latest gcr.io/<your-project-id>/dobhalapp:latest
   docker push gcr.io/<your-project-id>/dobhalapp:latest


## Script Deployment

1. **Terraform Configuration:**

   Use Terraform to create:
   - VPC with public and private subnets.
   - Compute Engine instance running the containerized Flask app.
   - Firewall rules for the application port.


3. **Terraform Commands:**
 ```bash
 terraform init
 terraform plan
 terraform apply
```
3. **Run the Application:**

   - Ensure the Compute Engine instance is running and accessible.
   - Use the `gcloud compute ssh` command to verify the container is running:
     ```bash
     gcloud compute ssh <instance-name> --zone <zone>
     docker ps
     ```
## Post-Deployment

### Cloud Build Workflow

Automate the build and deployment process using a Cloud Build YAML file.

#### Test the Workflow
Run the following command to test the workflow:
```bash
gcloud builds submit --config=cloudbuild/cloudbuild.yaml
```
### 2. Cloud Build YAML Example
Below is the YAML configuration used for Cloud Build:
```yaml
steps:
- name: 'gcr.io/cloud-builders/docker'
  args: ['build', '-t', 'gcr.io/<your-project-id>/dobhalapp:latest', '.']
- name: 'gcr.io/cloud-builders/docker'
  args: ['push', 'gcr.io/<your-project-id>/dobhalapp:latest']
- name: 'gcr.io/cloud-builders/gcloud'
  args: ['compute', 'instances', 'reset', '<instance-name>', '--zone', '<zone>']
```

## Key Features
- Fully automated deployment pipeline using Terraform and Cloud Build.
- Containerized application for scalability and portability.
- Custom VPC setup with controlled access.
- Follows GCP best practices for security and cost optimization.

---
## Results and Outputs

1. **Docker Image Built and Pushed to Artifact Registry**
2. **Terraform Deployment**
3. **Application Running on Compute Engine**
4. **Cloud Build History**
---

## Version Control and Repository Setup

To ensure proper version control and to push your deployment scripts to a GitHub repository, follow the steps below:

### Git Configuration

Configure your Git username and email if not already done:
```bash
git config --global user.name "Your Name"
git config --global user.email "your-email@example.com"
```
## Adding Files to Repository

1. Add the project files to the Git staging area:
   ```bash
   git add .

2. Commit the changes with a meaningful message:
   ```bash
   git commit -m "Added CloudFormation/Terraform files and deployment scripts"

## Pushing to GitHub

1. Push the changes to the main branch:
   ```bash
   git push origin main
2. Ensure authentication using your GitHub credentials or a Personal Access Token (PAT) if required.

Example Commands Used During This Project

Below are the specific commands executed during this project to push the deployment configuration:
   ```bash
   git config --global user.email "dhruvdobhal97@gmail.com"
   git config --global user.name "Dhruv Dobhal"
   git add .
   git commit -m "Added cloudbuild.yaml for automated deployment"
   git push origin main
   ```
These steps ensure that all deployment artifacts, scripts, and configurations are safely stored in your GitHub repository.

## Instructions to Replicate
1. Clone the repository:
2. Build and Push Docker Image:
   ```bash   
   cd docker
   docker build -t dobhalapp:latest .
   docker tag dobhalapp:latest gcr.io/<your-project-id>/dobhalapp:latest
   docker push gcr.io/<your-project-id>/dobhalapp:latest
   ```
3. Deploy Infrastructure with Terraform:
   ```bash
   cd terraform
   terraform init
   terraform apply
   ```
5. Test the Deployment: Access the application in your browser using the public IP of the Compute Engine instance.
