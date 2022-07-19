# openshift-node-exporter-systemd

## Background

By default OpenShift has disabled the systemd metrics for the node exporter.

- https://access.redhat.com/solutions/4844141

If you still need to monitor your systemd units you have the option to deploy a additional, custom node exporter. This repository shows you how to do so.

## What do you need

- A `DaemonSet` with the node-exporter (runs privilged because of some hostPath volumes)
- A headless `Service` (also creates the SSL certificate for you)
- A `ServiceMonitor` to enable the scraping in the Prometheus instance
- A `PrometheusRule` with your alert definitions 

## TODOs

This example use the `kube-rbac-proxy` image from OpenShift. It works fine, but there is no easy way to check if there is an update available for this image. Maybe the exporter should use the native SSL termination and/or the 401 basic auth feature from the node exporter itself.
