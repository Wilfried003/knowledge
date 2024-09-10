Outils d'orchestration des conteneurs.

# Créer un cluster
Un cluster est composer de plusieurs noeuds (host).

```
minikube start
```

vous pouvez ouvrir le dashbord pour surveiller graphiquement le système.

```dashboard
kubectl dashboard / kubectl dashboard --url
```

# Créer un déploiement
qd on parle de deploiment en k8s, pense a pod, Un Deployment dans Kubernetes gère un ensemble de Pods et s'assure qu'un certain nombre d'instances d'un Pod soient toujours en cours d'exécution.
pour creer un deployment, on a besoin d'une image (pour le conteneur).


```deployment
kubectl create deployment hello-node --image=registry.k8s.io/e2e-test-images/agnhost:2.39 -- /agnhost netexec --http-port=8080
```

- Les commandes de base
```get
kubectl get deployments
kubectl get pods
kubectl get events
kubectl get services
kubectl config view
kubectl logs podName
```

- S'attacher à un pod ou conteneur
```attach
kubectl exec -ti podname /bin/bash
kubectl exec -it my-pod -c my-container -- /bin/sh
```

Ensuite pour accéder à l'application après avoir créé le déploiement, vous devez exposer le Pod via un Service Kubernetes. Un Service vous permet de rendre les Pods accessibles à d'autres Pods dans le cluster, ou même à des clients externes, comme votre machine locale.

# Exposer un deployment

```expose
kubectl expose deployment hello-node --type=LoadBalancer --port=8080
```

- --type=LoadBalancer indique qu'on veut exposer le service hors du cluster.



## Creer un cluster

- Le noeud maitre coordonne le cluster (planifications des applications, gestion de l'etat des applications, la mise a l'echelle des applications, le deploiements de nouvelles mises à jours)
- les noeuds worker sont les serveurs qui exécutent des applications


Chaque noeud est doté d'un Kubelet qui est un agent qui permet de gérer le noeud et communiquer avec l'e maitre.
Le noeud est egalement doter de gestionnaire de conteneur comme docker.

Les noeuds communiquent aves le maitere a l'aide de l'API kubernetes que le maitre expose. Les utilisateurs finaux utilisent egalement l'api kubernets

Lorsque vous créez un déploiement, vous devez spécifier l’image conteneur de votre application et le nombre de réplicas que vous souhaitez exécuter.

Formatd'un commande k8s
```
kubectl action ressource
action = create, describe or delete, logs, exec
ressource = 
```
Utiliser l'option --help apres une sous commance pour voir les option possible

Kubernetes choisira ou deployer les applications (pod) en fonction des nodes disponible

[Les pods](https://kubernetes.io/docs/concepts/workloads/pods/) qui s’exécutent dans Kubernetes s’exécutent sur un réseau privé et isolé. Par défaut, ils sont visibles à partir d’autres pods et services au sein du même cluster Kubernetes, mais pas en dehors de ce réseau.

Les conteneurs d'un meme pod partagent les ressources tq:
- Stockage partagé, en tant que volumes
- Mise en réseau, en tant qu’adresse IP de cluster unique
- Informations sur l’exécution de chaque conteneur, telles que la version de l’image du conteneur ou les ports spécifiques à utiliser

un node execute au moins :
- kubelet
- runtime de conteneur
```
kubectl describe pod podName
```


# Les services
Bien que chaque espace ait une adresse IP unique, ces adresses IP ne sont pas exposées en dehors du cluster sans service. Les services permettent à vos applications de recevoir du trafic. Les services peuvent être exposés de différentes manières en spécifiant a dans la spécification du service :`type`

- _ClusterIP_ (par défaut) : expose le service sur une adresse IP interne dans le cluster. Ce type rend le service accessible uniquement à partir du cluster.
- _NodePort_ : expose le service sur le même port que chaque nœud sélectionné dans le cluster à l’aide de NAT. Rend un service accessible depuis l’extérieur du cluster à l’aide de . Sur-ensemble de ClusterIP.`<NodeIP>:<NodePort>`
- _LoadBalancer_ : crée un équilibreur de charge externe dans le cloud actuel (s’il est pris en charge) et attribue une adresse IP externe fixe au service. Sur-ensemble de NodePort.
- _ExternalName_ - Associe le service au contenu du champ (par exemple, ), en renvoyant un enregistrement avec sa valeur. Aucun proxy d’aucune sorte n’est mis en place. Ce type nécessite la version 1.7 ou ultérieure de ou la version 0.0.8 ou ultérieure de CoreDNS.`externalName``foo.bar.example.com``CNAME``kube-dns`

```
kubectl expose deployment deploymentname --type=NodePort --port 8080
```

```
kubectl describe services kubernetes-bootcamp
```

Pour voir la page dans un navigateur web, la commande describle donne le port sur lequel k8s xpose et on utilise minikube ip (puis que c'st minikube qui creer le cluster) pour avoir l'ip qu'on doit interroger

# Les labels 
Les **labels** (étiquettes) dans Kubernetes sont des paires clé-valeur qui sont attachées aux objets tels que les pods, services, nœuds, etc. Ils sont utilisés pour organiser et sélectionner des sous-ensembles d'objets.

```label
kubectl label pods "$POD_NAME" version=v1
kubectl get pods -l version=v1
```

```delteSevice
kubectl delete service -l app=kubernetes-bootcamp
```


# Mise à l'echelle d'une application

il est possible de creer des replique d'instance  des le deploiement avec *--replicate=x* 

Le replicat permetra d'avoir une haute disponibilité de l'aplication en interrogeant le noeuds disponible.
il permet egalement de faire des moter de version ou une mise a jour sans interompre le service.

```
kubectl get deployments
```
- READY_ affiche le rapport entre les répliques CURRENT/DESIRE
- AVAILABLE_ affiche le nombre de répliques de l’application disponibles pour vos utilisateurs.
```
kubectl get rs
```

```replicas
kubectl scale deployment namedeployment --replicas=4
```
*PS C:\Users\ASUS TUF GAMING> kubectl get rs
NAME                             DESIRED   CURRENT   READY   AGE
hello-node-55fdcd95bf            1         1         1       19h
kubernetes-bootcamp-644c5687f4   4         4         1       11h
PS C:\Users\ASUS TUF GAMING> kubectl get rs
NAME                             DESIRED   CURRENT   READY   AGE
hello-node-55fdcd95bf            1         1         1       19h
kubernetes-bootcamp-644c5687f4   4         4         4       11h*

```
kubectl get pods -o wide
```
Cette commmade montre les pods en cours d'utilisations

ce u'on fait lorsqu'on reduit les pods, c'est qu'il se mettent en status terminer mais sont pas supprime.
Lorsqu'on veut hauser les nombre de pods encore, ils sont lance.

# Mise ajour d'une application 

Les mises à jour propagées permettent les actions suivantes :

- Promouvoir une application d’un environnement à un autre (via des mises à jour d’images de conteneurs)
- Retour aux versions précédentes
- Intégration continue et livraison continue des applications sans temps d’arrêt

```maj
kubectl set image deployment kubernetes-bootcamp kubernetes-bootcamp=docker.io/jocatalin/kubernetes-bootcamp:v2
```

# Verification d'une maj
```
kubectl rollout status deployments/kubernetes-bootcamp
```

# Annuler une maj
```undo
kubectl rollout undo deployments/kubernetes-bootcamp
```