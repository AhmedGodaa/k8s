# Installation

## Download K8s

1. Download **Api-Server**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kube-apiserver"
chmod +x kube-apiserver
```

2. Download **Controller-Manager**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kube-controller-manager"
chmod +x kube-controller-manager
```

3. Download **Scheduler**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kube-scheduler"
chmod +x kube-scheduler
```

4. Download **Kube-Proxy**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kube-proxy"
chmod +x kube-proxy
```

5. Download **Kubelet**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kubelet"
chmod +x kubelet
```

6. Download **Kubectl**

```shell
curl -LO "https://dl.k8s.io/v1.27.4/bin/linux/amd64/kubectl"
chmod +x kubectl
```

7. Download **etcd**

```shell
curl -LO "https://github.com/etcd-io/etcd/releases/download/v3.5.9/etcd-v3.5.9-linux-amd64.tar.gz"
tar -xvf etcd-v3.5.9-linux-arm64.tar.gz
rm -r etcd-v3.5.9-linux-arm64.tar.gz
```

* **After download all files should be executable**

![image](https://github.com/AhmedGodaa/k8s/assets/73083104/88867d6d-16e8-460d-82a2-09e15aef3dc5)

## Running K8s

### Running etcd

1.Run  **etcd**

```shell
cd etcd-v3.5.9-linux-amd64
./etcd
```

2. Validate **etcd**

```shell
./etcdctl member list -w table
```

- **Output** - etcd running local on port 2379

```text
+------------------+---------+---------+-----------------------+-----------------------+------------+
|        ID        | STATUS  |  NAME   |      PEER ADDRS       |     CLIENT ADDRS      | IS LEARNER |
+------------------+---------+---------+-----------------------+-----------------------+------------+
| 8e9e05c52164694d | started | default | http://localhost:2380 | http://localhost:2379 |      false |
+------------------+---------+---------+-----------------------+-----------------------+------------+
```

3. check tables headlth

```shell
./etcd-v3.5.9-linux-amd64/etcdctl endpoint status -w table
```

- **output**

```text
+----------------+------------------+---------+---------+-----------+------------+-----------+------------+--------------------+--------+
|    ENDPOINT    |        ID        | VERSION | DB SIZE | IS LEADER | IS LEARNER | RAFT TERM | RAFT INDEX | RAFT APPLIED INDEX | ERRORS |
+----------------+------------------+---------+---------+-----------+------------+-----------+------------+--------------------+--------+
| 127.0.0.1:2379 | 8e9e05c52164694d |   3.5.9 |   20 kB |      true |      false |         2 |          4 |                  4 |        |
+----------------+------------------+---------+---------+-----------+------------+-----------+------------+--------------------+--------+
```

### Running api-server

1. Run kube-apiserver

```shell
./kube-apiserver --etcd-servers=http://localhost:2379
```

2. validate stored values after running apiserver

```shell
./etcd-v3.5.9-linux-amd64/etcdctl get / --prefix --keys-only
```

3. get stored namespaces

```shell
./etcd-v3.5.9-linux-amd64/etcdctl get / --prefix --keys-only | grep namespaces
```

4. get stored deployments

```shell
./etcd-v3.5.9-linux-amd64/etcdctl get / --prefix --keys-only | grep deployments
```


