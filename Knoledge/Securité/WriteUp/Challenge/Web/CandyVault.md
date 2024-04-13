---
tags:
  - Challenge
  - CodeSource
  - Docker
  - Web
  - NoSQLI
---
# Description

The malevolent spirits have concealed all the Halloween treats within their secret vault, and it's imperative that you decipher its enigmatic seal to reclaim the candy before the spooky night arrives.

# Write Up

#### Adresse : 83.136.255.150:41222

![[Pasted image 20240413232404.png]]

Une fois sur le site, on observe cette interface. On essaie une combinaison qui pourrai idéalement marchée mais sans succès *login failed*.

On essaie alors de voir à quoi correspond la requête qu'on envoie grâce à *burpsuite* et aussi jeter un coup d'œil sur le code mis à notre disposition (pourquoi s'en privé ?).

On voit dans le code que le site utilise une bdd *mongodb* qui est une base de données NoSQL.
> Pourquoi ne pas essayé une attaque [[NoSQL injection | NoSQLI]] ?

Sur *burpsuite*, on ca comme requête de login:
![[Pasted image 20240413235456.png]]

On peut essayer de faire une injection avec :

et on a :
![[Pasted image 20240414000150.png]]

Le flag est : 
```flag
HTB{s4y_h1_t0_th3_c4andy_v4u1t!}
```