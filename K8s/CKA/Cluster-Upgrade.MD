### Upgrade Cluster using kubeadm

Reference Documentation : https://kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade/ <br>
Another good reference : https://devopscube.com/upgrade-kubernetes-cluster-kubeadm/ <br>

Standard procedure is to upgrade as follows: <br>
1. Control plane <br>
2. Worker Nodes <br>

The following components also need to be upgraded: <br>
1. kubeadm <br>
2. kubelet <br>
3. kubectl <br>

SSH into control plane first:
```
kubectl get nodes

# If you are on some other node, ssh into control plane
ssh controlplane

```

Following are the steps for upgrading control plane: <br>

1. Login to control plane <br>
2. Check the existing version <br>
3. unhold kubeadm and Install the latest kubeadm version <br>
4. Decide on the upgrade version by running a kubeadm upgrade plan (Same version patch or new version) <br>
5. Apply Kubeadm upgrade <br>
6. Evict all workloads from control plane except daemonsets<br>
7. Upgrade kubectl and kubelet<br>
8. Make the control plane schedulable (Uncordon)<br>

```
# Check kubeadm version
kubeadm version -o json

# un-hold kubeadm so that we can upgrade
sudo apt-mark unhold kubeadm 
## Output --> Canceled hold on kubeadm

# Check available updates
sudo apt-cache madison kubeadm | tac

# Check the latest version & upgrade to it
sudo apt-get update -y

# Upgrading to kubeadm version 1.29.5-1.1 (can be replaced as per your need)
sudo apt-get install -y kubeadm=1.29.5-1.1

# After the update, hold on to this version (stop automatic updates)
sudo apt-mark hold kubeadm
## Output --> kubeadm set on hold.

# Check which compatible versions we can upgrade to
sudo kubeadm upgrade plan

# Apply kubeadm upgrade plan
sudo kubeadm upgrade apply v1.29.5

# Check & verify kubeadm version
kubeadm version -o json

# We now need to drain the node and then upgrade kubelet & kubectl

# drain control plane
kubectl drain controlplane --ignore-daemonsets

# Upgrade kublet & kubectl
sudo apt-mark unhold kubelet kubectl

sudo apt-get update && sudo apt-get install -y kubelet=1.29.5-1.1 kubectl=1.29.5-1.1

sudo apt-mark hold kubelet kubectl

# Restart kubelet service
sudo systemctl daemon-reload
sudo systemctl restart kubelet

# Un-cordon control plane
kubectl uncordon controlplane

# Check if kubelet & kubectl have been upgraded to correct versions
kubectl version --client
kubelet --version

kubectl get Nodes
# Verify if controlplane is on the upraded version

```

Control plane has been upgraded and we can upgrade worker nodes one by one <br>
###IMPORTANT : ssh into worker node: <br>

```
sudo apt-mark unhold kubeadm && \
sudo apt-get update && sudo apt-get install -y kubeadm=1.29.5-1.1 && \
sudo apt-mark hold kubeadm

# perform the Upgrade
sudo kubeadm upgrade node

```
###Get back onto control plane & drain the worker node <br>

```
# Perform this from control plane
sudo kubectl drain node01 --ignore-daemonsets --delete-emptydir-data
```

### IMPORTANT : Perform this from worker node: <br>

```
# Upgrade kubectl and kubelet
sudo apt-mark unhold kubelet kubectl && \
sudo apt-get update && sudo apt-get install -y kubelet=1.29.5-1.1 kubectl=1.29.5-1.1 && \
sudo apt-mark hold kubelet kubectl

# Restart kubelet
sudo systemctl daemon-reload
sudo systemctl restart kubelet

# Check & verify kubelet and kubectl versions
kubectl version --client 
kubelet --version

```

### Uncordon worker node from control plane

```
kubectl uncordon node01
kubectl get nodes
```
