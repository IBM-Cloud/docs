---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}

L'environnement d'exécution Go dans {{site.data.keyword.Bluemix}} repose sur le pack go_buildpack.
Le pack go_buildpack fournit un environnement d'exécution complet pour les applis Go.
{: shortdesc}

Le pack go_buildpack est utilisé si votre application contient un fichier nommé *.go.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Go.  L'application de démarrage Go est une appli Go simple qui peut servir de modèle pour votre appli. Vous pouvez expérimenter cette application de démarrage et effectuer des modifications, puis les envoyer par commande push vers l'environnement Bluemix. Pour obtenir de l'aide sur son utilisation, voir [Utilisation des applications de démarrage](/docs/cfapps/starter_app_usage.html).

## Versions d'environnement d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Go à utiliser par votre appli en définissant la propriété GoVersion dans le fichier Godeps/Godeps.json qui se trouve à la racine de votre appli. Par exemple :

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.6.1",
	"Deps": []
}
```
{: codeblock}
Pour plus d'informations, voir [godep](https://github.com/tools/godep){: new_window}.

### Versions disponibles :
{: #available_versions}

Les versions de Go suivantes sont disponibles dans le [pack de construction Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.7.5){: new_window} qui est installé dans {{site.data.keyword.Bluemix}} :

* 1.4.2
* 1.4.3
* 1.5.3
* 1.5.4
* 1.6
* 1.6.1

Si votre application requiert une version de Go qui n'est pas répertoriée ci-dessus, vous pouvez utiliser le
[pack de construction Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externe pour déployer
l'application.

# rellinks
{: #rellinks}
## general
{: #general}

* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
