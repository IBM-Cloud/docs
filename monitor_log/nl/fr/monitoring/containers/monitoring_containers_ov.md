---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Surveillance du service IBM Bluemix Container
{: #monitoring_bmx_containers_ov}

Dans {{site.data.keyword.Bluemix}}, les métriques de conteneur sont collectées automatiquement depuis l'extérieur du conteneur, sans avoir à installer et à gérer des agents dans le conteneur.
{:shortdesc}

Les agents internes au conteneur peuvent être trop lourds et avoir des temps de préparation significatifs pour des instances cloud et des groupes de reprise automatique simples à exécution courte dans lesquels les conteneurs peuvent être rapidement créés et détruits. Cette
approche de collecte de données hors bande élimine ces problèmes et supprime le fardeau de surveillance par les utilisateurs.

Un processus
s'exécutant sur l'hôte effectue une surveillance des métriques sans intervention d'agent. Ce processus, également dénommé moteur de balayage, collecte par défaut en continu les métriques suivantes de tous les conteneurs :

* UC
* Mémoire
* Informations réseau

Les données de métriques sont collectées dans Graphite et affichées dans l'interface utilisateur de {{site.data.keyword.Bluemix_notm}} et dans Grafana. 

Vous pouvez lancer Grafana depuis l'interface utilisateur de {{site.data.keyword.Bluemix_notm}} ou directement depuis un navigateur. Pour plus d'informations, voir [Analyse de métriques dans Grafana](../grafana/monitoring_analyzing_metrics_grafana.html#analyzing_metrics_grafana).

Les conventions Docker et les informations de comptabilité des groupes sont utilisées comme mécanisme de base pour la collecte de données de surveillance.

**Conservation des métriques**

Jusqu'à un point de données par minute est collecté. Les métriques de conteneurs qui n'ont pas été actualisées pendant
7 jours sont supprimées.
    
**Tri des métriques**

Les données sont affichées et organisées par ID de conteneur. 

Depuis la ligne de commande, vous pouvez lancer la commande `cf ic ps` pour afficher la liste des ID de conteneur de tous les conteneurs dans votre registre d'images {{site.data.keyword.Bluemix_notm}} privé.

