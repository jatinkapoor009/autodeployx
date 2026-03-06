# autodeployx# 

##  AutoDeployX: End-to-End DevSecOps Pipeline

 Automated CI/CD pipeline for a web application with integrated security scanning, multi-stage deployment, and cloud monitoring.



##  Features

* **Continuous Integration:** Automated builds using Jenkins Pipeline.
* **DevSecOps (Security):** Integrated **Trivy** for Critical Vulnerability Scanning in Docker images.
* **Containerization:** Multi-tagged Docker images pushed to Docker Hub.
* **Deployment Strategy:** Two-stage deployment (Staging on port 8081 and Production on port 80).
* **Quality Gate:** Manual approval step via **Blue Ocean UI** before Production release.
* **Monitoring:** AWS CloudWatch alarms for EC2 CPU utilization and SNS email alerts.

---

## Pipeline Architecture

1.  **Clone Repo:** Fetches the latest code from GitHub.
2.  **Build:** Creates a Docker image with unique build numbers.
3.  **Security Scan:** Trivy scans the image. If `CRITICAL` issues are found, the build fails (Security Gate).
4.  **Push:** Secure images are pushed to Docker Hub.
5.  **Staging:** App is deployed to a staging container for testing.
6.  **Approval:** Manual intervention required to proceed.
7.  **Production:** Final deployment to the live environment.

---

##  Getting Started


### Prerequisites
* Ubuntu EC2 Instance (t3.medium recommended)
* Docker & Jenkins installed
* Trivy (Security Scanner) installed
* Docker Hub account with credentials configured in Jenkins

### How to use
1. Clone this repository:
   ```bash
   git clone [https://github.com/jatinkapoor009/autodeployx.git](https://github.com/jatinkapoor009/autodeployx.git)
