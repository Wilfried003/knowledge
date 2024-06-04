---
tags:
  - Challenge
  - Web
  - OsCommandInjection
---
# Description

We've built the most secure networking tool in the market, come and check it out!
# Write Up

#### Adresse : 83.136.253.251:59760

![[Pasted image 20240415220545.png]]

Une fois sur le site et après avoir analysé l'interface, on se rend compte que l'application exécute le ping de l'adresse ip qu'on renseigne.
 > Et si on essayait de lancer une commande à la suite de l'adresse ip ?
 
![[Pasted image 20240415221230.png]]

Le flag est : 
```flag
HTB{I_f1n4lly_l00k3d_thr0ugh_th3_rc3}
```
