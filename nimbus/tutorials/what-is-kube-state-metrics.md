# What is Kube-state-metrics?

Kube-state-metrics is an open-source tool that provides cluster-level metrics for Kubernetes, a popular container orchestration system. It collects information about the state of objects in the Kubernetes cluster, such as nodes, pods, and services, and exposes them as metrics that can be scraped by a monitoring system, such as Prometheus.

Some common kube-state-metrics metrics include:
1. Node metrics: number of nodes, node capacity and utilization, and node conditions (e.g. ready, out-of-disk).
2. Pod metrics: number of pods, pod status (e.g. running, pending, failed), pod restart count, and container resource usage (e.g. CPU, memory).
3. Deployment metrics: number of deployments, desired and current replica counts, and deployment status (e.g. progressing, paused).
4. Service metrics: number of services, service endpoints, and service resource usage (e.g. CPU, memory).
5. ReplicaSet metrics: number of ReplicaSets, desired and current replica counts, and ReplicaSet status (e.g. progressing, paused).
5. DaemonSet metrics: number of DaemonSets, desired and current node counts, and DaemonSet status (e.g. progressing, paused).

These metrics can provide valuable insights into the health and performance of a Kubernetes cluster, and can help identify potential issues or bottlenecks. They can also be used to trigger alerts or notifications based on certain thresholds or conditions.
