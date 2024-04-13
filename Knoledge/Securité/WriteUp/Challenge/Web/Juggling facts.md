---
tags:
  - Challenge
  - Docker
  - CodeSource
---

# Description

An organization seems to possess knowledge of the true nature of pumpkins. Can you find out what they honestly know and uncover this centuries-long secret once and for all?

# Write Up

#### Adresse : 94.237.62.149:31129

![[Pasted image 20240410231234.png]]

Lorsqu'on accède à la page et qu'on regarde le code source, on se rend compte que le code ne relève le mot de passe que si on se connecte avec le type *secrets*.

##### Le code
![[Pasted image 20240410231658.png]]

Les hypothèse par rapport au code : 
> - Soit on arrive à modifier le *$_SERVER['REMOTE_ADDR']* à '127.0.0.1' n'est j'y arrive pas
> - Soit on essaie un SQLI mais le code utilise ici une requête préparée
> - Ou on essaie de se connecter avec le type *secrets* et rentré dans la condition *switch* et échapper aux conditions *if*.

![[Pasted image 20240410232143.png]]

Une manière de se jouer des conditions ici est de mettre le type à *true*, et on aura switch (true).

```
{
"type" : true
}
```

on a ensuite le flag :
```flag
HTB{juggl1ng_1s_d4ng3r0u5!!!}
```

