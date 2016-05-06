{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Contexte d'exécution Swift
{: #swift_runtime}
*Dernière mise à jour : 19 février 2016*

Le contexte d'exécution Swift sur {{site.data.keyword.Bluemix}} repose sur le pack swift_buildpack.
Le pack swift_buildpack fournit un environnement d'exécution complet pour les applis Swift.
{: shortdesc}

Le pack swift_buildpack sera utilisé si le répertoire racine de votre appli contient un fichier Package.swift.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Swift. L'application de démarrage Swift est une application Swift simple que vous pouvez utiliser pour découvrir les types d'application serveur que vous pouvez développer à l'aide du programme d'application Swift. Cet exemple d'application crée un serveur de base qui renvoie un message d'accueil HTML au client.  

**Remarque :** Cette application de démarrage n'est pas une application prête pour la production.  En revanche, elle est destinée à être utilisée pour des besoins de formation.  Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}. Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions de contexte d'exécution
{: #runtime_versions}

Vous pouvez spécifier la version de Swift que votre application doit utiliser en utilisant un fichier `.swift`-version dans la racine de votre référentiel :

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-02-03-a
```
{: pre}

Pour obtenir la liste complète des versions prises en charge par Swift, voir le fichier  [manifest.yml](https://github.com/cloudfoundry-community/swift-buildpack/blob/master/manifest.yml) du pack de construction.

Pour plus d'informations sur la version du pack de construction Swift qui est installée dans {{site.data.keyword.Bluemix}}, voir les [informations sur l'édition](https://github.com/cloudfoundry-community/swift-buildpack/releases/tag/v1.0.3).

Etant donné que le langage swift est fréquemment modifié, il est recommandé d'inclure un fichier .swift-version de sorte que votre application soit "épinglée" à la version Swift avec laquelle sa compatibilité est reconnue.

# rellinks
## general
* [Cloud Foundry buildpack for Swift](https://github.com/cloudfoundry-community/swift-buildpack)
* Documentation du [langage Swift](https://swift.org/)
