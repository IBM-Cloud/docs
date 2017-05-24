---

copyright:
years: 2016, 2017
lastupdated: "2017-04-10"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Interface d'application : scénario 1 (bêta)
{: #scenario}

Utilisez les informations suivantes pour créer un scénario dans lequel deux
capteurs de température publient des événements sur
{{site.data.keyword.iot_short_notm}}. L'un de ces capteurs mesure la température en degrés Celsius. L'autre capteur mesure la température en degrés Fahrenheit. Ces mesures
sont mappées à un unique relevé de température exprimé en degrés Celsius. Lorsqu'une nouvelle mesure de température est publiée par ces terminaux, la valeur de la
propriété associée à l'état du terminal concerné change.

## Conditions prérequises

Vous devez disposer d'une instance d'organisation {{site.data.keyword.iot_short_notm}} et d'une clé d'API ou d'un jeton pour cette organisation. Pour plus d'informations sur les clés d'API et les jetons, consultez
[API REST HTTP pour les
applications](../applications/api.html#authentication).

## A propos de cette tâche

Dans ce scénario, deux terminaux sont configurés.

L'un des terminaux se nomme *TemperatureSensor1*. Ce terminal publie des événements de température qui sont mesurés en degrés Celsius. L'événement de température est publié sur la rubrique (topic)
`iot-2/evt/tevt/fmt/json` et comporte l'exemple de contenu suivant :
```
{
  “t” : 34.5
}
```

**Remarque :** L'identificateur d'événement est *tevt*. Cet identificateur est requis lorsque vous ajoutez un événement de température de ce type à l'interface physique et lorsque vous définissez des mappages dans le but de mapper une propriété associée à un événement entrant de ce type à une propriété définie dans votre interface d'application. Dans ce scénario, la propriété définie dans l'interface d'application se nomme **temperature**.

L'autre terminal se nomme *TemperatureSensor2*. Ce terminal publie des événements de température qui sont mesurés en degrés Fahrenheit. L'événement de température est publié sur la rubrique `iot-2/evt/tempevt/fmt/json` et comporte l'exemple de contenu suivant :
```
{
  “temp” : 72.55
}
```

**Remarque :** L'identificateur d'événement est *tempevt*. Cet identificateur est requis lorsque vous ajoutez un événement de température de ce type à l'interface physique et lorsque vous définissez des mappages dans le but de mapper une propriété associée à un événement entrant de ce type à une propriété définie dans votre interface d'application. Dans ce scénario, la propriété définie dans l'interface d'application se nomme **temperature**.

Une interface d'application est également configurée. Cette interface d'application représente l'état des terminaux de ce type dans la structure suivante :
```
{
  “temperature” : <valeur de température actuelle exprimée en degrés Celsius>
  }
```
Cette configuration signifie que vous pouvez configurer votre application pour traiter la
valeur associée à **temperature** au lieu de la configurer
pour traiter d'une part la valeur associée à **t**, d'autre
part la valeur associée à **temp** après sa conversion
en degrés Celsius.

![Mappage entre terminaux du type capteur de température et une application sur {{site.data.keyword.iot_short_notm}}.](images/Information "Mappage entre terminaux du type capteur de température et une application sur {{site.data.keyword.iot_short_notm}}")  

Utilisez l'exemple suivant pour mettre en place votre propre environnement d'interfaces.

## Si nécessaire, ajoutez un type de terminal et un terminal
{: #step14}

Dans ce scénario, on utilise deux types de terminaux et deux instances de terminaux. L'instance de terminal *TemperatureSensor1* est associée au type de terminal *EnvSensor1*. L'instance de terminal *TemperatureSensor2* est associée au type de terminal *EnvSensor2*.

Pour plus d'informations sur l'utilisation de l'API REST servant à ajouter un type de
terminal, consultez la documentation correspondante dans le document
[API
REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types) (en anglais).

## Etape 1 : créez un fichier schéma d'événement
{: #step1}

Pour les besoins de ce scénario, créez deux fichiers schéma d'événement afin de définir la structure de chaque événement de température entrant.

**Important :** pour les charges utiles à
structure [JSON ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://json-schema.org/){:new_window},
assurez-vous que chaque niveau d'imbrication est correctement enveloppé dans une entrée `"properties"`. Par exemple, si la charge utile était `{"d":{"t":<temp>}}`, vous pourriez utiliser la structure suivante :
```
 "properties" : {
    "d" : {
      "properties" : {
        "t" : {
          "description" : "Temperature in degrees Celsius",
          "type" : "number",
          "minimum" : -273.15,
          "default" : 0.0
        }
      },
      "required" : ["t"]
    }
  },
  "required" : ["d"]
```

L'exemple suivant montre comment créer un fichier schéma nommé *tEventSchema.json*. Ce fichier définit la structure d'un événement entrant, issu d'un capteur de température
mesurant la température en degrés Celsius :

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor1 tEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Celsius",
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
**Astuce :** Utilisez le paramètre “required” pour indiquer qu'une propriété est requise. Les propriétés requises doivent être incluses dans un message de terminal afin que
Watson IoT Platform mette à jour l'état d'un terminal avec les données de ce terminal. Un message qui n'inclut pas de propriété requise n'est pas traité.   

Le nom de fichier schéma *tEventSchema* est utilisé lorsque vous créez une ressource Schéma d'événement pour votre type d'événement.

L'exemple suivant montre comment créer un fichier schéma nommé *tempEventSchema.json*. Ce fichier définit la structure d'un événement entrant, issu d'un capteur de température
mesurant la température en degrés Fahrenheit :

```
{
  "$schema": "http://json-schema.org/draft-04/schema#",
  "type" : "object",
  "title" : "EnvSensor2 tempEvent Schema",
  "description" : “defines the structure of a temperature event in degrees Fahrenheit",
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
Le nom de fichier schéma *tempEventSchema* est utilisé lorsque vous créez une ressource Schéma d'événement pour votre type d'événement.   

## Etape 2 : créez une ressource Schéma d'événement pour votre type d'événement
{: #step2}

Pour créer une ressource Schéma d'événement, utilisez l'API suivante :

```
POST /schemas
```

Les paramètres suivants sont requis :  

Paramètre	|	Description  
------	|	-----  
name	|	Nom que vous donnez au schéma d'événement que vous créez.  
schemaFile	|	Chemin du fichier JSON local contenant le schéma d'événement.  



Pour plus d'informations, consultez la documentation de l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) (en anglais).

L'exemple suivant montre comment utiliser cURL pour créer la ressource Schéma d'événement *tEventSchema.json* :

```curl
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
  "name" : “tEventSchema",
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

L'exemple suivant montre comment utiliser cURL pour créer la ressource Schéma d'événement *tempEventSchema.json* :

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

## Etape 3 : créez un type d'événement qui fasse référence au schéma d'événement
{: #step3}

Chaque type d'événement fait référence à un schéma d'événement adéquat parmi ceux qui ont été
créés dans l'exemple précédent. Il utilise à cet effet l'identificateur de schéma figurant dans la
réponse à la méthode POST utilisée pour créer la ressource Schéma d'événement.

Pour créer un type d'événement, utilisez l'API suivante :

```
POST /event/types
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
name	|	Nom que vous donnez au type d'événement que vous créez.
schemaId	|	Identificateur créé précédemment pour la ressource Schéma d'événement.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types) (en anglais).


L'exemple suivant montre comment utiliser cURL afin de créer un type d'événement pour un événement de température mesuré en degrés Celsius :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

L'identificateur de schéma *5846cd7c6522050001db0e0d* est utilisé pour ajouter le schéma d'événement au type d'événement. Cet identificateur a été renvoyé en réponse à la méthode POST qui a été utilisée pour créer la ressource Schéma d'événement *tEventSchema.json*.

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
L'identificateur de schéma *5846cee36522050001db0e0e* est utilisé pour ajouter le schéma d'événement au type d'événement. Cet identificateur a été renvoyé en réponse à la méthode POST qui a été utilisée pour créer la ressource Schéma d'événement *tempEventSchema.json*.

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "createdBy" : "a-8x7nmj-9iqt56kfil",
  "schemaId" : "5846cee36522050001db0e0e",
  "created" : "2016-12-06T15:00:20Z",
  "id" : "5846d2846522050001db0e10",
  "updated" : "2016-12-06T15:00:20Z",
  "name" : “tempEvent”,
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
L'identificateur de type d'événement *5846d2846522050001db0e10* qui est renvoyé en réponse à la méthode POST est utilisé pour ajouter un type d'événement à l'interface physique.

## Etape 4 : créez une interface physique
{: #step7}

Pour créer une interface physique, utilisez l'API suivante :

```
POST /physicalinterfaces
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
name	|	Nom que vous donnez à l'interface physique que vous créez.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) (en anglais).

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

## Etape 5 : ajoutez le type d'événement à l'interface physique
{: #step8}

Pour ajouter un type d'événement à votre interface physique, utilisez l'API suivante :

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
eventId	|	Nom d'événement issu de la charge utile de l'événement émis par le terminal.
eventTypeId	|	Identificateur créé précédemment pour le type d'événement.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces) (en anglais).

Dans ce scénario, les types d'événement suivants sont ajoutés aux interfaces physiques spécifiées :
- L'événement de température en degrés Celsius, *tevt*, est ajouté à l'interface physique dont
l'identificateur est *5847d1df6522050001db0e1a* en utilisant l'*eventId* issu de la rubrique (topic)
et l'*eventTypeId* résultant de la création de la ressource Schéma d'événement.
- L'événement de température en degrés Fahrenheit, *tempevt*,
est ajouté à l'interface physique dont l'identificateur
est *5847d1df6522050001db0e1b* en utilisant l'*eventId* issu de la rubrique (topic) et
l'*eventTypeId* résultant de la création de la ressource Schéma d'événement.


L'exemple suivant montre comment utiliser cURL pour ajouter l'événement de
température *tevt* à l'interface physique dont l'identificateur
est *5847d1df6522050001db0e1a* :

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

L'exemple suivant illustre une réponse à la méthode POST :

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

L'exemple suivant montre comment utiliser cURL pour ajouter l'événement de
température *tempevt* à l'interface physique dont l'identificateur
est *5847d1df6522050001db0e1b* :

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
  "eventId" : “tempevt"
}
```

## Etape 6 : mettez à jour le type de terminal pour connecter l'interface physique
{: #step9}

Pour mettre à jour un type de terminal, utilisez l'API suivante :

```
PUT /device/types/{typeId}
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
physicalInterfaceId	|	Identificateur créé pour l'interface physique.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

Dans ce scénario, le type de terminal *EnvSensor1* est mis à jour pour se connecter à l'interface physique *5847d1df6522050001db0e1a* et le type de terminal *EnvSensor2* est mis à jour pour se connecter à l'interface physique *5847d1df6522050001db0e1b*.

L'exemple suivant montre comment utiliser cURL pour mettre à jour le type de terminal *EnvSensor1* :

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
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
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b”}’
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



## Etape 7 : créez un fichier schéma d'interface d'application
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

## Etape 8 : créez une ressource Schéma d'interface d'application
{: #step5}

Pour créer une ressource Schéma d'interface d'application, utilisez l'API suivante :

```
POST /schemas
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
name	|	Nom que vous donnez au schéma d'interface d'application que vous créez.
schemaFile	|	Chemin du fichier JSON local contenant le schéma d'interface d'application.


Pour plus d'informations, consultez la documentation de l'[API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas) (en anglais).

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
Utilisez l'identificateur de schéma *5846ec826522050001db0e11* retourné dans la réponse à la méthode POST pour
ajouter le schéma d'interface d'application à l'interface d'application.

## Etape 9 : créez une interface d'application faisant référence à un schéma d'interface d'application
{: #step6}

Pour créer une interface d'application, utilisez l'API suivante :

```
POST /applicationinterfaces
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
name	|	Nom que vous donnez à l'interface d'application que vous créez.
schemaId	|	Identificateur créé précédemment pour la ressource Schéma d'interface d'application.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces) (en anglais).

Dans ce scénario, utilisez l'identificateur de schéma
*5846ec826522050001db0e11* qui a été renvoyé dans la réponse précédente pour
ajouter le schéma d'interface d'application à l'interface d'application.

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
Dans ce scénario, utilisez l'identificateur d'interface d'application
*5846ed076522050001db0e12* retourné dans la réponse à la méthode POST
pour ajouter votre interface d'application à votre type de terminal. Vous pouvez également utiliser cet identificateur pour mapper un événement de terminal
entrant à une propriété définie par l'interface d'application.

## Etape 10 : ajoutez l'interface d'application à un type de terminal
{: #step10}

Pour ajouter une interface d'application à un type de terminal, utilisez l'API suivante :

```
POST /device/types/{typeId}/applicationinterfaces
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
id	|	Identificateur créé précédemment pour l'interface d'application.
name	|	Nom du type du terminal.
schemaId	|	Identificateur créé pour la ressource Interface d'application.
refs/schema	|	Chemin de la ressource Interface d'application. Généralement : /schemas/*schemaId*


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

Dans ce scénario, l'interface d'application est associée au type de terminal *EnvSensor1* et au type de terminal *EnvSensor2*.

L'exemple suivant montre comment utiliser cURL pour ajouter l'interface
d'application *5846ed076522050001db0e12*, qui fait référence à
l'identificateur de schéma d'application *5846ec826522050001db0e11*, au type
de terminal *EnvSensor1* :

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
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

L'exemple suivant montre comment utiliser cURL pour ajouter l'interface
d'application *5846ed076522050001db0e12* associée à l'identificateur de
schéma d'application *5846ec826522050001db0e11* au type de terminal
*EnvSensor2* :

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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface”
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

## Etape 11 : définissez les mappages entre propriétés des événements entrants et propriétés dans l'interface d'application
{: #step11}

Pour mapper des événements, utilisez l'API suivante :

```
POST /device/types/{typeId}/mappings
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
applicationInterfaceId	|	Identificateur précédemment créé pour l'interface d'application.
propertyMappings	|	Structure JSON valide mettant en correspondance les propriétés définies pour l'interface d'application avec les propriétés contenues dans la charge utile des événements du terminal. Consultez les exemples ci-dessous.


Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

Dans ce scénario, nous définissons des mappages pour le type de terminal
*EnvSensor1* afin de mapper la propriété **t** de
l'événement entrant *tevt* à la propriété **temperature**
de l'interface d'application. Nous définissons également des mappages pour le type de
terminal *EnvSensor2* afin de mapper la propriété
**temp** de l'événement entrant *tempevt* à la propriété
**temperature** de l'interface d'application.

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

**Important :** pour les charges utiles à
structure [JSON ![Icône de lien externe](../../../icons/launch-glyph.svg "Icône de lien externe")](http://json-schema.org/){:new_window},
assurez-vous que l'entrée $event.*propriété* est bien adaptée à la structure JSON de vos propriétés. Par exemple, si la charge utile est `{"d":{"t":<temp>}}`, utilisez `$event.d.t`

Spécifiez d'une part le type de terminal *EnvSensor1*, d'autre
par l'identificateur d'interface d'application *5846ed076522050001db0e12* (l'ID obtenu plus tôt dans la réponse à la méthode POST
ayant servi à créer l'interface d'application).

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

Spécifiez d'une part le type de terminal *EnvSensor2*, d'autre
par l'identificateur d'interface d'application *5846ed076522050001db0e12* (l'ID obtenu plus tôt dans la réponse à la méthode POST
ayant servi à créer l'interface d'application).
Une conversion est appliquée pour changer la valeur mesurée en degrés Fahrenheit en son équivalent en degrés Celsius.


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

## Etape 12 : déployez la configuration
{: #step15}

Déployez la configuration de mise à jour de l'état du terminal pour chaque type de terminal. Cette configuration inclut vos schémas, types d'événements, interfaces physiques, interfaces d'application et mappages.

Pour déployer votre configuration de type de terminal, utilisez l'API suivante :

```
PATCH /device/types/{typeId}
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
typeId	|	Identificateur du type de terminal.

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

Dans ce scénario, nous devons déployer une configuration pour deux types de terminaux.

L'exemple suivant montre comment utiliser cURL afin de déployer la configuration pour le type de terminal *EnvSensor1* :

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
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

## Etape 13 : publiez un événement de terminal entrant
{: #step12}

Publiez un événement de température issu de *TemperatureSensor1* sur
la rubrique (topic) `iot-2/evt/tevt/fmt/json` et un événement de température
issu de *TemperatureSensor2* sur la rubrique
`iot-2/evt/tempevt/fmt/json`.

Pour plus d'informations sur la publication d'un événement entrant provenant d'un terminal,
consultez [Connectivité MQTT pour les applications](../applications/mqtt.html#publishing_device_events).


## Etape 14 : vérifiez que l'état du terminal se met à jour
{: #step13}

Pour vérifier l'état de terminal, utilisez l'API suivante :
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

Les paramètres suivants sont requis :  

Paramètre	|	Description
------	|	-----
typeId	|	Identificateur du type de terminal.
deviceId	|	Identificateur du terminal.
applicationInterfaceId	|	Identificateur créé précédemment pour l'interface d'application.

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

L'exemple suivant montre comment utiliser cURL pour obtenir l'état actuel
de *TemperatureSensor1* en faisant référence à l'identificateur de l'interface
d'application qui a été créée :
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificateur d'interface d'application *5846ed076522050001db0e12* est utilisé dans la méthode GET. Il s'agit de l'identificateur obtenu dans la réponse à la méthode POST que nous avons utilisée précédemment pour créer l'interface d'application.
L'exemple suivant illustre une réponse à la méthode GET :
```
{
  "temperature":34.5
}
```
L'exemple suivant montre comment utiliser cURL pour obtenir l'état actuel de *TemperatureSensor2* en faisant référence à l'identificateur de l'interface d'application qui a été créée :
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

L'identificateur d'interface d'application *5846ed076522050001db0e12* est utilisé dans la méthode GET. Il s'agit
de l'identificateur obtenu dans la réponse à la méthode POST que nous avons utilisée précédemment pour créer l'interface d'application.
L'exemple suivant illustre une réponse à la méthode GET :
```
{
  "temperature":22.5
}
```
Notez que la mesure de température renvoyée est exprimée en degrés Celsius et non en degrés Fahrenheit.

Votre application peut ainsi traiter ces données normalisées sans qu'aucune configuration
ne soit nécessaire pour interpréter ou convertir les différentes échelles de température.


**Remarque :** Pour récupérer la dernière configuration déployée, utilisez l'API suivante :

```
GET /device/types/<typeId>/deployedconfiguration
```
Utilisez cette API pour obtenir la configuration qui a été déployée la dernière fois que la demande PATCH avec l'opération 'deploy' a réussi. Pour obtenir la configuration d'une ressource dont l'état change mais qui n'est pas
déployée, utilisez la méthode GET classique en l'associant à la ressource en question.

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types) (en anglais).

L'exemple suivant montre comment utiliser cURL pour obtenir la dernière configuration déployée :
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
L'exemple suivant illustre une réponse à la méthode GET :

```
{
    "schemas": [
        {
          "name" : “tEventSchema",
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "content": "ew0KICAiJHNjaGVtYSI6ICJodHRwOi8vanNvbi1zY2hlbWEub3JnL2RyYWZ0LTA0L3NjaGVtYSMiLA0KICAidHlwZSIgOiAib2JqZWN0IiwNCiAgInRpdGxlIiA6ICJFbnZTZW5zb3IxIHRFdmVudCBTY2hlbWEiLA0KICAiZGVzY3JpcHRpb24iIDog4oCcZGVmaW5lcyB0aGUgc3RydWN0dXJlIG9mIGEgdGVtcGVyYXR1cmUgZXZlbnQgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgInByb3BlcnRpZXMiIDogew0KICAgICJ0IiA6IHsNCiAgICAgICJkZXNjcmlwdGlvbiIgOiAidGVtcGVyYXR1cmUgaW4gZGVncmVlcyBDZWxzaXVzIiwNCiAgICAgICJ0eXBlIiA6ICJudW1iZXIiLA0KICAgICAgIm1pbmltdW0iIDogLTI3My4xNSwNCiAgICAgICJkZWZhdWx0IiA6IDAuMA0KICAgIH0NCiAgfSwNCiAgInJlcXVpcmVkIiA6IFsidCJdDQp9"
        }
    ],
    "eventTypes": [
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
        },
        {
          "createdBy" : "a-8x7nmj-9iqt56kfil",
          "schemaId" : "5846cee36522050001db0e0e",
          "created" : "2016-12-06T15:00:20Z",
          "id" : "5846d2846522050001db0e10",
          "updated" : "2016-12-06T15:00:20Z",
          "name" : “tempEvent”,
          "refs" : {
            "schema" : "/schemas/5846cee36522050001db0e0e"
          },
          "updatedBy" : "a-8x7nmj-9iqt56kfil"
        }
    ],
    "physicalInterface": {
          "events":[
            {
                  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
            },
            {
                "eventTypeId" : "5846d2846522050001db0e10",
                "eventId" : “tempevt"
            }
          ],
        "updatedBy" : "a-8x7nmj-9iqt56kfil",
          "refs" : {
            "events" : "/physicalinterfaces/5847d1df6522050001db0e1a/events"
          },
  "id" : "5847d1df6522050001db0e1a",
  "name" : "Env sensor physical interface 1",
  "created" : "2016-12-07T09:09:51Z",
  "updated" : "2016-12-07T09:09:51Z",
  "createdBy" : "a-8x7nmj-9iqt56kfil"
    },
    "applicationInterfaces": [
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
    ],
    "mappings": [
        {
          "propertyMappings" : {
            "tevt" : {
               "temperature" : "$event.t"
            },
            "tempevt" : {
                  "temperature" : "($event.temp - 32) / 1.8"
    }
          },
          "applicationInterfaceId" : "5846ed076522050001db0e12"
        }
    ]
}
```
