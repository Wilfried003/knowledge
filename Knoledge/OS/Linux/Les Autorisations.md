### Autorisations de fichiers
Il est possible de voir les autorisations d'un fichier avec la commande *ls -l*. 
```
d | rwx | r-x | r-x
```
Il se découpe en 4 parties.
> 1. Le type de fichier (dir (d), file (-), etc).
> 2. Autorisation lié à l'utilisateur qui lance la commande
> 3. Autorisation lié au groupe auquel appartient l'utilisateur
> 4. les autres

Les symboles (r: read, w: write, w: executable, -: vide).

### Modification des autorisations
La commande pour modifier les autorisations sur un fichier est la commande *chmod*. Elle peut être utilisé de différentes manières.
> La première manière est avec les opérateurs - et +
```
chmod u+rw file
```
Ici, avec l'utilisateur (u), on ajoure les droits de lecture (r) et d'écriture (w).
```
chmod ug-rwx file
```
Vous l'aurez compris, ici on retire les autorisations sur l'utilisateur et le groupe.

> La deuxième manière est d'utiliser des chiffres

Le principe est de convertir le binaire en décimal.
on a l'ordre *r w x*  la permission sur *r* correspond à *1 0 0* (4), sur *w* *1 0* (2) et sur *x 1* (1) et on addition les décimaux. Donc pour avoir tout les autorisations on a *7*.
```
chmod 574 file
```
5 = 4 +1 (pour l'user)
7 = 4 + 2 + 1 (pour le group)
4 = 4 (pour les autres)

### Changer le propriétaire d'un répertoire ou d'un fichier
La commande utilisée pour changer de propriétaire est la commande *chown* comme *change owner*.
```
sudo chown username filename
sudo chown user:group filename
sudo chown -R user file
```
La commande *-R* permet de change de manière récursive le propriétaire d'un fichier ou un répertoire et tout ce qu'il contient.  
La commande doit être exécuté en *sudo*.

Comment selon vous changez le groupe propriétaire d'un fichier
```
sudo chgrp root file 
```


