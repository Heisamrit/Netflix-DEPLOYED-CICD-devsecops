<p>
  <span style="color:#E50914; font-weight:bold;">Netflix Clone DevSecOps Implementation</span> 🚀<br><br>

  This project is a 
  <span style="color:#ff9800; font-weight:bold;">Netflix Clone DevSecOps implementation</span> 
  where I automated the complete 
  <span style="color:#2196F3; font-weight:bold;">CI/CD lifecycle</span> 
  using 
  <span style="color:#d32f2f; font-weight:bold;">Jenkins</span>.  

  The pipeline includes 
  <span style="color:#4CAF50; font-weight:bold;">code quality checks</span>, 
  <span style="color:#9C27B0; font-weight:bold;">security scanning</span>, 
  <span style="color:#FF5722; font-weight:bold;">Docker image creation</span>, 
  <span style="color:#795548; font-weight:bold;">vulnerability analysis</span>, 
  and deployment to both a 
  <span style="color:#3F51B5; font-weight:bold;">Docker container</span> 
  and an 
  <span style="color:#009688; font-weight:bold;">AWS EKS Kubernetes cluster</span>.
</p>

<div align="center">
  <img src="img src/pipeline.png" alt="Logo" width="100%" height="100%">
  <p align="center">Pipeline Overview</p>
</div>

<p align="center">Clean Workspace</p>
First, the pipeline cleans the Jenkins workspace to avoid conflicts from previous builds. This ensures reproducibility and eliminates leftover artifacts.

<p align="center">Git Checkout</p>
In this stage, Jenkins pulls the latest code from GitHub main branch. This ensures the pipeline always works on the latest committed version.
git link - https://github.com/Heisamrit/Netflix-clone-for-devsecops.git
<div align="center">
  <img src="img src/git.png" alt="Logo" width="100%" height="100%">
  <p align="center">Git Repo</p>
</div>

<p align="center">SonarQube Code Analysis</p>
Here I integrated static code analysis using SonarQube to detect code smells, bugs, vulnerabilities, and maintainability issues.
<div align="center">
  <img src="img src/sonarqube.png" alt="Logo" width="100%" height="100%">
  <p align="center">Snoarqube</p>
</div>
<div align="center">
  <img src="img src/jenkins sonar.png" alt="Logo" width="100%" height="100%">
  <p align="center">Jenkins+Sonarqube Scan</p>
</div>
<h3>From Logs:</h3>
<ol>
    <li>TypeScript analyzed</li>
    <li>Kubernetes YAML analyzed</li>
    <li>Dockerfile analyzed</li>
    <li>Quality Gate: ✅ PASSED</li>
</ol>


<p align="center">Install Dependencies</p>
This stage installs all Node.js dependencies required for the React/Vite application


<p align="center">OWASP Dependency Check</p>
This stage performs Software Composition Analysis to identify known CVEs in third-party dependencies.
<h3>What it does:</h3>
<ol>
    <li>Scans <code>package.json</code></li>
    <li>Matches CVEs from NVD</li>
    <li>Generates XML report</li>
    <li>Publishes report in Jenkins</li>
</ol>

<p align="center">Trivy File System Scan</p>
This stage scans the entire file system for vulnerabilities and secrets.
It scans:
Dependencies
Hardcoded secrets
Misconfigurations
IaC vulnerabilities

<p align="center">Docker Build & Push</p>
"In this stage, the application is containerized using multi-stage Docker build."
<div align="center">
  <img src="img src/docker.png" alt="Logo" width="100%" height="100%">
  <p align="center">Docker</p>
Builder Stage:

Uses Node 16 Alpine

Installs dependencies

Builds Vite production bundle

<p align="center">Trivy Image Scan</p>
After building the Docker image, I scan the image itself to detect OS-level and package-level vulnerabilities.

<p align="center">Deploy to Docker Container</p>
"Before Kubernetes deployment, I run the container locally to verify the image is working correctly."

It:

Removes old container

Pulls latest image

Runs on port 8081

Uses restart=always

<p align="center">Deploy to Kubernetes (AWS EKS)</p>
"Finally, the application is deployed to AWS Elastic Kubernetes Service."

Steps:

Update kubeconfig

Apply Deployment YAML

Apply Service YAML

Restart rollout


<p align="center">Email Notification</p>
"At the end of the pipeline, Jenkins sends an email notification about build success or failure."

This ensures:

Monitoring

Immediate alert system
