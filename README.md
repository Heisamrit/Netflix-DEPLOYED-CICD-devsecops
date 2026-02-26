This project is a Netflix Clone DevSecOps implementation where I automated the complete CI/CD lifecycle using Jenkins. The pipeline includes code quality checks, security scanning, Docker image creation, vulnerability analysis, and deployment to both Docker container and AWS EKS Kubernetes cluster.This project is a Netflix Clone DevSecOps implementation where I automated the complete CI/CD lifecycle using Jenkins. The pipeline includes code quality checks, security scanning, Docker image creation, vulnerability analysis, and deployment to both Docker container and AWS EKS Kubernetes cluster.

<div align="center">
  <img src="img src/pipeline.png" alt="Logo" width="100%" height="100%">
  <p align="center">Pipeline Overview</p>
</div>

Clean Workspace
First, the pipeline cleans the Jenkins workspace to avoid conflicts from previous builds. This ensures reproducibility and eliminates leftover artifacts.

Git Checkout
In this stage, Jenkins pulls the latest code from GitHub main branch. This ensures the pipeline always works on the latest committed version.
git link - https://github.com/Heisamrit/Netflix-clone-for-devsecops.git
<div align="center">
  <img src="img src/git.png" alt="Logo" width="100%" height="100%">
  <p align="center">Git Repo</p>
</div>

