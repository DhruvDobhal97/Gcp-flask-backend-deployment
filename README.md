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

-Use Terraform to create:

-VPC with public and private subnets

-Compute Engine instance running the containerized Flask app

-Firewall rules for the application port
