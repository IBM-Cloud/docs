---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-06"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Versions disponibles
{: #available_versions}

{{site.data.keyword.Bluemix}} fournit tous les
[contextes d'exécution Node.js disponibles actuellement](http://nodejs.org/dist/). Pour ceux-ci, IBM propose des versions comportant des améliorations et des correctifs. Pour plus d'informations, voir [Mises à jour les plus récentes du pack de construction Node.js](/docs/runtimes/nodejs/updates.html).
{: shortdesc}

Le pack de construction IBM Node.js met en cache les versions de l'environnement d'exécution IBM. Par conséquent, si vous utilisez l'environnement d'exécution IBM SDK for Node.js dans votre
application, vous obtenez de meilleures performances pour l'application lorsque celle-ci est envoyée dans Bluemix.

Utilisez le paramètre **node** de la section **engines** du fichier **package.json** pour définir la version
de l'environnement d'exécution Node.js à exécuter.

Utilisez le paramètre **npm** de la section **engines** du fichier **package.json** pour définir une version de npm différente de celle qui est intégrée à Node.js.  

Voir l'exemple suivant :

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
     "npm": "3.10.10"
  }
}
```
{: codeblock}

La version de Node doit toujours être précisée dans le fichier **package.json**. Si elle est omise, la version la plus
récente est utilisée.
