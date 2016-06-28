{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# Environnement d'exécution Swift
{: #swift_runtime}
*Dernière mise à jour : 10 juin 2016*
{: .last-updated}

L'environnement d'exécution Swift sur {{site.data.keyword.Bluemix}} repose sur le pack de construction Swift pour Bluemix (c'est-à-dire swift_buildpack).
Le pack de construction swift_buildpack fournit un environnement d'exécution complet pour les applications Swift.
{: shortdesc}

Le pack de construction swift_buildpack sera utilisé si le répertoire racine de votre appli contient un fichier Package.swift.

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une application de démarrage Swift. L'application de démarrage Swift est une application Swift simple que vous pouvez utiliser pour découvrir les types d'application serveur que vous pouvez développer à l'aide du programme d'application Swift. Cet exemple d'application crée un serveur HTTP de base qui renvoie un contenu HTML au client. 

**Remarque :** Cette application de démarrage n'est pas une application prête pour la production.  En revanche, elle est destinée à être utilisée pour des besoins de formation.  Vous pouvez expérimenter cette application et effectuer des modifications puis les envoyer par commande push vers l'environnement {{site.data.keyword.Bluemix}}. Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Versions d'environnement d'exécution
{: #runtime_versions}

Le pack de construction swift_buildpack installé sur Bluemix prend en charge la version `DEVELOPMENT-SNAPSHOT-2016-05-03-a` des fichiers binaires Swift. Si vous souhaitez utiliser une autre version de Swift sur Bluemix pour votre application, vous pouvez spécifier la version avec un fichier `.swift-version` dans la racine de votre référentiel : 

```
cat .swift-version
swift-DEVELOPMENT-SNAPSHOT-2016-04-25-a
```
{: pre}

En plus d'inclure un fichier `.swift-version`, vous devez également ajouter le paramètre `-b https://github.com/IBM-Swift/swift-buildpack` à la commande `cf push`, comme indiqué ci-dessous :

```
cf push -b https://github.com/IBM-Swift/swift-buildpack
```

Pour obtenir la liste complète des versions prises en charge par Swift, voir le fichier  [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/bluemix-buildpack/manifest.yml) du pack de construction.

Pour plus d'informations sur la version du pack de construction Swift qui est installée dans {{site.data.keyword.Bluemix}}, voir les [informations sur l'édition](https://github.com/IBM-Swift/swift-buildpack/releases/tag/1.1.1).

Etant donné que le langage swift est fréquemment modifié, il est recommandé d'inclure un fichier `.swift-version` de sorte que votre application soit "épinglée" à la version Swift avec laquelle sa compatibilité est reconnue. En outre, n'oubliez pas que si vous utilisez une version de Swift autre que `DEVELOPMENT-SNAPSHOT-2016-05-03-a`, vous devez spécifier le paramètre `-b https://github.com/IBM-Swift/swift-buildpack` lorsque vous envoyez votre application par commande push (comme illustré ci-dessus). 

# rellinks
{: #rellinks}
## general
{: #general}
* [Pack de construction Swift pour Bluemix](https://github.com/IBM-Swift/swift-buildpack)
* Documentation du [langage Swift](https://swift.org/)
