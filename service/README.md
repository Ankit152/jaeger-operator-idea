# Service

In Kubernetes, a Service is a method for exposing a network application that is running as one or more Pods in the cluster.
A key aim of Services in Kubernetes is that we don't need to modify our existing application to use an unfamiliar service discovery mechanism. We can run code in Pods, whether this is code designed for a cloud-native world or an older app you've containerized. We use a Service to make that set of Pods available on the network so that clients can interact with it.

### What?

To interact with Jaeger UI, we need to port forward the pods, deployment or service which is created by the OpenTelemetry Operator. The idea is to create a new service for extensions which can be consumed by Ingress and users will be able to interact with the UI directly.

### How?

<img src="https://github.com/Ankit152/jaeger-operator-idea/blob/main/service/img/service.png">

Once a user creates a Jaeger instance, the operator will create a service for extensions if the ports are defined. If not defined, the service won't be created.

### Implementation

This is being implemented [here](https://github.com/open-telemetry/opentelemetry-operator/pull/3403).