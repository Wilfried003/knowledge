---
tags:
  - Challenge
  - CodeSource
  - Docker
  - Web
  - PathTraversal
---
# Description

In order to decipher the alien communication that held the key to their location, she needed access to a decoder with advanced capabilities - a decoder that only The Orbital firm possessed. Can you get your hands on the decoder?

# Write up

#### Adresse : 94.237.62.195:47476

![[Pasted image 20240416001046.png]]

Une technique qu'on pourrait utiliser serait de chercher les *user/pwd* les plus utilisés sur internet et grâce à *burpsuite* faire un brute force.
Mais, il y a plus simple ici, *lire le code source.* 

![[Pasted image 20240416001436.png]]

on se connecte ici par *(admin/ichlliebedich)*.

Une fois connecté, on regarde tout ce qu'il est possible de faire sur la page. Ici, seul le téléchargement *mp3* est possible.
> Attention : Quelquefois sur burp, une action est possible sans faire apparaitre la requête. il faut juste retenir que pour toute action qui se fait une ou des requête(s) est/sont envoyé(e)s. Si rien ne s'affiche, activer "intercept is on".

Une fois avoir vu quelle requête est envoyée pour télécharger le *mp3*, on peut essayer n'importe quelle attaque sur le *json*.

> Et si on essayait une attaque [[Path Traversal | path traversal]] (voir le guide perso ou sur [[https://portswigger.net/web-security/file-path-traversal | port swigger]] )

![[Pasted image 20240416002511.png]]

Le flag est 
```flag
HTB{s3qu3l_4nd_lf1s_4r3_fun!!}
```

