# envoygw
## This document shows how to:
>   1 - Deploy Envoy implementation of Kubernetes Gateway <br />.
>   2 - deploy a shared gateway to create TCPRoutes to handle multiple backends across different namespaces <br />.


### Step1 - Deploy Envoy Gateway ( Note TCPRoute is implemented in release 0.3.0 onwards )

` kubectl apply -f https://github.com/envoyproxy/gateway/releases/download/v0.3.0/install.yaml `

`kubectl wait --timeout=5m -n envoy-gateway-system deployment/envoy-gateway --for=condition=Available`

### Step2 - Deploy Envoy GatewayClass

`kubectl apply -f gwclass.yaml` 

### Step3 - Deploy two three namespaces 

1 - db-gw ( dedicated gateway namespace )
2 - ns1 ( db1 backend runs here )
3 - ns2 ( db2 backend runs here )

`kubectl apply -f ns.yaml`

### Step4 - Deploy gateway`

`kubectl apply -f db-gw.yaml 

### Step5 - Deploy Backend, service and TCPRoutes 

`kubectl apply -f mysql1.yaml`
`kubectl apply -f mysql2.yaml`

### Step 6 -  Test the deployment and GW connetivity 

`GW=$(kubectl get gateway/db-gateway -o jsonpath='{.status.addresses[0].value}' -n db-gw)`
`nc $GW 3306`
`nc $GW 3307`
