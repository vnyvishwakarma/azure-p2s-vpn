# Create P2S VPN Connection on Azure

## Introduction

This guide outlines the steps to create a Point-to-Site (P2S) VPN connection between an "on-premises" user virtual machine and a virtual network in Azure. This setup is intended to enable secure access to Azure resources from a remote location, utilizing an Azure VPN gateway.

### Prerequisites

- Access to an Azure account and the Azure portal.
- A user VM to serve as the "on-premises" client.
- PowerShell access on the user VM.
- Internet connectivity for downloading necessary tools and accessing the Azure portal.

## Steps Overview

1. **Preparation**: Log into Azure Portal.
2. **Connect to User VM**: Access the user VM using Remote Desktop.
3. **Generate Certificates**: Create both a self-signed root certificate and a client certificate.
4. **Export the Public Key**: Export the public key from the root certificate.
5. **Configure the VPN Gateway**: Insert the public certificate data into the Azure VPN Gateway configuration.
6. **Install the VPN Client**: Download and install the VPN client on the user VM.
7. **Test Connectivity**: Ensure the VPN connection is established and functioning.

## Detailed Instructions

### 1. Preparation

- Ensure you are logged into the Azure portal using an incognito or private browser window to avoid session conflicts with your personal account.
- **Note**: The creation of the VPN gateway may take between 30-45 minutes.

### 2. Connect to User VM

- Utilize Remote Desktop to connect to your user VM using the provided public IP address and credentials.

### 3. Generate Certificates

#### Generate the Self-Signed Root Certificate

- Open PowerShell on the user VM.
- Run the following command to generate a self-signed root certificate:

```bash
$cert = New-SelfSignedCertificate -Type Custom -KeySpec Signature `
  -Subject "CN=P2SRootCert" -KeyExportPolicy Exportable `
  -HashAlgorithm sha256 -KeyLength 2048 `
  -CertStoreLocation "Cert:\CurrentUser\My" -KeyUsageProperty Sign -KeyUsage CertSign

New-SelfSignedCertificate -Type Custom -DnsName P2SChildCert -KeySpec Signature `
-Subject "CN=P2SChildCert" -KeyExportPolicy Exportable `
-HashAlgorithm sha256 -KeyLength 2048 `
-CertStoreLocation "Cert:\CurrentUser\My" `
-Signer $cert -TextExtension @("2.5.29.37={text}1.3.6.1.5.5.7.3.2")```
```

### 4. Export the Public Key

- Access the Certificate Manager to export the public key of the root certificate and copy its data.

### 5. Configure VPN Gateway

- Navigate to the virtual network gateway's Point-to-site configuration in the Azure portal.
- Enter the root certificate name and paste the copied public key data.
- Save your changes.

### 6. Install VPN Client

- Download the VPN client from within the Azure portal.
- Proceed to install the VPN client on the user VM.

### 7. Test Connectivity

- Establish a connection to the VPN and test it by pinging the server VM's private IP address.










# Mayank C. Koli

**Email:** [Mayank.c.koli@gmail.com](mailto:Mayank.c.koli@gmail.com)  
**Phone:** +91-8826634734  
**Nationality:** Indian  
**Portfolio:** [https://manukoli1986.github.io/cv](https://manukoli1986.github.io/cv)  
**LinkedIn:** [https://www.linkedin.com/in/mayankckoli](https://www.linkedin.com/in/mayankckoli)  
**GitHub:** [https://github.com/manukoli1986](https://github.com/manukoli1986)  

---

## Profile

Highly skilled Cloud & DevSecOps Specialist with over 10 years of experience in AWS, CI/CD, Kubernetes, Python, and Terraform IAAC. Proficient in planning, implementing, and maintaining infrastructures, business applications, and microservices in AWS, GCP, and hybrid cloud environments. Experienced in leveraging Configuration Management, Container Orchestration, and Continuous Integration tools to drive operational excellence. Implemented SRE principles to enhance existing architecture.

---

## Work Experience

**Senior Site Reliability Engineer**  
*Insight Enterprise, Gurugram, India*  
_Aug 2023 – Present_

- Spearheaded the development of an automated incident response system, reducing mean time to resolve incidents by 50% and improving overall system availability.
- Implemented monitoring and alerting systems to proactively detect and resolve issues, minimizing downtime by 70% and ensuring high system reliability.
- Designed, implemented, and optimized CI/CD processes using GitHub Actions, ensuring efficiency and reusability across multiple projects.
- Automated and improved build and deployment workflows, significantly reducing time-to-market and enhancing code quality.
- Collaborated with development teams to define resource requirements, facilitating effective and efficient resource utilization.

**Cloud and DevOps Specialist**  
*Cognizant Technology, Bengaluru, India*  
_Apr 2021 – Aug 2023_

- Automated the provisioning of new development and test environments in the cloud, significantly reducing turnaround time.
- Implemented IAAC templates on AWS and associated services such as IAM, VPC, EC2, RDS, S3, ELB, Auto Scaling, Route 53, Cloud Watch, Cloud Trail, SQS, SNS, Deploy, Code Build, and Code Pipeline.
- Automated Kubernetes native PAAS platform using Python boto3 and Terraform.

**Senior DevOps Engineer**  
*HCL Technology Pvt Ltd, Noida, India*  
_Jul 2018 – Apr 2021_

- Defined and supervised cloud and platform consulting engagements.
- Conducted workshops with clients to evaluate cloud and platform requirements and presented tailored recommendations.
- Implemented cutting-edge cloud and platform solutions, such as running compute workloads on green energy.
- Developed a machine learning-based platform for running TensorFlow workloads.
- Explored novel cloud solutions on AWS and GCP to automate and remediate compliance issues.
- Managed cloud and platform implementations for clients and developed a serverless framework for different verticals.

**DevOps Engineer**  
*Atem Corp Pvt Ltd, Chennai, India*  
_Feb 2017 – May 2018_

- Provided day-to-day support for code build/deploy and ensured availability of SDLC environments.
- Configured and deployed applications in a Kubernetes cluster.
- Automated infrastructure through Terraform for efficient infra-automation (PaaS).
- Utilized Docker and Ansible to streamline DevOps processes.

**System Administrator**  
*Aspen Communication Pvt. Ltd, Delhi, India*  
_Aug 2016 – Dec 2016_

**Linux System Engineer**  
*CHI Networks Pvt. Ltd, Noida, India*  
_Jan 2015 – Aug 2016_

**System Administrator**  
*Progression Infonet Pvt. Ltd, Gurugram, India*  
_Sep 2014 – Jan 2015_

**Linux System Administrator**  
*INS E Solution Pvt Ltd, Delhi, India*  
_Mar 2011 – Sep 2014_

---

## Skills

- **Cloud Platforms:** AWS, GCP, Hybrid Cloud
- **DevOps Tools:** CI/CD, Kubernetes, Docker, Ansible, Terraform, GitHub Actions
- **Programming Languages:** Python
- **Monitoring & Automation:** SRE Principles, Incident Response, Monitoring Systems
- **Infrastructure as Code:** Terraform, Python boto3
- **Configuration Management:** Ansible, Jenkins
- **Version Control:** Git, Bitbucket
- **Other Tools:** Helm, JIRA, Confluence, Apache Maven, Apache Ant, Unix Shell Scripting

---

## Education

- **Bachelor’s Degree in Computer Science or Relevant Field** _(or relevant work experience)_

---

## Certifications

- Relevant Cloud Certifications (AWS, GCP)
- DevOps and CI/CD Related Certifications

---

## Languages

- English (Professional Proficiency)

---

## Additional Information

- Enjoys working with an international and diverse team.
- Available to work onsite or remotely within Germany or Austria.
- Open to learning and experiencing German culture.

---
