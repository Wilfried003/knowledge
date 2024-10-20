
### Installation de VirtualBox
*Voir le site officiel*

### Installation d'une image kali pour VirtualBox
Il est possible de télécharger directement une image précompiler pour VirtualBox ou VMWare afin d'éviter l'installation de zéro de l'OS. 

#### Configuration de kali

-  *Choisir le mode brigde ou accès par pond* (les mode d'acces)

![[Pasted image 20240911152210.png]]

- *Monter un dossier partager entre mon hôte et ma VM.*


#### Configuration du clavier en FR

```
sudo dpkg-reconfigure locales
```

- *menu > settings > keyboard > disposition > ajouter > French.*

### Installation de metasploitable 2

Metaploitable est une machine virtuelle open source volontairement vulnérable. 
link : https://sourceforge.net/projects/metasploitable/

Après téléchargement, on dézippe et on crée une machine virtuel sans spécifier l'image ISO.
Par contre on monte notre metasploit comme virtual Hard disk
![[Pasted image 20240911160922.png]]
le user / pwd est :  msfadmin/msfadmin

#### Configuration du clavier en FR:  
```fr
	sudo loadkeys fr
```

### Installation de Windows 10
link : https://developer.microsoft.com/en-us/microsoft-edge/tools/vms
Construite son image iso windows 10, et le lancer.
Il peut arriver qu'une erreur concernant un *ProductKey* se produise. Il faut juste désactiver la disquette (floppy) dans l'ordre d'amorçage du système, supprimer l'image qui se créait et relancer l'installation. 

#### Installation de Xamp
il est judicieux de prendre une version de *xamp* compatible avec la version de *php* utilisée pour faire l'application à utiliser. Ici j'utilise la version *7.2.2 de xamp*.

#### Télécharger mutillidae2 
Après aavoir télécharger *mutillidae 2*, il faut le placer dans le dossier *xamp/htdocs*.
L'application sera disponible via l'url *127.0.0.1/mutillidae*
il est possible qu'une erreur se produise lors du reset de la base de donnée
1. Ajouter le bin msql au path du system
2. jouer : "mysql -u root -p -h 127.0.0.1 -P 3306" sans pwd pour se connecter à la bdd
3. Et faire des recherches, tu peux le faire !



# Enregistrer une sauvegarde de l'etat de la machine

- VirtualBox > machine > outils > Instantanés > prendre.

kali : 192.168.1.58
metasploit : 192.168.1.113
windows : 192.168.1.63