# Prometheus
Prometheus is an open-source monitoring and alerting system that was originally developed by SoundCloud. It is designed to collect metrics from various sources, store them, and provide a query language to retrieve and analyze them. Prometheus is known for its scalability, flexibility, and robustness, making it a popular choice for monitoring large, distributed systems.

# How Prometheus works
Prometheus gets metric from an exposed HTTP endpoint. A number of client libraries are available to provide this application integration when building software. With an available endpoint, Prometheus can scrape numerical data and store it as a time series in a local time series database. It can also integrate with remote storage options.

In addition to the stored time series, impermanent times series from the source are produced by queries. These series are recognized by metric name and key value pairs known by labels. Queries are generated using PromQL (Prometheus Query Language) that enables users to choose and aggregate time series data in real time. PromQL is also used to establish alert conditions that can then transmit notifications outside sources such as PagerDuty, Slack or email. These data can be displayed in graph or tabular form in Prometheus’s Web UI. Alternatively, and commonly, API integrations with alternative display solutions such as Grafana may be used.

# Prerequisites
Users must have basic knowledge of Kubernetes.
First we will have our cluster up and running next we will connect to our cluster and make sure we have an admin privileges to create cluster roles.
A Kubernetes cluster should be available where we can set up. Prometheus and Grafana.

# Create a Namespace & ClusterRole
First of all we will create a Kubernetes namespace for all our monitoring components. The name for our namespace will be "monitoring". If you don’t create a dedicated namespace, all the Prometheus kubernetes deployment objects get deployed on the default namespace. We will use the following command to create a new namespace named monitoring:
# Follow steps to set up Prometheus
kubectl create namespace monitoring
Step 1: Create a file named clusterRole.yaml inside should be ClusterRole & ClusterRoleBinding.
Step 2: Create the role using the following command.
kubectl create -f clusterRole.yaml
Step 3: Create a file called config-map.yaml
Step 4: Execute the following command to create the config map in Kubernetes.
kubectl create -f config-map.yaml
Step 5: Create a file named prometheus-deployment.yaml
kubectl create -f prometheus-deployment.yaml
Step 6:Connecting To Prometheus Dashboard
kubectl get pods --namespace=monitoring
kubectl port-forward your_prometheus_pod_name 8080:9090 -n monitoring
Step 7: Now, if you access http://localhost:8080 on your browser, you will get the Prometheus home page.


# Usage 
Without Helm for Kubernetes, we rely on Kubernetes YAML files to configure Kubernetes workloads. These YAML files specify everything needed for deploying containers. Everything, from the way each Pod needs to be configured to how load balancing is done by the Kubernetes cluster, has to be mentioned in those YAML files. Thus, to set up a new Kubernetes workload, we need to create a YAML file for that workload. To do it manually means writing multiple YAML files — one for each workload we create. Workloads can be deployments, service, configMaps, secrets and configuration files.

##  Installing Grafana
Grafana is an open-source observability platform for visualizing metrics, logs, and traces collected from your applications. It’s a cloud-native solution for quickly assembling data dashboards that let you inspect and analyze your stack.

First of all in order to connect to our Grafana Dashboard we need to expose our Grafana using Ingress. If you have an existing ingress controller setup, you can create an ingress object to route the Grafana DNS to the Prometheus backend service.

Also, you can add SSL for Grafana in the ingress layer.

# Follow steps to set up Grafana
Step 1: Create a file named grafana-datasource-config.yaml
Step 2: Create the configmap using the following command.
kubectl create -f grafana-datasource-config.yaml
Step 3: Create a file named deployment.yaml
Note: This Grafana deployment does not use a persistent volume. If you restart the pod all changes will be gone. Use a persistent volume if you are deploying Grafana for your project requirements. It will persist all the configs and data that Grafana uses.
Step 4: Create the deployment
kubectl create -f deployment.yaml
Step 5: Create a service file named service.yaml










## Conclusion
Grafana is a very powerful tool when it comes to Kubernetes monitoring dashboards.

It is used by many organizations to monitor their Kubernetes workloads. With the wide range of pre-built templates, you can get started with the templates pretty quickly.

## Useful Resources

| Name | Type |
|------|------|
| [Install Prometheus Operator with Grafana Cloud for Kubernetes](https://grafana.com/docs/grafana-cloud/kubernetes-monitoring/other-methods/prometheus/prometheus_operator/) | resource |
| [Kubernetes cluster monitoring (via Prometheus)](https://grafana.com/grafana/dashboards/315-kubernetes-cluster-monitoring-via-prometheus/) | resource |
| [Elasticsearch data source Grafana documentation](https://grafana.com/docs/grafana/latest/datasources/elasticsearch/) | resource |
| [How to Setup Prometheus Monitoring On Kubernetes Cluster](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/) | resource |
| [How To Setup Grafana On Kubernetes](https://devopscube.com/setup-grafana-kubernetes/) | resource |
| [Grafana documentation](https://grafana.com/docs/grafana/latest/) | resource |
| [How to Setup Nginx Ingress Controller On Kubernetes – Detailed Guide](https://devopscube.com/setup-ingress-kubernetes-nginx-controller/) | resource |










