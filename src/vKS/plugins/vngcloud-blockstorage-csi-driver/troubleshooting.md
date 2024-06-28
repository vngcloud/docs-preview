<div style="float: right;"><img src="../../../images/01.png" width="160px" /></div><br>

# Troubleshooting
- The table below lists common **issues** and **solutions** for the **VNG Cloud BlockStorage CSI Driver**.
  
  |#|Issue|Solution|Notes|
  |-|-|-|-|
  |[Issue 1](#issue-1)|_Multi-Attach error for volume "pvc-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" Volume is already exclusive attached to one node and can't be attached to another_|<ul><li>[sol-csi-01](#sol-csi-01)</li><li>[sol-csi-02](#sol-csi-02)</li></ul>|![](../../../images/csi/issue/01.png)|

# Solutions
## Issue 1
### Reason
- The issue `Multi-Attach error for volume "pvc-xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" Volume is already exclusive attached to one node and can't be attached to another` in Kubernetes indicates that a **Persistent Volume Claim (PVC)** is trying to be used by **multiple pods** on **different nodes**, but the volume is **already attached** to a specific node and **CANNOT** be attached to another node simultaneously.

### Solutions
#### sol-csi-01
- Ensure Pods Using the Same PVC are Scheduled on the Same Node:
  - You can use `nodeAffinity` or `podAffinity` to ensure that pods using the same `PVC` are scheduled on the same node.
  - Example with `nodeAffinity`:
    ```yaml
    apiVersion: apps/v1
    kind: Deployment
    metadata:
      name: my-app
    spec:
      replicas: 1
      selector:
        matchLabels:
          app: my-app
      template:
        metadata:
          labels:
            app: my-app
        spec:
          containers:
          - name: my-app-container
            image: my-app:latest
            volumeMounts:
            - mountPath: /data
              name: my-volume
          volumes:
          - name: my-volume
            persistentVolumeClaim:
              claimName: my-pvc
          affinity:
            nodeAffinity:
              requiredDuringSchedulingIgnoredDuringExecution:
                nodeSelectorTerms:
                - matchExpressions:
                  - key: kubernetes.io/hostname
                    operator: In
                    values:
                    - node1
    ```

#### sol-csi-02
- Delete and recreate the pod using the PVC:
  - As a temporary workaround, if the volume is no longer needed on the old node, you can delete the pod and let Kubernetes reschedule it. Kubernetes will detach the volume from the old node and attach it to the new node.
  - Example:
    ```bash
    kubectl delete pod <pod-name>
    ```