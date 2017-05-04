---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Astuces pour l'exécution locale de votre application Node.js
{: #hints}

Les informations ci-dessous permettent d'exécuter l'application Node.js à la fois en local et sur Bluemix.
{: shortdesc}

L'exemple suivant montre une partie du code source d'un fichier **js** :
```
var port = (process.env.PORT || 3000);
```
{: codeblock}

Avec ce code, lorsque l'application s'exécute sur Bluemix, la variable d'environnement PORT contient la valeur de port interne à Bluemix, sur laquelle l'appli est à l'écoute des connexions entrantes. Lorsque l'application s'exécute en local, PORT n'est pas définie. La valeur **3000** est donc utilisée comme numéro de port. Le code rédigé ainsi permet d'exécuter l'application localement à des fins de test et sur Bluemix sans autres modifications.
