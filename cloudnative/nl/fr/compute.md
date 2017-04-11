---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Compute
{: #compute}

Quand vous générez une application de canal numérique de cloud native pour web et mobile, la meilleure façon de procéder est d'avoir une architecture BFF (Backend for Frontend) qui est dédiée à votre canal numérique ou offre la même prise en charge de données et d'intégration logique pour les applications client mobiles et web. Pour plus d'informations sur cette architecture, voir [Microservices for web and mobile ![Icône de lien externe](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

Le diagramme suivant présente une architecture BFF.

![Architecture BFF](images/bff-arch.png)

Figure 1 : Architecture BFF

Le concept à la base d'une architecture BFF est de faire abstraction de la logique applicative et de la logique d'intégration depuis vos microservices ou vos services cloud {{site.data.keyword.Bluemix}} à forte valeur.

Avec cette architecture, vous pouvez déployer et publier des mises à jour sur votre application mobile ou Web et déployer de nouvelles versions de votre architecture BFF en utilisant des pipelines de livraison continue avec le service DevOps.

Si vous avez une architecture BFF pour iOS et une architecture BFF séparée pour Android, les équipes d’ingénierie qui distribuent les options pour cette application ne sont pas contraintes d'en publier les fonctionnalités selon un planning de publication d'API centralisé. Les architectures de canaux numériques et de microservices poursuivent un but commun, celui d'éviter aux équipes d'avoir à publier souvent les nouvelles options et fonctionnalités, en étant tenues de respecter strictement le planning des autres équipes.

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## Intégration d'un client mobile avec BFF
{: #integration}

Pour faciliter l'intégration entre un client mobile et une architecture BFF, {{site.data.keyword.Bluemix_notm}} prend en charge une génération SDK de client mobile pour iOS et Android en langage Swift et Java, respectivement. Pour activer cette fonction, vous devez exposer votre intégration BFF en utilisant un document de spécification Open API (Swagger), qui peut être au format JSON ou YAML.

Le générateur SDK client se sert du fichier de définition Open API pour définir un SDK développeur optimisé client qui est facile à consommer dans votre application mobile native. Il accélérera l'intégration de votre architecture BFF dans votre application mobile.


## Définition d'une API
{: #definition}

L'architecture BFF doit exposer un fichier de définition d'API conforme à la spécification Open API qui s'exécute sur un noeud final de serveur opérationnel. Pour activer {{site.data.keyword.Bluemix_notm}} Developer Experience et l'interface de ligne de commande du SDK {{site.data.keyword.Bluemix_notm}} afin de découvrir ce noeud final, vous devez ajouter une variable d'environnement à votre application Cloud Foundry, intitulée `OPENAPI_SPEC`. Cette variable d'environnement doit se référer à la spécification en utilisant un chemin relatif.

Pour ajouter la variable d'environnement `OPENAPI_SPEC` dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Connectez-vous à [{{site.data.keyword.Bluemix_notm}} ![Icône de lien externe](../icons/launch-glyph.svg)](http://bluemix.net).
2. Sélectionnez une application Cloud Foundry.
3. Sélectionnez **Exécution**.
4. Sélectionnez **Variables d'environnement**.
5. Cliquez sur **Ajouter** dans la section **Défini par l'utilisateur**.
6. Spécifiez `OPENAPI_SPEC` pour **NOM** et un chemin d'URL relatif dans votre fichier de définition Open API.
7. Cliquez sur **Enregistrer**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

Exemple :

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

Les applications {{site.data.keyword.apiconnect_long}} et Loopback fonctionnent particulièrement bien en utilisant cette approche. Vous pouvez vous servir de Loopback et {{site.data.keyword.apiconnect_short}} pour définir un modèle persistant et exposer l'opération CRUD (Create, Read, Update et Delete) en utilisant le fichier de définition Open API.

Vous pouvez également définir des opérations de logique applicative.


### Eléments de la spécification Open API pris en charge
{: #supported-elements notoc}

La seule portion de la spécification Open API qui n'est complètement prise en charge est la structure de fichier. La spécification autorise le fractionnement en différents fichiers de portions de la définition et leur référencement en utilisant la zone json `$ref`. L'ensemble de votre définition doit être contenu dans un fichier.


## Exemple de BFF (Backend for Frontend) utilisant Bluegen
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} a créé une architecture BFF de référence utilisant {{site.data.keyword.apiconnect_short}} et Strongloop, qui mappe un modèle de produit à {{site.data.keyword.cloudant}} et une API d'images pour le référencement des images dans {{site.data.keyword.objectstorageshort}}.

Vous pouvez utiliser cette architecture BFF pour vous lancer rapidement dans le provisionnement d'une architecture BFF totalement opérationnelle dans {{site.data.keyword.Bluemix_notm}} et vous en servir pour comprendre comme il est facile d'intégrer une architecture BFF dans un projet mobile et générer des SDK natifs pour iOS et Android sous Swift et Java, respectivement.

Suivez les instructions du fichier [README ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) pour créer un projet et l'installer.


## Utilisation de BFF (Backend for Frontend) avec un projet Developer Experience
{: #bff-devex}

L'expérience {{site.data.keyword.Bluemix_notm}} Mobile Developer Experience est conçue pour simplifier la définition d'un projet mobile avec un certain nombre de services de cloud associés. Vous pouvez facilement ajouter des services [{{site.data.keyword.mobilepushshort}} ![Icône de lien externe](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![Icône de lien externe](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html) et Data ou Storage.

La console {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} introduit la possibilité d'intégrer une infrastructure BFF dans un projet mobile, dans la page **Compute**. Vous pouvez ajouter des instances de service de calcul existantes à votre projet mobile. Une fois cet ajout effectué, vous pouvez générer un SDK natif pour votre choix de langue ou générer le projet complet et le SDK sera intégré dans le package source du projet de la page **Code**, ce qui est particulièrement utile quand vous procédez à une intégration à des architectures BFF qui sont déjà bien définies.

Une fois que vous avez téléchargé votre projet, vous pouvez l'ouvrir avec Xcode ou Android et le compiler avec le SDK client.


## Utilisation de l'interface de ligne de commande
{: #cli}

Pendant que vous développez votre infrastructure BFF, votre spécification API peut changer. Pour prendre en charge ces changements, vous disposez des deux options ci-après.

* Régénérez l'ensemble du projet dans une nouvelle branche GitHub et fusionnez les changements dans votre branche de développement.
* Régénérez le SDK directement en utilisant l'outil de ligne de commande et n'actualisez que la partie SDK du projet mobile.

Pour utiliser l'outil de ligne de commande, vous devez l'[installer](sdk_cli.html#installation).

Utilisez la commande suivante pour répertorier les actions que vous pouvez exécuter.

```
bluemix sdk
```
{: codeblock}

Utilisez la commande suivante pour répertorier les instances Cloud Foundry en cours d'exécution dans votre espace {{site.data.keyword.Bluemix_notm}} actuel.

```
bluemix sdk list
```
{: codeblock}

Chaque application est répertoriée et l'API est validée si la variable d'environnement `OPENAPI_SPEC` est définie. Dans la colonne `VALID`, vous voyez une coche verte ou un `X` rouge. Une coche dans la colonne `VALID` de l'application signifie qu'une définition Open API ouverte valide est présente. Un `X` dans la colonne `VALID` de l'application peut indiquer l'une des situations suivantes :

* aucune variable d'environnement `OPENAPI_SPEC` n'est définie pour votre application OU
* la définition d'API n'est pas valide par rapport à la spécification Open API

Utilisez la commande suivante pour afficher l'URL complète pour l'API. L'URI et la route complète de la spécification d'API est répertoriée. Vous pouvez afficher la spécification brute dans un navigateur, la consommer directement dans l'outil de ligne de commande ou vérifier que la variable BFF `OPENAPI_SPEC` est correctement définie.

```
bluemix sdk list --url
```
{: codeblock}

Utilisez la commande suivante pour valider le fichier de définition Open API d'`<NomApp>` afin de déterminer s'il peut être utilisé pour générer un SDK. La commande trouve `<NomApp>` dans votre espace actuel et utilise le chemin relatif de la variable d'environnement `OPENAPI_SPEC` pour localiser la spécification pour la validation.

```
bluemix sdk validate <NomApp>
```
{: codeblock}

Utilisez la commande suivante pour générer un SDK pour la `<plateforme>` native de votre choix et placer un fichier compressé dans votre répertoire de travail actuel.

```
bluemix sdk generate <NomApp> <NomSDK> --<Plateforme>
```
{: codeblock}

L'utilisation de l'option `--unzip` extrait automatiquement le SDK dans votre répertoire de travail actuel. Vous pouvez, si vous le souhaitez, spécifier l'emplacement où extraire le SDK en utilisant l'option `--output`. Vous pouvez gérer votre code source avec GitHub et créer une nouvelle branche spécifiquement pour la mise à jour du SDK. L'utilisation de cette approche facilite la visualisation des changements et la fusion de votre SDK mis à jour dans votre branche de développement.


## Utilisation de modèles de SDK générés et d'API
{: #models-apis}

Maintenant que votre architecture BFF est intégrée dans votre application mobile en utilisant un SDK généré, vous pouvez commencer à l'utiliser.

Le SDK est livré avec une documentation complète dans les répertoires `docs` et `source`. Vous pouvez ouvrir le fichier `README.html` pour une vue Web des documents ou ouvrir le fichier `README.md` pour une vue Markdown. Les documents Markdown sont utiles quand vous publiez le SDK dans Cocoapods ou Maven Central.

Dans la documentation, vous pouvez voir une liste des API qui sont générées. Vous pouvez cliquer sur une API pour afficher un fragment de code que vous pouvez directement coller dans votre application mobile.
