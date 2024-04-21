### Standard Out (stdout)

Pour rediriger la sortie d'une commande vers une autre tache pour les textes, on peut utiliser:
```
echo Hello World > texte.txt
```
Cette commande écrase le contenu du fichier *texte.txt* et ajoute le contenue à la sortie de *echo*
Pour ajouter sans écraser le contenu d'un fichier, on peut :
```
echo Hello World >> texte.txt
```

### Standard In (stdin)
De la même manière, que la sortir, il est possible d'utiliser une entrée. Par exemple, une commande linux peut prendre en entré un fichier ou quelque chose d'autre pour renvoyer en sortie un résultat.
```
cat < test.text > test1.txt
```
Ici on copie  le contenu du fichier test dans test1 mais on rentrant dans le détail, la commande cat prend comme paramètre un fichier, on redirige alors le fichier test comme entre de cat.
> il était également possible de faire simplement :

```
cat test.text > test1.txt
```
Mais pour l'exemple, nous avons fait autrement.

### Standard error (stderr)
Que se passe t'il lorsqu'on veut stocker une commande qui revoie une erreur? 
Et bien, il n'est pas possible d'utiliser le caractère *>*. Dans ce cas on utilise un autre type de descripteur de fichiers (des chiffres).
En s'harmonisant que le 0 -> stdin, 1 -> stdout et 2 -> stderr, pour retourner une erreur dans un fichier on fait:
```
ls /fake/dir 2> error.txt
```

Il est également possible de rediriger le stdout et le stderr grâce aux commandes.
```
ls /fake/dir 2>&1 stdouterr.txt
ls /fake/dir &> stdouterr.txt
```
Tout deux sont équivalentes.
Il est également possible comme dans le stdout, d'ajouter à la suite du fichier avec *>>*
```
ls /fake/dir 2>>&1 stdouterr.txt
ls /fake/dir &>> stdouterr.txt
```

Dans le cas ou la sortie d'une commande ne nous intéresse pas et l'on ne veut pas l'afficher ni la stocker, on la redirige vers */dev/null*.
```
ls /fake/dir 2>&1 /dev/null
ls /fake/dir &> /dev/null
ls /fake/dir 2> /dev/null
```

### Pipe and tee
J'ai longtemps confondu l'utilité du *|* et *>* , mais l'utilité est différente. Mais si tout deux font référence à *stdout* l'utilité du *>* est pour rediriger la sortie de la commande passée vers un *fichier* qui existe déjà ou qui est crée. Tandis que *|* redirige la sortie de la commande passé vers tout ce qu'on veut (fichier, commande, etc ).
Dans les exemples qui suit on va rediriger une sortie vers la commande *less* et dans le suivant vers un fichier.
```
ls /etc | less
ls /etc | tee text1 text2 ..
```

Si on avait fait:
```
ls /etc > less
```
on aurait crée un fichier *less* sans le prendre comme une commande tandis qu'ici.

La commande *tee* permet de créer un fichier avec le contenu injecté en entré avec la particularité d'afficher dans un premier temps le texte à enregistrer dans le fichier.
```
echo hello word | tee text1 text2
echo add without override | tee text
```

### Environnement 
Il existe des variables d'environnement sous linux consultable via la commande :
```
env
```

Par exemple :
```
$USER 
```
Donne le nom de l'utilisateur: *whoami*

```
$HOME
```
Le répertoire de ton utilisateur comme *cd ~*

Il est également possible de crée ses propres variables d'environnement.
```
NomDeVariable=/root/home/kali/Download
```
```
$NomDeVariable
```

### La commande cut
Ici, nous allons apprendre à travailler sur les textes, en occurrence, les couper.

```
cut -c1 text.txt
cut -c1-2 text.txt
```
Permet de couper un texte en se basant sur les *caractère c*.

```
cut -f1 text.txt
```
Permet de couper des *fields* en se basant sur son délimiteur par défaut *tab*.

Pour spécifier un délimiteur personnel, on utilise l'option -d.
```
cut -d ";" -f1 text.txt
```

Avec *cut*, on compte à partir de 1.

### La commande paste
Cette commande permet coller des caractères d'un fichier en fonction du délimiteur utilisé sachant que celui de base est *tab*.

```
paste -s filename
paste -d ' ' -s filename
```

### La commande head
Celle-ci permet de montrer un certain nombre de ligne d'un fichier (10 de base).
```
head longfile
head -n10 10firstline
head -c12 12firstcaratere 
```

### La commande tail
Vous vous y attendez surement ! Il est bien sur possible de lire les dernière ligne d'un fichier par cette commande.
```
tail -n2 2lastline
tail -c10 10lostcaratere
```

Une option intéressant qu'on a avec cette commande est *-f* qui permet d'interagir directement avec  le fichier en mettant à jour les dernières lignes si le fichier est modifié.
```
tail -f 10updatelastline
```