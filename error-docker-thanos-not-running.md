I installed docker extensions and there is already minkube running in the background
I installed Bitnami Helm charts 🚀
I installed Thanos on Minikube 🛠️
I saw Thanos working on Minikube 👀
I got an error when trying to install Thanos using Docker ❗

### Possible Reasons for Thanos Installation Failure on Docker

1. **Resource Constraints**: Docker might not have enough allocated resources (CPU, memory) to run Thanos properly.
2. **Network Issues**: There could be network configuration problems preventing Thanos from communicating with other services.
3. **Configuration Errors**: Incorrect or incomplete configuration settings in the Docker setup can lead to failures.
### Steps to Restart Thanos Installation on Docker from Scratch

1. **Remove Existing Containers and Images**:
    ```sh
    docker rm -f $(docker ps -aq)
    docker rmi -f $(docker images -q)
    ```

2. **Clean Up Docker Volumes**:
    ```sh
    docker volume prune -f
    ```

3. **Pull the Latest Thanos Docker Image**:
    ```sh
    docker pull thanosio/thanos:latest
    ```

```sh
docker pull thanosio/thanos:latest
```
```
Error response from daemon: manifest for thanosio/thanos:latest not found: manifest unknown: manifest unknown
```


### Troubleshooting the Error

If you encounter the error `manifest for thanosio/thanos:latest not found: manifest unknown: manifest unknown`, it means that the `latest` tag does not exist for the Thanos Docker image. You should specify a valid version tag instead.

1. **Find the Correct Version Tag**:
    - Visit the [Thanos Docker Hub page](https://hub.docker.com/r/thanosio/thanos/tags) to find the available tags.

2. **Pull a Specific Version**:
    ```sh
    docker pull thanosio/thanos:v0.23.1
    ```

Replace `v0.23.1` with the latest available version from the Docker Hub page.

3. **Update Docker Run Commands**:
    - **Thanos Store**:
        ```sh
        docker run -d --name thanos-store --network thanos-network thanosio/thanos:v0.23.1 store
        ```

The rewritten markdown content that would fit at $SELECTION_PLACEHOLDER$ wrapped with -+-+-+-+-+ is:
    - **Thanos Query**:
        ```sh
        docker run -d --name thanos-query --network thanos-network -p 10902:10902 thanosio/thanos:v0.23.1 query
        ```
        The rewritten markdown content that would fit at $SELECTION_PLACEHOLDER$ wrapped with -+-+-+-+-+ is:

        ```sh
        error: docker: Error response from daemon: Conflict. The container name "/thanos-query" is already in use by container "a66e55fb37bcdda6eff3605fd29195c5f58d45490df947d4973634dec929df87". You have to remove (or rename) that container to be able to reuse that name.
        ```

        ### Resolving Container Name Conflict

        If you encounter the error `Conflict. The container name "/thanos-query" is already in use`, you need to remove or rename the existing container.

        1. **Remove the Existing Container**:
            ```sh
            docker rm -f thanos-query
            ```

        2. **Run Thanos Query Again**:
            ```sh
            docker run -d --name thanos-query --network thanos-network -p 10902:10902 thanosio/thanos:v0.23.1 query
            ```

        By removing the existing container, you can reuse the name and run Thanos Query without conflicts.

By specifying a valid version tag, you can avoid the manifest not found error and successfully run Thanos on Docker.

4. **Create a Docker Network**:
    ```sh
    docker network create thanos-network
    ```

5. **Run Thanos Components**:
    - **Thanos Store**:
        ```sh
        docker run -d --name thanos-store --network thanos-network thanosio/thanos:latest store
        ```
    - **Thanos Query**:
        ```sh
        docker run -d --name thanos-query --network thanos-network -p 10902:10902 thanosio/thanos:latest query
        ```

6. **Verify Installation**:
    - Check running containers:
        ```sh
        docker ps
        ```
    - Access Thanos Query UI at `http://localhost:10902`

By following these steps, you can ensure a clean slate and a fresh installation of Thanos on Docker.