---

copyright:
years: 2016, 2017
lastupdated: "2017-04-11"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Interface d'application : scénario 2 (bêta)
{: #scenario}

L'interface d'application élimine la nécessité pour l'application d'avoir à comprendre comment un terminal ou un objet est configuré. Par exemple, vous pourriez mesurer la température d'une pièce à l'aide d'un seul terminal. Vous pourriez
aussi la calculer en faisant la moyenne des mesures de plusieurs terminaux. L'application a seulement besoin de connaître
l'état (en l'occurrence, la propriété de température) d'une ou de plusieurs pièces. Peu importe comment la valeur de température reçue par l'application est calculée.

Dans ce scénario, des capteurs de température et d'humidité publient des données environnementales qu'ils recueillent dans
deux salles de réunion. Les données de ces deux capteurs sont mappées séparément à deux interfaces d'application Type de terminal, une
pour le type de terminal Thermomètre et l'autre pour le type de terminal Hygromètre. Un type d'objet nommé *RoomType* est ensuite créé, ainsi que deux instances de
ce type d'objet respectivement nommées *meetingroom1* et *meetingroom2*.

Dans ce scénario, nous mettons en place une composition incluant les interfaces d'application
Thermomètre et Hygromètre, puis nous mappons les capteurs environnementaux adéquats à chaque instance de
salle. Par exemple, *temperatureSensor1* et
*humiditySensor1* sont mappés à *meetingroom1*.

## Conditions prérequises
{: #pre_req}

Ce scénario est une extension du précédent [scénario d'interface d'application (scénario 1](im_index_scenario).

Avant de continuer, vérifiez les points suivants :
- Vous utilisez la même instance d'organisation
{{site.data.keyword.iot_short_notm}} et la même clé d'API ou le même jeton pour
cette organisation. Pour plus d'informations sur les clés d'API et les jetons, consultez
[API REST HTTP pour les
applications](../applications/api.html#authentication).
- Vous avez créé deux interfaces d'application, une pour le capteur de température et une autre pour le capteur d'humidité. Pour des informations sur la configuration d'une interface d'application convenant à un capteur de température,
consultez le [scénario 1](../information_management/im_index_scenario).

## A propos de cette tâche
{: #about}

Dans {{site.data.keyword.iot_short_notm}}, un objet (ou une chose) peut comprendre un certain nombre de terminaux et d'objets. Un type d'objet définit de quelle manière les instances d'un objet sont composées. Une interface d'application peut être associée à un type d'objet. Cette association définit la structure de l'état généré pour une instance de ce type d'objet. Des mappages sont utilisés pour définir comment les propriétés de terminaux et d'objets agrégés sont liées aux
propriétés d'un état d'objet.

Dans ce scénario, deux capteurs de température et deux capteurs d'humidité publient des événements
sur {{site.data.keyword.iot_short_notm}}. Un capteur de température et un capteur d'humidité sont installés dans la salle de réunion 1 d'un
immeuble de bureaux. Les deux autres capteurs (l'une de température, l'autre d'humidité) sont installés dans la salle de réunion 2.

![Mappage entre objets Température et Humidité et une application sur {{site.data.keyword.iot_short_notm}}.](images/Information "Mappage entre plusieurs capteurs environnementaux d'une même salle et une application sur {{site.data.keyword.iot_short_notm}}")

Un type d'objet nommé *RoomType* est utilisé pour définir comment les instances de salles sont composées. Une interface d'application est associée à *RoomType*. Elle définit que les événements entrants
sont mappés à un unique relevé indiquant à la fois la température et l'humidité. C'est cet unique relevé qui représente l'état d'objet. Des mappages sont utilisés pour définir comment les propriétés des capteurs de température et d'humidité sont liées à
cet état d'objet. Lorsqu'une nouvelle mesure est publiée par ces capteurs, la valeur de la
propriété associée à l'état d'objet change.

Les quatre terminaux suivants sont inclus :

Terminal/Type | Evénement | Charge utile événement/Propriété
------------- |  ------------- | -------------
*temperatureSensor1*/Thermomètre (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermomètre (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygromètre (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygromètre (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

L'interface d'application Type d'objet représente l'état d'objet dans la structure suivante :
```
{
  “temperature” : <valeur de température actuelle en degrés Celsius>
  "humidity" : <valeur d'humidité actuelle>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

Utilisez l'exemple suivant pour mettre en place votre propre environnement d'interfaces.  

## Si nécessaire, ajoutez un type de terminal et un terminal  
{: #add_device}  
Dans ce scénario, on utilise deux types de terminaux et quatre instances de terminaux. Les instances de terminaux *temperatureSensor1* et *temperatureSensor2* sont associées au
type de terminal *Thermomètre*. Les instances de terminaux *humiditySensor1* et *humiditySensor2* sont associées au
type de terminal *Hygromètre*.

Pour plus d'informations sur l'utilisation de l'API REST servant à ajouter un type de
terminal, consultez la documentation correspondante dans le document
[API
REST HTTP de {{site.data.keyword.iot_short_notm}}](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types) (en anglais).

## Etape 1 : créez un fichier schéma de composition  
{: #crt_composition_file}  
Créez un fichier schéma de composition désignant chaque interface d'application par son identificateur, une pour le type de terminal Thermomètre et
une autre pour le type de terminal Hygromètre.  

L'exemple suivant montre comment créer un fichier schéma de composition nommé *Room Type Schema*.  
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "Room Type Schema",
   "description" : "JSON Schema that defines the structure of the Room Thing Type.",
   "properties" : {
       "temperatureSensor": {
           "description": "The temperature sensor device",
           "$applicationInterfaceRef": "58c135e352faff0001198a89"
       },
       "humiditySensor": {
           "description": "The humidity sensor device",
           "$applicationInterfaceRef": "58c135ea52faff0001678f06"
       }
   },
   "required" : [
       "temperatureSensor",
       "humiditySensor"
   ]
}
```
**Astuce :** Utilisez le paramètre “required” pour indiquer qu'une propriété est requise. Les propriétés requises doivent être incluses dans un message de terminal afin que
Watson IoT Platform mette à jour l'état d'un terminal avec les données de ce terminal. Un message qui n'inclut pas de propriété requise n'est pas traité.   
**Remarque :** Lorsque vous créez votre type d'objet, vous devez spécifier l'identificateur de schéma qui a été généré
lorsque vous avez créé le fichier schéma de type d'objet.  

## Etape 2 : créez une ressource Schéma de composition  
{: #crt_composition_resource}  

Créez la ressource Schéma en téléchargeant le fichier schéma de type d'objet qui a été généré à l'étape précédente.  
Pour télécharger le fichier schéma de type d'objet, utilisez l'API suivante :  
```
POST /schemas
```  
Les paramètres suivants sont requis :  
<table>
<tr>
<th>	Paramètre	</th><th>	Description	</th>
</tr>
<tr>
<td>	name	</td><td>	Nom que vous donnez au schéma de composition que vous créez.	</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	Chemin du fichier JSON local contenant le schéma de composition.	</td>
</tr>
</table>

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) (en anglais).  

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## Etape 3 : créez un type d'objet  
{: #crt_thing_type}  

Les types d'objets servent à modéliser des instances d'objets. Un type d'objet doit être créé dans une organisation avant qu'une instance d'objet de ce type puisse être
créée. Pour les besoins de ce scénario, nous n'allons créer qu'un seul type d'objet.  
C'est le schéma associé à un type d'objet (thing type) qui définit quels types d'objets
sont agrégés pour composer une instance d'un objet de ce type. Le type d'objet doit contenir une référence à la ressource Schéma de type d'objet que vous avez créée à l'étape précédente.  
Pour créer un type d'objet, utilisez l'API suivante :
```
POST /thing/types
```
Les paramètres suivants sont requis :  
<table>
<tr><th>Paramètre</th><th>Description</th></tr>
<tr><td>Id</td><td>Identificateur que vous donnez au type d'objet que vous créez.</td></tr>
<tr><td>name</td><td>Nom que vous donnez au type d'objet que vous créez.</td></tr>
<tr><td>schemaId</td><td>Identificateur créé précédemment pour la ressource Schéma de composition.</td></tr>
</table>

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) (en anglais).  

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## Etape 4 : créez un fichier schéma d'interface d'application  
{: #crt_ai_schema_file}
Dans votre interface d'application, vous pouvez définir la structure des données stockées en tant qu'état d'objet. Pour ce scénario, nous créons une interface d'application qui définit les propriétés température et
humidité. Nous l'associons au type d'objet *RoomType* en désignant par son identificateur
l'interface d'application qui a été générée lorsque vous avez créé la ressource Interface d'application.  
L'exemple suivant montre comment créer un fichier schéma d'interface d'application nommé *RoomType Schema*.
```
{
   "$schema": "http://json-schema.org/draft-04/schema#",
   "type" : "object",
   "title" : "RoomType Schema",
   "description" : "JSON Schema that defines the canonical room state structure",
   "properties" : {
       "temperature" : {
           "description" : "Temperature in degrees celsius",
           "type" : "number",
           "minimum" : -273.15,
           "default" : 0.0
       },
       "humidity" : {
           "description" : "Percentage humidity",
           "type" : "number",
           "minimum" : 0,
           "maximum" : 100,
           "default" : 0.0
       }
   },
   "required" : [
       "temperature",
       "humidity"
   ]
}
```  
## Etape 5 : créez une ressource Schéma d'interface d'application  
{: #crt_ai_schema_resource}  
Pour créer une ressource Schéma d'interface d'application pour votre type d'objet,
téléchargez le fichier schéma d'interface d'application que vous avez créé à l'étape précédente. Pour cela,
utilisez l'API suivante :  
```
POST /schemas
```  
Les paramètres suivants sont requis :  
<table>
<tr>
<th>Paramètre</th><th>Description</th>
</tr>
<tr>
<td>name</td><td>Nom que vous donnez au schéma d'interface d'application que vous créez.</td>
</tr>
<tr>
<td>schemaFile</td><td>Chemin du fichier JSON local contenant le schéma d'interface d'application.</td>
</tr>
</table>  

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas) (en anglais).  

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

Utilisez l'identificateur de schéma pour
ajouter la ressource Schéma d'interface d'application à l'interface d'application de votre type d'objet.  

## Etape 6 : créez une interface d'application pour le type d'objet  
{: #crt_thing_ai}  
L'interface d'application doit contenir une référence à la ressource Schéma d'interface d'application que vous avez créée à l'étape précédente.  
Pour créer une interface d'application, utilisez l'API suivante :  
```
POST /applicationinterfaces
```  
Les paramètres suivants sont requis :  
<table>
<tr>
<th>	Paramètre	</th><th>	Description	</th>
</tr>
<tr>
<td>	name	</td><td>	Nom que vous donnez à l'interface d'application que vous créez.	</td>
</tr>
<tr>
<td>	description	</td><td>	Description que vous donnez de l'interface d'application.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Chemin du fichier JSON local contenant le schéma d'interface d'application.	</td>
</tr>
</table>  

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces) (en anglais).  
Utilisez l'identificateur de schéma qui a été renvoyé dans la réponse précédente pour
ajouter le schéma d'interface d'application à l'interface d'application.  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

Utilisez l'identificateur d'interface d'application pour ajouter votre interface d'application à votre type de terminal. Vous pouvez également utiliser cet identificateur pour mapper un événement de terminal entrant à une propriété définie par l'interface d'application.  

## Etape 7 : ajoutez l'interface d'application au type d'objet  
{: #add_thing_ai}  
Pour ajouter une interface d'application à un type d'objet, utilisez l'API suivante :  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
Les paramètres suivants sont requis :  
<table>
<tr>
<th>	Paramètre	</th><th>	Description	</th>
</tr>
<tr>
<td>	id	</td><td>	Identificateur créé précédemment pour le type d'objet.	</td>
</tr>
<tr>
<td>	name	</td><td>	Nom que vous donnez à l'interface d'application que vous créez.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Identificateur créé précédemment pour la ressource Interface d'application.	</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	Chemin de la ressource Interface d'application. Généralement : /schemas/*schemaId*	</td>
</tr>
</table>  

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) (en anglais).  
Dans ce scénario, l'interface d'application est associée au type d'objet *RoomType*.

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## Etape 8 : définissez les mappages
{: #define_Thing_type_mappings}

Définissez les mappages décrivant comment associer les propriétés de l'état des terminaux ou objets
agrégés aux propriétés définies dans l'interface d'application Type d'objet.

Pour mapper des événements, utilisez l'API suivante :  
```
POST /thing/types/{thingtypeId}/mappings
```  

Les paramètres suivants sont requis :  
<table>
<tr>
<th>	Paramètre	</th><th>	Description	</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	Identificateur créé précédemment pour l'interface d'application.	</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	Structure JSON valide mettant en correspondance les propriétés définies pour l'interface d'application avec les propriétés contenues dans la charge utile des événements du terminal.	</td>
</tr>
</table>  

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) (en anglais).

<!--  The following example shows how to use Python to add a mapping to thing type *RoomType*:

```python
mappings = {
     "humiditySensor": {
       "humidity": "$event.humidity"
     },
     "temperatureSensor": {
       "temperature": "$event.temperatureC"
     }
 }

 result = api.addMappingsToThingType(thingType, "applicationInterfaceId", mappings)
``` -->

L'exemple suivant contient une entrée pour le paramètre propertyMappings :

```
{
  "applicationInterfaceId": "58dd849752faff0001638851",
  "propertyMappings": {
       "humiditySensor": {
         "humidity": "$event.humidity"
       },
       "temperatureSensor": {
         "temperature": "$event.temperatureC"
       }
   }
}
```

L'objet *humiditySensor* est défini dans le schéma d'objet. La propriété "$event.humidity" est définie dans le schéma d'interface d'application
dont l'identificateur est "58c135ea52faff0001678f06".
L'objet *temperatureSensor* est défini dans le schéma d'objet. La propriété "$event.temperatureC" est définie dans le schéma d'interface d'application
dont l'identificateur est "58c135e352faff0001198a89".

## Etape 9 : déployez la configuration associée au type d'objet  
{: #deploy_Thing_config}   
Déployez la configuration de mise à jour de l'état d'objet pour chaque type d'objet. Cette configuration inclut les schémas, les interfaces d'application et les mappages.

Vous devez déployer la configuration du type d'objet avant de pouvoir créer une instance de celui-ci.

Pour déployer votre configuration de type d'objet, utilisez l'API suivante :

```
PATCH /thing/types/{thingtypeId}
```
Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types) (en anglais).

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## Etape 10 : créez une instance d'un type d'objet
{: #create_Thing_instances}

Un objet est une instance d'un type d'objet. Il permet d'agréger en un seul objet une ou plusieurs instances d'un terminal ou d'un objet.

Pour créer un objet, utilisez l'API suivante :

```
POST /thing/types/{thingTypeId}/things
```

Les paramètres suivants sont requis :  
<table>
<tr>
<th>	Paramètre	</th><th>	Description	</th>
</tr>
<tr>
<td>	typeId	</td><td>		Identificateur du type d'objet que vous avez créé plus tôt.</td>
</tr>
<tr>
<td>	thingId	</td><td>	Nom que vous donnez à l'instance d'objet que vous créez.	</td>
</tr>
</table>

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things) (en anglais).

Dans ce scénario, nous devons créer deux instances d'objets du type *RoomType*. Une instance d'objet sera appelée *meetingroom1* et l'autre, *meetingroom2*.

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom1*. *meetingroom1* is associated with the *temperatureSensor1* and *humiditySensor1* device instances.

```python
thingId = "meetingroom1"
 meetingroom1AggregatedObjects = {
   "temperatureSensor": {
     "type": "device",
     "typeId": "TemperatureSensor",
     "id": "temperatureSensor1"
   },
   "humiditySensor": {
     "type": "device",
     "typeId": "HumiditySensor",
     "id": "humiditySensor1"
   }
 }
 result = api.createThing(thingType, thingId, "Meeting Room 1", "The big meeting room!!!", aggregatedObjects = meetingroom1AggregatedObjects)
``` -->

L'identificateur d'objet créé est utilisé dans l'URL de la méthode POST appelée pour ajouter un événement de température à l'interface d'application de l'objet.

<!-- The following example shows how to use Python to create a thing instance that is called *meetingroom2*. *meetingroom2* is associated with the *temperatureSensor2* and *humiditySensor2* device instances.

```python
thingId = "meetingroom2"
   meetingroom2AggregatedObjects = {
    "temperatureSensor": {
      "type": "device",
      "typeId": "TemperatureSensor",
      "id": "temperatureSensor2"
    },
    "humiditySensor": {
      "type": "device",
      "typeId": "HumiditySensor",
      "id": "humiditySensor2"
    }
  }
result = api.createThing(thingType, thingId, "Meeting Room 2", "The little meeting room!!!", aggregatedObjects = meetingroom2AggregatedObjects)  
``` -->

## Etape 11 : vérifiez que les événements de terminal mappés sont publiés sur l'interface d'application  
{: #publish_event}  
Publiez les événements suivants pour les terminaux agrégés en objet *meetingroom1* :  
 - un événement de température issu de *temperatureSensor1* sur
la rubrique (topic) `iot-2/evt/tevt/fmt/json`  
 - un événement d'humidité issu de *humiditySensor1* sur la rubrique `iot-2/evt/hevt/fmt/json`  
Publiez les événements suivants pour les terminaux agrégés en objet *meetingroom2* :  
 - un événement de température issu de *temperatureSensor2* sur
la rubrique (topic) `iot-2/evt/tempevt/fmt/json`  
 - un événement d'humidité issu de *humiditySensor2* sur la rubrique `iot-2/evt/humevt/fmt/json`  
Pour plus d'informations sur la publication d'un événement entrant provenant d'un terminal,
consultez [Connectivité MQTT pour les applications](../applications/mqtt.html#publishing_device_events).  

## Etape 12 : vérifiez que l'état de l'objet se met à jour  
{: #verify_Thing_state}  
Pour vérifier l'état d'objet, utilisez l'API suivante :  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

Les paramètres suivants sont requis :  
<table>
<tr>
<th>Paramètre	</th><th>	Description</th>
</tr>
<tr>
<td>thingtypeId	</td><td>Identificateur du type d'objet</td>
</tr>
<tr>
<td>thingId	</td><td>	Identificateur de l'objet.</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>Identificateur créé précédemment pour l'interface d'application.</td>
</tr>
</table>  

Pour plus d'informations, consultez la documentation de l'[ API REST HTTP {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types) (en anglais).  

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
