## Monitoring Stack Deployment with Flux

## Overview

This setup deploys a comprehensive monitoring and observability stack on Kubernetes using Flux. The deployment includes monitoring for nodes, pods, logs, and specific applications, along with alerting rules and dashboards in Grafana.

## Components Deployed

* Blackbox Exporter - For external endpoint monitoring.

* OpenTelemetry Collector - Collects and exports traces and metrics.

* Jaeger - Distributed tracing system.

* Prometheus Remote Write Exporter - Sends metrics to a remote storage.

* Loki - Centralized log aggregation.

* Promtail - Log collection agent for Loki.

* Kube-Prometheus-Stack (Prometheus and Grafana) - Full monitoring stack for Kubernetes.

* Nodes, Pods, and Logs Dashboards - Preconfigured dashboards in Grafana.

* Alerting Rules - Monitors node disk and RAM utilization with alerts.

* PodMonitor for Flux - Monitors Flux with associated Grafana dashboards.

* ServiceMonitors - Ensures all services are properly monitored.

## Deployment

The entire stack is deployed using Flux, ensuring GitOps-based continuous delivery and automated updates.

## Prerequisites

* Kubernetes cluster

* Flux installed and configured

* A configured Git repository with Flux manifests

## Installation Steps

Clone the repository containing the Flux configuration:

    git clone <your-repo-url>
    cd <your-repo-directory>

Apply the Flux configuration to your cluster:

    flux reconcile source git flux-system
    flux reconcile kustomization monitoring

Verify deployments:

    kubectl get pods -n monitoring

Access Grafana:

    kubectl port-forward svc/grafana -n monitoring 3000:80

Default credentials:

    User: admin

    Password: (Check your Helm values or secrets)

Monitoring and Alerts

* Dashboards for nodes, pods, logs, and Flux are available in Grafana.

* Alerts are configured for node disk and RAM utilization.

* OpenTelemetry integrates tracing with Jaeger.

## Customization

## Modify values.yaml in your Helm charts to:

* Adjust alert thresholds

* Configure data retention policies

* Add custom dashboards

* Enable/disable exporters

## Troubleshooting

Check pod logs:

    kubectl logs -n monitoring <pod-name>

Verify service discovery:

    kubectl get servicemonitors -n monitoring

Debug Flux reconciliation:

    flux get kustomizations

## Conclusion

This setup ensures a robust monitoring and observability stack for Kubernetes, managed efficiently using Flux for GitOps-based automation.
>>>>>>> d54db6d (monitoring stack deployment with flux)
