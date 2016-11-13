# kube-demos

    dnf install -y git-core pv dnf kubernetes etcd

    systemctl enable --now etcd kube-apiserver kube-controller-manager kube-scheduler kubelet docker kube-proxy

open /etc/kubernetes/apiserver and remove "ServiceAccount" from the list of admission controllers

    vi /etc/kubernetes/apiserver

    systemctl restart kube-apiserver

    kubectl get pod -w

    kubectl exec -it demo bash

Create a node1

    192.168.122.164 master.example.local
    192.168.122.157 node1.example.local

#### on node1

    sudo dnf install -y kubernetes-node flannel


#### on master

    vi /etc/kubernetes/apiserver

change

    KUBE_API_ADDRESS="--insecure-bind-address=127.0.0.1"
    KUBE_API_ADDRESS="--insecure-bind-address=0.0.0.0"

    vi /etc/etcd/etcd.conf

change

    ETCD_LISTEN_CLIENT_URLS="http://localhost:2379"
    to
    ETCD_LISTEN_CLIENT_URLS="http://0.0.0.0:2379"

and

    ETCD_ADVERTISE_CLIENT_URLS="http://localhost:2379"
    to
    ETCD_ADVERTISE_CLIENT_URLS="http://master.example.local:2379"

You can also use ipaddress of this master instead of the name "master.example.local"


    systemctl restart kube-apiserver etcd

    sudo dnf install -y flannel


    vi /etc/sysconfig/flanneld

on master etcd is localhost
on node etcd is on master



#### create flannel

    vi flanneld-conf.json

    {
      "Network": "172.16.0.0/12",
      "SubnetLen: 24,
      "Backend": {
        "Type": "vxlan"
      }
    }


    curl -L http://localhost:2379/v2/keys/atomic.io/network/config -XPUT --data-urlencode value@flanneld-conf.json

    curl -L http://master.example.local:2379/v2/keys/atomic.io/network/config -XPUT --data-urlencode value@flanneld-conf.json


    etcdctl get /atomic.io/network/config


    start flannel on master

    systemctl start flanneld

    systemctl status flanneld.service
