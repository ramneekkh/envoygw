# envoygw
## This document shows how to 
1 - Deploy Envoy implementation of Kubernetes Gateway 
2 - deploy a shared gateway to create TCPRoutes to handle multiple backends across different namespaces.


### Step1 - Deploy Envoy Gateway ( Note TCPRoute is implemented in release 0.3.0 onwards )

` kubectl apply -f https://github.com/envoyproxy/gateway/releases/download/v0.3.0/install.yaml `

`kubectl wait --timeout=5m -n envoy-gateway-system deployment/envoy-gateway --for=condition=Available`

### Step2 - Deploy Envoy GatewayClass

`kubectl apply -f gwclass.yaml` 
