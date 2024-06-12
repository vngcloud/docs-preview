<div style="float: right;"><img src="../../images/01.png" width="160px" /></div><br>


# User Managed
- The **[NVIDIA GPU Operator](https://github.com/NVIDIA/gpu-operator)** is an operator that simplifies the deployment and management of GPU nodes in Kubernetes clusters. It provides a set of Kubernetes custom resources and controllers that work together to automate the management of GPU resources in a Kubernetes cluster.
- In this guide, we will show you how to:
  - Create a nodegroup with NVIDIA GPUs in a VKS cluster.
  - Install the NVIDIA GPU Operator in a VKS cluster.
  - Deploy some GPU workload in a VKS cluster.
  - Configure GPU Sharing in a VKS cluster.
  - Monitor GPU resources in a VKS cluster.
  - Autoscale GPU resources in a VKS cluster.

# Prerequisites
- A VKS cluster with at least **one NVIDIA GPU nodegroup**.
- `kubectl` command-line tool installed on your machine. For more information, see [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
- `helm` command-line tool installed on your machine. For more information, see [Installing Helm](https://helm.sh/docs/intro/install/).
- Other tools and libraries required by your GPU workload.
  - `kubectl-view-allocations` plugin for monitoring cluster resources. For more information, see [kubectl-view-allocations](https://github.com/davidB/kubectl-view-allocations)


<div style="float: right;">
<i>Cuong. Duong Manh - 2024/06/12</i>
</div>