---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Surveillance et journalisation
{: #monitoringandlogging}

{{site.data.keyword.Bluemix}} est une plateforme Cloud Computing {{site.data.keyword.IBM_notm}} permettant de générer, d'exécuter et de gérer des applications et des services. {{site.data.keyword.Bluemix_notm}} combine une plateforme sous forme de services (PaaS) à une infrastructure sous forme de services (IaaS). De plus, {{site.data.keyword.Bluemix_notm}} propose un large catalogue de services de cloud que vous pouvez intégrer facilement à la plateforme sous forme de services et à l'infrastructure sous forme de services afin de construire des applications métier rapidement. {{site.data.keyword.Bluemix_notm}} inclut des services de journalisation et de surveillance intégrés sur l'ensemble de la plateforme. 
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} offre des services de journalisation et de surveillance dans différents services de calcul, tels que Cloud Foundry et {{site.data.keyword.containershort}}. Vous pouvez développer, exécuter et gérer des applications dans n'importe quel contexte d'exécution de calcul sans être confronté à la complexité que représentent la création et la gestion de l'infrastructure qui est généralement liée au développement et au lancement d'une application. 

**Remarque :** Les fonctions de surveillance et de journalisation sont disponibles dans la région du Sud des États-Unis et dans la région du Royaume-Uni.

Vous pouvez utiliser les fonctions de surveillance dans {{site.data.keyword.Bluemix_notm}} pour collecter et mesurer automatiquement des métriques principales à partir de votre environnement et de vos applications. Aucune instrumentation spéciale n'est requise pour collecter les métriques. Par exemple, vous pouvez utiliser les informations fournies par les métriques de performance pour surveiller le fonctionnement d'un service dans le cloud, détecter des goulots d'étranglement de ressources et garder un oeil sur l'accord sur les niveaux de licence. Par exemple, lorsque vous analysez les données de performance d'un service, vous pouvez détecter des situations susceptibles de générer un goulot d'étranglement des ressources et d'affecter votre accord sur les niveaux de licence fournis à vos clients. En agissant suffisamment tôt, vous pouvez empêcher que des situations pouvant avoir un effet négatif sur votre activité ne se produisent.  

Vous pouvez utiliser les fonctions de journalisation de {{site.data.keyword.Bluemix_notm}} pour comprendre le comportement de la plateforme cloud et les ressources qui s'exécutent sur cette dernière. Aucune instrumentation spéciale n'est requise pour collecter les journaux de sortie standard et d'erreur standard. Par exemple, vous pouvez utiliser des journaux pour fournir une analyse rétrospective relative à une application, détecter des problèmes dans votre service, identifier des vulnérabilités, dépanner vos déploiements d'application et le comportement d'exécution, détecter des problèmes dans l'infrastructure où vos applications s'exécutent, suivre votre application parmi les composants de la plateforme cloud et détecter des modèles que vous pouvez utiliser pour préempter des actions qui pourraient affecter votre accord sur les niveaux de service.

## Surveillance des ressources d'infrastructure de calcul
{: #monitoring_sl_ov}

Chaque serveur {{site.data.keyword.Bluemix_notm}} comprend une fonction de surveillance et des rapports faciles à lire qui sont toujours disponibles. Pour plus d'informations, voir  [Surveillance et reporting de l'infrastructure ![Icône de lien externe](../icons/launch-glyph.svg "Icône de lien externe")](https://www.ibm.com/cloud-computing/bluemix/infrastructure-monitoring){: new_window}.


## Surveillance de {{site.data.keyword.Bluemix}} pour les services de calcul
{: #monitoring_bmx_ov}

Par défaut, {{site.data.keyword.Bluemix_notm}} collecte et affiche des métriques de performance relatives à l'utilisation de l'unité centrale, à l'utilisation de la mémoire et aux entrées-sorties de réseau. Ces métriques fournissent des informations sur les performances de ressources de cloud individuelles. Vous pouvez surveiller les performances de ces ressources dans votre environnement de cloud via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Vous pouvez afficher des données en quasi temps réel et des données d'historique. 

Vous pouvez également configurer et surveiller d'autres métriques de performance. Vous pouvez visualiser et analyser ces métriques en dehors de {{site.data.keyword.Bluemix_notm}}. Par exemple, vous pouvez utiliser Grafana pour surveiller d'autres métriques lorsque vous exécutez votre application dans {{site.data.keyword.containershort}}. Vous pouvez personnaliser des tableaux de bord par instance de conteneur ou par espace dans lesquels vous visualisez et analysez les données de performance.

![Vue de surveillance Grafana d'un conteneur s'exécutant dans {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Vous pouvez utiliser la surveillance de plateforme de {{site.data.keyword.Bluemix_notm}} pour :

* En savoir plus sur le fonctionnement de l'application, par exemple détecter les goulots d'étranglement potentiels ou déterminer la nécessité d'une mise à niveau.
* Définir des tendances qui vous serviront à planifier les exigences d'application futures dans votre plateforme cloud.

Pour plus d'informations sur la surveillance d'applications qui s'exécutent sur Cloud Foundry, voir [Surveillance d'applications qui s'exécutent sur Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Pour plus d'informations sur la surveillance dans {{site.data.keyword.containershort}}, voir [Surveillance dans {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

## Journalisation dans {{site.data.keyword.Bluemix}}
{: #logging_bmx_ov}

Les fonctions de journalisation de {{site.data.keyword.Bluemix_notm}} sont intégrées à la plateforme et la collecte des données est activée automatiquement pour les ressources de cloud. Par défaut, {{site.data.keyword.Bluemix_notm}} collecte et affiche des journaux pour vos applications, vos contextes d'exécution d'application et vos contexte d'exécution de traitement dans lesquels ces applications s'exécutent. 

Lorsque vous exécutez vos applications dans le cloud, il se peut que vous ne puissiez pas ouvrir une session SSH ou FTP dans l'infrastructure sur laquelle vos applications s'exécutent pour accéder aux journaux, par exemple, si votre application s'exécute dans Cloud Foundry. En revanche, vous pouvez exécuter votre application dans {{site.data.keyword.containershort}}, autre contexte d'exécution de traitement disponible dans {{site.data.keyword.Bluemix_notm}} et sur lequel vous pouvez ouvrir une session SSH pour accéder aux journaux. Indépendamment du contexte d'exécution de traitement, l'accès aux journaux est primordial et {{site.data.keyword.Bluemix_notm}} vous offre une expérience commune pour la visualisation et l'analyse des journaux dans votre plateforme cloud.

{{site.data.keyword.Bluemix_notm}} enregistre les données de journal générées par la plateforme Cloud Foundry et par les applications Cloud Foundry. Ces journaux comportent les erreurs, les avertissements et les messages d'information qui sont générés pour votre application. Pour plus d'informations sur la journalisation dans Cloud Foundry, voir [Journalisation des applications Cloud Foundry dans {{site.data.keyword.Bluemix}}](logging_cf_apps.html#logging_bluemix_cf_apps).

{{site.data.keyword.Bluemix_notm}} enregistre les données de journal générées par {{site.data.keyword.containershort}}. Pour plus d'informations sur la journalisation dans {{site.data.keyword.containershort}}, voir [Journalisation dans {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_logs.html#container_ml_logs).   


Grâce à la fonctionnalité de journalisation offerte par {{site.data.keyword.Bluemix_notm}}, vous pouvez :

* Visualiser vos ressources de cloud et connaître leurs niveaux de performances et savoir si elles fonctionnent correctement.
* Définir des tendances destinées à vous aider à identifier les scénarios qui nécessitent une action de votre part.
* Définir des traces de données pour une application, par exemple, que vous pouvez utiliser pour le contrôle.
* Réduire le temps et l'effort qui sont requis pour identifier un problème dans une application et la résoudre. 
* Surveiller le déploiement de vos applications dans la plateforme cloud.
* Détecter qu'un service ou une application est arrêté ou en panne.
* Suivre l'exécution d'application et le flux de données.
* Identifier des vulnérabilités sur votre application.
* Détecter des problèmes dans l'infrastructure.
* Détecter des problèmes dans le contexte d'exécution d'application.


