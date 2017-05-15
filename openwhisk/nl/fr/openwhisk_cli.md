---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}

{{site.data.keyword.openwhisk_short}} offre une interface de ligne de commande puissante qui permet de gérer tous les aspects du système.

## Configuration de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} 

Vous pouvez utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour configurer votre espace de nom et votre clé d'autorisation.
Accédez à la page de [configuration de l'interface de ligne de commande](https://console.{DomainName}/openwhisk/cli) et suivez les instructions d'installation.

La configuration de deux propriétés est requise pour pouvoir utiliser l'interface de ligne de commande :

1. L'**hôte d'API** (nom ou adresse IP) pour le déploiement d'{{site.data.keyword.openwhisk_short}} que vous souhaitez utiliser.
2. La **clé d'autorisation** (nom d'utilisateur et mot de passe) qui vous permet d'accéder à l'API {{site.data.keyword.openwhisk_short}}.

Exécutez la commande suivante pour définir l'hôte d'API :

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

Si vous connaissez votre clé d'autorisation, vous pouvez configurer l'interface de ligne de commande afin de l'utiliser. 

Exécutez la commande suivante pour définir la clé d'autorisation :

```
wsk property set --auth <clé_autorisation>
```
{: pre}

**Indication :**l'interface CLI d'OpenWhisk stocke par défaut dans `~/.wskprops` les propriétés définies. L'emplacement de ce fichier peut être modifié par le biais de la variable d'environnement `WSK_CONFIG_FILE`. 

Pour vérifier votre configuration d'interface de ligne de commande, essayez de [créer et d'exécuter une action](./index.html#openwhisk_start_hello_world).

## Utilisation de l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}}

Après avoir configuré votre environnement, vous pouvez commencer à utiliser l'interface de ligne de commande d'{{site.data.keyword.openwhisk_short}} pour effectuer les actions suivantes :

* Exécuter vos fragments de code, ou vos actions, dans {{site.data.keyword.openwhisk_short}}. Voir [Création et appel d'actions](./openwhisk_actions.html).
* Utiliser des déclencheurs et des règles pour que vos actions puissent répondre à des événements. Voir [Création de déclencheurs et de règles](./openwhisk_triggers_rules.html).
* Découvrir comment les packages regroupent des actions et configurer des sources d'événements externes. Voir [Utilisation et création de packages](./openwhisk_packages.html).
* Explorer le catalogue de packages et améliorer vos applications avec des services externes tels qu'une [source d'événements Cloudant](./openwhisk_cloudant.html). Voir [Utilisation de services compatibles avec OpenWhisk](./openwhisk_catalog.html).

## Configuration de l'interface de ligne de commande pour l'utilisation d'un proxy HTTPS

L'interface de ligne de commande peut être configurée en vue de l'utilisation d'un proxy HTTPS. Pour configurer un proxy HTTPS, vous devez créer une variable d'environnement appelée `HTTPS_PROXY`. Celle-ci doit avoir pour valeur l'adresse du proxy HTTPS et son port au format suivant :
`{IP PROXY}:{PORT PROXY}`.
