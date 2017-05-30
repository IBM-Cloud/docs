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

# Gestion des ressources dans vos environnements 
{: #managing}

{{site.data.keyword.bplong}} simplifie la gestion de vos environnements. Vous pouvez modifier vos ressources déployées et redéployer plusieurs fois des modifications à la demande. 

{:shortdesc}

Les modifications apportées à votre environnement peuvent être déployées avec un processus léger. Lorsque vous voulez changer les ressources qui sont allouées, vous codez les modifications de votre configuration avec une syntaxe déclarative, ce qui signifie que vous indiquez uniquement le résultat souhaité. Avec {{site.data.keyword.bpshort}}, vous pouvez afficher un aperçu de vos modifications avant le déploiement. 


## Mise à jour des ressources à l'aide de l'interface graphique 
{: #gui}

Si vous préférez une vue graphique pour gérer les ressources dans vos environnements, vous pouvez utiliser le tableau de bord {{site.data.keyword.bpshort}}.
{:shortdesc}

Après avoir publié les modifications de code de votre configuration dans GitHub ou modifié des variables dans l'interface graphique, procédez comme suit pour déployer les mises à jour dans votre environnement :

1. Dans le tableau de bord **{{site.data.keyword.bpshort}}**, sélectionnez **Environments**.

2. Cliquez sur la ligne de l'environnement spécifique à mettre à jour. 

3. Cliquez sur **Plan** et recherchez d'éventuelles erreurs dans votre journal de plan. L'environnement est verrouillé jusqu'à ce que vous ou vos collaborateurs sur votre compte {{site.data.keyword.Bluemix_notm}} appliquiez le plan ou l'annuliez.  

4. Cliquez sur **Apply** pour déployer les mises à jour.  


## Mise à jour des ressources à l'aide de l'interface de ligne de commande 
{: #cli}

Vous pouvez mettre à jour des ressources à l'aide d'un programme dans vos environnements avec l'interface de ligne de commande de {{site.data.keyword.bpshort}}.
{:shortdesc}

Après avoir publié les modifications de code de votre configuration dans GitHub, procédez comme suit pour déployer les mises à jour dans votre environnement :

1. Exécutez la commande `plan`. L'interface de ligne de commande de {{site.data.keyword.bpshort}} extrait la configuration d'environnement mise à jour depuis GitHub et génère un aperçu qui montre la façon dont vos ressources diffèrent par rapport à votre déploiement en cours. 

  ```
  bx schematics action plan --id ID_ENVIRONNEMENT
```
  {: codeblock}

2. Affichez la sortie du plan dans le journal d'activité. 

  ```
  bx schematics activity log --id ID_ACTIVITE
  ```
  {: codeblock}

3. Déployez votre plan en exécutant la commande `apply`.  

  ```
  bx schematics action apply --id ID_ENVIRONNEMENT
  ```
  {: codeblock}


## Mise à jour des ressources à l'aide de l'API 
{: #api}

Vous pouvez gérer les ressources à l'aide d'un programme dans vos environnements avec l'API {{site.data.keyword.bpshort}}.
{:shortdesc}

Après avoir publié les modifications de code de votre configuration dans GitHub, procédez comme suit pour déployer les mises à jour dans votre environnement :

1. Exécutez l'appel `POST v1/environments/<ID_environnement>/plan`. L'API {{site.data.keyword.bpshort}} extrait la configuration d'environnement mise à jour depuis GitHub et la compare avec le fichier d'état Terraform pour afficher la façon dont vos ressources diffèrent par rapport à votre déploiement en cours. 

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Exemple de réponse :
  ```
  {
    "activityid": "<ID_activité>"
  }
  ```
  {: screen}

2. Affichez la sortie du plan dans le journal d'activité. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities/<ID_activité>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}

3. Déployez votre plan en exécutant l'appel `PUT /v1/environments/<ID_environnement>/apply`.  

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Audit des modifications apportées à vos environnements 
{: #auditing}

Les configurations peuvent être auditées dans l'historique de version de votre référentiel de contrôle des sources. Afin que vous puissiez surveiller les déploiements effectués dans votre environnement ou afficher les journaux de déploiements précédents, {{site.data.keyword.bpshort}} propose les options d'affichage des journaux d'audit suivantes : 

### Depuis le tableau de bord {{site.data.keyword.bpshort}} 
{: #auditing-gui}

1. Sélectionnez la ligne de l'environnement afin d'accéder à la page des détails de l'environnement. 

2. Surveillez la section **Recent Activities**. Vous pouvez aussi afficher les journaux d'historique de plans et de déploiements précédents. 

### A l'aide de l'interface de ligne de commande de {{site.data.keyword.bpshort}} 
{: #auditing-cli}

1. Procédez à l'extraction de votre ID d'environnement. 

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Procédez à l'extraction des ID d'activité pour votre environnement. Les ID d'activité sont affectés à des actions de plan, d'application, de destruction et de suppression. La commande suivante répertorie toutes les activités qui ont été exécutées pour votre environnement :

  ```
  bx schematics activity list --id ID_ENVIRONNEMENT
```
  {: codeblock}

3. Procédez à l'extraction des données relatives à une activité spécifique, comme l'auteur des modifications apportées à un environnement, et l'horodatage de ces modifications. 

  ```
  bx schematics activity show --id ID_ACTIVITE
  ```
  {: codeblock}

4. Facultatif : pour afficher un journal détaillé, comme une sortie de plan ou d'application, exécutez la commande `log`.  

  ```
  bx schematics activity log --id ID_ACTIVITE
  ```
  {: codeblock}

### A l'aide de l'API {{site.data.keyword.bpshort}} 
{: #auditing-api}

1. Procédez à l'extraction de votre ID d'environnement. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}
  
  Le corps de réponse contient tous les environnements de votre compte {{site.data.keyword.Bluemix_notm}}. Localisez la valeur `id` de l'environnement spécifique à auditer. 

2. Procédez à l'extraction des ID d'activité des actions exécutées pour votre environnement. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}

3. Obtenez une activité spécifique pour un environnement.  

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities/<ID_activité> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}

4. Examinez un journal détaillé de la sortie Terraform. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities/<ID_activité>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}
