# kube-demos

dnf install -y git-core pv dnf kubernetes etcd

systemctl enable --now etcd kube-apiserver kube-controller-manager kube-scheduler kubelet docker kube-proxy

open /etc/kubernetes/apiserver and remove "ServiceAccount" from the list of admission controllers

vi /etc/kubernetes/apiserver
