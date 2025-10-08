# Containerized Next.js App with Docker, GitHub Actions, and Minikube

This project demonstrates a complete CI/CD pipeline for a Next.js application. The application is containerized using Docker, automatically built and pushed to GitHub Container Registry (GHCR) using GitHub Actions, and deployed to a local Kubernetes cluster (Minikube).

## Prerequisites

Before you begin, ensure you have the following tools installed:
- **Docker:** To build and run container images.
- **Minikube:** To run a local Kubernetes cluster.
- **kubectl:** The Kubernetes command-line tool.
- **Git:** For version control.

## Project Structure
.
├── .github/workflows/  # GitHub Actions CI/CD pipeline
│   └── main.yml
├── k8s/                # Kubernetes manifests
│   ├── deployment.yaml
│   └── service.yaml

├── index.js
├── .dockerignore
├── Dockerfile
├── package.json
└── README.md


## Local Setup and Run

To run the application locally using Docker:

1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YOUR_USERNAME/YOUR_REPO.git](https://github.com/YOUR_USERNAME/YOUR_REPO.git)
    cd YOUR_REPO
    ```

2.  **Build the Docker image:**
    ```bash
    docker build -t nextjs-app-local .
    ```

3.  **Run the Docker container:**
    ```bash
    docker run -p 3000:3000 nextjs-app-local
    ```
    The application will be accessible at `http://localhost:3000`.

## Deployment to Minikube

Follow these steps to deploy the application to your local Minikube cluster.

1.  **Start Minikube:**
    ```bash
    minikube start
    ```

2.  **Apply the Kubernetes manifests:**
    Navigate to the root of the project and apply the `deployment` and `service` configurations.
    ```bash
    kubectl apply -f k8s/
    ```

3.  **Verify the deployment:**
    Check that the pods are running correctly. You should see 2 pods with a `Running` status.
    ```bash
    kubectl get pods
    ```
    Check that the service has been created.
    ```bash
    kubectl get service my-nextjs-app-service
    ```

## How to Access the Deployed Application

Minikube provides a simple command to get the URL of the exposed service.

1.  **Get the application URL:**
    ```bash
    minikube service my-nextjs-app-service --url
    ```

2.  **Access the application:**
    Open the URL provided by the command in your web browser to see your deployed Next.js application.

## CI/CD with GitHub Actions

This project is configured with a GitHub Actions workflow (`.github/workflows/main.yml`) that automates the following process:

1.  **Trigger:** On every push to the `main` branch.
2.  **Build:** It builds the Docker image based on the `Dockerfile`.
3.  **Push:** It pushes the newly built image to the GitHub Container Registry (GHCR).

The container image for this repository can be found at:
`ghcr.io/YOUR_USERNAME/YOUR_REPO:main`
