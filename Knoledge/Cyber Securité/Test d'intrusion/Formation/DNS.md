Le Domaine Name Server est un dictionnaire permettant de convertir une adresse ip en un nom.

Lors d'une recherche sur internet d'un site web, les événements suivant se produisent:
1. Recherche dans le cache perso et le cache dns du navigateur. 
Le cache dns du navigateur fait une correspondance entre le "HostName" et "l'adresse IP"
```chrome
chrome://net-internals/#dns
```

2. Demande au cache de OS
```windows
ipconfig /displaydns
```

3. Le cache manuel *HOST*

4. Server DNS Resolver

5. les 13 Server racine DNS
- fr, com, net

6. Server DNS autoritaire
a qui appartient l'adresse en question, qui nous donne son ip et on retourne jusqu'à nous.


*Outils DIG sur kali pour comprendre le fonctionner du dns*.
