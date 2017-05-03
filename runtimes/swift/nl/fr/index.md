---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Contexte d'exécution IBM Bluemix pour Swift
{: #swift_runtime}

Le contexte d'exécution pour Swift sur {{site.data.keyword.Bluemix}} repose sur le [pack de construction IBM Bluemix pour Swift](https://github.com/IBM-Swift/swift-buildpack) (swift_buildpack).
Ce pack de construction fournit un environnement d'exécution complet pour les applications Swift.
{: shortdesc}

## Application de démarrage
{: #starter_application}

{{site.data.keyword.Bluemix}} propose une [application de démarrage](https://github.com/IBM-Bluemix/Kitura-Starter) Swift basée sur Kitura. L'application de démarrage Kitura est une application Swift simple que vous pouvez utiliser pour découvrir les types d'applications serveur que vous pouvez développer en utilisant le langage de programmation Swift. Cette application exemple crée un serveur HTTP Kitura de base qui renvoie un contenu HTML au client.

**Remarque :** L'application de démarrage Kitura est destinée à être utilisée pour répondre à des besoins de formation. Vous pouvez expérimenter cette application en effectuant des modifications puis en les envoyant par push vers l'environnement {{site.data.keyword.Bluemix}}. Voir [Utilisation des applications de démarrage](../../cfapps/starter_app_usage.html) pour obtenir de l'aide.

## Changement du nom de votre application
{: #renaming_your_app}

Si vous voulez renommer votre application, depuis l'application de démarrage Kitura ou en général, vous devez effectuer un certain nombre de modifications, qui vous éviteront des problèmes et assureront un déploiement sans erreur.

- Renommez le dossier de projet de l'application afin qu'il corresponde au nom de votre application.
- `Package.swift` - changez les entrées suivantes :
    - `name` - doit correspondre au nom de l'application.
    - `targets[Target(name:)]` - doit correspondre au nom de l'application.
- `manifest.yml` - changez les entrées suivantes :
    - `name` - doit correspondre au nom de l'application.
    - `command` - nom de l'exécutable de démarrage de votre application (doit correspondre au nom indiqué dans le fichier Package.swift).

## Versions d'environnement d'exécution
{: #runtime_versions}

Par défaut, le contexte d'exécution pour Swift (swift_buildpack) hébergé sur {{site.data.keyword.Bluemix}} utilise la dernière version GA des binaires Swift. Il s'agit de la seule version de Swift directement prise en charge par IBM et c'est aussi la version qu'il vous est conseillé d'utiliser dans votre application. Pour connaître les détails de cette version, examinez les [informations relatives à la dernière édition](https://github.com/IBM-Swift/swift-buildpack/releases) du pack de construction swift_buildpack. Il est possible que ce pack répertorie d'autres versions Swift, comme illustré dans son fichier [manifest.yml](https://github.com/IBM-Swift/swift-buildpack/blob/master/manifest.yml). Ces versions de Swift courantes, mais non prises en charge, sont préalablement mises en cache dans le pack de construction, ce qui réduit le temps de mise à disposition.

Si vous voulez utiliser une autre version de Swift sur {{site.data.keyword.Bluemix}} pour votre application, vous pouvez spécifier la version avec un fichier `.swift-version` dans la racine de votre référentiel. Ce fichier `.swift-version` définit la version Swift qui doit être utilisée par la pack de construction swift_buildpack.

```
$ cat .swift-version
3.0
```
{: pre}

Puisque le langage Swift est fréquemment mis à jour, vous devez toujours inclure un fichier `.swift-version` de façon à ce que votre application soit "épinglée" à la version Swift avec laquelle sa compatibilité est reconnue.

Notez que vous pouvez spécifier toute version valide de Swift dans votre fichier `.swift-version`. Ces autres versions, qui doivent correspondre aux dénominations utilisées, sont extraites directement de [Swift.org![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/download/). Alors que l'utilisation d'une version non mise en cache prendra un peu plus de temps lors de sa mise à disposition, il n'y a pas de différence de performance au niveau de l'exécution de votre application Swift.

Le pack de construction swift_buildpack par défaut dans {{site.data.keyword.Bluemix}} est utilisé si le répertoire racine de votre application contient un fichier `Package.swift`.  Si vous voulez utiliser un autre pack de construction, vous devez le spécifier en ajoutant une entrée `buildpack: {buildpackUrl}` dans le fichier manifest.yml de votre application. Il vous est aussi possible, si vous préférez, de définir ceci au moment du déploiement, en utilisant l'argument de commande `cf push -b {buildpackUrl}`.


## Environnements de développeurs

Les développeurs disposent de plusieurs options lors de la création d'applications côté serveur avec Swift. Ceux utilisant un périphérique MacOS d'Apple peuvent préférer se servir de l'environnement IDE Xcode, même si ce n'est pas obligatoire.  Les applications basées sur Swift qui seront déployées et s'exécuteront sur {{site.data.keyword.Bluemix}} peuvent utiliser l'éditeur de programmation ou l'environnement IDE de leur choix.  Les fonctions de mise en évidence de syntaxe et d'analyse de code pour Swift sont disponibles pour la plupart des éditeurs couramment utilisés. L'outil de ligne de commande Swift REPL inclus dans les binaires en provenance de [Swift.org![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/) permet une compilation locale et un test avant le déploiement dans {{site.data.keyword.Bluemix}}.

Pour les utilisateurs MaxOS, vous pouvez vous servir des outils [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/) qui simplifient la création, le déploiement, la gestion et le contrôle des applications Swift côté serveur s'exécutant sur {{site.data.keyword.Bluemix}}.  


## Intégration plus poussée

L'utilisation de l'[infrastructure Web Kitura](http://ibm-swift.github.io/Kitura/) permet d'accéder à de nombreuses fonctions. Kitura est modulaire par nature et vous aurez vite envie d'étendre ses fonctionnalités avec les logiciels SDK packagés afin de fournir des fonctions comme l'authentification, l'accès aux services reposant sur Watson ainsi qu'à un large éventail de bases de données.  Kitura fournit une prise en charge pour de nombreuses bases de données directement, alors que les autres projets open source mettent à disposition des logiciels SDK pour diverses plateformes de base de données. Vous trouverez ci-dessous une liste non exhaustive des logiciels SDK fournis par Kitura pour utiliser des ressources externes.

- [IBM Watson](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/swift-watson-sdk)
- [IBM DB2 et DashDB](https://swiftpkgs.ng.bluemix.net/package/IBM-DTeam/swift-for-db2)
- [IBM Cloudant et CouchDB](https://swiftpkgs.ng.bluemix.net/package/cloudant/swift-cloudant)
- [IBM ObjectStorage](https://swiftpkgs.ng.bluemix.net/package/ibm-bluemix-mobile-services/bluemix-objectstorage-serversdk-swift)
- [Apache Cassandra](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Kassandra)
- [Aphid MQTT](https://swiftpkgs.ng.bluemix.net/package/IBM-Swift/Aphid)

Pour trouver d'autres packages Swift à inclure dans votre application, consultez le catalogue [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/) et effectuez une recherche sur votre base de données ou service cible. Le catalogue des packages vous permet de localiser facilement les packages que vous pouvez inclure dans vos applications Swift. Les packages peuvent être ajoutés à une application Swift en incluant l'URL Git du package et les détails de version dans le fichier `Package.swift` de l'application. Pour plus de détails sur la gestion des packages, voir la [section Package Manager de Swift.org](https://swift.org/package-manager/).


## Informations associées

D'autres outils en ligne sont également proposés par IBM au développeur Swift.
- [IBM Swift Developer Center](https://developer.ibm.com/swift/) - site principal permettant d'accéder à toutes les informations relatives à IBM Swift. Vous pouvez y trouver des détails sur les offres IBM, des blogues, des événements sociaux, de la documentation, entre autres choses.
- [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/) - ce site vous fournit un environnement qui vous permet de tester rapidement et facilement des fragments de code Swift, dans diverses version de Swift, et même sur différentes plateformes d'exécution Swift. Vous pouvez aussi enregistrer des exemples de code et les partager avec d'autres utilisateurs ou explorer des exemples populaires fournis par d'autres personnes.


# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [IBM Swift Developer Center](https://developer.ibm.com/swift/)
* [IBM Cloud Tools for Swift](http://cloudtools.bluemix.net/)
* [IBM Swift Package Catalog](https://swiftpkgs.ng.bluemix.net/)
* [IBM Swift Sandbox](https://swiftlang.ng.bluemix.net/)
* [Kitura - Documentation et API](http://ibm-swift.github.io/Kitura/)
* [Application de démarrage Kitura pour Bluemix](https://github.com/IBM-Bluemix/Kitura-Starter)
* [Pack de construction IBM Bluemix pour Swift](https://github.com/IBM-Swift/swift-buildpack)
* [Pack de construction IBM Bluemix pour Swift - Notes sur l'édition](https://github.com/IBM-Swift/swift-buildpack/releases)
* [Swift.org ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/)
* [Documentation du langage Swift ![Icône de lien externe](../../icons/launch-glyph.svg "Icône de lien externe")](https://swift.org/documentation)
