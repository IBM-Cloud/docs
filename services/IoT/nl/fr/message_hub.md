---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Connexion et configuration d'un service historique à l'aide de {{site.data.keyword.messagehub}}  
{: #messagehub_main}

Le fait de connecter {{site.data.keyword.messagehub_full}} à {{site.data.keyword.iot_short}} permet d'obtenir un bus de messages à débit élevé évolutif pour le stockage de données d'historique. {{site.data.keyword.messagehub}} repose sur Apache Kafka, système de messagerie à débit élevé open source qui fournit une plateforme à faible temps d'attente pour la gestion des flux de données en temps réel.

## Avant de commencer  
{: #byb}

Avant de connecter {{site.data.keyword.messagehub}} à votre service {{site.data.keyword.iot_short}}, exécutez les tâches suivantes :

- Configurez {{site.data.keyword.messagehub}} dans le même espace {{site.data.keyword.Bluemix_notm}} que votre instance {{site.data.keyword.iot_short_notm}} à l'aide du catalogue {{site.data.keyword.Bluemix_notm}}. Pour plus d'informations sur {{site.data.keyword.messagehub}}, voir le document [Getting started with {{site.data.keyword.messagehub}} ![](../../icons/launch-glyph.svg)](https://console.{DomainName}/docs/services/MessageHub/index.html){: new_window}.

- Vérifiez que vous disposez des privilèges de développeur dans l'organisation {{site.data.keyword.Bluemix_notm}} et que vous êtes connecté via {{site.data.keyword.Bluemix_notm}}. Si vous n'êtes pas connecté via {{site.data.keyword.Bluemix_notm}} ou si vous ne disposez pas de privilèges de développeur dans cette organisation {{site.data.keyword.Bluemix_notm}},  vous ne pourrez pas autoriser la liaison entre {{site.data.keyword.messagehub}} et {{site.data.keyword.iot_short_notm}}.

## Connexion

Pour connecter {{site.data.keyword.messagehub}} à des fins de stockage de données d'historique :

1. Sur votre tableau de bord {{site.data.keyword.iot_short}}, cliquez sur **Extensions** dans la barre de navigation.
2. Dans la vignette Stockage des données historiques, cliquez sur **Configuration**.
4. Sélectionnez le service {{site.data.keyword.messagehub}} que vous souhaitez connecter.  
Tous les services {{site.data.keyword.messagehub}} disponibles au sein du même espace {{site.data.keyword.Bluemix_notm}} que votre service {{site.data.keyword.iot_short}} sont répertoriés dans la section Configuration du stockage des données d'historique.
5. Sélectionnez vos options de configuration {{site.data.keyword.messagehub}} :
 1. Sélectionnez un fuseau horaire.  
 Les horodatages figurant sur les données de terminal qui sont envoyés à {{site.data.keyword.messagehub}} sont convertis dans le fuseau horaire sélectionné.
 2. Sélectionnez une rubrique par défaut.  
 Les événements de terminal sont envoyés à la rubrique par défaut éventuellement définie ici. Pour utiliser des affectations de rubrique plus granulaires, laissez la zone de rubrique par défaut non renseignée et ajoutez des règles d'acheminement personnalisées.
 3. Facultatif : Spécifiez des règles d'acheminement personnalisées.  
 Spécifiez des règles supplémentaires pour les événements de terminal d'acheminement. Seuls les événements correspondant aux règles d'acheminement personnalisées sont transmis.  
 **Remarque :** Un événement peut correspondre à plusieurs règles d'acheminement et peut être transmis à plusieurs rubriques {{site.data.keyword.messagehub}}.
 4. Facultatif : Configurer des rubriques.  
 Pour créer les rubriques avec plus de deux partitions par défaut, vous pouvez spécifier la configuration de partition.
 5. Cliquez sur **Terminé**.
5. Cliquez sur **Autoriser**.
6. Dans la boîte de dialogue Autorisation, cliquez sur **Confirmer**.

Vos données de terminal sont désormais stockées dans {{site.data.keyword.messagehub}}.
