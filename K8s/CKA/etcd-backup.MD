# etcd backup & restore

etcdctl is the command line utility that interacts with etcd for snapshots. <br>

Login to the controlplane & check if etcdctl is present, if not, it has to be installed:

```
# try this from controlplane

etcdctl
# -bash: etcdctl: command not found

sudo apt install etcd-client

etcdctl

```

The following information is required to create a snapshot of etcd:

-etcd endpoint (–endpoints) <br>
-ca certificate (–cacert)<br>
-server certificate (–cert)<br>
-server key (–key)<br>

You can obtain this information either by describing etcd pod that is running or by looking at its manifest that's present here: <br>
/etc/kubernetes/manifests/etcd.yaml <br>

Following is the typical etcd manifest:

- command:
    - etcd
    - --advertise-client-urls=https://10.0.0.10:2379   (endpoint)
    - --cert-file=/etc/kubernetes/pki/etcd/server.crt  (cert-file)
    - --client-cert-auth=true
    - --data-dir=/var/lib/etcd
    - --experimental-initial-corrupt-check=true
    - --experimental-watch-progress-notify-interval=5s
    - --initial-advertise-peer-urls=https://10.0.0.10:2380
    - --initial-cluster=controlplane=https://10.0.0.10:2380
    - --key-file=/etc/kubernetes/pki/etcd/server.key (key-file)
    - --listen-client-urls=https://127.0.0.1:2379,https://10.0.0.10:2379
    - --listen-metrics-urls=http://127.0.0.1:2381
    - --listen-peer-urls=https://10.0.0.10:2380
    - --name=controlplane
    - --peer-cert-file=/etc/kubernetes/pki/etcd/peer.crt
    - --peer-client-cert-auth=true
    - --peer-key-file=/etc/kubernetes/pki/etcd/peer.key
    - --peer-trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt (ca-file)
    - --snapshot-count=10000
    - --trusted-ca-file=/etc/kubernetes/pki/etcd/ca.crt
	
Based on above inputs, the following command needs to be run to create a snapshot:

```
# become root
sudo su

# backup gets saved to /home/vagrant/backup/etcd.db - create the folder if it does not exist
ETCDCTL_API=3 etcdctl \
  --endpoints=https://10.0.0.10:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save /home/vagrant/backup/etcd.db
  
# 2024-06-13 15:55:16.866781 I | clientv3: opened snapshot stream; downloading
# 2024-06-13 15:55:17.225818 I | clientv3: completed snapshot read; closing
# Snapshot saved at /home/vagrant/backup/etcd.db

# Verify the backup
ETCDCTL_API=3 etcdctl --write-out=table snapshot status /home/vagrant/backup/etcd.db

+----------+----------+------------+------------+
|   HASH   | REVISION | TOTAL KEYS | TOTAL SIZE |
+----------+----------+------------+------------+
| f11c855f |     2518 |       1028 |     5.1 MB |
+----------+----------+------------+------------+

```

Restore command:

ETCDCTL_API=3 etcdctl snapshot restore <backup-file-location>

