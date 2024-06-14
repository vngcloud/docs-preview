<div style="float: right;"><img src="../images/01.png" width="160px" /></div><br>


# Addons
- **[Keda](https://keda.sh/)** _(tested on VKS)_:
  ```bash
  helm install --wait kedacore \
    --namespace keda --create-namespace \
    oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/keda \
    --version 2.14.2
  ```

- **[Metrics Server](https://github.com/kubernetes-sigs/metrics-server)** _(tested on VKS)_:
  ```bash
  helm install --wait metrics-server \
  --namespace monitoring --create-namespace \
  oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/metrics-server \
  --version 3.12.1 \
  --set args[0]="--kubelet-insecure-tls"
  ```

- **[Prometheus Adapter](https://github.com/kubernetes-sigs/prometheus-adapter)** _(tested on VKS)_:
  ```bash
  prometheus_service=$(kubectl get svc -n prometheus -lapp=kube-prometheus-stack-prometheus -ojsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}')
  helm install --wait prometheus-adapter \
    --namespace prometheus --create-namespace \
    oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/prometheus-adapter \
    --version 4.10.0 \
    --set prometheus.url=http://${prometheus_service}.prometheus.svc.cluster.local
  ```

- **[Prometheus Stack](https://github.com/prometheus-community/helm-charts/tree/main/charts/kube-prometheus-stack)** _(tested on VKS)_:
  ```bash
  helm install --wait prometheus-stack \
    --namespace prometheus --create-namespace \
    oci://vcr.vngcloud.vn/81-vks-public/vks-helm-charts/kube-prometheus-stack \
    --version 60.0.2 \
    --set prometheus.prometheusSpec.serviceMonitorSelectorNilUsesHelmValues=false
  ```