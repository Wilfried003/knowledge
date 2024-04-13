---
tags:
  - Challenge
  - Web
  - HTML
  - JS
---
# Description
Intergalactic Ministry of Spies tested Pandora's movement and intelligence abilities. She found herself locked in a room with no apparent means of escape. Her task was to unlock the door and make her way out. Can you help her in opening the door?


# Write up

#### Adresse : 94.237.54.170:58893

![[Pasted image 20240413031648.png]]

Une fois sur le site, on se rend compte du contexte de la page, qui est déterminer le bon code pour afficher le flag.
O recherche alors quelle fonction est appelée lorsqu'on clique sur *Enter*, une fonction js *checkPin* apparemment dont le corps est :

![[Pasted image 20240413032939.png]]

Quelle est alors le pin à utiliser ? 

![[Pasted image 20240413033032.png]]

Toutefois le chiffre *0* n'existe pas sur notre IHM. 
On va donc créer une liste currentPin =  [1, 0, 6, 9] et ensuite appelé la fonction *checPin*. On a : 

![[Pasted image 20240413033341.png]]
Le flag est 
```flag
HTB{vi3w_cli13nt_s0urc3_S3cr3ts!}
```

