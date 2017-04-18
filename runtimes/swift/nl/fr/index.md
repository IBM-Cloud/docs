{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .pre}


# IBM Bluemix Runtime for Swift
{: #swift_runtime}
Dernière mise à jour : 19 septembre 2016
{: .last-updated}

Runtime for Swift on {{site.data.keyword.Bluemix}} repose sur le [pack de
construction IBM Bluemix pour Swift](https://github.com/IBM-Swift/swift-buildpack) (c'est-à-dire, swift_buildpack).
Ce pack de construction fournit un environnement d'exécution complet pour les applications Swift.
{: shortdesc}

## Application de démarrage 
{: #starter_application}

{{site.data.keyword.Bluemix}} met à disposition une [application de
démarrage](https://github.com/IBM-Swift/Kitura-Starter-Bluemix) Swift reposant sur Kitura. L'application de démarrage Kitura est une application Swift simple que vous pouvez utiliser pour découvrir les types d'application serveur que vous pouvez développer à l'aide du langage de programmation Swift. Ce modèle d'application crée un serveur HTTP
Kitura de base qui renvoie un contenu HTML au client.


**Remarque :** l'application de démarrage Kitura a été conçue à des fins d'apprentissage. Vous pouvez tester l'application de
démarrage en l'améliorant, puis en envoyant vos modifications dans l'environnement {{site.data.keyword.Bluemix}}. Voir
[Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour apprendre à utiliser l'application de démarrage.


## Renommer votre application 
{: #renaming_your_app}

Si vous voulez renommer votre application depuis le module de démarrage Kitura ou plus généralement, vous devez effectuer plusieurs modifications. Vous
éviterez ainsi toute confusion et assurerez un déploiement sans erreur.


- Renommez le dossier du projet de l'application pour que son nom corresponde à celui de votre application. 
- `Package.swift` - Changez les entrées suivantes : 
    - `name` - Doit correspondre au nom de l'application. 
    - `targets[Target(name:)]` - Doit correspondre au nom de l'application. 
- `manifest.yml` - Changez les entrées suivantes : 
    - `name` - Doit correspondre au nom de l'application. 
    - `host` - Représente le segment de l'hôte principal dans l'adresse URL de l'application. 
- `Procfile` - La valeur de `web` doit correspondre au nom de répertoire de l'application.
Il s'agit de la commande exécutée après la compilation pour démarrer l'application Web. 


## Versions du contexte d'exécution 
{: #runtime_versions}

Par défaut, le contexte d'exécution Runtime for Swift (swift_buildpack) hébergé dans {{site.data.keyword.Bluemix}} utilise la version GA
(Disponibilité générale) la plus récente des fichiers binaires Swift.
Il s'agit de la seule version de Swift directement prise en charge par IBM, et la version dont l'utilisation vous est recommandée dans votre application. Vous pouvez identifier cette version prise en charge en consultant les
[notes sur l'édition les plus récentes](https://github.com/IBM-Swift/swift-buildpack/releases) de swift_buildpack. Il se peut
que le pack de construction répertorie d'autres versions de Swift, comme indiqué dans son fichier
[manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Ces versions de Swift courantes, mais non prises
en charge, sont mises en cache préalablement dans le pack de construction, afin de réduire le temps de mise à disposition.


Si vous voulez utiliser une autre version de Swift dans {{site.data.keyword.Bluemix}} pour votre application, vous pouvez la spécifier avec
un fichier `.swift-version` à la racine de votre référentiel. Ce fichier `.swift-version` définit la version Swift qui
doit être utilisée par swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Etant donné que le langage Swift est fréquemment mis à jour, il est recommandé de toujours inclure un fichier `.swift-version` pour
que votre application soit "épinglée" avec la version Swift qu'elle utilise.


Notez que vous pouvez spécifier toute version valide de Swift dans votre fichier `.swift-version`. Ces versions alternatives
sont extraites directement de [Swift.org](https://swift.org/download/) et doivent respecter les conventions de dénomination de Swift. La mise à disposition
d'une version qui n'est pas en cache prend un peu plus de temps, mais il n'existe pas de différence en termes de performances du contexte d'exécution
de votre application Swift.


Le pack de construction swift_buildpack par défaut présent dans {{site.data.keyword.Bluemix}} est utilisé si le répertoire racine de votre
application contient un fichier `Package.swift`. Si vous voulez utiliser un autre pack de construction, vous devez le spécifier en
ajoutant une entrée `buildpack: {UrlPackConstruction}` dans le fichier manifest.yml de votre application. Vous pouvez aussi le
définir au moment du déploiement à l'aide de l'argument de commande `cf push -b {UrlPackConstruction}`. 


## Environnements de développeur 

Les développeurs disposent de plusieurs options pour créer des applications côté serveur avec Swift. Ceux qui utilisent un périphérique MacOS
d'Apple préféreront probablement utiliser Xcode IDE, mais ce n'est pas obligatoire. Les applications reposant sur Swift qui seront déployées et
exécutées dans {{site.data.keyword.Bluemix}} peuvent utiliser n'importe quel éditeur de programmation ou environnement de développement intégré.
La mise en évidence de la syntaxe et l'utilisation de Lint pour Swift sont disponibles dans de nombreux éditeurs très appréciés.
L'outil de ligne de commande Swift REPL inclus dans les fichiers binaires de [Swift.org](https://swift.org/) permet la compilation locale
et le test avant le déploiement dans {{site.data.keyword.Bluemix}}.

Les utilisateurs MacOS peuvent utiliser le jeu d'outils [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/), qui simplifie la
création, le
déploiement, la gestion et le contrôle des applications Swift côté serveur s'exécutant dans {{site.data.keyword.Bluemix}}.  


## Intégration améliorée

L'[infrastructure Web Kitura](http://ibm-swift.github.io/Kitura/) fournit un grand nombre de fonctions.
Kitura est modulaire par nature. Rapidement, vous aurez envie d'étendre sa fonctionnalité avec les logiciels SDK conditionnés afin de disposer de
fonctions telles que l'authentification, l'accès à des services reposant sur Watson, et un grand éventail de bases de données.
Kitura prend en charge de nombreuses bases de données directement, tandis que d'autres projets open source fournissent également des logiciels SDK pour
un grand nombre de plateformes de base de données.
Voici une liste non exhaustive de logiciels SDK fournis par Kitura pour l'utilisation de ressources externes :


- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 and DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant and Couchbase](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Pour découvrir d'autres packages Swift que vous pouvez inclure dans votre application, consultez le
[catalogue des packages IBM Swift](https://swiftpkgs.ng.bluemix.net/) et recherchez votre base de données ou votre service cible.
Le catalogue des packages permet de trouver facilement des packages que vous pouvez inclure dans vos applications Swift. Vous pouvez ajouter des packages
à une application Swift en incluant l'adresse URL Git du package ainsi que les détails de version dans le fichier `Package.swift` de
l'application. Pour plus de détails sur la gestion des packages, voir la [section Package Manager sur Swift.org](https://swift.org/package-manager/).


## Informations connexes 

IBM propose également d'autres outils en ligne pour les développeurs Swift. 
- [IBM Swift DevCenter](https://developer.ibm.com/swift/) - Site d'arrivée principal pour toutes les informations IBM
Swift.
Vous y trouverez des informations sur nos offres, des blogues, des événements sociaux, la documentation, etc. 
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - Ce site fournit un environnement dans lequel vous pouvez tester
rapidement et facilement des fragments de code Swift dans diverses versions de Swift, et même sur différentes plateformes d'exécution Swift. Vous pouvez
également sauvegarder et partager des exemples de code avec d'autres, et découvrir des exemples populaires mis à disposition par d'autres.



# rellinks
{: #rellinks}
## general
{: #general}
* [IBM Swift DevCenter](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Documentation et API Kitura](http://ibm-swift.github.io/Kitura/)
* [Application de démarrage Kitura pour Bluemix](https://github.com/IBM-Swift/Kitura-Starter-Bluemix)
* [Pack de construction IBM Bluemix pour Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Notes sur l'édition du pack de construction IBM Bluemix pour Swift](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org](https://swift.org/)
* [Documentation du langage Swift](https://swift.org/documentation)
