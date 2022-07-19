# openshift-node-exporter-systemd

## Background

By default OpenShift has disabled the systemd metrics for the node exporter.

- https://access.redhat.com/solutions/4844141

If you still need to monitor your systemd units you have the option to deploy a additional, custom node exporter. You can run the node exporter only for the systemd metrics and disable all other metrics. This repository shows you how you setup the node exporter and add it to the OpenShift Cluster Monitoring.

## What do you need

- A `DaemonSet` with the node-exporter (runs privilged because of some hostPath volumes)
- A headless `Service` (also creates the SSL certificate for you)
- A `ServiceMonitor` to enable the scraping in the Prometheus instance
- A `PrometheusRule` with your alert definitions

Examples are stored in the `manifests` folder.

## TODOs

This example use the `kube-rbac-proxy` image from OpenShift. It works fine, but there is no easy way to check if there is an update available for this image. Maybe the exporter should use the native SSL termination and/or the 401 basic auth feature from the node exporter itself.
