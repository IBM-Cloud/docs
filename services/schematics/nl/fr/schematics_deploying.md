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

# Déploiement de ressources dans vos environnements 
{: #deploying}

Avec {{site.data.keyword.bplong}}, vous pouvez déployer vos dernières modifications de code directement depuis votre code source. Lorsque vous déployez votre environnement, vous déployez les ressources qui sont définies par vos fichiers de configuration. Ensuite, vous pouvez gérer la mise à disposition, les orchestrations et le cycle de vie de l'environnement depuis {{site.data.keyword.bpshort}}.
{:shortdesc}

## Déploiement dans vos environnements à l'aide de l'interface graphique 
{: #gui}

Si vous préférez une vue graphique pour déployer votre environnement, vous pouvez utiliser le tableau de bord {{site.data.keyword.bpshort}}.
{:shortdesc}


### Configuration requise 
{: #gui-prereq}

* Stockez une configuration Terraform dans le contrôle des sources. Les configurations peuvent être écrites avec une syntaxe HCL (HashiCorp Configuration Language) ou JSON. Voir la <a href="https://www.terraform.io/docs/configuration/index.html">documentation relative à la configuration de Terraform <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour des informations sur la syntaxe HCL et des instructions relatives à l'écriture de configurations. Voir le <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">fournisseur de cloud {{site.data.keyword.IBM_notm}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pour les ressources disponibles. 

Après avoir stocké votre configuration : 

1. Dans le tableau de bord **{{site.data.keyword.bpshort}}**, sélectionnez **Environments**.

2. Cliquez sur **Create Environment** pour ajouter un environnement ou sélectionnez la ligne d'un environnement existant à déployer. 

3. Cliquez sur **Plan** pour prévisualiser les ressources qui seront mises à disposition lorsque vous déploierez votre environnement. Lorsque vous exécutez un plan, {{site.data.keyword.bpshort}} extrait les variables qui figurent dans les détails de votre environnement et la dernière version de votre configuration depuis le contrôle des sources. La sortie du plan compare la configuration aux éléments déployés en fonction de votre fichier d'état Terraform. Votre environnement est verrouillé et ne peut plus être modifié jusqu'à ce que le plan lui soit appliqué ou soit annulé.  

4. Affichez le journal dans la section **Recent Activity** afin d'examiner la sortie du plan. Celle-ci indique si des erreurs existent et quelles sont les ressources que le service prévoit de créer, de changer ou de détruire. 

5. Lorsque vous êtes prêt à lancer votre plan, cliquez sur **Apply**. Vous pouvez surveiller le journal d'activité pour vous assurer que l'application du plan a abouti au cours de la dernière exécution.  


## Déploiement dans vos environnements à l'aide de l'interface de ligne de commande 
{: #cli}

Vous pouvez utiliser le plug-in {{site.data.keyword.bpshort}} pour l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}} afin de déployer des mises à jour dans votre environnement.
{:shortdesc}

### Configuration requise 
{: #cli-prereq}

* Stockez une configuration Terraform dans le contrôle des sources. 
* Si vous ne l'avez pas déjà fait, installez l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}} pour votre système d'exploitation depuis le [référentiel d'interface de ligne de commande {{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/home.html).

Après vous être connecté à l'interface de ligne de commande de {{site.data.keyword.Bluemix_notm}} : 

1. Installez le plug-in d'interface de ligne de commande de {{site.data.keyword.bpshort}} en exécutant la commande suivante :
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  Le plug-in {{site.data.keyword.bpshort}} apparaît sous `bx plugin list` si l'installation aboutit.  

2. Créez un environnement à partir de votre configuration. Lorsque vous créez votre environnement, vous faites pointer le service vers votre contrôle des sources pour qu'il puisse extraire le code le plus récent.  
  
  ```
  bx schematics environment create --file NOM_FICHIER
  ```
  {: codeblock}
  
  <table summary="Description de la commande environment create.">
  <caption>Tableau 1. Description de la commande environment create.

</caption>
  <thead>
  <th colspan="1">Commande </th>
  <th colspan="1">Action</th>
  </thead>
  <tbody>
  <tr>
  <td>--file NOM_FICHIER </td>
  <td>Fichier JSON dans lequel sont stockés les détails de votre environnement.
  <p>
  <p>Exemple de fichier JSON :
  <pre>{
      "description": "(Optional) Description of the environment",
      "frozen": false,
      "name": "Name of the environment",
      "sourceurl": "The GitHub URL that points to the Terraform configuration",
      "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Optional) variable_1",
          "secure": false,
          "value": "Visible value"
      },
      {
          "name": "(Optional) variable_2_secret",
          "secure": true,
          "value": "Secured value"
      }]
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  Notez la valeur `ID` qui est renvoyée. `ID` est un identificateur unique qui est affecté à votre environnement et utilisé dans les commandes qui suivent. 
  
3. Exécutez la commande `plan` pour un aperçu des changements qui seront appliqués à votre environnement. La commande plan affiche les ressources qui changeront ainsi que leur nombre comparé aux éléments déployés, mais les changements ne sont pas appliqués tant que vous n'exécutez pas la commande `apply`. 
  
  ```
  bx schematics action plan --id ID_ENVIRONNEMENT
```
  {: codeblock}
  
  <table summary="Description de la commande plan.">
  <caption>Tableau 2. Description de la commande plan.
  </caption>
  <thead>
  <th colspan="1">Commande </th>
  <th colspan="1">Action</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ID_ENVIRONNEMENT </td>
  <td>Environnement spécifique pour lequel lancer un plan d'exécution. Vous pouvez exécuter <code>bx schematics list</code> si vous devez extraire la valeur de l'ID d'environnement.
  </td>
  </tbody></table>
  
  Un ID d'activité `ID_ACTIVITE` est affecté au plan et enregistré dans le journal d'activité.  

4. Procédez à l'extraction du journal d'activité pour afficher la sortie du plan Terraform. 

  ```
  bx schematics activity log --id ID_ACTIVITE
  ```
  {: codeblock}

  <table summary="Description de la commande log.">
  <caption>Tableau 3. Description de la commande log.
  </caption>
  <thead>
  <th colspan="1">Commande </th>
  <th colspan="1">Action</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ID_ACTIVITE </td>
  <td>Activité spécifique pour laquelle afficher le journal. Vous pouvez exécuter <code>bx schematics activity list --id ID_ENVIRONNEMENT</code> si vous devez extraire la valeur de l'ID d'activité.
</td>
  </tbody></table>
  
5. Exécutez la commande `apply` pour déployer des ressources dans votre environnement. 
  
  ```
  bx schematics action apply --id ID_ENVIRONNEMENT
  ```
  {: codeblock}
  
  <table summary="Description de la commande apply.">
  <caption>Tableau 4. Description de la commande apply.
  </caption>
  <thead>
  <th colspan="1">Commande </th>
  <th colspan="1">Action</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ID_ENVIRONNEMENT </td>
  <td>Environnement spécifique dans lequel déployer des mises à jour. Vous pouvez exécuter <code>bx schematics list</code> si vous devez extraire la valeur de l'ID d'environnement.
  </td>
  </tbody></table>
  
6. Surveillez la sortie d'application pour vérifier que le déploiement a abouti.  

  ```
  bx schematics activity log --id ID_ACTIVITE
  ```
  {: codeblock}

  Si le déploiement a réussi, la ligne suivante apparâit vers la fin de la sortie : 
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
  
## Déploiement dans vos environnements à l'aide de l'API 
{: #api}

Vous pouvez déployer votre environnement à l'aide d'un programme avec l'API {{site.data.keyword.bpshort}}.
{:shortdesc}

Les appels de l'<a href="https://us-south.schematics.bluemix.net/swagger-api/">API {{site.data.keyword.bpshort}} <img src="../../icons/launch-glyph.svg" alt="Icône de lien externe"></a> pointent vers le noeud final de base suivant : 

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Configuration requise 
{: #api-prereq}

* Stockez une configuration Terraform dans le contrôle des sources. 

Procédez comme suit pour déployer des ressources dans votre environnement : 

1. Générez un jeton OAuth IAM à utiliser dans votre en-tête d'authentification. La commande génère un jeton UAA et un jeton IAM. 
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Exemple de sortie : 
  ```
  IAM token:  Bearer eyJraWQ...
  ```
  {: screen}
    
  La sortie `Bearer eyJraWQ...` est un exemple tronqué du jeton IAM. Incluez le jeton complet dans l'en-tête de vos appels d'API. 
  
2. Créez un environnement en exécutant un appel `POST v1/environments`. 

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Optional) Description of the environment",
    "frozen": false,
    "name": "Name of the environment",
    "sourceurl": "The GitHub URL that points to the Terraform configuration",
    "tags": [
      "(Optional) metadata_tag_1",
      "(Optional) metadata_tag_2"
    ],
    "terraformversion": "0.9",
    "variablestore": [{
        "name": "(Optional) variable_1",
        "secure": false,
        "value": "Visible value"
    },
    {
        "name": "(Optional) variable_2_secret",
        "secure": true,
        "value": "Secured value"
    }]
  }'
  ```
  {: codeblock}
    
  La sortie suivante dénote la réussite de l'opération : 
  ```
  {
    "id": "Environment ID",
    "name": "Environment name",
    "description": "Description of the environment",
    "account": "{{site.data.keyword.Bluemix_notm}} account GUID",
    "owner": "The IBMid of the user who created the environment",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "The GitHub URL that points to the configuration",
    "statefile": "The reference to the Terraform state file",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Optional) variable_1",
        "value": "Visible value"
      }
    ]
  }
  ```
  {: screen}
    
  Notez la valeur `id` qui est renvoyée. `id` est un identificateur unique qui est affecté à votre environnement et utilisé dans les appels qui suivent. 
  
3. Exécutez l'appel `POST v1/environments/<ID_environnement>/plan` pour un aperçu des ressources qui seront déployées dans votre environnement lorsque vous appliquerez votre configuration. Les plans extraient les configurations d'environnement dans la branche maître de votre référentiel. 
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  Une réponse dénotant la réussite de l'opération renvoie un élément `activityid`. La valeur de l'ID d'activité est nécessaire pour afficher les journaux, comme la sortie du plan et de l'application. 
  ```
  {
    "activityid": "<ID_activité>"
  }
  ```
  {: screen}

4. Exécutez l'appel `GET v1/environments/<ID_environnement>/activities/<ID_activité>/log` pour afficher la sortie du plan. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities/<ID_activité>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}

5. Déployez votre environnement en exécutant l'appel `PUT v1/environments/<ID_environnement>/apply/`. 
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <jeton_IAM>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Surveillez le déploiement en exécutant l'appel `GET v1/environments/<ID_environnement>/activities/<ID_activité>/log` pour afficher la sortie de l'application. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<ID_environnement>/activities/<ID_activité>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <jeton_IAM>'
  ```
  {: codeblock}

  Si le déploiement a réussi, la ligne suivante apparaît vers la fin de la sortie : 
  
  ```
  Apply complete! Resources: N added, N changed, N destroyed.
  ```
  {: screen}
