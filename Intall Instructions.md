
Install K3S
```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.34.2+k3s1" INSTALL_K3S_EXEC="server" sh -s - --disable=traefik --disable=servicelb --node-taint 'node-role.kubernetes.io/master=true:NoSchedule'
```

Join Cluster
```sh
curl -sfL https://get.k3s.io | INSTALL_K3S_VERSION="v1.34.2+k3s1" K3S_TOKEN="K10451089c8a9fdad5c740595b146f1db6a92d64f978b6143fd6c31757f03386ab0::server:a22f3676092b3ee4b498fd66d7114737" K3S_URL="https://192.168.3.10:6443" K3S_NODE_NAME="k3s-node-3" sh -
```

Install Cert Manager
```sh
helm install \
  cert-manager oci://quay.io/jetstack/charts/cert-manager \
  --version v1.19.2 \
  --namespace cert-manager \
  --create-namespace \
  --set crds.enabled=true
```

Install MetalLB
```sh
kustomize build ./k8s/metallb | kubectl apply -f -
```

Install Traefik

```sh
helm upgrade -f k8s/traefik/values.yaml \
  --install \
  --create-namespace \
  --namespace traefik \
  traefik oci://ghcr.io/traefik/helm/traefik
```

Install Rancher
```sh
helm upgrade --install --wait --create-namespace -n cattle-system rancher rancher-latest/rancher \
  --values ./k8s/rancher-values.yaml
```