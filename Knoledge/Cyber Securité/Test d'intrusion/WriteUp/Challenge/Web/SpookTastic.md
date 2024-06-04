---
tags:
  - Challenge
  - Docker
  - CodeSource
  - XSS
---

# Description
On a moonless night, you delve into the dark web to uncover the hacker group "The Cryptic Shadows." You find an encrypted message guiding you to a web challenge. They claim a cursed amulet, the 'Amulet of Samhain,' can unveil their treasures location

# Write Up 
#### Adresse : 83.136.254.223:31107

![[Pasted image 20240412115602.png]]

Une fois sur la page, on essaie d'interagir avec celui-ci. La seule partie on l'on peut interagir est l'input *Enter your email*. 
Quel genre d'attaque on peut tenter ici ? un SSTI ? un XSS ? ...
> L'option SSTI n'a pas l'air de fonctionner.
> Qu'est ce qu'il en ait du XSS ?

Liens utiles : [[https://book.hacktricks.xyz/pentesting-web/xss-cross-site-scripting | Hacktricks]], [[https://portswigger.net/web-security/cross-site-scripting | portswigger]] ou ma petite doc perso.

En essayant certains payload, on arrive sur celui ci

```copier
<img src=1 onerror=alert(1)>
```

et on a :

![[Pasted image 20240413030152.png]]

Le flag est :
```flag
HTB{al3rt5_c4n_4nd_w1l1_c4us3_jumpsc4r35!!}
```


