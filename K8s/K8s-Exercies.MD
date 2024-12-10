###  Kubernetes Exercises to Try out

Pod: <br>
1. My-Pod : https://github.com/rchidana/Kubernetes/blob/master/Pod/my-pod.yaml <br>
1. Pod with label : https://github.com/rchidana/Kubernetes/blob/master/Example2/mynodeapp-manual-label.yaml <br>
1. Pod with node selector : https://github.com/rchidana/Kubernetes/blob/master/Example2/mynodeapp-manual-node-selector.yaml <br>
1. Pod anti-affinity : https://github.com/rchidana/Kubernetes/tree/master/Example2/affinity <br>
1. Pod with toleration : https://github.com/rchidana/Kubernetes/blob/master/Example2/taints/mynodeapp-with-tolerations.yaml <br>

Probes:<br>
1. Liveness & Readiness Probes : https://kubernetes.io/docs/tasks/configure-pod-container/configure-liveness-readiness-startup-probes/ <br>

Command & Arguments:<br>
1. https://github.com/rchidana/Kubernetes/blob/master/Arguments/commands.yaml <br>
1. https://github.com/rchidana/Kubernetes/blob/master/Arguments/command2.yml <br>

Environment Variables:<br>
1. https://github.com/rchidana/Kubernetes/blob/master/ENV/envvar-demo.yml <br>
1. https://github.com/rchidana/Kubernetes/blob/master/ENV/env-print-demo.yml <br>

ConfigMap: <br>
1. https://github.com/rchidana/Kubernetes/tree/master/ConfigMap <br>

Secrets: <br>
1. https://github.com/rchidana/Kubernetes/tree/master/Secret <br>

Resources:<br>
1. Assign Memory Req + limit : https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/ <br>
1. Assign CPU Req + limit : https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/ <br>
1. Pod QOS :  https://kubernetes.io/docs/tasks/configure-pod-container/quality-service-pod/ <br>

Multi-Container Pod & Volume:<br>
1. https://github.com/rchidana/Kubernetes/tree/master/Volumes <br>

PV & PVC:<br>
1. https://kubernetes.io/docs/tasks/configure-pod-container/configure-persistent-volume-storage/ <br>

Namespace: <br>
1. https://github.com/rchidana/Kubernetes/tree/master/My-Namespace <br>
1. Resource Quotas for namespace : https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/quota-memory-cpu-namespace/ <br>

Service & DNS:<br>
1. https://github.com/rchidana/Kubernetes/tree/master/Service <br>
DNS Look Up command --> kubectl -n demo run tmp-shell --rm -i --tty --image nicolaka/netshoot -- /bin/bash <br>

Controllers & Workload Objects: <br>
1. ReplicaSet : https://github.com/rchidana/Kubernetes/blob/master/ReplicaSet/mynodeapp-rs.yaml <br>
1. Deployment : https://kubernetes.io/docs/concepts/workloads/controllers/deployment/ <br>
1. DaemonSet : https://github.com/rchidana/Kubernetes/tree/master/DaemonSet <br>
1. Job : https://github.com/rchidana/Kubernetes/tree/master/JobResource <br>
1. CronJob : https://github.com/rchidana/Kubernetes/blob/master/JobResource/whalesay_cj.yaml <br>
1. HPA : https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/ <br>


###Others:

InitContainers : https://kubernetes.io/docs/tasks/configure-pod-container/configure-pod-initialization/ <br>
Injecting data into Applications : https://kubernetes.io/docs/tasks/inject-data-application/ <br>
Pod Security Context : https://kubernetes.io/docs/tasks/configure-pod-container/security-context/ <br>
CRDs : https://kubernetes.io/docs/tasks/extend-kubernetes/custom-resources/custom-resource-definitions/ <br>
Network Policy : https://kubernetes.io/docs/concepts/services-networking/network-policies/ <br>
