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

- The image below shows my machine setup, it will be used in this guide:
  ```bash
  # Check kubectl CLI version
  kubectl version

  # Check Helm version
  helm version
  
  # Check kubectl-view-allocations version
  kubectl view-allocations --version
  ```

<center>

  ![](./../../images/nodegroup/02.png)

</center>

# Prerequisites
- A VKS cluster with at least **one NVIDIA GPU nodegroup**.
- `kubectl` command-line tool installed on your machine. For more information, see [Install and Set Up kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).
- `helm` command-line tool installed on your machine. For more information, see [Installing Helm](https://helm.sh/docs/intro/install/).
- (Optional) Other tools and libraries that you can use to monitor and manage your Kubernetes resources:
  - `kubectl-view-allocations` plugin for monitoring cluster resources. For more information, see [kubectl-view-allocations](https://github.com/davidB/kubectl-view-allocations).

- The image below is my cluster with 1 NVIDIA GPU nodegroup, it will be used in this guide, execute the following command to check the nodegroup in your cluster:
  ```bash
  kubectl get nodes -owide
  ```

<center>

  ![](./../../images/nodegroup/01.1.png)

</center>

# Install GPU Operator


<div style="float: right;">
<i>Cuong. Duong Manh - 2024/06/12</i>
</div>