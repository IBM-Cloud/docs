---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} traitement des incidents 
{: #ts_geospatial}


Vous trouverez dans cette section les réponses à plusieurs questions fréquentes concernant l'utilisation de {{site.data.keyword.geospatialshort_Geospatial}} dans {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Lorsque j'arrête mon app, le service continue de surveiller les régions
{: #stop-monitoring}


L'arrêt de votre app n'entraîne pas automatiquement l'arrêt de {{site.data.keyword.geospatialshort_Geospatial}}.
{:shortdesc}


Vous avez arrêté votre application qui utilise {{site.data.keyword.geospatialshort_Geospatial}}, mais vous constatez dans le tableau de bord d'administration du service que le service continue de surveiller les régions que vous avez spécifiées dans votre app.
{: tsSymptoms}


Si vous arrêtez votre application, votre instance de service {{site.data.keyword.geospatialshort_Geospatial}} continue de s'exécuter. Le service continue de surveiller les régions jusqu'à ce que vous l'arrêtiez, que votre application soit en cours d'exécution ou non.
{: tsCauses}


Arrêtez {{site.data.keyword.geospatialshort_Geospatial}} depuis le tableau de bord d'administration du service. Ou bien, modifiez votre app pour arrêter le service avec l'API REST, puis envoyez vos modifications par commande push à {{site.data.keyword.Bluemix_short}}.
{: tsResolve}

##Le service surveille des régions que je n'ai pas spécifiées dans mon app
{: #unspecified-region}



Si plusieurs applications sont liées à la même instance de service, il se peut qu'une autre application ait ajouté ces régions.
{:shortdesc}



Lorsque vous affichez votre instance {{site.data.keyword.geospatialshort_Geospatial}} dans le tableau de bord d'administration du service, vous constatez qu'elle surveille plus de régions que celles que vous avez spécifiées dans l'une de vos applis.
{: tsSymptoms}

Une instance unique de {{site.data.keyword.geospatialshort_Geospatial}} surveille les régions de toutes les applis liées. Cela signifie que lorsque vous consultez votre tableau de bord d'administration du service, vous voyez des informations relatives aux régions spécifiées par toutes vos applis.
{: tsCauses}

Pour que {{site.data.keyword.geospatialshort_Geospatial}} ne surveille plus certaines régions :

1. Arrêtez le service.
2. Modifiez votre ou vos applis afin de retirer ces régions.
3. Envoyez votre ou vos applis par commande push à {{site.data.keyword.Bluemix_short}}.
{: tsResolve}


##Traitement des incidents depuis le tableau de bord d'administration du service
{: #dashboard}

Lorsque vous traitez des incidents liés à votre application, vous pouvez accéder au tableau de bord d'administration du service pour vérifier le statut de votre instance de service. Si elle ne traite pas les données, vous pouvez peut-être résoudre le problème en arrêtant et en redémarrant le service.
{:shortdesc}

Le statut de votre instance de service {{site.data.keyword.geospatialshort_Geospatial}} est distinct du statut de votre application, et plusieurs applications peuvent être liées à la même instance de service. 

Le tableau de bord d'administration du service fournit des informations sur le statut de {{site.data.keyword.geospatialshort_Geospatial}}, mais pas sur les applications liées. Avec la distinction des statuts de votre instance de service et de votre ou vos applications, si vous arrêtez votre application, votre instance de service {{site.data.keyword.geospatialshort_Geospatial}} continue de s'exécuter. Le service continue de surveiller les régions que vous avez choisies jusqu'à ce que vous les retiriez, que votre application soit en cours d'exécution ou non.
