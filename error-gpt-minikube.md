Prerequisites
### 🚀 Step 1: Set Up Minikube Cluster

Start your Minikube cluster:

```bash
minikube start --memory=4096 --cpus=2
```

#### Example Output:

```bash
minikube start --memory=4096 --cpus=2
😄  minikube v1.34.0 on Ubuntu 20.04 (docker/amd64)
✨  Using the docker driver based on existing profile
❗  You cannot change the memory size for an existing minikube cluster. Please first delete the cluster.
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.45 ...
🤷  docker "minikube" container is missing, will recreate.
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.31.0 on Docker 27.2.0 ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
❗  Enabling 'storage-provisioner' returned an error: running callbacks: [sudo KUBECONFIG=/var/lib/minikube/kubeconfig /var/lib/minikube/binaries/v1.31.0/kubectl apply --force -f /etc/kubernetes/addons/storage-provisioner.yaml: Process exited with status 1
stdout:

stderr:
error: error validating "/etc/kubernetes/addons/storage-provisioner.yaml": error validating data: failed to download openapi: Get "https://localhost:8443/openapi/v2?timeout=32s": dial tcp [::1]:8443: connect: connection refused; if you choose to ignore these errors, turn validation off with --validate=false
]
❗  Enabling 'default-storageclass' returned an error: running callbacks: [sudo KUBECONFIG=/var/lib/minikube/kubeconfig /var/lib/minikube/binaries/v1.31.0/kubectl apply --force -f /etc/kubernetes/addons/storageclass.yaml: Process exited with status 1
stdout:

stderr:
error: error validating "/etc/kubernetes/addons/storageclass.yaml": error validating data: failed to download openapi: Get "https://localhost:8443/openapi/v2?timeout=32s": dial tcp [::1]:8443: connect: connection refused; if you choose to ignore these errors, turn validation off with --validate=false
]
🌟  Enabled addons: 

❌  Exiting due to K8S_APISERVER_MISSING: wait 6m0s for node: wait for apiserver proc: apiserver process never appeared
💡  Suggestion: Check that the provided apiserver flags are valid, and that SELinux is disabled
🍿  Related issues:
    ▪ https://github.com/kubernetes/minikube/issues/4536
    ▪ https://github.com/kubernetes/minikube/issues/6014
```

#### Troubleshooting:

- **Memory Size Error**: You cannot change the memory size for an existing Minikube cluster. Please delete the cluster first.
- **Kubernetes Components Verification Error**: Errors related to enabling 'storage-provisioner' and 'default-storageclass' due to validation issues. Consider turning validation off with `--validate=false`.
- **API Server Missing**: Ensure that the provided apiserver flags are valid and that SELinux is disabled. Refer to the related issues for more information.

Verify the cluster is up:

```bash
kubectl get nodes
```

#### Example Output:

```bash
E1018 11:12:09.837337   34926 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.49.2:8443/api?timeout=32s\": dial tcp 192.168.49.2:8443: connect: connection refused"
E1018 11:12:09.838822   34926 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.49.2:8443/api?timeout=32s\": dial tcp 192.168.49.2:8443: connect: connection refused"
E1018 11:12:09.840133   34926 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.49.2:8443/api?timeout=32s\": dial tcp 192.168.49.2:8443: connect: connection refused"
E1018 11:12:09.841421   34926 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.49.2:8443/api?timeout=32s\": dial tcp 192.168.49.2:8443: connect: connection refused"
E1018 11:12:09.842747   34926 memcache.go:265] "Unhandled Error" err="couldn't get current server API group list: Get \"https://192.168.49.2:8443/api?timeout=32s\": dial tcp 192.168.49.2:8443: connect: connection refused"
The connection to the server 192.168.49.2:8443 was refused - did you specify the right host or port?
```

#### Troubleshooting:

- **Connection Refused**: Ensure that Minikube is running and that you have specified the correct host and port. You can restart Minikube with:

```bash
minikube stop
minikube start
```
### 🧹 Step 1.5: Clean Up Environment

Before proceeding, ensure your environment is clean to avoid conflicts. Run the following commands to delete any existing Minikube cluster and Helm releases:

#### 🛑 Stop Minikube:

```bash
minikube stop
```

**Example Output:**

```bash
minikube stop
✋  Stopping node "minikube"  ...
✋  Stopping node "minikube"  ...
✋  Stopping node "minikube"  ...
✋  Stopping node "minikube"  ...
✋  Stopping node "minikube"  ...
✋  Stopping node "minikube"  ...

❌  Exiting due to GUEST_STOP_TIMEOUT: Unable to stop VM: docker container inspect minikube --format=<no value>: exit status 1
stdout:


stderr:
Error response from daemon: No such container: minikube


╭───────────────────────────────────────────────────────────────────────────────────────────╮
│                                                                                           │
│    😿  If the above advice does not help, please let us know:                             │
│    👉  https://github.com/kubernetes/minikube/issues/new/choose                           │
│                                                                                           │
│    Please run `minikube logs --file=logs.txt` and attach logs.txt to the GitHub issue.    │
│    Please also attach the following file to the GitHub issue:                             │
│    - /tmp/minikube_stop_020cbdfafb3addd44ca10e374123151e03b1d8b9_0.log                    │
│                                                                                           │
╰───────────────────────────────────────────────────────────────────────────────────────────╯
```

#### 🗑️ Delete Minikube Cluster:

```bash
minikube delete
```

**Example Output:**

```bash
minikube delete
🔥  Deleting "minikube" in docker ...
🔥  Removing /home/codespace/.minikube/machines/minikube ...
💀  Removed all traces of the "minikube" cluster.
```

```bash
minikube status
```

```bash
$ minikube start
😄  minikube v1.34.0 on Ubuntu 20.04 (docker/amd64)
✨  Automatically selected the docker driver. Other choices: none, ssh
📌  Using Docker driver with root privileges
👍  Starting "minikube" primary control-plane node in "minikube" cluster
🚜  Pulling base image v0.0.45 ...
🔥  Creating docker container (CPUs=2, Memory=2200MB) ...
🐳  Preparing Kubernetes v1.31.0 on Docker 27.2.0 ...
    ▪ Generating certificates and keys ...
    ▪ Booting up control plane ...
    ▪ Configuring RBAC rules ...
🔗  Configuring bridge CNI (Container Networking Interface) ...
🔎  Verifying Kubernetes components...
    ▪ Using image gcr.io/k8s-minikube/storage-provisioner:v5
🌟  Enabled addons: storage-provisioner, default-storageclass
🏄  Done! kubectl is now configured to use "minikube" cluster and "default" namespace by default
```

```bash
@alibvr ➜ /workspaces/thanos (main) $ minikube status
minikube
type: Control Plane
host: Running
kubelet: Running
apiserver: Running
kubeconfig: Configured
```

```bash
@alibvr ➜ /workspaces/thanos (main) $ minikube profile list
|----------|-----------|---------|--------------|------|---------|---------|-------|----------------|--------------------|
| Profile  | VM Driver | Runtime |      IP      | Port | Version | Status  | Nodes | Active Profile | Active Kubecontext |
|----------|-----------|---------|--------------|------|---------|---------|-------|----------------|--------------------|
| minikube | docker    | docker  | 192.168.49.2 | 8443 | v1.31.0 | Running |     1 | *              | *                  |
|----------|-----------|---------|--------------|------|---------|---------|-------|----------------|--------------------|
```

```bash
@alibvr ➜ /workspaces/thanos (main) $ kubectl get nodes
NAME       STATUS   ROLES           AGE   VERSION
minikube   Ready    control-plane   30s   v1.31.0
```

Now, you can proceed with a clean environment.

### 🛠️ Step 2: Install Helm

If Helm isn’t already installed, run:

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

Verify Helm installation:

```bash
helm version
```
### 🛠️ Step 2: Install Helm

If Helm isn’t already installed, run:

```bash
curl https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3 | bash
```

Verify Helm installation:

```bash
helm version
```

### 📊 Step 3: Install Prometheus

Prometheus will be used to collect and store metrics.

Add the Prometheus Helm repository:

```bash
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo update
```

Install Prometheus:

```bash
helm install prometheus prometheus-community/prometheus --namespace monitoring --create-namespace
```

Verify Prometheus installation:

```bash
kubectl get pods -n monitoring
```

Expose Prometheus for access:

```bash
kubectl --namespace monitoring port-forward deploy/prometheus-server 9090
```

Now, Prometheus is accessible via [http://localhost:9090](http://localhost:9090).

### 📈 Step 4: Install Grafana

Grafana will be used to visualize metrics from Prometheus.

Add the Grafana Helm repository:

```bash
helm repo add grafana https://grafana.github.io/helm-charts
```

Install Grafana:

```bash
helm install grafana grafana/grafana --namespace monitoring
```

Get the Grafana admin password:

```bash
kubectl get secret --namespace monitoring grafana -o jsonpath="{.data.admin-password}" | base64 --decode ; echo
```

Expose Grafana:

```bash
kubectl --namespace monitoring port-forward svc/grafana 3000:80
```

Now, access Grafana at [http://localhost:3000](http://localhost:3000) using `admin` and the password retrieved.

Connect Prometheus to Grafana:
- In Grafana, go to Configuration > Data Sources > Add Data Source.
- Select Prometheus, and in the URL field, enter: `http://prometheus-server.monitoring.svc.cluster.local:9090`.
- Click Save & Test.

### Adding Prometheus as a Data Source in Grafana

To add Prometheus as a data source in Grafana, follow these steps:

1. **Access Grafana**:
    - Ensure Grafana is running and accessible. If not, start it with:
      ```bash
      kubectl --namespace monitoring port-forward svc/grafana 3000:80
      ```
    - Open your browser and go to [http://localhost:3000](http://localhost:3000).

2. **Log In to Grafana**:
    - Use the default credentials: `admin` for the username and the password you retrieved earlier.

3. **Add Prometheus Data Source**:
    - In Grafana, navigate to **Configuration** > **Data Sources**.
    - Click **Add data source**.
    - Select **Prometheus** from the list of available data sources.

4. **Configure Prometheus Data Source**:
    - In the **HTTP** section, set the URL to:
      ```plaintext
      http://prometheus-server.monitoring.svc.cluster.local:9090
      ```
    - Leave other settings as default unless you have specific requirements.

5. **Save and Test**:
    - Click **Save & Test** to verify the connection to Prometheus.
    - Ensure you see a message indicating the data source is working.

#### Troubleshooting:

- **Error Message**: If you encounter an error such as:
    ```plaintext
    Post "http://prometheus-server.monitoring.svc.cluster.local:9090/api/v1/query": dial tcp 10.97.135.124:9090: i/o timeout
    ```
    This indicates there was an error querying the Prometheus API.

- **Finding the Correct URL**: To find the correct URL for Prometheus, you can use the following command to get the service details:
    ```bash
    kubectl get svc -n monitoring
    ```
    Look for the `prometheus-server` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
    ```plaintext
    http://<CLUSTER-IP>:<PORT>
    ```

- **Example**:
    ```bash
    kubectl get svc -n monitoring
    ```
    Output:
    ```plaintext
    NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    prometheus-server       ClusterIP   10.97.135.124    <none>        9090/TCP   10m
    ```
    The URL would be:
    ```plaintext
    http://10.97.135.124:9090
    ```

    Output:

    ```bash
    kubectl get svc -n monitoring
    ```
    ```plaintext
    NAME                                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    grafana                               ClusterIP   10.96.115.7      <none>        80/TCP     31m
    prometheus-alertmanager               ClusterIP   10.106.148.243   <none>        9093/TCP   32m
    prometheus-alertmanager-headless      ClusterIP   None             <none>        9093/TCP   32m
    prometheus-kube-state-metrics         ClusterIP   10.97.74.45      <none>        8080/TCP   32m
    prometheus-prometheus-node-exporter   ClusterIP   10.98.254.165    <none>        9100/TCP   32m
    prometheus-prometheus-pushgateway     ClusterIP   10.99.93.15      <none>        9091/TCP   32m
    prometheus-server                     ClusterIP   10.97.135.124    <none>        80/TCP     32m
    ```

    The URL would be:
    ```plaintext
    http://10.97.135.124:80
    ```

    ```plaintext
    output: Successfully queried the Prometheus API.
    ```

    ### 🔍 Step 4.5: Verify Prometheus Data Source in Grafana

    After adding Prometheus as a data source in Grafana, follow these steps to ensure it is working correctly:

    1. **Access Grafana**:
        - Open your browser and go to [http://localhost:3000](http://localhost:3000).

    2. **Log In to Grafana**:
        - Use the default credentials: `admin` for the username and the password you retrieved earlier.

    3. **Navigate to Data Sources**:
        - Go to **Configuration** > **Data Sources**.
        - Click on the Prometheus data source you added.

    4. **Test the Data Source**:
        - Click the **Save & Test** button.
        - Ensure you see a message indicating the data source is working.

        ```plaintext
        output: Successfully queried the Prometheus API.
        ```

    5. **Create a Simple Dashboard**:
        - **Go to Create > Dashboard**:
            - In the Grafana UI, navigate to the left-hand side menu and click on the **+** (plus) icon.
            - Select **Dashboard** from the dropdown menu.
        - **Click Add new panel**:
            - In the new dashboard view, click on the **Add new panel** button.
        - **In the Query section, select Prometheus as the data source**:
            - In the panel editor, locate the **Query** section.
            - From the **Data source** dropdown, select **Prometheus**.
        - **Enter a simple query like `up` to check if Prometheus is collecting metrics**:
            - In the query input field, type `up`.
            - This query checks the status of the Prometheus targets and returns `1` if they are up.
        - **Click Apply to add the panel to the dashboard**:
            - After entering the query, click the **Apply** button at the top right of the panel editor.
            - This will save the panel and add it to your dashboard.
        - **Save the Dashboard**:
            - Click on the **Save** icon (diskette) at the top of the dashboard.
            - Provide a name for your dashboard and click **Save**.

    By following these steps, you will create a simple Grafana dashboard panel that displays the status of your Prometheus targets.
    ```plaintext
    output: Successfully queried the Prometheus API.
    ```

    ### 🔍 Step 4.5: Verify Prometheus Data Source in Grafana

    After adding Prometheus as a data source in Grafana, follow these steps to ensure it is working correctly:

    1. **Access Grafana**:
        - Open your browser and go to [http://localhost:3000](http://localhost:3000).

    2. **Log In to Grafana**:
        - Use the default credentials: `admin` for the username and the password you retrieved earlier.

    3. **Navigate to Data Sources**:
        - Go to **Configuration** > **Data Sources**.
        - Click on the Prometheus data source you added.

    4. **Test the Data Source**:
        - Click the **Save & Test** button.
        - Ensure you see a message indicating the data source is working.

        ```plaintext
        output: Successfully queried the Prometheus API.
        ```

    5. **Create a Simple Dashboard**:
        - Go to **Create** > **Dashboard**.
        - Click **Add new panel**.
        - In the **Query** section, select **Prometheus** as the data source.
        - Enter a simple query like `up` to check if Prometheus is collecting metrics.
        - Click **Apply** to add the panel to the dashboard.

    6. **Verify the Panel**:
        - Ensure the panel displays data, indicating that Prometheus is successfully collecting and Grafana is able to query it.

    #### Troubleshooting:

    - **Timeout Error**: If you encounter a timeout error like:
      ```plaintext
      Post "https://10.97.135.124:9090/api/v1/query": dial tcp 10.97.135.124:9090: i/o timeout
      ```
      This indicates there was an error querying the Prometheus API.

    - **Finding the Correct URL**: To find the correct URL for Prometheus, you can use the following command to get the service details:
      ```bash
      kubectl get svc -n monitoring
      ```
      Look for the `prometheus-server` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
      ```plaintext
      http://<CLUSTER-IP>:<PORT>
      ```

    - **Example**:
      ```bash
      kubectl get svc -n monitoring
      ```
      Output:
      ```plaintext
      NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
      prometheus-server       ClusterIP   10.97.135.124    <none>        9090/TCP   10m
      ```
      The URL would be:
      ```plaintext
      http://10.97.135.124:9090
      ```

    - **Update Grafana Configuration**: Use the obtained URL to update the Prometheus data source configuration in Grafana.

    By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.

    #### Troubleshooting:

    - **No Data Displayed**: If no data is displayed, ensure that Prometheus is running and accessible.
    - **Error Messages**: Check for any error messages in the panel or data source configuration and address them accordingly.

    By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.
    6. **Verify the Panel**:
        - Ensure the panel displays data, indicating that Prometheus is successfully collecting and Grafana is able to query it.

    #### Troubleshooting:

    - **Timeout Error**: If you encounter a timeout error like:
      ```plaintext
      Post "https://10.97.135.124:9090/api/v1/query": dial tcp 10.97.135.124:9090: i/o timeout
      ```
      This indicates there was an error querying the Prometheus API.

    - **Finding the Correct URL**: To find the correct URL for Prometheus, you can use the following command to get the service details:
      ```bash
      kubectl get svc -n monitoring
      ```
      Look for the `prometheus-server` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
      ```plaintext
      http://<CLUSTER-IP>:<PORT>
      ```

    - **Example**:
      ```bash
      kubectl get svc -n monitoring
      ```
      Output:
      ```plaintext
      NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
      prometheus-server       ClusterIP   10.97.135.124    <none>        9090/TCP   10m
      ```
      The URL would be:
      ```plaintext
      http://10.97.135.124:9090
      ```

    - **Update Grafana Configuration**: Use the obtained URL to update the Prometheus data source configuration in Grafana.

    By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.

    #### Troubleshooting:

    - **No Data Displayed**: If no data is displayed, ensure that Prometheus is running and accessible.
    - **Error Messages**: Check for any error messages in the panel or data source configuration and address them accordingly.

    By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.

By following these steps, you can troubleshoot and resolve issues related to querying the Prometheus API.

- **Update Grafana Configuration**: Use the obtained URL to update the Prometheus data source configuration in Grafana.

### 🔍 Step 4.5: Verify Prometheus Data Source in Grafana

After adding Prometheus as a data source in Grafana, follow these steps to ensure it is working correctly:

1. **Access Grafana**:
    - Open your browser and go to [http://localhost:3000](http://localhost:3000).

2. **Log In to Grafana**:
    - Use the default credentials: `admin` for the username and the password you retrieved earlier.

3. **Navigate to Data Sources**:
    - Go to **Configuration** > **Data Sources**.
    - Click on the Prometheus data source you added.

4. **Test the Data Source**:
    - Click the **Save & Test** button.
    - Ensure you see a message indicating the data source is working.

    ```plaintext
    output: Post "https://10.97.135.124:9090/api/v1/query": dial tcp 10.97.135.124:9090: i/o timeout - There was an error returned querying the Prometheus API.
    ```

5. **Create a Simple Dashboard**:
    - Go to **Create** > **Dashboard**.
    - Click **Add new panel**.
    - In the **Query** section, select **Prometheus** as the data source.
    - Enter a simple query like `up` to check if Prometheus is collecting metrics.
    - Click **Apply** to add the panel to the dashboard.

6. **Verify the Panel**:
    - Ensure the panel displays data, indicating that Prometheus is successfully collecting and Grafana is able to query it.

#### Troubleshooting:

- **Timeout Error**: If you encounter a timeout error like:
  ```plaintext
  Post "https://10.97.135.124:9090/api/v1/query": dial tcp 10.97.135.124:9090: i/o timeout
  ```
  This indicates there was an error querying the Prometheus API.

- **Finding the Correct URL**: To find the correct URL for Prometheus, you can use the following command to get the service details:
  ```bash
  kubectl get svc -n monitoring
  ```
  Look for the `prometheus-server` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
  ```plaintext
  http://<CLUSTER-IP>:<PORT>
  ```

- **Example**:
  ```bash
  kubectl get svc -n monitoring
  ```
  Output:
  ```plaintext
  NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
  prometheus-server       ClusterIP   10.97.135.124    <none>        9090/TCP   10m
  ```
  The URL would be:
  ```plaintext
  http://10.97.135.124:9090
  ```

- **Update Grafana Configuration**: Use the obtained URL to update the Prometheus data source configuration in Grafana.

By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.

#### Troubleshooting:

- **No Data Displayed**: If no data is displayed, ensure that Prometheus is running and accessible.
- **Error Messages**: Check for any error messages in the panel or data source configuration and address them accordingly.

By following these steps, you can verify that the Prometheus data source is correctly configured and working in Grafana.


6. **Troubleshooting**:
    - If you encounter an error such as `401 Unauthorized`, ensure that Prometheus is running and accessible.
    - Verify the Prometheus server URL and check for any network policies or firewall rules that might be blocking access.

Now, you can use Prometheus as a data source in Grafana to create dashboards and visualize metrics.


### 📜 Step 5: Install Loki

Loki will be used for log aggregation.

Install Loki:

```bash
helm install loki grafana/loki-stack --namespace monitoring --set grafana.enabled=false,promtail.enabled=true
```

Verify Loki installation:

```bash
kubectl get pods -n monitoring
```

```plaintext
NAME                                                 READY   STATUS    RESTARTS   AGE
grafana-565c8644c-82h98                              1/1     Running   0          49m
loki-0                                               1/1     Running   0          111s
loki-promtail-t7c2x                                  1/1     Running   0          111s
prometheus-alertmanager-0                            1/1     Running   0          51m
prometheus-kube-state-metrics-75b5bb4bf8-mw5c2       1/1     Running   0          51m
prometheus-prometheus-node-exporter-zg7q8            1/1     Running   0          51m
prometheus-prometheus-pushgateway-84557d6c79-chj98   1/1     Running   0          51m
prometheus-server-644d686bc6-mvmtz                   2/2     Running   0          51m
```

Connect Loki to Grafana:
- In Grafana, go to Configuration > Data Sources > Add Data Source.
- Select Loki, and in the URL field, enter: `http://loki.monitoring.svc.cluster.local:3100`.
- Click Save & Test.

#### Troubleshooting:

- **Unable to Connect with Loki**: If you encounter an error such as:
    ```plaintext
    Unable to connect with Loki. Please check the server logs for more details.
    ```
    Ensure that Loki is running and accessible. Verify the Loki service URL and check for any network policies or firewall rules that might be blocking access.
- **Finding the Correct URL**: To find the correct URL for Loki, you can use the following command to get the service details:
    ```bash
    kubectl get svc -n monitoring
    ```

    ```plaintext
    NAME                                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    grafana                               ClusterIP   10.96.115.7      <none>        80/TCP     54m
    loki                                  ClusterIP   10.103.40.243    <none>        3100/TCP   6m59s
    loki-headless                         ClusterIP   None             <none>        3100/TCP   6m59s
    loki-memberlist                       ClusterIP   None             <none>        7946/TCP   6m59s
    prometheus-alertmanager               ClusterIP   10.106.148.243   <none>        9093/TCP   56m
    prometheus-alertmanager-headless      ClusterIP   None             <none>        9093/TCP   56m
    prometheus-kube-state-metrics         ClusterIP   10.97.74.45      <none>        8080/TCP   56m
    prometheus-prometheus-node-exporter   ClusterIP   10.98.254.165    <none>        9100/TCP   56m
    prometheus-prometheus-pushgateway     ClusterIP   10.99.93.15      <none>        9091/TCP   56m
    prometheus-server                     ClusterIP   10.97.135.124    <none>        80/TCP     56m
    ```

    Look for the `loki` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
    ```plaintext
    http://<CLUSTER-IP>:<PORT>
    ```

- **Example**:
    ```bash
    kubectl get svc -n monitoring
    ```
    ```plaintext
    NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    loki                   ClusterIP   10.97.135.124    <none>        3100/TCP   10m
    ```
    The URL would be:
    ```plaintext
    http://10.97.135.124:3100
    ```

- **Adding Loki Data Source in Grafana**:
    - In Grafana, go to **Configuration** > **Data Sources** > **Add Data Source**.
    - Select **Loki** from the list of available data sources.
    - In the **HTTP** section, set the URL to:
      ```plaintext
      http://loki.monitoring.svc.cluster.local:3100
      ```

    - Click **Save & Test** to verify the connection to Loki.
    - Ensure you see a message indicating the data source is working.

#### Troubleshooting:

- **Unable to Connect with Loki**: If you encounter an error such as:
    ```plaintext
    Unable to connect with Loki. Please check the server logs for more details.
    ```
    Ensure that Loki is running and accessible. Verify the Loki service URL and check for any network policies or firewall rules that might be blocking access.
- **Finding the Correct URL**: To find the correct URL for Loki, you can use the following command to get the service details:
    ```bash
    kubectl get svc -n monitoring
    ```

    ```plaintext
    NAME                                  TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    loki                                  ClusterIP   10.103.40.243    <none>        3100/TCP   6m59s
    ```

    Look for the `loki` service and note its `CLUSTER-IP` and `PORT`. The URL should be in the format:
    ```plaintext
    http://<CLUSTER-IP>:<PORT>
    ```

- **Example**:
    ```bash
    kubectl get svc -n monitoring
    ```
    ```plaintext
    NAME                    TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)    AGE
    loki                   ClusterIP   10.103.40.243    <none>        3100/TCP   10m
    ```
    The URL would be:
    ```plaintext
    http://10.103.40.243:3100
    ```

- **Adding Loki Data Source in Grafana**:
    - In Grafana, go to **Configuration** > **Data Sources** > **Add Data Source**.
    - Select **Loki** from the list of available data sources.
    - In the **HTTP** section, set the URL to:
      ```plaintext
      http://10.103.40.243:3100
      ```

    - Click **Save & Test** to verify the connection to Loki.
    - Ensure you see a message indicating the data source is working.
    - Click **Save & Test** to verify the connection to Loki.
    - Ensure you see a message indicating the data source is working.

By following these steps, you can verify that Loki is correctly installed and connected to Grafana.
    ```

By following these steps, you can troubleshoot and resolve issues related to connecting Loki to Grafana.

By following these steps, you can verify that Loki is correctly installed and connected to Grafana.
- Click Save & Test.

### 🔍 Step 6: Install Elasticsearch, Fluentd, and Kibana (EFK Stack)

This stack will be used for log collection (Fluentd), storage (Elasticsearch), and visualization (Kibana).

Install the Elastic Helm chart repository:

```bash
helm repo add elastic https://helm.elastic.co
```

Install Elasticsearch:

```bash
helm install elasticsearch elastic/elasticsearch --namespace logging --create-namespace
```

Install Kibana:

```bash
helm install kibana elastic/kibana --namespace logging
```

Create a `fluentd.yaml` file for the Fluentd DaemonSet configuration:

```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
    name: fluentd
    namespace: logging
spec:
    selector:
        matchLabels:
            app: fluentd
    template:
        metadata:
            labels:
                app: fluentd
        spec:
            containers:
            - name: fluentd
                image: fluent/fluentd-kubernetes-daemonset
                env:
                - name: FLUENT_ELASTICSEARCH_HOST
                    value: "elasticsearch-master"
                - name: FLUENT_ELASTICSEARCH_PORT
                    value: "9200"
```

Deploy Fluentd:

```bash
kubectl apply -f fluentd.yaml
```

Expose Kibana:

```bash
kubectl --namespace logging port-forward svc/kibana-kibana 5601:5601
```

Access Kibana at [http://localhost:5601](http://localhost:5601).

### 📊 Step 7: Setting Up Dashboards in Grafana

Metrics Dashboards:
- Go to Grafana.
- Import the popular Prometheus dashboards by going to Dashboards > Import, and use Prometheus as the data source.

Logs Dashboards:
- Create dashboards based on Loki for logs. You can create panels that visualize log patterns, log counts, and log levels.

### ✅ Step 8: Verify the Setup

- **Prometheus**: Check that metrics are being collected by querying in the Prometheus UI ([http://localhost:9090](http://localhost:9090)).
- **Grafana**: Check that dashboards are displaying metrics and logs.
- **Loki**: Verify that logs are collected and visualized in Grafana.
- **EFK**: Access Kibana ([http://localhost:5601](http://localhost:5601)) and check that logs are indexed and searchable.

