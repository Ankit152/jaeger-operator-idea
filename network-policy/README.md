# Network Policy

### Pod Networking

Pods in Kubernetes are given unique IP addresses within a cluster, enabling direct communication between them.
By default, each Pod is isolated and has its own IP address, which allows for secure communication and avoid port conflict.

### Network Policy

Kubernetes offers network policies as a means to control traffic flow between pods. Network policies define rules that specify which pods can communicate with each other based on various parameters such as IP addresses, ports, and protocols. By enforcing network policies, we can segment the application’s network traffic and add an additional layer of security.

## What?

Jaeger stores traces in `in-memory` and in `database` e.g., cassandra, elasticsearch, and etc. The idea is to leverage the use of `NetworkPolicy` between the database and Jaeger deployments in a Kubernetes cluster.

## How?

<img src="https://github.com/Ankit152/jaeger-operator-idea/blob/main/network-policy/img/networkpolicy.png">

1. Users or Cluster Admins will create a database deployment with their configurations in the cluster.
2. Once the database deployment is ready, users will create a Jaeger instance in the cluster setting the config in the `OpenTelemetryCollector` kind and using Jaeger V2 image.
3. Once the user performs `kubectl apply`, the OpenTelemetery Operator will create a `NetworkPolicy` behind the scenes which will establish connection between the Jaeger instance and the database pod.

## Why?

Using `NetworkPolicy` will isolate the database deployment and restricting its communication just with Jaeger. Users can also create multiple replicas of the database which will tackle `single-point-of-failure` if one of the pods goes down. 

## Implementation

This can be implemented by adding a function for creating `network policy` similar to [`extension service`](https://github.com/open-telemetry/opentelemetry-operator/pull/3403) and [`ingress`](https://github.com/open-telemetry/opentelemetry-operator/pull/3441) in Opentelemetry Operator codebase. 

