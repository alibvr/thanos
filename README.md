# thanos## Installation Guide for Thanos on Codespaces with Minikube

### Prerequisites

Ensure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Minikube](https://minikube.sigs.k8s.io/docs/start/)
- [Helm](https://helm.sh/docs/intro/install/)

### Steps

1. **Start Minikube:**
    ```sh
    minikube start
    ```

2. **Add Bitnami Repository:**
    ```sh
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm repo update
    ```

3. **Install Thanos:**
    ```sh
    helm install thanos bitnami/thanos
    ```

4. **Verify Installation:**
    ```sh
    kubectl get pods -l app.kubernetes.io/name=thanos
    ```

### Accessing Thanos

To access Thanos components, you can use port forwarding. For example, to access the Thanos Query component:
```sh
kubectl port-forward svc/thanos-query 9090:9090
```

Now you can access Thanos Query at `http://localhost:9090`.

### Cleanup

To uninstall Thanos and clean up resources:
```sh
helm uninstall thanos
minikube stop
```