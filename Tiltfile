# if cluster not reachable, create one (idempotent)
if local('kubectl cluster-info > /dev/null 2>&1', quiet=True).exit_code != 0:
  local('kind create cluster --name beaulink-dev')

# ensure Envoy Gateway is installed (idempotent helm upgrade)
local('helm repo add envoy-gateway https://charts.envoyproxy.io')
local('helm upgrade --install envoy-gateway envoy-gateway/envoy-gateway -n gateway-system --create-namespace')

# load all gateway YAMLs
k8s_yaml('../edge-gateway/configs')
