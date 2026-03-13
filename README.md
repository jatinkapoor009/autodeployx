🚀 AutoDeployX: Next-Gen DevSecOps CI/CD Pipeline.

AutoDeployX is a robust, secure, and highly available DevSecOps pipeline designed to automate the bridge between development and production. This project integrates industry-standard tools like Jenkins, Docker, Trivy, and AWS to ensure a scalable and secure software delivery lifecycle.

🏗️ System Architecture

The pipeline follows a strict sequential flow to ensure quality and security:
GitHub Commit ➔ Jenkins Pipeline ➔ Trivy Security Scan ➔ Docker Hub Push ➔ Staging Deployment (Port 8081) ➔ Manual Approval Gate ➔ Production Deployment (Port 80) via ALB

✨ Key Features

🛠️ Automation & CI/CD

Pipeline-as-Code: Entire workflow defined within a Jenkinsfile for version control and repeatability.
Containerization: Application is containerized using Docker with automated multi-tagging (Build Number & Latest).
Two-Stage Deployment: Separate environments for Staging (testing) and Production (live).

🛡️ DevSecOps (Security First)

Vulnerability Scanning: Integrated Trivy to scan Docker images for 'CRITICAL' vulnerabilities.
Security Gate: The pipeline is configured to fail automatically if any critical security threats are detected, preventing insecure images from reaching production.

☁️ Infrastructure & High Availability (AWS)

Traffic Management: Utilizes AWS Application Load Balancer (ALB) to distribute incoming traffic efficiently across healthy instances.
High Availability: Configured Auto Scaling Group (ASG) with a defined capacity (Min: 1, Max: 3) to ensure the application remains available under varying loads.
Proactive Monitoring: AWS CloudWatch alarms monitor CPU utilization and trigger scaling events or SNS email alerts when thresholds are crossed.

🛠️ Tech Stack

CI/CD: Jenkins
Security: Trivy
Containerization: Docker
Cloud Provider: Amazon Web Services (AWS)
AWS Services: EC2, ALB, ASG, CloudWatch, SNS
Registry: Docker Hub
Version Control: GitHub

### How to use

1. Clone this repository:
 git clone [https://github.com/jatinkapoor009/autodeployx.git](https://github.com/jatinkapoor009/autodeployx.git)
