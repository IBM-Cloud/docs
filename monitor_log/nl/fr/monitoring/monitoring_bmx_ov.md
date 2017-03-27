---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Surveillance dans Bluemix
{: #monitoring_bmx_ov}

Par défaut, {{site.data.keyword.Bluemix_notm}} collecte et affiche des métriques de performance relatives à l'utilisation de l'unité centrale, à l'utilisation de la mémoire et aux entrées-sorties de réseau. Ces métriques fournissent des informations sur les performances de ressources de cloud individuelles. Vous pouvez surveiller les performances de ces ressources dans votre environnement de cloud via l'interface utilisateur {{site.data.keyword.Bluemix_notm}}. Vous pouvez afficher des données en quasi temps réel et des données d'historique.
{:shortdesc}

Vous pouvez utiliser les fonctions de surveillance dans {{site.data.keyword.Bluemix_notm}} pour collecter et mesurer automatiquement des métriques principales à partir de votre environnement et de vos applications. Aucune instrumentation spéciale n'est requise pour collecter les métriques. Par exemple, vous pouvez utiliser les informations fournies par les métriques de performance pour surveiller le fonctionnement d'un service dans le cloud, détecter des goulots d'étranglement de ressources et garder un oeil sur l'accord sur les niveaux de licence. Lorsque vous analysez les données de performance d'un service, vous pouvez détecter des situations susceptibles de générer un goulot d'étranglement des ressources et d'affecter votre accord sur les niveaux de licence fournis à vos clients. En agissant suffisamment tôt, vous pouvez empêcher que des situations pouvant avoir un effet négatif sur votre activité ne se produisent.  

Vous pouvez également configurer et surveiller d'autres métriques de performance. Vous pouvez visualiser et analyser ces métriques en dehors de {{site.data.keyword.Bluemix_notm}}. Par exemple, vous pouvez utiliser Grafana pour surveiller d'autres métriques lorsque vous exécutez votre application dans {{site.data.keyword.containershort}}. Vous pouvez personnaliser des tableaux de bord par instance de conteneur ou par espace dans lesquels vous visualisez et analysez les données de performance.

![Vue de surveillance d'un conteneur dans Grafana qui s'exécute dans {{site.data.keyword.Bluemix_notm}}](images/monitoring_default_container_grafana_view.jpg)

Vous pouvez utiliser la surveillance de plateforme de {{site.data.keyword.Bluemix_notm}} pour :

* En savoir plus sur le fonctionnement de l'application, par exemple détecter les goulots d'étranglement potentiels ou déterminer la nécessité d'une mise à niveau.
* Définir des tendances qui vous serviront à planifier les exigences d'application futures dans votre plateforme cloud.

Pour plus d'informations sur la surveillance d'applications qui s'exécutent sur Cloud Foundry, voir [Surveillance d'applications qui s'exécutent sur Cloud Foundry](monitoring_cf_apps.html#monitoring_bluemix_apps).

Pour plus d'informations sur la surveillance dans {{site.data.keyword.containershort}}, voir [Surveillance dans {{site.data.keyword.containershort}}](/docs/containers/monitoringandlogging/container_ml_monitor.html#container_ml_monitor).   

