### Généralité
Le système d'exploitation peut être diviser en 3 partie.
Tout d'abord, nous avons la partie matérielle composée du disque, le processeur, la RAM, les ports réseaux, etc
La seconde partie est le noyau, le cœur du système d'exploitation. Il a pour du de gérer les différents processus et la mémoire, faire le pont entre la troisième partie et le matériel.
Et enfin, nous avons la dernière partie, la partie des utilisateurs avec le shell, le GUI et autres applications.

### Niveaux de privilèges
Sous linux, il existe 4 niveaux de privilège (architecture x86). Ces niveaux de privilèges accordent plus d'autorisation du *ring 0* vers le *ring 3*.
- Le Ring 0
C'est le niveau de privilège du noyau, il est le plus élevé. Il permet de lancer directement des appels système et gérer complètement le matériel (mémoire, carte réseau, webcam), C'est Dieu !!

- Le Ring 1 et 2
Ce sont deux niveaux de privilège qui ne sont pas utilisé.

- Le Ring 3
C'est le niveau de privilège des utilisateurs. il ne sont pas prioritaire et occupe un petite partie de la plage libre. Il est également sujet à beaucoup de contrôle lors de sont utilisation.
*Il est important de savoir qu'e l'utilisateur root s'exécute en mode noyau (ring 0) et revient en mode utilisateur (ring 3)*

Pour cela, on distingue généralement deux modes, le mode utilisateur et le mode noyau

### Appel système
Tout à l'heure on avait parlé de comment l'utilisateur *root* exécutait une tache, nous allons rentrer plus en détail grâce au *appels systèmes.*
Un appel système est comme une interface que le système met à disposition au utilisateurs pour pouvoir demander au noyau d'effectuer une action. Il est toujours lancer en *mode noyau*
Lorsqu'un utilisateur lance une tache, il lance la tache avec ses *uid, gid et le pid* du processus. une fois le processus crée un appel système vers le noyau peut être sollicité. Le noyau a son tour détermine si l'utilisateur peut lancer ce processus et le lance si oui. 
Il est possible de voir le processus de l'appel système d'une commande par *strace*.
```
strace ls
```

#### Types d'appels systèmes
> Gestion de fichiers (read, close, write, open).
> Gestion des processus (exec, fork, wait)
> Gestion des ressources (malloc, brk)
> Gestion des permissions (chmod, chown, chgrp)
> Gestion d'interprocessus (pipe, msgget)
> Gestion du temps (time, sleep)
> Gestion du reseau (socket, bind connect)


### Installation d'un noyau
Il est possible d'installer plusieurs noyau sur un même OS et de choisir sur lequel on veut lancer notre OS au démarrage grâce au chargeur d'amorçage (ex :GRUB).
La commande pour télécharger un noyau est la suivante:
```
sudo apt install dist-upgrade nom_du_noyau
```

La commande pour avoir des informations su l'os est :
```
uname
```

Celle pour avoir des informations sur la version du noyau est:
```
uname -r
```

 Lorsque vous ajoutez un nouveau noyau à votre OS, les fichiers de ces OS sont présents dans le répertoire */boot*
### Modules du noyau
Il est possible d'ajouter, supprimer de nouveau module à un noyau. Par exemple, ajoutons un noyau de Bluetooth à notre noyau. La commande à exécuter est:
```
sudo modprobe bluetooth
```

Pour supprimer, on a:
```
sudo modprobe -r bluetooth
```

et pour lister, on fait
```
lsmod
```
