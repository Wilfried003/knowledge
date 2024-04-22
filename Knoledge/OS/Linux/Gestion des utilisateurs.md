### Utilisateurs et groupes
Sous linux, chaque utilisateurs a sont répertoire dans */root/home/username* et est identifié par est *uid*. 
Les autorisations sous linux sont gérés à partir des groupes et chaque groupe est identifié par un *gid*
Il existe plusieurs utilisateurs sous linux (pas seulement des personnes physique), ils sont crées par le système pour lancer des processus pour le bon fonctionnement du système (voir les utilisateurs dans /etc/passwd).
Il existe un super utilisateur appelé *root*. 

### La commande su
```
su kali
```
Cette commande permet de changer d'utilisateur.

### Le fichier /etc/passwd
Ce fichier répertorie la liste des utilisateurs ainsi que certains informations sur eux, à savoir:
```
root:x:0:0:root:/root:/bin/bash
```
> 1. Le nom 
> 2. Le mot de passe (x = caché,  = sans mot de passe, * = ne peut se connecté)
> 3. Le uid
> 4. Le gid
> 5. Description sur l'user
> 6. Le répertoire personnel de l'utilisateur
> 7. Le shell de l'utilisateur

Il est possible d'ajouter un utilisateur ici avec la commande *vipw* mais il est préférable d'utiliser les commande *useradd* et *userdel*
Le fichier n'a pas besoin de permission *root* pour être lancé comme le prochain.

### Le fichier /etc/shadow
Ce fichier présente les informations de connexion ou d'authentification d'un utilisateur.
Sa structure est la suivante:
```
root:MyEPTEa$6Nonsense:15000:0:99999:7:::
```
> 1. Le nom de l'utilisateur
> 2. Le mot de passe crypté
> 3. Date du dernier changement du mot de passe
> 4. Âge minimum du mot de passe
> 5. Âge maximum de mot de passe
> 6. Période d'avertissement du mot de passe
> 7. Période d'inactivité du mot de passe
> 8. Date d'expiration du compte
> 9. Champ réservé pour une utilisation ultérieur 

### Le fichier /etc/group
Ce fichier présente les informations sur un groupe.
```
root:*:0:pete
```
> 1. Le nom du group
> 2. Le mot de passe du groupe
> 3. Le gid
> 4. Les membres du groupe (pete, paul, ...)

### Outils de gestions des utilisateurs
Il existe plusieurs moyens de créer, modifier et supprimer un utilisateurs dont celle-ci:
```
sudo useradd username
sudo passwd username
sudo userdel username
```
il est également possible de créer un user en l'ajoutant à un groupe dès sa création.
```
sudo useradd -G nom_du_groupe nom_utilisateur
```
ou de l'ajouter après
```
sudo usermod -aG nom_du_groupe nom_utilisateur
```

Un autre fichier tout aussi important que les autres dont je voulais parler est le */etc/sudoers*
Ce fichier répertorie l'ensemble des permissions qu'un utilisateur ou un groupe peut avoir ou non.
Il est à modifier de préférence avec *visudo*.
```
# User privilege specification
root    ALL=(ALL:ALL) ALL
```
Ici on donne à l'utilisateur *root* de pouvoir sur toute les machines (car les fichiers sudoers peuvent être déployés sur plusieurs machine d'un système) exécuté en tant que n'importe quel utilisateur toute les commandes.

```
# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) ALL
```
De même on peut faire des règles que des groupes ( ici le groupe sudo).

Il est également possible de faire des *alias de users et de commande*
