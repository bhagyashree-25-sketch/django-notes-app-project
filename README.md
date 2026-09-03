# Django Simple Notes App - CI/CD Pipeline Automation
A full-stack notes application built with React (frontend) and Django (backend), automated with a complete CI/CD pipeline from code push to Kubernetes deployment.

# Access the deployed application via AWS EC2 Public DNS and Kubernetes NodePort:
 http://ec2-13-200-252-55.ap-south-1.compute.amazonaws.com:30627

 # Application Output / Working UI
1.  📓 My Notes
Note #5
Does the time not update or something? tests
2.  📅 6/2/2026
Note #4
Looks like everything is working so far This is a test update ok ev...
3.  📅 1/20/2023
Note #3
This a new note now REACT is integrated with Django!
4.  📅 1/20/2023
Note #2
This is a new note XD
5.  📅 1/20/2023
Note #1
One - Two - Three
6.  📅 1/20/2023

# Installation
Clone the repository
git clone https://github.com/adhya2020/django-notes-app.git

Build the app
docker build -t my-note-app .

Run the app
docker run -p 8000:8000 my-note-app

# Architecture
GitHub → Jenkins pipeline → Docker Image → DockerHub → Kubernetes Cluster

# Pipeline Flow Diagram
┌──────────────┐    ┌──────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Code Clone  │───▶│    Build     │───▶│  Push to Docker  │───▶│  Deploy to K8s    │
│  from GitHub │    │  Docker Image│    │     DockerHub    │    │   Cluster         │
└──────────────┘    └──────────────┘    └──────────────────┘    └───────────────────┘

# Tech Stack
| Component        | Technology            |
|------------------|-----------------------|
| Backend          | Django                |
| Containerization | Docker                |
| CI/CD            | Jenkins (Declarative Pipeline) |
| Image Registry   | DockerHub             |
| Orchestration    | Kubernetes            |
| Version Control  | Git/GitHub            |


# Pipeline Stages
1. Code Cloning
Clones the source code from the main branch of the GitHub repository.
2. Build
Builds a Docker image from the Dockerfile present in the root directory.
Image is tagged as my-note-app.
3. Push Image to DockerHub
Authenticates with DockerHub using stored Jenkins credentials.
Tags and pushes the image as:
<dockerhub-username>/my-note-app:microdegree
4. Deploy to Kubernetes
Applies Kubernetes manifests (deployment.yaml and service.yaml) located in the notesapp/ directory.
Uses Kubernetes credentials configured in Jenkins.

# Prerequisites
Jenkins running with the following plugins:
1. Docker Pipeline Plugin
2. Kubernetes CLI Plugin
3. Git Plugin
4. Credentials Binding Plugin
5. Docker installed on the Jenkins agent
6. kubectl installed on the Jenkins agent
7. Kubernetes cluster up and running
8. DockerHub account with a repository created

# Jenkins Credentials Setup
Before running the pipeline, configure the following credentials in Jenkins:
1. Credential ID
2. Type
3. Description
4. dockerHub	Username & Password	DockerHub login credentials
5. kuberenetes	Kubernetes Config	Kubeconfig for cluster access

# Steps to add credentials:

Go to Jenkins Dashboard → Manage Jenkins → Credentials
Click System → Global credentials → Add Credentials
Add DockerHub credentials with ID dockerHub
Add Kubernetes kubeconfig with ID kuberenetes

# Project Structure
django-notes-app/
├── Dockerfile                 # Docker image definition
├── Jenkinsfile               # Jenkins pipeline configuration
├── notesapp/
│   ├── deployment.yaml        # Kubernetes Deployment manifest
│   └── service.yaml           # Kubernetes Service manifest
├── manage.py                  # Django management script
├── requirements.txt           # Python dependencies
└── ...                        # Django project files
