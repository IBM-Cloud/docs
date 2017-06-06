---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Analyse d'une zone de message JSON qui fait partie d'une entrée de journal de conteneur
{: #logging_containers_analyze_json_field}

Dans Kibana, pour analyser les données de journal de votre conteneur, vous pouvez définir de nouvelles recherches et appliquer des filtres pour les zones de type de chaîne qui sont définies dans une zone de message au format JSON.
{:shortdesc}

Procédez comme suit pour analyser une zone de type JSON dans Kibana :

1. Pour scinder une zone de message JSON en plusieurs zones, consignez le message au format JSON dans un fichier au lieu de l'envoyer dans la sortie standard (STDOUT). 

    Lorsque des entrées de journal JSON sont envoyées au fichier de journal Docker d'un conteneur sous la forme de sortie standard STDOUT, elles ne sont pas analysées en tant qu'entrées JSON. Vous ne pouvez pas trier les messages à l'aide de la zone @timestamp pour modifier leur l'ordre d'affichage.  

2. Ajoutez le fichier journal à la liste des journaux non définis par défaut qui sont disponibles pour analyse à partir d'un conteneur. Pour plus d'informations, voir [Collecte de données de journaux autres que ceux par défaut d'un conteneur](logging_containers_other_logs.html#logging_containers_collect_data). 

3. Analysez votre journal dans Kibana. Pour plus d'informations, voir [Analyse de journal avancée avec Kibana](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).

    **Remarque :** si une zone est déterminée comme étant de type JSON valide, elle est analysée et de nouvelles zones sont créées à partir d'elle. Seules les valeurs de zone de type chaîne peuvent être filtrées et triées dans Kibana.
    
    La valeur de zone @timestamp affichée correspond à l'horodatage auquel l'entrée de journal a été reçue par ElasticSearch. L'horodatage qui indique le moment où l'entrée de journal a été générée dans le conteneur s'affiche dans le cadre des zones de message.
    


