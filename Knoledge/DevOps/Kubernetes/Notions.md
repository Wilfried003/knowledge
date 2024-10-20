- Nouds : serveurs physiques ou virtuels (master or worker)
- Pods : instance de k8s (avec un ou plusieurs conteneurs)
- Service : couple (ip, port) pour communiquer avec des pods et des conteneurs
- Volume : Persistents ou non (lieu d'echange entre les pods)
- Deploiement : Creation et suppresion de pods, scaling
- Le namesspaces : cluster virtuel au sein de k8s pour gestion de droit.


# Minikube
- Cluster sur un noeud



pas de swap
sudo -s vs su


apt-get update && apt-get install -y apt-transport-https curl

curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | apt-key add -

sudo add-apt-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main" 

apt-get update

sudo apt-get install -y kubelet kubeadm kubectl kubernetes-cni

