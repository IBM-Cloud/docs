---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Journalisation des applications CF qui s'exécutent dans les environnements dédié et local
{: #hybrid_apps_logs_ov}

Dans {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm}}, la journalisation est intégrée dans les applications Cloud Foundry. Vous pouvez examiner les données collectées par vos applications dans la console {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

Les applications Cloud Foundry utilisent Cloud Foundry loggregator pour surveiller et réacheminer les journaux vers l'extérieur de votre application. Il n'est pas nécessaire d'installer des agents au sein de l'application.

## Configuration matérielle requise


| **Condition requise** |    **1 noeud**     | **3 noeuds pour haute disponibilité** |
|-----------------|-------------------|-------------------|
| UC virtuelle | 19 | 57 |
| Mémoire | 80 Go | 240 Go |
| Stockage local | 2,98 To | 8,94 To |
{: caption="Tableau 2. Consignation de la configuration matérielle requise pour {{site.data.keyword.Bluemix_local_notm}}" caption-side="top"}

## Configuration

Dans {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm}}, les journaux sont activés par défaut pour toutes les applications. Pour plus d'informations sur la lecture des journaux standard, voir [Journalisation des applications qui s'exécutent dans Cloud Foundry](../logging_cf_apps.html#logging_bluemix_cf_apps). En outre, il est possible d'activer la journalisation avancée dans les environnements {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm}}.

* Pour avoir confirmation de l'activation de la journalisation avancée dans vos environnements {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm}}, suivez les étapes décrites dans [Affichage des journaux](#hybrid_apps_logs_dash). Si vous ne disposez pas du bouton **Vue avancée**, la fonction n'est pas activée.

* Pour activer la journalisation avancée dans votre environnement, suivez les étapes indiquées dans la documentation de [{{site.data.keyword.Bluemix_dedicated_notm}}](/docs/dedicated/index.html#dedicated) ou de [{{site.data.keyword.Bluemix_local_notm}}](/docs/local/index.html#local).

## Conservation des journaux

Dans les applications Cloud Foundry de {{site.data.keyword.Bluemix_dedicated_notm}} et de {{site.data.keyword.Bluemix_local_notm}}, les données de journal sont stockées pendant 30 jours par défaut.

## Affichage des journaux des applications Cloud Foundry dans les environnements dédié et local
{: #hybrid_apps_logs_dash}

Vous pouvez consulter les journaux des applications que vous exécutez sur {{site.data.keyword.Bluemix_dedicated_notm}} et {{site.data.keyword.Bluemix_local_notm}}.
{:shortdesc}

Pour afficher les journaux de vos applications, procédez comme suit :
1. Sélectionnez une application en cours d'exécution.
2. Cliquez sur **Journaux**. La vue **Journaux** contient les journaux de votre application en cours d'exécution.
4. Cliquez sur le bouton **Vue avancée**. La **Vue avancée** est une vue plus détaillée des journaux ; elle utilise Kibana, un outil de visualisation qui se sert des journaux et des données d'horodatage pour créer des visualisations personnalisées. Pour plus d'informations sur l'utilisation de la vue avancée, voir la documentation [Kibana](https://www.elastic.co/guide/en/kibana/current/index.html).

Vous pouvez ensuite personnaliser un tableau de bord Kibana. Pour plus d'informations, voir [Analyse des journaux dans Kibana](../logging_view_kibana3.html#analyzing_logs_Kibana3).
