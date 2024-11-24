# Ingress

An Ingress is a Kubernetes API resource that manages external access to services within a cluster. It acts as an entry point for HTTP(S) traffic and provides advanced routing capabilities, allowing you to define rules for directing requests to the appropriate backend services.

### What?

To interact with Jaeger UI, we need to port forward the pods, deployment or service which is created by the OpenTelemetry Operator. The idea is to create a new service for extensions which can be consumed by Ingress and users will be able to interact with the UI directly.

### How?

<img src="https://github.com/Ankit152/jaeger-operator-idea/blob/main/ingress/img/ingress.png">

Once a user creates a Jaeger instance, the operator will create a service for extensions if the ports are defined. If not defined, the service won't be created. OpenTelemetry Operator will also create an ingress for the extensions if the user specifies the values of the parameter. This ingress allow user to interact with the UI directly without needing to port-forward all the time.

### Implementation

This is being implemented [here](https://github.com/open-telemetry/opentelemetry-operator/pull/3441).