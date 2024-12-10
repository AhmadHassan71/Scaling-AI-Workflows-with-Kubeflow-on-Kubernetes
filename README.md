# Scaling AI Workflows with Kubeflow on Kubernetes

This project demonstrates how to create and manage AI workflows using Kubeflow on Kubernetes. The main focus is on building a Kubeflow pipeline for training and predicting with an IRIS classifier model.

## Prerequisites

Before running the Kubeflow pipeline, make sure you have the following prerequisites installed:

- Docker
- Minikube
- Kubernetes

### Installation

1. Add Docker's official GPG key:

    ```bash
    sudo apt-get update
    sudo apt-get install ca-certificates curl gnupg
    sudo install -m 0755 -d /etc/apt/keyrings
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg
    sudo chmod a+r /etc/apt/keyrings/docker.gpg
    ```

2. Add the Docker repository to Apt sources:

    ```bash
    echo "deb [arch=\$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] https://download.docker.com/linux/ubuntu \$(. /etc/os-release && echo \$VERSION_CODENAME) stable" | sudo tee /etc/apt/sources.list.d/docker.list > /dev/null
    ```

3. Update the package list:

    ```bash
    sudo apt-get update
    ```

4. Install Docker and related packages:

    ```bash
    sudo apt-get install docker-ce docker-ce-cli containerd.io docker-buildx-plugin docker-compose-plugin
    ```

5. Download and install Minikube:

    ```bash
    curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube_latest_amd64.deb
    sudo dpkg -i minikube_latest_amd64.deb
    ```

6. Start the Minikube cluster:

    ```bash
    sudo usermod -aG docker $USER && newgrp docker
    minikube start
    ```

7. Interact with the Kubernetes cluster:

    ```bash
    kubectl get po -A
    ```

8. Deploy Kubeflow Pipelines:

    ```bash
    export PIPELINE_VERSION=2.0.2
    kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/cluster-scoped-resources?ref=$PIPELINE_VERSION"
    kubectl wait --for condition=established --timeout=60s crd/applications.app.k8s.io
    kubectl apply -k "github.com/kubeflow/pipelines/manifests/kustomize/env/platform-agnostic-pns?ref=$PIPELINE_VERSION"
    ```

### Usage

1. Start a Minikube cluster, if not already running:

    ```bash
    minikube start
    ```

2. Verify that the Kubeflow Pipelines UI is accessible by port forwarding:

    ```bash
    kubectl port-forward -n kubeflow svc/ml-pipeline-ui 8080:80
    ```

## Topics Covered

**Kubeflow Pipeline Building Demo - IRIS classifier Model training and prediction**

1. Python function needed to train and predict
2. Creating components from python functions
3. Initialise kubeflow pipeline
4. Define the pipeline function and put together all the components
5. Mounting volume for component's output storage
6. Compiling pipeline and generating yaml - it can be directly uploaded to kubeflow and create experiments and runs using UI
7. Create run from pipeline function using the code
8. How to disable cache to see the each steps output on second and successive runs

## Reference

I have learned and followed the steps from this repository: [KubeFlow-Pipeline-IRIS-Classifier-Demo](https://github.com/at0m-b0mb/KubeFlow-Pipeline-IRIS-Classifier-Demo)
