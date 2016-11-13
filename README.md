# kube-demos

dnf install -y git-core pv dnf kubernetes etcd

systemctl enable --now etcd kube-apiserver kube-controller-manager kube-scheduler kubelet docker kube-proxy

open /etc/kubernetes/apiserver and remove "ServiceAccount" from the list of admission controllers

vi /etc/kubernetes/apiserver

systemctl restart kube-apiserver

kubectl get pod -w

kubectl exec -it demo bash

 



Create a node1
192.168.122.155 master
192.168.122.57 node1

#### on node1

sudo dnf install -y kubernetes-node flannel


#### on master

cd /etc/kubernetes
ls
vi apiserver
change
KUBE_API_ADDRESS="--insecure-bind-address=127.0.0.1"
KUBE_API_ADDRESS="--insecure-bind-address=0.0.0.0"


cd /etc/etcd
vi etcd.conf
change
ETCD_LISTEN_CLIENT_URLS="http://localhost:2379"
to
ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"

and

ETCD_ADVERTISE_CLIENT_URLS="http://localhost:2379"
to
ETCD_ADVERTISE_CLIENT_URLS="http://master:2379"
You can also use ipaddress of this master instead of the name "master"


systemctl restart kube-apiserver etcd

sudo dnf install -y flannel
