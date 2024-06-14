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

- **[Prometheus Stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)**
  ```bash
  helm install --wait prometheus-stack \
    --namespace prometheus --create-namespace \
    oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/kube-prometheus-stack \
    --version 60.0.2 \
    --set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false
  ```

- **[Prometheus Adapter](https://github.com/kubernetes-sigs/prometheus-adapter)**
  ```bash
  prometheus_service=$(kubectl get svc -n prometheus -lapp=kube-prometheus-stack-prometheus -ojsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}')
  helm install --wait prometheus-adapter \
    --namespace prometheus --create-namespace \
    oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/prometheus-adapter \
    --version 4.10.0 \
    --set prometheus.url=http://${prometheus_service}.prometheus.svc.cluster.local
  ```