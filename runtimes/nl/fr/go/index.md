---

Copyright :
  Années : 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Go
{: #go_runtime}
*Dernière mise à jour : 16 mars 2016*

Le contexte d'exécution Go dans {{site.data.keyword.Bluemix}} repose sur le pack go_buildpack.
Le pack go_buildpack fournit un environnement d'exécution complet pour les applis Go.
{: shortdesc}

Le pack go_buildpack est utilisé si votre application contient un fichier nommé *.go.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Go.  L'application de démarrage Go est une appli Go simple qui fournit un modèle que vous pouvez utiliser pour votre appli. Vous pouvez expérimenter cette appli et effectuer des modifications, puis les envoyer par commande push vers l'environnement Bluemix. Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions de contexte d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Go à utiliser par votre appli en définissant la propriété GoVersion dans le fichier Godeps/Godeps.json qui se trouve à la racine de votre appli. Par exemple :

```
{
	"ImportPath": "gohelloworld",
	"GoVersion": "go1.3.3",
	"Deps": []
}
```
{: codeblock}
Pour plus d'informations, voir [godep](https://github.com/tools/godep){: new_window}.

### Versions disponibles :
{: #available_versions}

Les versions de Go suivantes sont disponibles dans le [pack de construction Go](https://github.com/cloudfoundry/go-buildpack/releases/tag/v1.6.2){: new_window} qui est installé dans {{site.data.keyword.Bluemix}} :

* 1.2.1
* 1.2.2
* 1.3.2
* 1.3.3
* 1.4.2
* 1.4.3
* 1.5
* 1.5.1

Si votre application requiert une version de Go qui n'est pas répertoriée ci-dessus, vous pouvez utiliser le
[pack de construction Go](https://github.com/cloudfoundry/go-buildpack.git){: new_window} externe pour déployer
l'application.

# rellinks
## general
* [GoLang](http://golang.org/){: new_window}
* [Cloud Foundry buildpack for Go](https://github.com/cloudfoundry/go-buildpack){: new_window}
