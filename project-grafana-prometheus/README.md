# Prometheus
Prometheus is a free software application used for event monitoring and alerting. It records real-time metrics in a time series database built using a HTTP pull model, with flexible queries and real-time alerting. Prometheus can collect metrics about your application and infrastructure. Metrics are small concise descriptions of an event: date, time, and a descriptive value. While prometheus does store or ‘log’ metrics, metrics should not be confused with logs, which can include reams of data. Rather than gathering a great deal of data about one thing, Prometheus uses the approach of gathering a little bit of data about many things to help you understand the state and trajectory of your system. It has become very popular in the industry because it has many powerful features for monitoring metrics and providing alerts that can, with orchestration systems (e.g. Kubernetes), automate responses to changing conditions.

# Prometheus Architecture
The Prometheus is a multi-component system. While the following integrate into a Prometheus deployment, there is flexibility in which of these pieces are actually implemented.

Prometheus server (scrapes and stores metrics as time series data)
Client libraries for instrumenting application code
Push gateway (supports metrics collection from short-lived jobs)
Special-purpose exporters (Supports tools like HAProxy, StatsD, Graphite, etc.)
Alertmanager ( sends alerts based on triggers)
Additional support tools.
Prometheus can scrape metrics from jobs directly or, for short-lived jobs by using a push gateway when the job exits. The scraped samples are stored locally and rules are applied to the data to aggregate and generate new time series from existing data or generate alerts based on user-defined triggers. While Prometheus comes with a functional Web dashboard or other API consumers can be used to visualize the collected data, with Grafana being the de facto default.

# How Prometheus works
Prometheus gets metric from an exposed HTTP endpoint. A number of client libraries are available to provide this application integration when building software. With an available endpoint, Prometheus can scrape numerical data and store it as a time series in a local time series database. It can also integrate with remote storage options.

In addition to the stored time series, impermanent times series from the source are produced by queries. These series are recognized by metric name and key value pairs known by labels. Queries are generated using PromQL (Prometheus Query Language) that enables users to choose and aggregate time series data in real time. PromQL is also used to establish alert conditions that can then transmit notifications outside sources such as PagerDuty, Slack or email. These data can be displayed in graph or tabular form in Prometheus’s Web UI. Alternatively, and commonly, API integrations with alternative display solutions such as Grafana may be used.

# Prerequisites
Users must have basic knowledge of Kubernetes.
First we will have our cluster up and running next we will connect to our cluster and make sure we have an admin privileges to create cluster roles.
A Kubernetes cluster should be available where we can set up. Prometheus and Grafana.

# Create a Namespace & ClusterRole
First of all we will create a Kubernetes namespace for all our monitoring components. The name for our namespace will be "monitoring". If you don’t create a dedicated namespace, all the Prometheus kubernetes deployment objects get deployed on the default namespace. We will use the following command to create a new namespace named monitoring:

kubectl create namespace monitoring

This diagram illustrates the architecture of Prometheus and Grafana and its ecosystem components:






# Usage 
Without Helm for Kubernetes, we rely on Kubernetes YAML files to configure Kubernetes workloads. These YAML files specify everything needed for deploying containers. Everything, from the way each Pod needs to be configured to how load balancing is done by the Kubernetes cluster, has to be mentioned in those YAML files. Thus, to set up a new Kubernetes workload, we need to create a YAML file for that workload. To do it manually means writing multiple YAML files — one for each workload we create. Workloads can be deployments, service, configMaps, secrets and configuration files.

##  Installing Grafana
Grafana is an open-source observability platform for visualizing metrics, logs, and traces collected from your applications. It’s a cloud-native solution for quickly assembling data dashboards that let you inspect and analyze your stack.

First of all in order to connect to our GRafana Dashboard we need to expose our Grafana using Ingress. If you have an existing ingress controller setup, you can create an ingress object to route the Grafana DNS to the Prometheus backend service.

Also, you can add SSL for Grafana in the ingress layer.

## Conclusion
Grafana is a very powerful tool when it comes to Kubernetes monitoring dashboards.

It is used by many organizations to monitor their Kubernetes workloads. With the wide range of pre-built templates, you can get started with the templates pretty quickly.

## Useful Resources

| Name | Type |
|------|------|
| [Install Prometheus Operator with Grafana Cloud for Kubernetes](https://grafana.com/docs/grafana-cloud/kubernetes-monitoring/other-methods/prometheus/prometheus_operator/) | resource |
| [Kubernetes cluster monitoring (via Prometheus)](https://grafana.com/grafana/dashboards/315-kubernetes-cluster-monitoring-via-prometheus/) | resource |
| [Elasticsearch data source |  Grafana documentation](https://grafana.com/docs/grafana/latest/datasources/elasticsearch/) | resource |
| [How to Setup Prometheus Monitoring On Kubernetes Cluster](https://devopscube.com/setup-prometheus-monitoring-on-kubernetes/) | resource |
| [How To Setup Grafana On Kubernetes](https://devopscube.com/setup-grafana-kubernetes/) | resource |
| [Grafana documentation](https://grafana.com/docs/grafana/latest/) | resource |
| [How to Setup Nginx Ingress Controller On Kubernetes – Detailed Guide](https://devopscube.com/setup-ingress-kubernetes-nginx-controller/) | resource |

##  Dashboards Prometheus and Grafana looks like:









