---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Initiation à {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} est un service de traitement distribué et géré par des événements, également appelé traitement sans serveur ou
Function as a
Service (FaaS). {{site.data.keyword.openwhisk_short}} exécute une
logique d'application en réponse à des événements ou à des appels directs provenant d'applications Web ou mobiles via HTTP. Les événements peuvent être fournis par des services Bluemix tels que Cloudant et par des sources externes. Les développeurs peuvent se consacrer à
l'écriture de la logique d'application et à la création d'actions qui sont exécutées à la demande. La fréquence d'exécution des actions correspond toujours à la fréquence des événements, ce qui assure une mise à l'échelle et une résilience inhérentes ainsi qu'une utilisation optimale. Vous ne payez que pour ce que vous utilisez et il n'est pas nécessaire de gérer un serveur. Vous pouvez aussi obtenir le [code source](https://github.com/openwhisk/openwhisk) et exécuter le système vous-même.
{: shortdesc}

Pour plus de détails sur le fonctionnement d'{{site.data.keyword.openwhisk_short}}, voir [A propos d'{{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Vous pouvez utiliser le navigateur ou l'interface de ligne de commande
pour développer vos applications {{site.data.keyword.openwhisk_short}}.
Ces deux fonctions sont dotées de capacités similaires pour le développement
d'applications. L'interface de ligne de commande offre cependant davantage de
contrôle sur le déploiement et les opérations.


## Développer dans votre navigateur
{: #openwhisk_start_editor}

Essayez {{site.data.keyword.openwhisk_short}} dans votre [navigateur](https://console.{DomainName}/openwhisk/editor){: new_window} pour créer des actions, automatiser les actions à l'aide de déclencheurs et explorer des packages publics.
Consultez la page [En savoir plus](https://console.{DomainName}/openwhisk/learn){: new_window} pour un tour d'horizon de l'interface utilisateur d'OpenWhisk.

## Configuration de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_configure_cli}

Vous pouvez utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour configurer votre espace de nom et votre clé d'autorisation. Accédez à la page de [configuration de l'interface de ligne de commande](https://new-console.{DomainName}/openwhisk/cli){: new_window} et suivez les instructions d'installation.

### Configuration de l'interface de ligne de commande pour l'utilisation d'un proxy HTTPS
{: #openwhisk_configure_https_proxy_cli}

L'interface de ligne de commande peut être configurée en vue de l'utilisation d'un proxy HTTPS. Pour configurer un proxy HTTPS, vous devez créer une variable d'environnement appelée `HTTPS_PROXY`. Celle-ci doit avoir pour valeur l'adresse du proxy HTTPS et son port au format suivant :
`{IP PROXY}:{PORT PROXY}`.

Une fois {{site.data.keyword.openwhisk_short}} configuré avec l'interface de ligne de commande, vous pouvez commencer à l'utiliser à partir de la ligne de commande.

## Utilisation de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_cli}

Une fois que vous avez [configuré votre environnement](https://new-console.{DomainName}/openwhisk/cli){: new_window}, vous pouvez commencer à utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour effectuer les opérations suivantes :

* Exécuter vos fragments de code, ou vos actions, dans {{site.data.keyword.openwhisk_short}}. Voir [Création et appel d'actions](./openwhisk_actions.html).
* Utiliser des déclencheurs et des règles pour que vos actions puissent répondre à des événements. Voir [Création de déclencheurs et de règles](./openwhisk_triggers_rules.html).
* Découvrir comment les packages regroupent des actions et configurer des sources d'événements externes. Voir [Utilisation et création de packages](./openwhisk_packages.html).
* Explorer le catalogue de packages et améliorer vos applications avec des services externes tels qu'une [source d'événements Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Voir [Utilisation de services compatibles avec {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Utilisation d'{{site.data.keyword.openwhisk_short}} depuis une application iOS
{: #openwhisk_start_using_ios}

Vous pouvez utiliser {{site.data.keyword.openwhisk_short}} depuis votre application mobile iOS ou depuis votre Apple Watch à l'aide du logiciel SDK {{site.data.keyword.openwhisk_short}} pour iOS. Pour plus de détails, voir la [documentation iOS](./openwhisk_mobile_sdk.html).

## Utilisation d'API REST avec {{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_using_restapi}

une fois votre environnement {{site.data.keyword.openwhisk_short}} activé, vous pouvez utiliser {{site.data.keyword.openwhisk_short}} avec vos applications Web ou mobiles à l'aide d'appels d'API REST.
Pour plus de détails sur les API pour les actions, les activations, les packages, les règles et les déclencheurs, voir la [documentation de l'API {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## Exemple Hello World d'{{site.data.keyword.openwhisk_short}}
{: #openwhisk_start_hello_world}
Pour vous initier à {{site.data.keyword.openwhisk_short}}, essayez l'exemple de code JavaScript ci-dessous.

```
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

    ```
    {
        "payload": "Hello, World!"
    }
    ```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Cette commande génère :

    ```
    {
        "payload": "Hello, Fred!"
    }
    ```
    {: screen}

Vous pouvez aussi utiliser les fonctions gérées par des événements dans {{site.data.keyword.openwhisk_short}} pour appeler cette action en
réponse à des événements. Suivez l'[exemple de service Alarm](./openwhisk_packages.html#openwhisk_packages_trigger) afin de configurer une
source d'événements pour appeler l'action `hello` à chaque fois qu'un événement régulier est généré.


## Détails du système
{: #openwhisk_system_details}

Vous trouverez des informations supplémentaires sur {{site.data.keyword.openwhisk_short}} dans les rubriques suivantes :

* [Noms d'entité](./openwhisk_reference.html#openwhisk_entities)
* [Sémantique d'action](./openwhisk_reference.html#openwhisk_semantics)
* [Limites](./openwhisk_reference.html#openwhisk_syslimits)
* [API REST](https://new-console.{DomainName}/apidocs/98)

# Liens connexes
{: #rellinks notoc}

## Référence d'API
{: #api}
* [Documentation de l'API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Liens connexes
{: #general}
* [Découvrez {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} sur IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
