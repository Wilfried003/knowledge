---
tags:
  - Challenge
  - Web
  - SSTI
  - CodeSource
  - Docker
---
# Description 

There's a new trend of an application that generates a spooky name for you. Users of that application later discovered that their real names were also magically changed, causing havoc in their life. Could you help bring down this application?

# Write Up

#### Adresse : 94.237.63.93:31522

![[Screenshot_2024-04-10_16-41-06.png]]

Lorsqu'on entre quelque chose, par exemple *azerty*, on voit le résultat suivant.

![[Pasted image 20240410165040.png]]

*!! Attention à l'url*

Et si on essayait de faire une attaque [[Knoledge/Securité/Note/Vulnerabilité/Web/SSTI|SSTI]] en testant des opérations voir [[ https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection | Hacktricks SSTI ]] ou [[https://portswigger.net/web-security/server-side-template-injection | Portswigger]] ?

#### Détection

![[Knoledge/Securité/Note/Vulnerabilité/Web/SSTI#^9a413b]]
![[Knoledge/Securité/Note/Vulnerabilité/Web/SSTI#^397cac]]

Ce site peut être vulnérable à une attaque SSTI
#### Identification [[Knoledge/Securité/Note/Vulnerabilité/Web/SSTI#^637bc7|(ref)]]


Ce site est vulnérable une attaque SSTI car elle interprète l'opération 
```copier
${7*7} 
```

Avec Wappalyzer, on voit que les langages de programmation utilisés pour ce site sont python et php.
	
![[Pasted image 20240410171909.png]]

Ensuite, il faut chercher un moteur de Template python, qui utilise cette manière de faire des opérations et enfin tester ses commandes d'appels systèmes qu'on injectera dans l'url.
une technique serait de provoquer une erreur et lire le code.

Mais ici, le code a été filtré, et on ne peut identifier le Template grâce au log d'erreur.

Toutefois, nous avons ici le code source du site et l'on peut identifier  le Template utilisé qui est *MakoTemplates*.

Grace au code source toujours, nous identifions on le flag est copié dans le Docker. On ouvre alors le fichier avec le payload suivant:
```copier
${open('/flag.txt').read()}
```
*!! Il est conseillé d'encoder en format url la commande qu'on veille jouer.*

On obtient le flag

```copier
HTB{t3mpl4t3_1nj3ct10n_C4n_3x1st5_4nywh343!!}
```