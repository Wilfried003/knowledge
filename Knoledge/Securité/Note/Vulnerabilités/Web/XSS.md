# Qu'est ce qu'un cross-site scripting XSS

Le XSS est un vulnerabilité web dans laquelle un attaquant injecte du code *js*  malveillant dans un site.
Il existe 3 types de XSS : 

> XSS Store

Dans le type d'attaque, le payload est chargé depuis une source de stockage et affecte toute les personne qui lisent ces données 
*Ex de site: un forum* 

> XXS Reflected 

Dans ce cas le payload est directement injecté via une requête HTTP du site par le biais *de lien, formulaire, url ... et envoyé a la victime

> XSS basé sur le DOM

Ce type d'attaque affecte la structure du DOM de la cicle. 

# Comment tester et trouver une vulnérabilité XSS

> XSS between HTML tags

```
<script>alert(document.domain)</script>
```
```
<script>alert(1)</script>
```
```
<img src=1 onerror=alert(1)>
```

