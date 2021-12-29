## Upgrade the kubernetes cluster with command
### Master node upgrade process

#### Disable the sechudling on Control Plance node (master node).
##### where ***master01*** is your master node name.

```
kubectl cordon master01
```
```
kubectl drain master01 --ignore-daemonsets --force
```
#### On the controlplane node,run the following commands:
##### This will update the package lists from the software repository.
```
apt update
```

#### This will install the kubeadm version 1.20
```
apt install kubeadm=1.20.0-00
```
#### This will upgrade kubernetes controlplane. Note that this can take a few minutes.
```
kubeadm upgrade apply v1.20.0
```
#### This will update the kubelet with the version 1.20.
```
apt install kubelet=1.20.0-00
```

#### You may need to restart kubelet after it has been upgraded.
##### Run bewlow command:
```
systemctl restart kubelet
```

### Worker node upgrade process

#### On the worker node,run the following commands:

#### Disable the sechudling on worker node.
##### where ***worker01*** is your worker node name.

```
kubectl cordon worker01
```

```
kubectl drain worker01 --ignore-daemonsets --force
```
##### This will update the package lists from the software repository.
```
apt update
```
#### This will install the kubeadm version 1.20
```
apt install kubeadm=1.20.0-00
```
#### This will upgrade kubernetes controlplane. Note that this can take a few minutes.
```
kubeadm upgrade node
```
#### This will update the kubelet with the version 1.20.
```
apt install kubelet=1.20.0-00
```

#### You may need to restart kubelet after it has been upgraded.
##### Run bewlow command:
```
systemctl restart kubelet
```
