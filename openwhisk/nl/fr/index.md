---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Initiation à {{site.data.keyword.openwhisk_short}}
*Dernière mise à jour : 17 février 2016*

{{site.data.keyword.openwhisk}} est un service de calcul géré par des événements. {{site.data.keyword.openwhisk_short}} exécute une
logique d'application en réponse à des événements ou à des appels directs provenant d'applications Web ou mobiles sur HTTP. Les événements peuvent être fournis par des services Bluemix tels que Cloudant et par des sources externes. Les développeurs peuvent se consacrer à
l'écriture de la logique d'application et à la création d'actions qui sont exécutées à la demande. La fréquence d'exécution des actions correspond toujours
à la fréquence des événements, ce qui assure une mise à l'échelle et une résilience inhérentes ainsi qu'une utilisation optimale. Vous ne payez que pour ce que vous utilisez et il n'est pas nécessaire de gérer un serveur. Vous pouvez aussi obtenir le
[code source](https://github.com/openwhisk/openwhisk) et exécuter le système vous-même.
{: shortdesc}

Pour plus de détails sur le fonctionnement d'{{site.data.keyword.openwhisk_short}}, voir [A propos d'{{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## Configuration d'{{site.data.keyword.openwhisk_short}}
Vous pouvez utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour configurer votre espace de nom et votre
clé d'autorisation. Accédez à la page de [configuration de l'interface de ligne de
commande](https://console.{DomainName}/openwhisk/cli){: new_window} et suivez les instructions d'installation. Python 2.7 doit être installé sur votre système pour que vous puissiez utiliser l'interface de ligne de commande.

Une fois {{site.data.keyword.openwhisk_short}} configuré avec l'interface de ligne de commande, vous pouvez commencer à l'utiliser à partir
de la ligne de commande ou via des API REST.

## Utilisation de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}
Une fois que vous avez configuré votre environnement, vous pouvez commencer à utiliser l'interface de ligne de commande
d'{{site.data.keyword.openwhisk_short}} pour effectuer les opérations suivantes :

* Exécuter vos fragments de code, ou vos actions, dans {{site.data.keyword.openwhisk_short}}. Voir
[Création et appel d'actions](./openwhisk_actions.html).
* Utiliser des déclencheurs et des règles pour que vos actions puissent répondre à des événements. Voir
[Création de déclencheurs et de règles](./openwhisk_triggers_rules.html).
* Découvrir comment les packages regroupent des actions et configurer des sources d'événements externes. Voir
[Utilisation et création de packages](./openwhisk_packages.html).
* Explorer le catalogue de packages et améliorer vos applications avec des services externes tels qu'une
[source d'événements Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Voir
[Utilisation de services compatibles avec {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Utilisation d'{{site.data.keyword.openwhisk_short}} depuis une application iOS
Vous pouvez utiliser {{site.data.keyword.openwhisk_short}} depuis votre application mobile iOS ou depuis votre Apple Watch à l'aide du
logiciel SDK {{site.data.keyword.openwhisk_short}} pour iOS. Pour plus de détails, voir la [documentation iOS](./openwhisk_mobile_sdk.html).

## Utilisation d'API REST avec {{site.data.keyword.openwhisk_short}}
une fois votre environnement {{site.data.keyword.openwhisk_short}} activé, vous pouvez utiliser {{site.data.keyword.openwhisk_short}}
avec vos applications Web ou mobiles à l'aide d'appels d'API REST. Pour plus de détails sur les API pour les actions, les activations, les
packages, les règles et les déclencheurs, voir la [documentation
de l'API {{site.data.keyword.openwhisk_short}}](https://new-console.{DomainName}/apidocs/98).

## Exemple Hello World d'{{site.data.keyword.openwhisk_short}}
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

Vous trouverez des informations supplémentaires sur {{site.data.keyword.openwhisk_short}} dans les rubriques suivantes :

* [Noms d'entité](./openwhisk_reference.html#openwhisk_entities)
* [Sémantique d'action](./openwhisk_reference.html#openwhisk_semantics)
* [Limites](./openwhisk_reference.html#openwhisk_syslimits)
* [API REST](https://new-console.{DomainName}/apidocs/98)

# rellinks
## api
* [Documentation de l'API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## general
* [Découvrez {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} sur IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
