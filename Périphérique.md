Une chose à retenir sous linux est que tout est fichier (application, périphérique, etc), tout est fichier.
La gestion des différents périphérique sous linux (disque dur, Ram, souris, sortie audio, etc) se fait à travers des fichiers dans */dev*
En ce qui concerne les fichiers dédiés au périphérique, il en existe plusieurs types.

### Type de périphériques
Les fichiers contenus dans */dev* sont des fichiers de périphérique. On peut observer par exemple:
```
$ ls -l /dev
  
brw-rw----   1 root disk      8,   0 Dec 20 20:13 sda
  
crw-rw-rw-   1 root root      1,   3 Dec 20 20:13 null
  
srw-rw-rw-   1 root root           0 Dec 20 20:13 log
  
prw-r--r--   1 root root           0 Dec 20 20:13 fdata
```
> 1. L'autorisation
> 2. Le propriétaire
> 3. Le groupe propriétaire
> 4. Numéro de l'appareil principal
> 5. Numéro de l'appareil mineur
> 6. Horadatage
> 7. Nom de l'appareil

On voit également sur le premier digit les différents type de fichier qu'il existe:
- b : block
- c : character
- s : socket
- p : pipe

#### Dispositif de character
Les périphériques utilisant les fichiers de type *character* sont des devices transmettant les informations caractère pas caractère.
Un exemple de device est par exemple le */dev/null*.

#### Dispositif de block
Ces périphérique transmettent des données par de grands blocks de taille fixe. (ex: disque dur, des systèmes de fichiers, etc).

#### Dispositif pipe
Ce sont des fichiers permettant à deux ou plusieurs processus de communiquer entre eux. La grande différence avec les fichiers *c* c'est que leur sortie est redirigé vers un autre processus et non un device.

#### Dispositif socket
Ils sont comme les *pipes*, ils permettent la communications entre plusieurs processus.

### Nom des appareils
> /dev/sdb : Deuxième disque SCSI
> /dev/sda2 : Deuxième partition du Premier disque SCSI
> /dev/hdd2 : Deuxième partition  du 4èm disque
> 	/dev/null : N'est pas un disque physique 
> /dev/zero