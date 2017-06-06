---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Destruction de ressources dans des environnements temporaires 
{: #destroying}

Vous pouvez utiliser {{site.data.keyword.bplong}} pour détruire vos ressources. Lorsque vous détruisez vos ressources, vous supprimez votre environnement et toutes les ressources associées.   
{:shortdesc}

**Avertissement** : l'opération de destruction des ressources est irréversible. La destruction des ressources n'est pas recommandée dans les environnements de production, mais peut être utile dans les environnements temporaires tels que les environnements de test ou d'assurance qualité. 

Avant de détruire vos ressources :  
* Assurez-vous qu'aucun trafic n'est dirigé vers vos ressources. 
* Assurez-vous d'avoir sauvegardé les données dont vous pourriez avoir besoin.  


## Destruction de ressources à l'aide de l'interface graphique 
{: #gui}

Vous pouvez utiliser le tableau de bord {{site.data.keyword.bpshort}} pour créer et supprimer des environnements temporaires.
{:shortdesc}

1. Dans le tableau de bord **{{site.data.keyword.bpshort}}**, sélectionnez l'onglet **Environments**. 

2. Cliquez sur la ligne de l'environnement spécifique à supprimer.  

3. Dans le menu d'options, sélectionnez **Destroy resources** ou **Delete environment**. Ces deux actions sont irréversibles. Pour déterminer l'option à sélectionner, déterminez si vous disposez de ressources actives. 
  * Sélectionnez **Destroy resources** si vous voulez arrêter et supprimer vos ressources actives. Il est recommandé d'exécuter un plan avant la destruction afin de vérifier que les ressources qui sont associées à l'environnement peuvent être supprimées. 
  * Sélectionnez **Delete environment** si vous voulez supprimer la configuration d'environnement du service {{site.data.keyword.bpshort}}. En général, cette option est utilisée si l'environnement n'est pas déployé et s'il ne comporte pas de ressources actives. Si vous sélectionnez cette option alors que des ressources sont actives, vous ne pourrez plus utiliser le service {{site.data.keyword.bpshort}} pour assurer le suivi des modifications ou déployer des modifications dans votre environnement. Les ressources actives devront être gérées individuellement, depuis leurs tableaux de bord de service. 
  
  Suivez les invites à l'écran pour confirmer votre choix.  


## Destruction de ressources à l'aide de l'interface de ligne de commande 
{: #cli}

Vous pouvez utiliser l'interface de ligne de commande de {{site.data.keyword.bpshort}} pour créer et supprimer des environnements temporaires.
{:shortdesc}

1. Exécutez la commande `destroy` pour supprimer votre environnement et vos ressources. 

  ```
  bx schematics action destroy --id ID_ENVIRONNEMENT
```
  {: codeblock}
  
2. Facultatif : exécutez la commande `delete` si vous voulez supprimer votre configuration du service. 

  ```
  bx schematics environment delete --id ID_ENVIRONNEMENT
```
  {: codeblock}


## Destruction de ressources à l'aide de l'API 
{: #api}

Vous pouvez utiliser l'API {{site.data.keyword.bpshort}} pour créer et supprimer des environnements temporaires.
{:shortdesc}

1. Exécutez l'appel `PUT v1/environments/<ID_environnement>/destroy` pour détruire vos ressources. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Facultatif : exécutez l'appel `DELETE v1/environments/<ID_environnement>` si vous voulez supprimer votre configuration du service {{site.data.keyword.bpshort}}. 

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}
