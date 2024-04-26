Le partage de réseau est un concept permettant au plusieurs hôtes su même réseau de partager des ressources communes (fichier, répertoire).
Il existe plusieurs protocole(ftp, smb, NFS, ...) et logiciel(smbcllient, scp, rsync, ..) permettant de le faire en fonction des différents OS auxquels appartiennent les hôtes. 
Un moyen simple de copier et télécharger un fichier et des répertoires sont les commandes:
```
scp filetosent username@remoteadresse://remote/dir
scp username@remotehost://filetoget /dir 
scp -r myDir username@remotehost://remote/dir
```

Ou le commande *rsync* qui est similaire *scp* avec des améliorations comme par exemple regarder l'existant du fichier à copier dans le répertoire cible:
```
rsync-zrv filetosent username@remoteadresse://remote/dir
rsync username@remotehost://filetoget /dir 
```
		- v : details
		- r : copie recursive dans le dir
		- z : compresse avan de transférer. Idéale pour les faibles connections
		
### SMB
*Smb Server Message Block*  est un protocole permettant le partage de fichier, répertoire entre un hôte linux et windows.
Un application utilisant ce protocole sous linux est samba. 
Après avoir installer *smb*, il est nécessaire d'indiquer le répertoire de partage avec les autres hôtes dans le fichier *smb.conf*.
```
sudo apt update
sudo apt install samba
vi /etc/samba/smb.conf
```

- Configurer un mot de passe.
```
sudo smbpasswd -a [username]
```

- Relancer le service.
```
sudo service smbd restart 
```

- Comment accéder aux fichiers partagés à partir de windows
Il suffit de consulter le répertoire *\\HOST\sharepointName*

- Comment accéder aux fichiers partagés à partir de linux
```
	smbclient //HOST/sharename -U [username]
```


### NFS
*Nfs Network File System*  est le protocole standard sous linux pour partager des fichiers entre hôtes linux.
Pour configurer un client *nfs*, on fait:
```
sudo service nfsclient start
sudo mount server:/dir /mount_fir
```


### Créer un server avec Simple HTTP Server
Pour le faire il suffit de jouer la commande suivant dans le répertoire souhaité:
```
python -m SimpleHTTPServer
```

Il sera accessible via un navigateur avec l'url:
```
http://IP_ADDRESS:8000
``` 