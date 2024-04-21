Le shell est un environnement ou l'on peut exécuter des lignes de commande. Son aspect peut varier d'une distribution à une autre mais se présente généralement ainsi :

> nom_utilisateur@nom_machine:repertoire_courant
> $ 

### Commande echo
```echo
echo elle sert à afficher du texte dans la console
```

### Commande Date 
```date
date
```
elle permet de retourner la date du jour.

### Commande whoami
```
whoami
```
Cette commande donne le nom de l'utilisateur courant à ne pas confondre avec le hostname.

### Commande hostname
```
hostname
```
Donne le nom de la machine.

### Commande Print Working Directory
```
pwd
```

### Commande Change Directory
```
cd /  pour aller au repertoire root
cd    pour se depllacer à partir du repertoire courant
cd .. pour se deplacer à partir du repertoire parrent
cd -  pour se rendre dans le repertoire precedemment visité
cd ~  pour ce rendre dans son repertoire home à lui (ex: home/kali)
```

### Commande List Directory
```
ls    liste le contenu du directory
ls -R le contenu mais de manière recurcive (cad le contenu de chaque dir enventuel)
ls -l le contenu mais sous un format 'long' 
ls -a tout le contenu 'all' (même les fichiers ou dir cachés)
ls -t affiche dans l'ordre du temps
ls -r reverse l'ordre normal de sortir (le premier devient le dernier)
```

### Commande pour créer un fichier vide
```
touch chemin/de/emplacement/nom_du_fichier
```

### Commande pour le type de fichier
```
file monfichier
```

### Commande lecture de petit fichier
```
cat monfichier
cat monfichier1 monfichier2 ouverture de multi-fichier
```

### Commande lecture de grand fichier
```
less chemin/monfichier
more chemin/monfichier
```
Il permet de lire un fichier page par page. Il comporte également des options comme:
> /passage qu'on recherche dans le texte
> q pour quitter

### Commande History
```
history
```
Cette commande fait ressortir toute les commandes executées en ligne de commande.

Toujours dans le même contexte, il est possible de rechercher un comme passer grâce au raccourci 
```
ctr + R
```

Il est possible de rejouer la dernière commande grâce à :
```
!!
```

### La commande clear
```
clear
```

### La commande copy
```
cp chemin/fichier dest/chemmin/
cp -r dir dest/dir copie de maniere recurcive pour le contenu de dir
cp *.jep dest      copie tout le contenu se terminant par .jep
cp -i              pour avoir la main si besoin d'ecraser ou non un fichiery est
```

### La commande move
```
mv fichier1 fichier2 pour renommer fichier1 en fichier
mv fichier1 chemin   pour deplacer le fichier1 dans le dir chemin
mv -i                pour pouvoir avoir une interraction comme dans cp
```

### La commande Make Directory
```
mkdir nomdir
mkdir -p creer/chemin/jusqua/mondossier (-p comme parent)
```

### La commande ReMove
```
rm fichier
rmdir mondirectory
rm -r               pour supprimer de manière recurcive tout les fichier de la dir
rm -f               forcer la suppression d'un fichier
rm -i               pour demander une confimation (interaction)
```

### La commande find
```
find -name nomdufichier
find home/kali -name *.jeg 
find -type d -name nomdufichier (d comme directory)
```

### La commande help
```
help echo    
echo --help  pour certaine commande
```

### La commande Manual
```
man ls
```

### La commande Whatis
```
whatis ls
```
petite description de la commande.

### La commande alias
```
alias nomalias='commande de alias'
alias lrt='ls -lrt'
unalias lrt
```

Les alias ne sont pas persistant, ils sont supprimés au redémarrage du système.
Pour persister cela, il faut les ajouter dans le fichier
```
~/.bashrc
```

### La commande exit
```
exit
logout
```
Pour sortir de la console