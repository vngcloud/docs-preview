<div style="float: right;"><img src="../images/01.png" width="160px" /></div><br>


# Addons
- **[Metrics Server](https://github.com/kubernetes-sigs/metrics-server)**
  ```bash
  helm install --wait metrics-server \
  --namespace monitoring --create-namespace \
  oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/metrics-server \
  --version 3.12.1 \
  --set args[0]="--kubelet-insecure-tls"
  ```