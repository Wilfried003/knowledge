# Qu'est ce qu'une Server-Side Template Injection SSTI

Certaines applications web utilisent des moteurs de Template afin de dynamiser leurs page et récupérer des variables en les interprétant en fonction des cas. Un exemple simple est le fait d'utiliser une meme page de bienvenu pour plusieurs utilisateurs en disant 'Bonjour nom'. 
Cependant, une mauvaise isolation du code peut permettre d'interpréter n'importe quoi et de mener à une ouverture vers le SI.

# Comment trouver une faille SSTI

## 1. Détection

^01a7fe

La première étape consiste à s'assurer ou pas que le site en face est vulnérable à un SSTI. <br>Pour cela, on peut jouer une séquence de caractère le plus souvent utilisé par les moteurs de recherche comme :  ^9a413b

```copier
${{<%[%'"}}@{%\.#{<%=
```

^397cac
Si une erreur se présente, le site peut être vulnérable à une attaque SSTI

## 2. Indentification du moteur de Template

^637bc7
Les méthodes d'identifications sont les suivantes :  

 > - Identifier quelle opération arithmétique est interprété par le site. 
 
```copier
{{7*7}}
```
```copier
${7*7}
```
```copier
${{7*7}}
```
```copier
<%= 7*7 %>
```
```copier
#{7*7}
```

> - Réalisé une erreur afin de connaitre à quel moteur de Template on a à faire
> - Chercher sur internet un RCE

Lien de référence intéressante :  [[ https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection | Hacktricks SSTI ]] et [[https://portswigger.net/web-security/server-side-template-injection | Portswigger ]]