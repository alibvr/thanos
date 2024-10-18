# thanos## Installation Guide for Thanos on Codespaces with Minikube

### Prerequisites

Ensure you have the following installed:
- [Docker](https://docs.docker.com/get-docker/)
- [Helm](https://helm.sh/docs/intro/install/)

### Steps

1. **Start Docker:**
    Ensure Docker is running on your machine.

2. **Add Bitnami Repository:**
    ```sh
    helm repo add bitnami https://charts.bitnami.com/bitnami
    helm repo update
    ```

3. **Install Thanos:**
    ```sh
    helm install thanos bitnami/thanos
    ```


4. **Install Thanos inside Docker:**
    ```sh


        ```sh
        # Ensure no existing Thanos container is running
        docker rm -f thanos || true

        # Run Thanos inside Docker
        docker run -d --name thanos bitnami/thanos

        # Verify Thanos container is running
        docker ps | grep thanos
        ```


    ```

5. **Verify Installation:**
    ```sh
    helm ls | grep thanos
    ```



### Accessing Thanos

To access Thanos components, you can use Docker port forwarding. For example, to access the Thanos Query component:
```sh
docker run -d -p 9090:9090 bitnami/thanos-query
```

Now you can access Thanos Query at `http://localhost:9090`.

### Cleanup

To uninstall Thanos and clean up resources:
```sh
helm uninstall thanos
```

