Prerequisites

### 🚀 Step 1: Set Up Minikube Cluster

Start your Minikube cluster:

```bash
minikube start --memory=4096 --cpus=2
```

Verify the cluster is up:

```bash
kubectl get nodes
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

Connect Loki to Grafana:
- In Grafana, go to Configuration > Data Sources > Add Data Source.
- Select Loki, and in the URL field, enter: `http://loki.monitoring.svc.cluster.local:3100`.
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

