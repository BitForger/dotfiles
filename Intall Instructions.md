

Install K3S
```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.28.15+k3s1" INSTALL_K3S_EXEC="server" sh -s - --disable=traefik --disable=servicelb --node-taint 'node-role.kubernetes.io/master=true:NoSchedule'
```

Join Cluster
```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.28.15+k3s1" K3S_TOKEN="<token>" K3S_URL="https://192.168.3.10:6443" K3S_NODE_NAME="k3s-node-1" sh -
```

Install Cert Manager
```sh
helm install \
  cert-manager jetstack/cert-manager \
  --namespace cert-manager \
  --create-namespace \
  --version v1.13.2 \
  --set installCRDs=true
```

Install MetalLB
```sh
helm repo add metallb https://metallb.github.io/metallb
helm install \
  metallb metallb/metallb \
  --namespace metallb \
  --create-namespace
```

Patch Metallb NS
```sh
kubectl label namespaces metallb-system pod-security.kubernetes.io/enforce=privileged pod-security.kubernetes.io/audit=privileged pod-security.kubernetes.io/warn=privileged
```

Install Rancher
```sh
helm upgrade --install --wait --create-namespace -n cattle-system rancher rancher-latest/rancher \
  --values ./k8s/rancher-values.yaml
```