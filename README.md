Django Simple Notes App CI/CD Pipeline Automation
This is a simple notes app built with React and Django.

Requirements
Python 3.9
Node.js
React

Architecture & Workflow
CI/CD Architecture Diagram

The CI/CD Flow:

Developer Push: Code is committed and pushed to the Git repository (GitHub).
Webhook Trigger: A Git webhook triggers the Jenkins pipeline automatically.
Build & Test: Jenkins pulls the code, installs dependencies, and runs Django unit tests.
Docker Build: Upon successful tests, Jenkins builds a new Docker image of the Django app.
Docker Push: The newly built image is tagged and pushed to DockerHub.
Kubernetes Deploy: Jenkins updates the Kubernetes deployment on AWS to pull the new image from DockerHub, triggering a Rolling Update.
