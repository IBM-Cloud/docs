---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Initiation à {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} est un service de traitement distribué et géré par des événements, également appelé traitement sans serveur ou Function as a Service (FaaS). {{site.data.keyword.openwhisk_short}} exécute une logique d'application en réponse à des événements ou à des appels directs provenant d'applications Web ou mobiles via HTTP. Les événements peuvent être fournis par des services Bluemix tels que Cloudant et par des sources externes. Les développeurs peuvent se consacrer à l'écriture de la logique d'application et à la création d'actions qui sont exécutées à la demande.
Les avantages de ce nouveau paradigme résident dans le fait que vous ne mettez pas à disposition des serveurs de manière explicite et vous n'avez pas à vous préoccuper de la mise à l'échelle automatique ni à vous soucier de la haute disponibilité, des mises à jour, de la maintenance, d'avoir à payer pour des heures de temps de processeur lorsque votre serveur est actif mais qu'il ne traite aucune demande.
Votre code s'exécute chaque fois que se produit un appel HTTP, un changement d'état de base de données ou tout autre type d'événement qui déclenche l'exécution de votre code.
Vous êtes facturé à la milliseconde de temps d'exécution (arrondie aux 100 ms supérieurs) et non à l'heure d'utilisation de machine virtuelle, que le travail effectué par celle-ci ait été utile ou non.
{: shortdesc}

Ce modèle de programmation est idéal pour les microservices, les appareils mobiles, IoT et de nombres autres applications. Vous bénéficiez implicitement d'une mise à l'échelle automatique et d'un équilibrage de charge clés en main sans avoir à configurer manuellement des clusters, des équilibreurs de charge, des plug-ins HTTP, etc. Si vous travaillez sur {{site.data.keyword.openwhisk}}, vous êtes déchargé de toutes les tâches d'administration, en effet, l'ensemble du matériel, du réseau et des logiciels sont gérés par IBM. Tout ce que vous avez à faire est fournir le code que vous souhaitez exécuter et le donner à {{site.data.keyword.openwhisk}}. Le reste se fait par magie. Vous trouverez une excellente présentation du modèle de programmation sans serveur sur le [blogue de Martin Fowler](https://martinfowler.com/articles/serverless.html).

Vous pouvez également obtenir le [code source Apache OpenWHisk](https://github.com/openwhisk/openwhisk) et exécuter le système vous-même.

Pour plus de détails sur le fonctionnement d'{{site.data.keyword.openwhisk_short}}, voir [A propos d'{{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Vous pouvez utiliser le navigateur ou l'interface de ligne de commande pour développer vos applications {{site.data.keyword.openwhisk_short}}.
Ces deux fonctions sont dotées de capacités similaires pour le développement d'applications. L'interface de ligne de commande offre cependant davantage de contrôle sur le déploiement et les opérations.

## Développer dans votre navigateur
{: #openwhisk_start_editor}

Essayez {{site.data.keyword.openwhisk_short}} dans votre [navigateur](https://console.{DomainName}/openwhisk/editor){: new_window} pour créer des actions, automatiser les actions à l'aide de déclencheurs et explorer des packages publics. 
Consultez la page [En savoir plus](https://console.{DomainName}/openwhisk/learn){: new_window} pour un tour d'horizon de l'interface utilisateur d'OpenWhisk.

## Développement à l'aide de l'interface de ligne de commande
{: #openwhisk_start_configure_cli}

Vous pouvez utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour configurer votre espace de nom et votre clé d'autorisation.
Accédez à la page de [configuration de l'interface de ligne de commande](https://new-console.{DomainName}/openwhisk/cli){: new_window} et suivez les instructions d'installation.

## Présentation
{: #openwhisk_start_overview}
- [Fonctionnement d'OpenWhisk](./openwhisk_about.html)
- [Scénarios d'utilisation courants pour les applications sans serveur](./openwhisk_use_cases.html)
- [Configuration et utilisation de l'interface de ligne de commande d'OpenWhisk](./openwhisk_cli.html)
- [Utilisation d'OpenWhisk depuis une application iOS](./openwhisk_mobile_sdk.html)

## Modèle de programmation
{: #openwhisk_start_programming}
- [Détails du système](./openwhisk_reference.html)
- [Catalogue de services fournis par OpenWhisk](./openwhisk_catalog.html)
- [Actions](./openwhisk_actions.html)
- [Déclencheurs et règles](./openwhisk_triggers_rules.html)
- [Flux](./openwhisk_feeds.html)
- [Packages](./openwhisk_packages.html)
- [Annotations](./openwhisk_annotations.html)
- [Actions Web](./openwhisk_webactions.html)
- [Passerelle d'API](./openwhisk_apigateway.html)
- [Noms d'entité](./openwhisk_reference.html#openwhisk_entities)
- [Sémantique d'action](./openwhisk_reference.html#openwhisk_semantics)
- [Limites](./openwhisk_reference.html#openwhisk_syslimits)

## Exemple Hello World d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Pour vous initier à {{site.data.keyword.openwhisk_short}}, essayez l'exemple de code JavaScript ci-dessous.

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Pour utiliser cet exemple, procédez comme suit :

1. Sauvegardez le code dans un fichier, par exemple *hello.js*.

2. Sur la ligne de commande de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}, créez l'action en entrant la
commande suivante :

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Ensuite, appelez l'action en entrant les commandes suivantes :

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Cette commande génère :

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Cette commande génère :

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

Vous pouvez aussi utiliser les fonctions gérées par des événements dans {{site.data.keyword.openwhisk_short}} pour appeler cette action en réponse à des événements. Suivez l'[exemple de service Alarm](./openwhisk_packages.html#openwhisk_packages_trigger) afin de configurer une source d'événements pour appeler l'action `hello` à chaque fois qu'un événement régulier est généré.


## Référence d'API
{: #openwhisk_start_api notoc}
* [Documentation de l'API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Liens connexes
{: #general notoc}
* [Découvrez {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} sur IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
* [Site Web de projet {{site.data.keyword.openwhisk_short}}](http://openwhisk.org){:new_window}
