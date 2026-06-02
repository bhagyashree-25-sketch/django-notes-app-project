# Django Simple Notes App CI/CD Pipeline Automation
This is a simple notes app built with React and Django.

Author
Bhagyashree
GitHub: bhagyashree-25-sketch

Architecture
GitHub → Jenkins pipeline → Docker Image → DockerHub → Kubernetes Cluster

Pipeline Flow Diagram
┌──────────────┐    ┌──────────────┐    ┌──────────────────┐    ┌───────────────────┐
│  Code Clone  │───▶│    Build     │───▶│  Push to Docker  │───▶│  Deploy to K8s    │
│  from GitHub │    │  Docker Image│    │     DockerHub    │    │   Cluster         │
└──────────────┘    └──────────────┘    └──────────────────┘    └───────────────────┘

Tech Stack
| Component        | Technology            |
|------------------|-----------------------|
| Backend          | Django                |
| Containerization | Docker                |
| CI/CD            | Jenkins (Declarative Pipeline) |
| Image Registry   | DockerHub             |
| Orchestration    | Kubernetes            |
| Version Control  | Git/GitHub            |


Pipeline Stages
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

Prerequisites
Jenkins running with the following plugins:
Docker Pipeline Plugin
Kubernetes CLI Plugin
Git Plugin
Credentials Binding Plugin
Docker installed on the Jenkins agent
kubectl installed on the Jenkins agent
Kubernetes cluster up and running
DockerHub account with a repository created

Jenkins Credentials Setup
Before running the pipeline, configure the following credentials in Jenkins:

Credential ID
Type
Description
dockerHub	Username & Password	DockerHub login credentials
kuberenetes	Kubernetes Config	Kubeconfig for cluster access

Steps to add credentials:

Go to Jenkins Dashboard → Manage Jenkins → Credentials
Click System → Global credentials → Add Credentials
Add DockerHub credentials with ID dockerHub
Add Kubernetes kubeconfig with ID kuberenetes

Project Structure
django-notes-app/
├── Dockerfile                 # Docker image definition
├── Jenkinsfile               # Jenkins pipeline configuration
├── notesapp/
│   ├── deployment.yaml        # Kubernetes Deployment manifest
│   └── service.yaml           # Kubernetes Service manifest
├── manage.py                  # Django management script
├── requirements.txt           # Python dependencies
└── ...                        # Django project files
