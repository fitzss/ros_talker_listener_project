# ROS Talker Listener Project

This project contains a simple ROS application with Talker and Listener nodes. It is structured to leverage modern CI/CD practices using Dagger, Tekton, Kubernetes, and Helm.

## Project Structure
ros talker listener project/
│
├── src/
│ ├── talker/
│ ├── listener/
│
├── docker/
│
├── pipeline/
│
├── helm/
│ ├── templates/
│
├── k8s/
│
├── scripts/
│
└── README.md

## Requirements

- Go installed
- Docker
- Kubernetes Cluster (KinD or any available cluster)
- Helm

## Getting Started

1. **Build Locally**: 
    ```sh
    go run pipeline/service-pipeline.go build src/talker
    ```

2. **Run Tests**:
    ```sh
    go run pipeline/service-pipeline.go test src/talker
    ```

3. **Publish Docker Image**:
    ```sh
    CONTAINER_REGISTRY=<YOUR_REGISTRY> CONTAINER_REGISTRY_USER=<YOUR_USER> go run pipeline/service-pipeline.go publish src/talker v1.0.0
    ```

4. **Deploy to Kubernetes**:
    ```sh
    helm install my-ros-app helm/
    ```

5. **Run Pipelines with Tekton**:
    ```sh
    kubectl apply -f pipeline/pipeline.yaml
    ```

## Running Remotely on Kubernetes

1. Create a Pod with Dagger:
    ```sh
    kubectl run dagger --image=registry.dagger.io/engine:v0.3.13 --privileged=true
    ```

2. Export Environment Variable:
    ```sh
    export _EXPERIMENTAL_DAGGER_RUNNER_HOST="kube-pod://dagger?context=kind-dev&namespace=default&container=dagger"
    ```

3. Run Build Remotely:
    ```sh
    go run pipeline/service-pipeline.go build src/talker
    ```

4. Tail Logs:
    ```sh
    kubectl logs -f dagger
    ```

## Monitoring & Visualization

- **Prometheus & Grafana**: Deploy using configurations in `k8s/`.

## Scripts

Helper scripts for building, testing, and deploying are available in the `scripts/` directory.

## License

This project is licensed under the MIT License - see the LICENSE file for details.

