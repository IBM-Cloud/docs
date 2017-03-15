---

copyright:
years: 2016, 2017
lastupdated: "2017-01-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilisation d'interfaces pour mapper des données de terminal (bêta)
{: #im_index}

Utilisez la fonction de mappage d'interface d'{{site.data.keyword.iot_full}} pour organiser et intégrer des données de terminal entrantes et sortantes.
{:shortdesc}

**Important :** Pour le moment, la fonction de mappage d'interface est disponible uniquement sous forme de fonction bêta. Avant l'édition finale, il est possible que les fonctions bêta incluent des modifications qui sont incompatibles avec la version en cours. Il est fortement recommandé de ne pas utiliser les fonctions bêta dans des applications en production avant l'édition finale. Pour recevoir d'autres informations et communiquer des commentaires en retour sur cette fonction bêta, merci de vous [inscrire au programme bêta IM](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050) et de nous faire part de vos impressions.

## Présentation
{: #overview}

Vous pouvez utiliser la fonction de mappage d'interface afin de développer des interfaces pour vos applications. Il existe différents types, différentes marques ou différents modèles de terminal ou de capteur à connecter à {{site.data.keyword.iot_short_notm}} et les données publiées par ces terminaux peuvent se présenter dans différents formats. Utilisez la fonction de mappage d'interface pour normaliser les données entrantes et pour simplifier vos applications en les dissociant des complexités liées à la façon dont vos terminaux spécifiques sont connectés.

Imaginons par exemple que vous possédiez deux capteurs thermiques. L'un d'eux mesure la température en degrés Celsius et l'autre en degrés Fahrenheit.

![Mappage entre des terminaux capteur thermique et une application sur {{site.data.keyword.iot_short_notm}}.](images/Information "Mappage entre des terminaux capteur thermique et une application sur {{site.data.keyword.iot_short_notm}}")

Le capteur thermique 1 publie le relevé de température `{ "t" : 34,5 }` sur {{site.data.keyword.iot_short_notm}}. La valeur indiquée dans ce relevé de température est exprimée en Celsius. Le capteur thermique 2 publie le relevé de température `{ "temp" : 72,55 }` sur {{site.data.keyword.iot_short_notm}}. Il s'agit d'un autre type de capteur thermique dont le relevé est exprimé en Fahrenheit. Les relevés de température sont publiés sous la forme d'événements distincts sur {{site.data.keyword.iot_short_notm}}.

La fonction de mappage d'interface vous permet de normaliser ces relevés afin de les rendre cohérents en vue de leur traitement. Vous n'avez pas besoin d'écrire votre application pour la compréhension ou la conversion de différentes échelles de température. L'application reçoit une seule vue normalisée et peut se connecter à **temperature** au lieu de se connecter à **t** et **temp**.

## Flux de données entre des terminaux et des applications
{: #mapping}

L'organigramme suivant illustre l'utilisation des différentes ressources dans la fonction de mappage d'interface :

![Flux entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}.](images/Information "Flux entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}")

Le diagramme suivant illustre l'utilisation de schémas dans ce flux :

![Flux entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}.](images/Information "Flux entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}")

Les schémas JSON permettent de définir et valider le format d'événements entrants et l'[état de terminal](#key_concepts). Pour plus d'informations sur ces schémas, voir [Schémas](#resources).

## Concepts clés
{: #key_concepts}

La fonction de mappage d'interface développe le concept actuel de [type de terminal](#resources) en ajoutant une ressource d'interface physique et une ressource d'interface d'application afin de mieux contrôler les données qui transitent via {{site.data.keyword.iot_short_notm}}.

Le diagramme suivant illustre le mappage logique entre des terminaux et des applications sur {{site.data.keyword.iot_short_notm}} à l'aide de [ressources](#resources) :

![Mappage logique entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "Mappage logique entre un terminal et une application sur {{site.data.keyword.iot_short_notm}}")

Le mappage d'interface fait référence au concept d'état de terminal. L'état de terminal correspond à un ensemble de propriétés définies par l'interface d'application. Les valeurs les plus récentes de ces propriétés sont stockées dans {{site.data.keyword.iot_short_notm}} et sont fournies sur demande à l'application à l'aide d'une API HTTP.

Pour traiter les données provenant d'événements entrants et mapper les propriétés de l'événement entrant aux propriétés définies sur l'interface d'application, les informations suivantes doivent être configurées :

- La structure d'un ou plusieurs événements entrants. Ces informations sont définies dans le schéma d'événement.  Chaque schéma d'événement définit la structure d'un événement entrant et est associé à un type d'événement. L'interface physique regroupe un ou plusieurs types d'événement.

    La structure et le format des données contenues dans un événement de terminal entrant est défini par un fichier schéma d'événement qui se présente au format de schéma JSON. Vous pouvez télécharger le fichier schéma d'événement sur {{site.data.keyword.iot_short_notm}} à l'aide d'une méthode POST pour créer une ressource de schéma nommée. Pour la version bêta, tous les événements entrants doivent être au format JSON.

- La structure de l'état de terminal souhaité. Ces informations sont définies dans le schéma d'interface d'application.

    L'état de terminal est une représentation de la structure de données et des données que votre application est configurée pour recevoir en tant que données du terminal. Les valeurs de propriété qui sont stockées dans l'état de terminal sont mises à jour en réponse à un événement de terminal entrant. Les valeurs d'état de terminal les plus récentes sont fournies sur demande à une application à l'aide d'une API HTTP.

- Les informations décrivant comment mapper les événements entrants à l'état de terminal préféré. Ces informations sont définies dans les mappages.

    Pour mapper les données contenues dans les propriétés d'un événement entrant aux propriétés appropriées sur l'interface d'application, vous devez créer un mappage. Le mappage explique comment mettre à jour les propriétés définies par une interface d'application spécifique en réponse à un événement entrant provenant d'un terminal.


## Ressources
{: #resources}

Vous pouvez gérer les ressources illustrées dans les diagrammes précédents à l'aide d'API REST. Pour plus d'informations sur les API REST, voir la documentation sur l'[{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).

Ressource                        | Description       
------------- | ------------- | -------------  
Schémas                         | Les schémas JSON sont utilisés pour définir la structure des événements entrants publiés sur {{site.data.keyword.iot_short_notm}} à partir de terminaux, ainsi que l'état de terminal souhaité. Pour plus d'informations sur les schémas JSON, voir [JSON Schema](http://json-schema.org/). Dans le mappage d'interface, deux schémas JSON sont référencés : le schéma d'événement et le schéma d'interface d'application. Les schémas d'événement sont utilisés pour définir la structure des événements publiés sur {{site.data.keyword.iot_short_notm}} par un terminal. Les schémas d'interface d'application sont référencés par l'interface d'application et sont utilisés pour définir la structure de l'[état de terminal](#key_concepts) qui est stocké sur {{site.data.keyword.iot_short_notm}}.
Type d'événement                         | Vous devez créer un type d'événement dans votre organisation de sorte que {{site.data.keyword.iot_short_notm}} puisse traiter les données contenues dans un événement spécifique. Tous les types d'événement doivent faire référence à un schéma d'événement. Pour la version bêta, tous les événements entrants doivent être au format JSON.   
Interface physique                         | L'interface physique peut être associée à un ou plusieurs types d'événement et définit les types d'événement qui sont associés à un type de terminal.  
Type de terminal                         | Chaque terminal connecté à Watson IoT Platform est associé à un type de terminal. Les types de terminal sont des groupes de terminaux ayant des caractéristiques ou des comportements communs. Dans le mappage d'interface, le type de terminal est étendu de manière à inclure une interface physique pour un terminal et une interface d'application qui peut être utilisée pour extraire l'état de terminal. Un type de terminal peut être configuré avec plusieurs interfaces d'application. Pour plus d'informations sur les types de terminal, voir la section "Identificateurs et type de terminal" dans [Modèle d'unité](../reference/device_model.html#id_and_device_types).
Interface d'application                         | L'interface d'application doit faire référence à un schéma d'interface d'application. Dans une interface d'application, vous pouvez définir la structure des données qui sont stockées en tant qu'état de terminal. L'état de terminal est une représentation de la structure de données et des données qu'une application est configurée pour recevoir en tant que données du terminal. Au moins une interface d'application doit être associée à un type de terminal pour que des mappages puissent être définis.
Mappages                         | Les mappages décrivent de quelle façon les propriétés associées à des événements entrants sont mappées aux propriétés définies sur une interface d'application spécifique. Un mappage doit spécifier l'identificateur d'interface d'application auquel il s'applique et l'interface d'application doit être associée au type de terminal auquel le mappage est ajouté.


## Flux de travaux de niveau supérieur
{: #workflow}



### Description de la tâche

Utilisez les étapes décrites ci-après pour vous aider à configurer les ressources dont vous avez besoin pour commencer à mapper vos données de terminal à l'aide d'interfaces.

Pour plus d'informations sur l'API, voir la documentation sur l'[{{site.data.keyword.iot_short_notm}} API REST HTTP](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).
Pour plus d'informations sur chacune de ces étapes, reportez-vous à l'[exemple de scénario](#scenario) ou cliquez sur les liens pour accéder directement à une étape spécifique dans l'exemple de scénario.

### Configuration de votre environnement pour commencer à utiliser des interfaces dans le but de mapper des données de terminal

1.  Si nécessaire, ajoutez un type de terminal et un terminal

  1. Créez un type de terminal en utilisant la méthode POST de l'API REST avec l'URI suivant :
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Le cas échéant, ajoutez un terminal.  
Pour plus d'informations sur l'ajout d'un type de terminal et d'un terminal, voir [Connexion de terminaux](../iotplatform_task.html#devices)

2. Créez une interface physique

  1. [Créez un fichier schéma d'événement](#step1). Il s'agit d'un fichier .JSON local qui définit la structure et le format d'un événement entrant.

  2. [Créez une ressource de schéma d'événement pour votre type d'événement](#step2) en utilisant la méthode POST de l'API REST avec l'URI suivant :
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Créez un type d'événement qui fait référence au schéma d'événement](#step3) en utilisant la méthode POST de l'API REST avec l'URI suivant :
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Ajoutez le type d'événement à votre schéma d'événement à l'aide de l'identificateur de schéma qui a été renvoyé en réponse à la méthode POST utilisée pour créer la ressource de schéma d'événement.

  4. [Créez une interface physique](#step7) en utilisant la méthode POST de l'API REST avec l'URI suivant :
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Ajoutez le type d'événement à l'interface physique](#step8) en utilisant la méthode POST de l'API REST avec l'URI suivant :
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Ajoutez le type d'événement à votre interface physique en utilisant l'identificateur *eventId* de la rubrique et l'identificateur de type d'événement *eventTypeId* qui a été renvoyé en réponse à la méthode POST utilisée pour créer le type d'événement.       

3. Ajoutez votre interface physique à votre type de terminal       

      [Mettez à jour le type de terminal pour connecter l'interface physique](#step9) en utilisant la méthode PUT de l'API REST avec l'URI suivant :
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Créez une interface d'application

  1. [Créez un fichier schéma d'interface d'application](#step4). Un fichier schéma d'interface d'application est un fichier .JSON local qui définit l'état de terminal.

  2. [Créez une ressource de schéma d'interface d'application](#step5) en utilisant la méthode POST de l'API REST avez l'URI suivant :
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Créez une interface d'application qui fait référence à un schéma d'interface d'application](#step6) en utilisant la méthode POST de l'API REST avec l'URI suivant :
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        L'interface d'application fait référence au schéma d'interface d'application à l'aide de l'identificateur de schéma qui a été renvoyé en réponse à la méthode POST utilisée pour créer la ressource de schéma d'interface d'application.

  4. [Ajoutez l'interface d'application à un type de terminal](#step10) en utilisant la méthode POST de l'API REST avec l'URI suivant :
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Ajoutez votre interface d'application à votre type de terminal en utilisant la réponse à la méthode POST qui a été utilisée pour créer l'interface d'application.

5. Définissez les mappages pour le type de terminal

  [Définissez les mappages permettant de mapper les propriétés de l'événement entrant aux propriétés de l'interface d'application](#step11) en utilisant la méthode POST de l'API REST avec l'URI suivant :       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Déployez la configuration qui est associée à votre type de terminal

  [Déployez la configuration](#step15) sur {{site.data.keyword.iot_short_notm}} en utilisant la méthode PATCH de l'API REST avec l'URI suivant :
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Assurez-vous que les événements de terminal mappés sont publiés sur l'interface d'application

  1. [Publiez un événement de terminal entrant](#step12)

  2. [Assurez-vous que l'état du terminal est modifié](#step13) en utilisant la méthode GET de l'API REST avec l'URI suivant :
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Exemple de scénario
{: #scenario}

Utilisez les informations ci-dessous pour créer un scénario dans lequel deux capteurs thermiques publient des événements sur {{site.data.keyword.iot_short_notm}}. L'un de ces capteurs mesure la température en degrés Celsius. L'autre capteur mesure la température en degrés Fahrenheit. Ces relevés sont mappés à un seul relevé de température exprimé en degrés Celsius. Lorsqu'un nouveau relevé de température est publié par ces terminaux, la valeur de la propriété associée à l'état de terminal est modifiée.

### Conditions prérequises

Vous devez disposer d'une instance d'organisation {{site.data.keyword.iot_short_notm}} et d'une clé d'API ou d'un jeton pour cette organisation. Pour plus d'informations sur les clés d'API et les jetons, voir [API REST HTTP pour les applications](../applications/api.html#authentication).

### Description de ce scénario

Dans ce scénario, deux terminaux sont configurés.

L'un des terminaux se nomme *TemperatureSensor1*. Ce terminal publie des événements de température qui sont mesurés en degrés Celsius. L'événement de température est publié sur la rubrique `iot-2/evt/tevt/fmt/json` et comporte l'exemple de contenu suivant :
```
{
  "t" : 34,5
}
```

**Remarque :** L'identificateur d'évènement est *tevt*. Cet identificateur est requis lorsque vous ajoutez un événement de température de ce type à l'interface physique et lorsque vous définissez des mappages dans le but de mapper une propriété associée à un événement entrant de ce type à une propriété définie dans votre interface d'application. Dans ce scénario, la propriété définie dans l'interface d'application se nomme **temperature**.

L'autre terminal se nomme *TemperatureSensor2*. Ce terminal publie des événements de température qui sont mesurés en degrés Fahrenheit. L'événement de température est publié sur la rubrique `iot-2/evt/tempevt/fmt/json` et comporte l'exemple de contenu suivant :
```
{
  "temp" : 72,55
}
```

**Remarque :** L'identificateur d'évènement est *tempevt*. Cet identificateur est requis lorsque vous ajoutez un événement de température de ce type à l'interface physique et lorsque vous définissez des mappages dans le but de mapper une propriété associée à un événement entrant de ce type à une propriété définie dans votre interface d'application. Dans ce scénario, la propriété définie dans l'interface d'application se nomme **temperature**.

Une interface d'application est également configurée. Cette interface d'application représente l'état des terminaux de ce type dans la structure suivante :
```
{
  "temperature" : <valeur de température en cours exprimée en degrés Celsius>
  }
```
Cette configuration signifie que vous pouvez configurer votre application pour traiter la valeur qui est associée à **temperature** au lieu de configurer votre application pour traiter la valeur qui est associée à **t** et pour traiter la valeur qui est associée à **temp** après la conversion de cette valeur en degrés Celsius.

## Procédure

Utilisez les informations suivantes pour configurer l'exemple de scénario à l'aide d'interfaces.

### Si nécessaire, ajoutez un type de terminal et un terminal
{: #step14}

Ce scénario part du principe qu'il existe deux types de terminal et deux instances de terminal. L'instance de terminal *TemperatureSensor1* est associée au type de terminal *EnvSensor1*. L'instance de terminal *TemperatureSensor2* est associée au type de terminal *EnvSensor2*.

Pour plus d'informations sur l'utilisation des API REST pour ajouter un type de terminal, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

### Créez un fichier schéma d'événement
{: #step1}

Pour les besoins de ce scénario, créez deux fichiers schéma d'événement afin de définir la structure de chaque événement de température entrant.

L'exemple suivant montre comment créer un fichier schéma nommé *tEventSchema.json*. Ce fichier définit la structure d'un événement entrant à partir d'un capteur thermique qui mesure la température en degrés Celsius :

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Celsius",
  "properties" : {
    "t" : {
      "description" : "temperature in degrees Celsius",
      "type" : "number",
      "minimum" : -273.15,
      "default" : 0.0
    }
  },
  "required" : ["t"]
}
  ```

Le nom de fichier schéma *tEventSchema* est utilisé lorsque vous créez une ressource de schéma d'événement pour votre type d'événement.

L'exemple suivant explique comment créer un fichier schéma nommé *tempEventSchema.json*. Ce fichier définit la structure d'un événement entrant à partir d'un capteur thermique qui mesure la température en degrés Fahrenheit :

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : "defines the structure of a temperature event in degrees Fahrenheit",
  "properties" : {
    "temp" : {
      "description" : "temperature in degrees Fahrenheit",
      "type" : "number",
      "minimum" : −459.67,
      "default" : 0.0
    }
  },
  "required" : ["temp"]
}
  ```
Le nom de fichier schéma *tempEventSchema* est utilisé lorsque vous créez une ressource de schéma d'événement pour votre type d'événement.   

### Créez une ressource de schéma d'événement pour votre type d'événement
{: #step2}

Pour créer une ressource de schéma d'événement, utilisez l'API suivante :

```
POST /schemas
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

L'exemple suivant montre comment utiliser cURL pour créer la ressource de schéma d'événement *tEventSchema.json* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "name" : "tEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "contentType" : "application/octet-stream",
  "updated" : "2016-12-06T14:38:52Z",
  "schemaFileName" : "tEventSchema.json",
  "created" : "2016-12-06T14:38:52Z",
  "id" : "5846cd7c6522050001db0e0d",
  "refs" : {
      "content" : "/schemas/5846cd7c6522050001db0e0d/content"
  },
  "schemaType" : "json-schema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificateur de schéma *5846cd7c6522050001db0e0d* qui est renvoyé en réponse à la méthode POST est requis lorsque vous ajoutez un schéma d'événement à votre type d'événement.

L'exemple suivant montre comment utiliser cURL pour créer la ressource de schéma d'événement *tempEventSchema.json* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "schemaType" : "json-schema",
  "schemaFileName" : "tempEventSchema.json",
  "updated" : "2016-12-06T14:44:51Z",
  "name" : "tempEventSchema",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "created" : "2016-12-06T14:44:51Z",
  "id" : "5846cee36522050001db0e0e",
  "refs" : {
      "content" : "/schemas/5846cee36522050001db0e0e/content"
  },
  "contentType" : "application/octet-stream",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificateur de schéma *5846cee36522050001db0e0e* qui est renvoyé en réponse à la méthode POST est requis lorsque vous ajoutez un schéma d'événement à votre type d'événement.

### Créez un type d'événement qui fait référence au schéma d'événement
{: #step3}

Chaque type d'événement fait référence au schéma d'événement approprié qui a été créé dans l'exemple précédent à l'aide de l'identificateur de schéma renvoyé dans la réponse à la méthode POST utilisée pour créer la ressource de schéma d'événement.

Pour créer un type d'événement, utilisez l'API suivante :

```
POST /event/types
```

Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


L'exemple suivant montre comment utiliser cURL afin de créer un type d'événement pour un événement de température mesuré en degrés Celsius :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
```

L'identificateur de schéma *5846cd7c6522050001db0e0d* est utilisé pour ajouter le schéma d'événement au type d'événement. Cet identificateur a été renvoyé en réponse à la méthode POST qui a été utilisée pour créer la ressource de schéma d'événement *tEventSchema.json*.

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "updated" : "2016-12-06T14:53:49Z",
  "schemaId" : "5846cd7c6522050001db0e0d",
  "refs" : {
    "schema" : "/schemas/5846cd7c6522050001db0e0d"
  },
  "name" : "tEvent",
  "created" : "2016-12-06T14:53:49Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846d0fd6522050001db0e0f",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificateur de type d'événement *5846d0fd6522050001db0e0f* qui est renvoyé en réponse à la méthode POST est utilisé pour ajouter un type d'événement à l'interface physique.

L'exemple suivant montre comment utiliser cURL afin de créer un type d'événement pour un événement de température mesuré en degrés Fahrenheit :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
L'identificateur de schéma *5846cee36522050001db0e0e* est utilisé pour ajouter le schéma d'événement au type d'événement. Cet identificateur a été renvoyé en réponse à la méthode POST qui a été utilisée pour créer la ressource de schéma d'événement *tempEventSchema.json*.

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificateur de type d'événement *5846d2846522050001db0e10* qui est renvoyé en réponse à la méthode POST est utilisé pour ajouter un type d'événement à l'interface physique.

### Créez une interface physique
{: #step7}

Pour créer une interface physique, utilisez l'API suivante :

```
POST /physicalinterfaces
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Dans ce scénario, nous avons besoin de deux interfaces physiques, une pour chaque type d'événement.

L'exemple suivant montre comment utiliser cURL pour créer la première interface physique :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
  },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificateur d'interface physique *5847d1df6522050001db0e1a* qui est renvoyé dans la réponse est utilisé dans l'URL de la méthode POST appelée pour ajouter un événement de température mesuré en degrés Celsius à l'interface physique.

L'exemple suivant montre comment utiliser cURL pour créer la seconde interface physique :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
    "events" : "/physicalinterfaces/5847d1df6522050001db0e1b/events"
  },
  "id" : "5847d1df6522050001db0e1b",
  "name" : "Env sensor physical interface 2",
  "created" : "2016-12-07T09:19:51Z",
  "updated" : "2016-12-07T09:19:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
}
```

L'identificateur d'interface physique *5847d1df6522050001db0e1b* qui est renvoyé dans la réponse est utilisé dans l'URL de la méthode POST appelée pour ajouter un événement de température mesuré en degrés Fahrenheit à l'interface physique.   

### Ajoutez le type d'événement à l'interface physique
{: #step8}

Pour ajouter un type d'événement à votre interface physique, utilisez l'API suivante :

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Dans ce scénario, les types d'événement suivants sont ajoutés aux interfaces physiques spécifiées :
- L'événement de température exprimé en degrés Celsius, *tevt*, est ajouté à l'interface physique avec l'identificateur *5847d1df6522050001db0e1a* à l'aide de l'identificateur *eventId* issu de la rubrique et de l'identificateur *eventTypeId* issu de la création de la ressource de schéma d'événement.
- L'événement de température exprimé en degrés Fahrenheit, *tempevt*, est ajouté à l'interface physique avec l'identificateur *5847d1df6522050001db0e1b* à l'aide de l'identificateur *eventId* issu de la rubrique et de l'identificateur *eventTypeId* issu de la création de la ressource de schéma d'événement.


L'exemple suivant montre comment utiliser cURL pour ajouter l'événement de température *tevt* à l'interface physique avec l'identificateur *5847d1df6522050001db0e1a* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

L'exemple suivant montre comment utiliser cURL pour ajouter l'événement de température *tempevt* à l'interface physique avec l'identificateur *5847d1df6522050001db0e1b* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : "tempevt"
}
```

### Mettez à jour le type de terminal pour connecter l'interface physique
{: #step9}

Pour mettre à jour un type de terminal, utilisez l'API suivante :

```
PUT /device/types/{typeId}
```

Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}} ](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Dans ce scénario, le type de terminal *EnvSensor1* est mis à jour pour se connecter à l'interface physique *5847d1df6522050001db0e1a* et le type de terminal *EnvSensor2* est mis à jour pour se connecter à l'interface physique *5847d1df6522050001db0e1b*.

L'exemple suivant montre comment utiliser cURL pour mettre à jour le type de terminal *EnvSensor1* :

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1a",
  "updatedDateTime" : "2016-12-07T09:49:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor1/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor1/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1a"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
L'identificateur de terminal *EnvSensor1* est requis lorsque vous ajoutez votre interface physique et votre interface d'application.

L'exemple suivant montre comment utiliser cURL pour mettre à jour le type de terminal *EnvSensor2* :

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "deviceInfo" : {},
  "physicalInterfaceId" : "5847d1df6522050001db0e1b",
  "updatedDateTime" : "2016-12-07T09:59:52+00:00",
  "refs" : {
    "mappings" : "/device/types/EnvSensor2/mappings",
    "applicationInterfaces" : "/device/types/EnvSensor2/applicationinterfaces",
    "physicalInterface" : "/physicalinterfaces/5847d1df6522050001db0e1b"
   },
  "id" : "EnvironmentSensor",
  "description" : "an environment sensor",
  "metadata" : {},
  "classId" : "Device",
  "createdDateTime" : "2016-12-07T09:49:52+00:00"
}
```
L'identificateur de terminal *EnvSensor2* est requis lorsque vous ajoutez votre interface physique et votre interface d'application.



### Créez un fichier schéma d'interface d'application
{: #step4}

L'exemple suivant montre comment créer un fichier schéma d'interface d'application nommé *envSensor.json*.

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
    "type" : "object",
    "title" : "Environment Sensor Schema",
    "description" : "Schema to represent a canonical environment sensor device",
    "properties" : {
        "temperature" : {
            "description" : "temperature in degrees Celsius",
            "type" : "number",
            "minimum" : -273.15,
            "default" : 0.0
        }
    },
    "required" : ["temperature"]
}
```

### Créez une ressource de schéma d'interface d'application
{: #step5}

Pour créer une ressource de schéma d'interface d'application, utilisez l'API suivante :

```
POST /schemas
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

L'exemple suivant montre comment utiliser cURL pour créer le schéma d'interface d'application :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "created" : "2016-12-06T16:51:14Z",
  "name" : "temperatureEventSchema",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "updated" : "2016-12-06T16:51:14Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "schemaType" : "json-schema",
  "contentType" : "application/octet-stream",
  "schemaFileName" : "envSensor.json",
  "refs" : {
    "content" : "/schemas/5846ec826522050001db0e11/content"
  },
  "id" : "5846ec826522050001db0e11"
}
```
Utilisez l'identificateur de schéma *5846ec826522050001db0e11* qui est renvoyé dans la réponse à la méthode POST pour ajouter le schéma d'interface d'application à l'interface d'application.

### Créez une interface d'application qui fait référence à un schéma d'interface d'application
{: #step6}

Pour créer une interface d'application, utilisez l'API suivante :

```
POST /applicationinterfaces
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

Dans ce scénario, utilisez l'identificateur de schéma *5846ec826522050001db0e11* qui a été renvoyé dans la réponse précédente pour ajouter le schéma d'interface d'application à l'interface d'application.

L'exemple suivant montre comment utiliser cURL pour créer une interface d'application :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "schemaId" : "5846ec826522050001db0e11",
  "created" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "id" : "5846ed076522050001db0e12",
  "updated" : "2016-12-06T16:53:27Z",
  "name" : "environment sensor interface"
}
```
Dans ce scénario, utilisez l'identificateur d'interface d'application *5846ed076522050001db0e12* qui est renvoyé dans la réponse à la méthode POST pour ajouter votre interface d'application à votre type de terminal. Vous pouvez également utiliser cet identificateur pour mapper un événement de terminal entrant à une propriété qui est définie par l'interface d'application.

### Ajoutez l'interface d'application à un type de terminal
{: #step10}

Pour ajouter une interface d'application à un type de terminal, utilisez l'API suivante :

```
POST /device/types/{typeId}/applicationinterfaces
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}} ](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Dans ce scénario, l'interface d'application est associée au type de terminal *EnvSensor1* et au type de terminal *EnvSensor2*.

L'exemple suivant montre comment utiliser cURL pour ajouter l'interface d'application *5846ed076522050001db0e12* qui fait référence à l'identificateur de schéma d'application *5846ec826522050001db0e11* au type de terminal *EnvSensor1* :

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
        }'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

L'exemple suivant montre comment utiliser cURL pour ajouter l'interface d'application *5846ed076522050001db0e12* associée à l'identificateur de schéma d'application *5846ec826522050001db0e11* au type de terminal *EnvSensor2* :

```
curl --request POST \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/applicationinterfaces \
--header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
--header 'content-type: application/json' \
--data '{"createdBy" : "a-8x7nmj-9iqt56kfil", \
          "refs" : {
              "schema" : "/schemas/5846ec826522050001db0e11"
          },
          "schemaId" : "5846ec826522050001db0e11", "created" : "2016-12-06T16:53:27Z", \
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
        }'
```


L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "refs" : {
      "schema" : "/schemas/5846ec826522050001db0e11"
  },
  "updated" : "2016-12-06T16:53:27Z",
  "updatedBy" : "a-8x7nmj-9iqt56kfil",
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "name" : "environment sensor interface",
  "created" : "2016-12-06T16:53:27Z",
  "id" : "5846ed076522050001db0e12",
  "schemaId" : "5846ec826522050001db0e11"
}
```

### Définissez les mappages permettant de mapper les propriétés de l'événement entrant aux propriétés de l'interface d'application
{: #step11}

Pour mapper des événements, utilisez l'API suivante :

```
POST /device/types/{typeId}/mappings
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}} ](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Dans ce scénario, nous définissons des mappages pour le type de terminal *EnvSensor1* afin de mapper la propriété **t** de l'événement entrant *tevt* à la propriété **temperature** de l'interface d'application. Nous définissons également des mappages pour le type de terminal *EnvSensor2* afin de mapper la propriété **temp** de l'événement entrant *tempevt* à la propriété **temperature** de l'interface d'application.

L'exemple suivant montre comment utiliser cURL pour ajouter un mappage au type de terminal *EnvSensor1* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tevt" : {
                  "temperature" : "$event.t"
              }
            }
          }'
```

Spécifiez l'identificateur d'interface d'application *5846ed076522050001db0e12* qui est renvoyé dans la réponse à la méthode POST utilisée pour créer l'interface d'application et le type de terminal *EnvSensor1*.

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "propertyMappings" : {
      "tevt" : {
       "temperature" : "$event.t"
              }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```
L'exemple suivant montre comment utiliser cURL pour ajouter un mappage au type de terminal *EnvSensor2* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/mappings \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"applicationInterfaceId" : "5846ed076522050001db0e12","propertyMappings" : {
              "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
              }
            }
          }'
```

Spécifiez l'identificateur d'interface d'application *5846ed076522050001db0e12* qui est renvoyé dans la réponse à la méthode POST utilisée pour créer l'interface d'application et le type de terminal *EnvSensor2*.
Une conversion est appliquée pour modifier la valeur mesurée en degrés Fahrenheit en une valeur mesurée en degrés Celsius.


L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "propertyMappings" : {
    "tempevt" : {
      "temperature" : "($event.temp - 32) / 1.8"
    }
  },
  "applicationInterfaceId" : "5846ed076522050001db0e12"
}
```

### Déployez la configuration
{: #step15}

Déployez la configuration relative à la mise à jour d'état de terminal pour chaque type de terminal. Cette configuration inclut vos schémas, types d'événement, interfaces physiques, interfaces d'application et mappages.

Pour déployer votre configuration de type de terminal, utilisez l'API suivante :

```
PATCH /device/types/{typeId}
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}} ](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Dans ce scénario, nous devons déployer une configuration pour deux types de terminal.

L'exemple suivant montre comment utiliser cURL afin de déployer la configuration pour le type de terminal *EnvSensor1* :

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

L'exemple suivant illustre une réponse à la méthode PATCH :

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor1' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor1"]
  },
 "failures": []
}
```

L'exemple suivant montre comment utiliser cURL afin de déployer la configuration pour le type de terminal *EnvSensor2* :

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

L'exemple suivant illustre une réponse à la méthode PATCH :

```
{
 "message": "CUDRS0520I: State update configuration for device type 'EnvSensor2' has been successfully submitted for deployment",
  "details": {
    "id": "CUDRS0520I",
    "properties": ["EnvSensor2"]
  },
 "failures": []
}
```

### Publiez un événement de terminal entrant
{: #step12}

Publiez un événement de température issu de *TemperatureSensor1* sur la rubrique `iot-2/evt/tevt/fmt/json` et un événement de température issu de *TemperatureSensor2* sur la rubrique `iot-2/evt/tempevt/fmt/json`.

Pour plus d'informations sur la publication d'un événement entrant à partir d'un terminal, voir [Connectivité MQTT pour les applications](../applications/mqtt.html#publishing_device_events).


### Assurez-vous que l'état du terminal est modifié
{: #step13}

Pour vérifier l'état de terminal, utilisez l'API suivante :
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
Pour plus d'informations, voir la documentation sur l'[API REST HTTP {{site.data.keyword.iot_short_notm}} ](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

L'exemple suivant montre comment utiliser cURL pour extraire l'état en cours de *TemperatureSensor1* en faisant référence à l'identificateur de l'interface d'application qui a été créée :
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificateur d'interface d'application *5846ed076522050001db0e12* est utilisé dans la méthode GET. Cet identificateur est renvoyé dans la réponse à la méthode POST qui a été utilisée pour créer l'interface d'application.
L'exemple suivant illustre une réponse à la méthode GET :
```
{
  "temperature":34,5
}
```
L'exemple suivant montre comment utiliser cURL pour extraire l'état en cours de *TemperatureSensor2* en faisant référence à l'identificateur de l'interface d'application qui a été créée :
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificateur d'interface d'application *5846ed076522050001db0e12* est utilisé dans la méthode GET. Cet identificateur est renvoyé dans la réponse à la méthode POST qui a été utilisée pour créer l'interface d'application.
L'exemple suivant illustre une réponse à la méthode GET :
```
{
  "temperature" : 22,5
}
```
Notez que le relevé de température qui est renvoyé est exprimé en degrés Celsius et non en degrés Fahrenheit.

Votre application peut traiter ces données normalisées sans qu'aucune configuration ne soit nécessaire pour comprendre ou convertir les différentes échelles de température.
