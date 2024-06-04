### 1. Installation de python
Sélénium est un outil d'automatisation de test existant sous plusieurs langage dont python et java. Les matières de l'installer sont soit d'utiliser un *environnement portable de python* ou *un environnement général*  sur le poste.
#### a. Python portable
L'avantage de cette méthode hors mis le fait qu'il soit portable est qu'il soit legé  en ne transportant que ce qui est utilise pour le projet. 
Dans ce cas, il est important d'ajouter les chemins de notre python portable dans les variables d'environnement de laptop
#### b. Python sur l'environnement général
Ici python est installé sur l'environnement de la machine, pas besoin d'ajouter les variables d'environnement qui y sont normalement.
### 2. Installation sélénium
Après avoir installé python et *pip* (le gestionnaire de package de python), nous pouvons installer sélénium (qui est un package) via la commande suivante:

```copier
pip install selenium
```

### 3. Webdriver
Ensuite on installe le *webdriver* du navigateur que nous voulons utiliser pour les tests. 
!!! Attention à ne pas confondre l'exécutable du navigateur et un webdriver de celui-ci. Le webdriver doit être également compatible avec la version du navigateur utilisée. Ci-après des liens vers des versions de navigateur et webdriver associé.
``` googlechromeGit
https://googlechromelabs.github.io/chrome-for-testing/
```
### 4. Mon premier test
Avant de rentrer dans les détails de l'univers sélénium, nous pouvons faire un bref test avec les éléments de base, à savoir:
- Connecter notre webdriver
- ouvrir une page
- lancer un site
- fermer la page

```
from selenium import webdriver

from selenium.webdriver.chrome.service import Service

from selenium.webdriver.common.keys import Keys

from selenium.webdriver.common.by import By

import time

# Chemin vers le WebDriver
driver_path = 'C:\Program Files\Google\Chrome\Application\chromedriver-win64\chromedriver.exe'  

# Créer un objet Service

service = Service(executable_path=driver_path)

# Initialiser le WebDriver avec le Service
driver = webdriver.Chrome(service=service)

# Ouvrir Google
driver.get("http://www.example.com")

# Attendre quelques secondes pour voir les résultats
time.sleep(2)    

# Fermer le navigateur
driver.quit()
```


Référence d'installation : 

``` Réference
https://selenium-python.readthedocs.io/installation.html
```
