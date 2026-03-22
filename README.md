<h1>End-to-End DevSecOps CI/CD Pipeline for Netflix Clone on AWS EKS</h1>
<p>This project is a Netflix Clone DevSecOps implementation where I automated the complete CI/CD lifecycle using Jenkins. The pipeline includes code quality checks, security scanning, Docker image creation, vulnerability analysis, and deployment to both Docker container and AWS EKS Kubernetes cluster.This project is a Netflix Clone DevSecOps implementation where I automated the complete CI/CD lifecycle using Jenkins. The pipeline includes code quality checks, security scanning, Docker image creation, vulnerability analysis, and deployment to both Docker container and AWS EKS Kubernetes cluster.</p>


<div align="center">
  <img src="img src/pipeline.png" alt="Logo" width="100%" height="100%">
  <p align="center">Pipeline Overview</p>
</div>
<div align="center">
  <img src="img src/running app.png" alt="Logo" width="100%" height="100%">
  <p align="center">APP DEPLOYED</p>
</div>

<h3>AWS Usage Summary</h3>
<ul>
    <li> Used Amazon Elastic Kubernetes Service (EKS) to deploy and manage the Netflix Clone container in a scalable Kubernetes cluster.</li>
    
  <li> Hosted Jenkins CI/CD server on Amazon EC2 to automate the complete DevSecOps pipeline.</li>
  <div align="center">
  <img src="img src/ec2.png" alt="Logo" width="100%" height="100%">
  <p align="center">ec2</p>
</div>
    
  <li> Configured secure access control using AWS Identity and Access Management (IAM) with role-based authentication and least-privilege permissions.</li>
   <div align="center">
  <img src="img src/user group.png" alt="Logo" width="100%" height="100%">
  <p align="center">IAM USER GROUP</p>
</div> 

    
  <li> Exposed the application externally using an AWS-managed load balancer via Elastic Load Balancing (ELB).</li>
  <div align="center">
  <img src="img src/load balancer.png" alt="Logo" width="100%" height="100%">
  <p align="center">load Balancer</p>
</div>
    
  <li> Followed AWS security best practices: IAM roles, no hardcoded credentials, secure networking, and RBAC-enabled Kubernetes access.</li>
    <div align="center">
  <img src="img src/roles.png" alt="Logo" width="100%" height="100%">
  <p align="center">IAM ROLES</p>
</div>
</ul>
<h3>CI/CD Automation using Jenkins</h3>
<p>
The complete CI/CD pipeline for this project is automated using Jenkins. 
It manages and executes each stage of the DevSecOps workflow in a structured 
and reliable manner.
</p>
<p>
Jenkins orchestrates the entire DevSecOps lifecycle — from code commit 
and build processes to security scanning and final deployment to Kubernetes.
</p>
<div align="center">
  <img src="img src/configure.png" alt="Logo" width="100%" height="100%">
  <p align="center">CONFIGURE</p>
</div>
<div align="center">
  <img src="img src/jenkins credentials.png" alt="Logo" width="100%" height="100%">
  <p align="center">CREDENTIALS REQUIRED</p>
</div>
<div align="center">
  <img src="img src/job executed.png" alt="Logo" width="100%" height="100%">
  <p align="center">JOB EXECUTED</p>
</div>



<h3>Clean Workspace</h3>
<p>
First, the pipeline cleans the Jenkins workspace to avoid conflicts from previous builds. 
This ensures reproducibility and eliminates leftover artifacts, allowing the build 
process to start in a fresh and consistent environment.
</p>

<h3>Git Checkout</h3>
<p>
In this stage, Jenkins pulls the latest code from the GitHub <strong>main</strong> branch. 
This ensures the pipeline always works on the most recently committed version of the project, 
maintaining consistency and enabling continuous integration.
</p>
<p>
Repository Link: 
<a href="https://github.com/Heisamrit/Netflix-clone-for-devsecops.git" target="_blank">
https://github.com/Heisamrit/Netflix-clone-for-devsecops.git
</a>
</p>
<div align="center">
  <img src="img src/git.png" alt="Logo" width="100%" height="100%">
  <p align="center">Git Repo</p>
</div>

<h3>SonarQube Code Analysis</h3>
<p>
In this stage, static code analysis is integrated using SonarQube to detect 
code smells, bugs, security vulnerabilities, and maintainability issues. 
This helps improve overall code quality and ensures the application 
meets defined quality standards before deployment.
</p>
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


<h3>Install Dependencies</h3>
<p>
This stage installs all required Node.js dependencies for the React/Vite application 
using the package manager. It ensures that all libraries and modules defined in 
package.json are properly installed before the build process begins.
</p>

<h3>OWASP Dependency Check</h3>
<p>
This stage performs Software Composition Analysis (SCA) to identify known CVEs 
(Common Vulnerabilities and Exposures) in third-party dependencies. 
It scans project libraries against vulnerability databases to detect 
security risks before deployment.
</p>
<h3>What it does:</h3>
<ol>
    <li>Scans <code>package.json</code></li>
    <li>Matches CVEs from NVD</li>
    <li>Generates XML report</li>
    <li>Publishes report in Jenkins</li>
</ol>

<h3>Trivy File System Scan</h3>

<p>
This stage scans the entire file system for vulnerabilities and exposed secrets.
It performs a comprehensive security check before containerization and deployment.
</p>

<ul>
    <li>Dependencies</li>
    <li>Hardcoded secrets</li>
    <li>Misconfigurations</li>
    <li>Infrastructure as Code (IaC) vulnerabilities</li>
</ul>

<h3>Docker Build &amp; Push</h3>
<p>
In this stage, the application is containerized using a multi-stage Docker build. 
This approach optimizes the final image size by separating the build environment 
from the production environment. After building the image, it is tagged and pushed 
to a container registry for deployment.
</p>
<div align="center">
  <img src="img src/docker.png" alt="Logo" width="100%" height="100%">
  <p align="center">Docker</p>
</div> 
<h4>Builder Stage:</h4>
<ul>
    <li>Uses Node 16 Alpine</li>
    <li>Installs dependencies</li>
    <li>Builds Vite production bundle</li>
</ul>

<h3>Trivy Image Scan</h3>
<p>
After building the Docker image, the image is scanned using Trivy to detect 
OS-level and package-level vulnerabilities. This helps identify security risks 
within the base image and installed libraries before pushing the image to the registry 
or deploying it to the cluster.
</p>

<h3>Deploy to Docker Container</h3>
<p>
Before deploying to Kubernetes, the Docker container is run locally to verify 
that the image is functioning correctly. This step ensures the application starts 
properly, required ports are exposed, and there are no runtime issues before 
moving to the cluster deployment stage.
</p>

<h4>Deployment Actions:</h4>
<ul>
    <li>Removes old container</li>
    <li>Pulls latest image</li>
    <li>Runs on port 8081</li>
    <li>Uses <code>--restart=always</code></li>
</ul>

<h3>Deploy to Kubernetes (AWS EKS)</h3>
<p>
Finally, the application is deployed to AWS Elastic Kubernetes Service (EKS). 
This enables scalable, highly available container orchestration in the cloud.
</p>
<div align="center">
  <img src="img src/cluster.png" alt="Logo" width="100%" height="100%">
  <p align="center">cluster</p>
</div>
<div align="center">
  <img src="img src/node groups.png" alt="Logo" width="100%" height="100%">
  <p align="center">Node Groups</p>
</div>
<div align="center">
  <img src="img src/node info.png" alt="Logo" width="100%" height="100%">
  <p align="center">Node Info</p>
</div>

<h4>Steps:</h4>
<ol>
    <li>Update kubeconfig</li>
    <li>Apply Deployment YAML</li>
    <li>Apply Service YAML</li>
    <li>Restart rollout</li>
</ol>

<h3>Argo CD</h3>
<p>
To implement GitOps-based continuous delivery, I integrated Argo CD with the Kubernetes cluster. 
This enables automated synchronization between the desired state defined in Git and the actual 
state running inside the cluster.
</p>
<p>
Argo CD ensures that the Kubernetes cluster state always matches the configuration stored in Git, 
providing version control, rollback capability, and improved deployment reliability.
</p>
<div align="center">
  <img src="img src/argocd.png" alt="Logo" width="100%" height="100%">
  <p align="center">ArgoCD</p>
</div>

<h3>Email Notification</h3>
<p>
At the end of the pipeline, Jenkins sends an email notification regarding 
the build status — whether it is a success or a failure. This helps maintain 
visibility and transparency in the CI/CD process.
</p>
<div align="center">
  <img src="img src/success mail.png" alt="Logo" width="100%" height="100%">
  <p align="center">Notification</p>
</div>
<h4>This ensures:</h4>
<ul>
    <li>Monitoring</li>
    <li>Immediate alert system</li>
</ul>

<h3>Monitoring &amp; Observability</h3>
<p>
To implement production-grade monitoring, I integrated industry-standard tools 
for metrics collection, alerting, and visualization within the Kubernetes environment.
</p>

<h4>Integrated Tools:</h4>
<ul>
    <li><strong>Prometheus</strong> – Metrics collection and alerting</li>
      <div align="center">
  <img src="img src/prometheus.png" alt="Logo" width="100%" height="100%">
  <p align="center">PROMETHEUS</p>
      </div>
  
  <li><strong>Grafana</strong> – Visualization dashboard</li>
  <div align="center">
  <img src="img src/grafana.png" alt="Logo" width="100%" height="100%">
  <p align="center">GRAFANA</p>
  </div>
</ul>

<p>
This setup enables real-time monitoring of the Kubernetes cluster and application, 
helping track resource usage, application performance, and system health while 
providing proactive alerting for potential issues.
</p>



<div align="center">
  <img src="img src/running app.png" alt="Logo" width="100%" height="100%">
  <p align="center">APP DEPLOYED</p>
</div>



<div align="center"><h2>Thank You!</h2></div
<p>
A big thank you for your time, attention, and interest in this project.  
I truly appreciate the opportunity to present my work on implementing a complete DevSecOps pipeline with CI/CD automation, security integration, and cloud-native deployment.
</p>
<p>
Your support and feedback are highly valued. Thank you once again!
</p>
<h3>Contact Information</h3>
<p>
<strong>Email:</strong> 
<a href="mailto:heisamrit@gmail.com">heisamrit@gmail.com</a>
</p>
<p>
<strong>LinkedIn:</strong> 
<a href="https://www.linkedin.com/in/heisamrit" target="_blank">
www.linkedin.com/in/heisamrit
</a>
</p>
