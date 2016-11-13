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

on node1

sudo dnf install -y kubernetes-node flannel


on master

cd /etc/kubernetes
ls
vi apiserver
change KUBE API ADDRESS to 0.0.0.0

cd /etc/etcd
vi etcd.conf

change listen lclient uril to 0.0.0.0

advertise client url to ipaddress of this node or by the name "master"
