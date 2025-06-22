# Load the extension to glob K8s YAML configs
load('ext://k8s_yaml_glob', 'k8s_yaml_glob')

local('bash -c "kubectl cluster-info >/dev/null 2>&1 || kind create cluster --name beaulink-dev"')

# 2) Install Envoy Gateway via Helm
local(
    """helm upgrade --install envoy-gateway oci://docker.io/envoyproxy/gateway-helm \
--version v1.4.1 -n gateway-system --create-namespace""",
    quiet=True
)

# 3) Load all YAML config files
k8s_yaml_glob('../edge-gateway/configs/*.y*ml')
