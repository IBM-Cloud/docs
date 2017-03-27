---



copyright:

  years: 2016, 2017

lastupdated: "2016-10-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

<!-- audience blue staging only begin -->

# Surveillance et journalisation des applications Cloud Foundry dans les environnements dédié et local
{: #dedicated_apps_ml_ov}


Dans {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm:}}, la journalisation est intégrée dans les applications Cloud Foundry. Vous pouvez examiner les données collectées par vos applications dans la console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Les applications Cloud Foundry utilisent Cloud Foundry loggregator pour surveiller et réacheminer les journaux vers l'extérieur de votre application. Il n'est pas nécessaire d'installer des agents au sein de l'application.

## Configuration matérielle requise


| **Condition requise** |    **1 noeud**     | **3 noeuds pour haute disponibilité** |
|-----------------|-------------------|-------------------|
UC virtuelle | 19 | 57 |
Mémoire | 80 Go | 240 Go |
Stockage local | 2,98 To | 8,94 To |
{: caption="Table 1. Logging hardware requirements for {{site.data.keyword.Bluemix_local_notm:}}" caption-side="top"}

## Configuration

Dans {{site.data.keyword.Bluemix}} dédié et dans {{site.data.keyword.Bluemix}} local, les journaux sont activés par défaut pour toutes les applications. Pour plus d'informations sur la lecture des journaux standard, voir Journalisation des applications qui s'exécutent dans Cloud Foundry. En outre, il est possible d'activer la journalisation avancée dans les environnements {{site.data.keyword.Bluemix}} dédié et {{site.data.keyword.Bluemix}} local.

## Conservation des journaux

Dans les applications Cloud Foundry de {{site.data.keyword.Bluemix}} dédié et de {{site.data.keyword.Bluemix}} local, les données de journal sont stockées pendant 30 jours par défaut.

## Affichage des journaux des applications Cloud Foundry dans {{site.data.keyword.Bluemix}} dédié et dans {{site.data.keyword.Bluemix}} local
{: #dedicated_apps_ml_logs_dash}

Vous pouvez consulter les journaux des applications que vous exécutez sur {{site.data.keyword.Bluemix_notm}} dédié et dans {{site.data.keyword.Bluemix_notm}} local.
{:shortdesc}

Pour afficher les journaux de vos applications, procédez comme suit :
1. Sélectionnez une application en cours d'exécution.
2. Cliquez sur **Journaux**. La vue **Journaux** contient les journaux de votre application en cours d'exécution.
4. Cliquez sur le bouton **Vue avancée**. La **Vue avancée** est une vue plus détaillée des journaux ; elle utilise Kibana, un outil de visualisation qui se sert des journaux et des données d'horodatage pour créer des visualisations personnalisées. Pour plus d'informations sur l'utilisation de la vue avancée, voir la documentation [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Vous pouvez ensuite personnaliser un tableau de bord Kibana. Pour plus d'informations, voir [Personnalisation de l'affichage des journaux dans le tableau de bord Kibana](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_dash_logs_custom).

<!-- audience blue staging only end comment -->
