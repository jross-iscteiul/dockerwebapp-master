# Docker Web App CI/CD Pipeline

This project automates the CI/CD process for deploying a Dockerized web application to Kubernetes using Jenkins, Docker, and Google Cloud.

## Overview

The pipeline automates the following steps:
1. **Checkout**: Retrieves the latest code from the repository.
2. **Build Image**: Builds and pushes a Docker image to Docker Hub.
3. **Deploy to Kubernetes**: Deploys the Docker image to a Google Kubernetes Engine (GKE) cluster.
4. **Expose Application**: Configures a Kubernetes service for the app.

## Technologies Used

- **Jenkins**: CI/CD automation.
- **Docker**: Containerization.
- **Kubernetes (GKE)**: Orchestrates deployments.
- **Google Cloud SDK**: Interacts with Google Cloud.

## Pipeline Stages

1. **Checkout**: Retrieves the source code from the repository.
2. **Build Image**: Builds and pushes the Docker image to Docker Hub.
3. **Deploy to Kubernetes**: Deploys the app to GKE, updating or creating the Kubernetes deployment.
4. **Set Services**: Exposes the app using a Kubernetes service.

## Setup

### Requirements:
1. **Jenkins**: With Docker, Kubernetes, and Google Cloud plugins.
2. **Docker Hub**: Account for storing images.
3. **Google Cloud**: GKE cluster and service account with necessary permissions.

### Configuration:
1. **Jenkins**: 
   - Install required plugins.
   - Configure Docker Hub and Google Cloud credentials.
2. **Kubernetes**: Ensure a running GKE cluster.
3. **Pipeline Script**: Add the pipeline script in Jenkins and adjust project-specific values.

## Usage

1. **Run Pipeline**: Jenkins will automatically build the Docker image, deploy it to GKE, and expose it as a service.
2. **Monitor**: View logs in Jenkins for status.

## Troubleshooting

- **Docker Issues**: Ensure Jenkins has Docker Hub credentials.
- **GKE Issues**: Verify `gcloud` credentials and cluster access.
