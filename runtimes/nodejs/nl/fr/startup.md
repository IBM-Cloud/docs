---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Commande de démarrage
{: #startup_commmand}

La méthode recommandée pour définir une commande de démarrage pour votre application Node.js Bluemix consiste à utiliser
un fichier **Procfile** ou **package.json**.
{: shortdesc}

Pour définir une commande de démarrage dans votre fichier **Procfile**, suivez le modèle ci-dessous. Ici, app.js correspond au script startup.js de votre application.
```
web: node app.js
```
{: codeblock}

Sauvegardez
le fichier **Procfile** dans le répertoire racine de votre application.

S'il n'existe pas de fichier **Procfile**, le pack de construction Node.js d'IBM
Bluemix recherche une entrée scripts.start dans le fichier **package.json**. Dans l'exemple ci-dessous, app.js est le script js de démarrage de votre application.
```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

Si une entrée de script de démarrage existe dans le fichier **package.json**, un fichier **Procfile** est généré
automatiquement. Le contenu du fichier **Procfile** généré automatiquement est le suivant :
```
    web: npm start
```
{: codeblock}

Pour plus d'informations sur les fichiers **Procfile** et **package.json**, consultez [Tips for Node.js Applications ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html).
