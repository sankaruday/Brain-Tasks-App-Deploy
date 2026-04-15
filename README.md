Brain React App: Code-to-Cloud Pipeline

This repository contains the source code and CI/CD configuration for the Brain React Application. The project demonstrates a streamlined automated deployment workflow using Jenkins, Docker, and AWS EC2, focused on high-performance delivery and reliable monitoring.

1. Pipeline Architecture & Explanation
   
The CI/CD pipeline is an automated workflow designed to move code from development to a live production environment with minimal manual intervention.

Stage 1: Git Clone (Source Control) – Automatically retrieves the latest source code from the GitHub repository to the build environment, ensuring the pipeline always uses the most recent developer commits.

Stage 2: Dockerize (Containerization) – Packages the React application into a lightweight container. It uses a multi-stage Dockerfile to build assets and serves them via Nginx on Port 80.

Stage 3: Bash Scripting (Automation) – Executes custom .sh scripts to automate the build and deployment logic, ensuring consistent commands are used across every run.

Stage 4: Version Control (Branching) – Utilizes a branching strategy where code is managed in a dev branch for testing before being merged into the master branch for production.

Stage 5: Image Registry (Docker Hub) – Pushes the built images to a public repository for development and a private repository for secure production storage.

Stage 6: Jenkins (Orchestration) – Manages the entire lifecycle via an automated pipeline. It listens for GitHub webhooks to trigger builds and deployments instantly.

Stage 7: AWS (Cloud Hosting) – Deploys the containerized application onto an AWS t3.micro instance within a configured VPC, exposing it to the public internet.

Stage 8: Monitoring (Observability) – Implements health checks to monitor the application's uptime and status, providing real-time visibility into the live environment.

2. Setup & Configuration Instructions
Prerequisites
Tools: Docker and Git installed on the workstation/server.

CI/CD: Jenkins server configured with necessary plugins and Docker group permissions.

Cloud: AWS Account with a t3.small instance and an attached Security Group allowing Port 80 and 22.

Step 1: Infrastructure Preparation (AWS)
Provision an Ubuntu-based instance in your preferred region.

Instance Type: t3.small (Free Tier eligible)

Command: ssh -i your-key.pem ubuntu@your-aws-ip

Step 2: Containerization & Automation
Create the Dockerfile and automation scripts in the project root.

Command: docker build -t brain-app .

Command: chmod +x build.sh deploy.sh

Step 3: Jenkins Pipeline Setup
Configure a Pipeline job in Jenkins to track your repository. Ensure the Jenkins user has permission to run Docker commands:

Command: sudo usermod -aG docker jenkins && sudo systemctl restart jenkins

Step 4: Monitoring Implementation
Set up an uptime monitor or health check to verify the application status.

3. Deployment Artifacts & Proof of Success

Application URL: http://ab268146f9b13492081a0071b7ce8b48-336869789.ap-south-1.elb.amazonaws.com

GitHub Repository: https://github.com/sankaruday/Brain-Tasks-App-Deploy

Docker Hub Repositories: https://hub.docker.com/u/sankaruday

Docker Hub Image : sankaruday/brain-app

AWS Region: ap-south-1 (Mumbai)
