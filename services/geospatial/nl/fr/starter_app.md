---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Utilisation de l'application de démarrage {{site.data.keyword.geospatialshort_Geospatial}}
{: #starter_app}


{{site.data.keyword.geospatialshort_Geospatial}} inclut une application de démarrage que vous pouvez utiliser comme modèle d'expérimentation ainsi que pour appliquer des changements et les envoyer à l'environnement {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

L'application de démarrage utilise des messages provenant d'un courtier MQTT de démonstration pour un ensemble simulé de périphériques en mouvement près de Las Vegas. L'application génère des informations sur le statut de ses opérations et les événements qu'elle détecte dans une page Web simple.


Un visualiseur lié depuis cette page Web surveille les périphériques au fur et à mesure qu'ils se déplacent sur une carte. Le visualiseur n'est pas lié à l'application de démarrage ; par conséquent, il n'est pas affecté par les modifications que vous apportez à votre copie de l'application de démarrage. Le code de l'application de démarrage, écrit en Node.js, montre comment configurer et contrôler le service {{site.data.keyword.geospatialshort_Geospatial}} via son API REST. 


Vous pouvez exécuter l'application de démarrage sans modification. Si vous souhaitez expérimenter le service plus en profondeur, vous pouvez modifier le code et renvoyer vos modifications dans l'environnement {{site.data.keyword.Bluemix_short}}.
