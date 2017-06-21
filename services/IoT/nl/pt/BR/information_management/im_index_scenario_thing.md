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

# Cenário de interface de aplicativo 2 (Beta)
{: #scenario}

A interface de aplicativo é usada para remover o requisito do aplicativo para entender como um
dispositivo ou item é configurado. Por exemplo, é possível medir a temperatura de uma sala usando um único
dispositivo ou é possível calcular a temperatura da sala fazendo a leitura média de um número de
dispositivos. O aplicativo requer informações sobre o estado de uma ou mais salas, um componente do qual uma
temperatura é propriedade. Não importa como o valor de temperatura que é recebido pelo aplicativo é
calculado.

Neste cenário, sensores de temperatura e sensores de umidade publicam dados ambientais que são coletados
em duas salas de reunião. Os dados de sensores de temperatura e de umidade são mapeados separadamente
para duas interfaces de aplicativo de tipo de dispositivo, uma para o tipo de dispositivo termômetro e outra
para o tipo de dispositivo higrômetro. Em seguida, um tipo de item chamado *RoomType* é
criado, junto com duas instâncias de item de sala: *meetingroom1* e *meetingroom2*.

Este cenário configura uma composição que inclui as interfaces de aplicativo termômetro e higrômetro e,
em seguida, mapeia os sensores ambientais corretos para cada instância da sala, por exemplo,
*temperatureSensor1* e *humiditySensor1* são mapeados para
*meetingroom1*.

## Pré-requisitos
{: #pre_req}

Este cenário é construído sobre o [Cenário de interface de aplicativo
1](im_index_scenario) anterior.

Antes de continuar, certifique-se de:
- Usar a mesma instância da organização do {{site.data.keyword.iot_short_notm}}
e uma chave API ou um token para esta organização. Para obter mais informações sobre chaves e tokens API, veja [API de REST HTTP para aplicativos](../applications/api.html#authentication).
- Ter criado duas interfaces de aplicativos, uma para um sensor de temperatura e outra para um sensor de
umidade. Para obter informações sobre como configurar uma interface de aplicativo para um sensor de
temperatura, consulte [Cenário de interface de
aplicativo de tipo de dispositivo](../information_management/im_index_scenario).

## Sobre essa Tarefa
{: #about}

No {{site.data.keyword.iot_short_notm}}, um item pode consistir em um número de dispositivos e
de itens. Um tipo de item define como instâncias de um item são compostas. Uma interface de aplicativo pode
ser associada a um tipo de item. Esta associação define a estrutura do estado que é gerada para uma instância
do tipo de item. Os mapeamentos são usados para definir como as propriedades dos dispositivos e
itens agregados são mapeados para propriedades em um estado de item.

Neste cenário, dois sensores de temperatura e dois sensores de umidade publicam eventos para
{{site.data.keyword.iot_short_notm}}. Um sensor de temperatura e um sensor de umidade estão na sala de
reunião 1 de um bloco de escritórios. O outro sensor de temperatura e de umidade está na sala
de reunião 2.

![Mapeamento entre o item de temperatura e umidade e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/Information "Mapeamento entre múltiplos sensores ambientais em uma sala e um aplicativo no {{site.data.keyword.iot_short_notm}}")

Um tipo de item chamado *RoomType* é usado para definir como as instâncias de salas são
compostas. Uma interface de aplicativo está associada ao *RoomType* e define que os eventos de
entrada são mapeados para uma única leitura que mostra tanto a temperatura quanto a umidade. Esta leitura
única é o estado do item. Os mapeamentos são usados para definir como as propriedades dos sensores de
temperatura e de umidade são mapeadas para este estado de item. Quando uma nova leitura é publicada por estes
sensores, o valor da propriedade que está associada ao estado de item é mudado.

Os quatro dispositivos a seguir estão incluídos:

Dispositivo/Tipo | Evento | Propriedade/Carga útil do evento
------------- |  ------------- | -------------
*temperatureSensor1*/Thermometer (meetingroom1) | `iot-2/evt/`*`tevt`*`/fmt/json` | `{ “t” : 34.5 }`/ **temperature1**
*temperatureSensor2*/Thermometer (meetingroom2) | `iot-2/evt/`*`tempevt`*`/fmt/json` | `{ “temp” : 34.5 }`/ **temperature2**  
*humiditySensor1*/Hygrometer (meetingroom1) | `iot-2/evt/`*`hevt`*`/fmt/json` | `{  “h” : "75%" }`/ **humidity1**
*humiditySensor2*/Hygrometer (meetingroom2) |`iot-2/evt/`*`humevt`*`/fmt/json` | `{  “hum” : "75%"}`/ **humidity2**

Esta interface de aplicativo de tipo de item representa o estado do item na estrutura a seguir:
```
{
  “temperature” : <current temperature value in Celsius>
  "humidity" : <current humidity value>
  }
```

<!--
The code that is used in this example is available in the updated {{site.data.keyword.iot_short_notm}} [[Python library ![External link icon](../../../icons/launch-glyph.svg "External link icon")](https://github.com/ibm-watson-iot/iot-python){: new_window} in GitHub, in the **thingDataTransform** sample.
-->  

Use o cenário de exemplo a seguir para configurar seu próprio ambiente de interfaces.  

## Se necessário, inclua um tipo de dispositivo e um dispositivo  
{: #add_device}  
Neste cenário, são usados dois tipos de dispositivo e quatro instâncias de dispositivo. As
instâncias de dispositivo *temperatureSensor1* e *temperatureSensor2* são
associadas ao tipo de dispositivo *Termômetro*. As instâncias de dispositivo
*humiditySensor1* e *humiditySensor2* são associadas ao tipo de dispositivo
*Higrômetro*.

Para obter informações sobre como usar as APIs de REST para incluir um tipo de dispositivo, consulte a
documentação
[API de
REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofThings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

## Etapa 1: Criar um arquivo de esquema de composição.  
{: #crt_composition_file}  
Crie um arquivo de esquema de composição que referencie os identificadores de interface de aplicativo de
dispositivo para cada tipo de dispositivo de temperatura e de umidade.  

O exemplo a seguir mostra como criar um arquivo de esquema de composição que é chamado *Esquema
de tipo de sala*.  
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
**Dica:** use o parâmetro “required” para marcar uma ou mais propriedades conforme necessário. As propriedades necessárias devem ser incluídas em uma mensagem do dispositivo para o Watson IoT Platform para atualizar o estado do dispositivo com os dados do dispositivo. Uma mensagem que não inclui a propriedade necessária não é processada.   
**Nota:** o identificador de esquema que é gerado quando você cria um arquivo de esquema
tipo de item deve ser especificado ao criar seu tipo de item.  

## Etapa 2: Criar um recurso de esquema de composição.  
{: #crt_composition_resource}  

Crie o recurso do esquema fazendo upload do arquivo de esquema de tipo de item que foi gerado na etapa
anterior.  
Faça upload do arquivo de esquema de tipo de item usando a API a seguir:  
```
POST /schemas
```  
Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>	Parâmetro	</th><th>	Descrição	</th>
</tr>
<tr>
<td>	nome	</td><td>	Forneça um nome para o esquema de composição que você está criando.	</td>
</tr>
<tr>
<td>	schemaFile	</td><td>	Caminho para o arquivo JSON do esquema de composição local.	</td>
</tr>
</table>

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).

<!-- The following example shows how to use Python to create the thing type schema resource:  
```python
roomTypeSchemaFile = open(schemasDir + "roomType.json", "r");
roomTypeSchema = roomTypeSchemaFile.read();
roomTypeSchemaFile.close();
"roomTypeSchemaId", result = api.createSchema("Room Type Schema", "roomType.json", roomTypeSchema)
```  -->

## Etapa 3: Criar um tipo de item  
{: #crt_thing_type}  

Tipos de item são usados para modelar instâncias de item. Um tipo de item deve ser criado em uma
organização antes que uma instância de item possa ser criada. Para este cenário, crie um tipo de item.  
O esquema que está associado a um tipo de item define o tipo de objetos que são agregados para criar
uma instância de um item. O tipo de item deve referenciar o recurso de esquema de tipo de item que você criou
na etapa anterior.  
Crie um tipo de item usando a API a seguir:
```
POST /thing/types
```
Os seguintes parâmetros são obrigatórios:  
<table>
<tr><th>Parâmetro</th><th>Descrição</th></tr>
<tr><td>ID</td><td>Forneça um ID para o tipo de item que você está criando.</td></tr>
<tr><td>name</td><td>Forneça um nome para o tipo de item que você está criando.</td></tr>
<tr><td>schemaId</td><td>O ID criado para o recurso de esquema de composição.</td></tr>
</table>

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

<!-- The following example shows how to use Python to create a thing type that is called *RoomType*.
```python
result = api.createThingType(thingType, "RoomType", "roomTypeSchemaId", "The Room Thing type")

```  -->

## Etapa 4: Criar um arquivo de esquema de interface de aplicativo  
{: #crt_ai_schema_file}
Em sua interface de aplicativo, é possível definir a estrutura dos dados que são armazenados como o estado de
item. Para este cenário, crie uma interface de aplicativo que defina propriedades de temperatura e de umidade. Associe a interface de aplicativo ao tipo de item *RoomType* referenciando o identificador
da interface de aplicativo que é gerado ao criar o recurso da interface de aplicativo.  
O exemplo a seguir mostra como criar um arquivo de esquema de interface de aplicativo que é chamado
*RoomType Esquema*.
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
## Etapa 5: Criar um recurso de esquema de interface de aplicativo.  
{: #crt_ai_schema_resource}  
Faça upload do arquivo de esquema de interface de aplicativo que foi criado na etapa anterior para criar um
recurso de esquema de interface de aplicativo para o seu tipo de item usando a API a seguir:  
```
POST /schemas
```  
Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>Parâmetro</th><th>Descrição</th>
</tr>
<tr>
<td>name</td><td>Forneça um nome para o esquema de interface de aplicativo que você está criando.</td>
</tr>
<tr>
<td>schemaFile</td><td>Caminho para o arquivo JSON do esquema de interface de aplicativo local.</td>
</tr>
</table>  

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Schemas).

<!-- The following example shows how to use Python to create the thing type application interface schema resource:  
```python
roomSchemaFile = open(schemasDir + "room.json", "r");
roomSchema = roomSchemaFile.read();
roomSchemaFile.close();
"roomSchemaId", result = api.createSchema("Room Schema", "room.json", roomSchema)
```  -->

Use o identificador de esquema para incluir o recurso de esquema de interface de aplicativo na interface
de aplicativo para o seu tipo de item.  

## Etapa 6: Criar uma interface de aplicativo para o tipo de item.  
{: #crt_thing_ai}  
A interface de aplicativo deve referenciar o recurso de esquema de interface de aplicativo que foi criado na
etapa anterior.  
Para criar uma interface de aplicativo, use a API a seguir:  
```
POST /applicationinterfaces
```  
Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>	Parâmetro	</th><th>	Descrição	</th>
</tr>
<tr>
<td>	nome	</td><td>	Forneça um nome para a interface de aplicativo que você está criando.	</td>
</tr>
<tr>
<td>	description	</td><td>	Forneça uma descrição da interface de aplicativo.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	Caminho para o arquivo JSON do esquema de interface de aplicativo local.	</td>
</tr>
</table>  

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Application_Interfaces).
Use o identificador de esquema que foi retornado na resposta anterior para incluir o
esquema de interface de aplicativo na interface de aplicativo.  

<!-- The following example shows how to use Python to create an application interface:  
```python
"applicationInterfaceId", result = api.createApplicationInterface("IRoom", "roomSchemaId")
```  -->

Use o identificador de interface de aplicativo para incluir sua interface de aplicativo no seu tipo de
dispositivo. Este identificador também é usado para mapear um evento de dispositivo de entrada para uma propriedade que é definida pela interface de aplicativo.  

## Etapa 7: Incluir a interface de aplicativo no tipo de item.  
{: #add_thing_ai}  
Para incluir uma interface de aplicativo em um tipo de item, use a API a seguir:  
```
POST /thing/types/{thingtypeId}/applicationinterfaces
```  
Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>	Parâmetro	</th><th>	Descrição	</th>
</tr>
<tr>
<td>	id	</td><td>	O ID criado para o tipo de item.	</td>
</tr>
<tr>
<td>	nome	</td><td>	Forneça um nome para a interface de aplicativo que você está criando.	</td>
</tr>
<tr>
<td>	schemaId	</td><td>	O ID criado para o recurso da interface de aplicativo.	</td>
</tr>
<tr>
<td>	refs/schema	</td><td>	O caminho para o recurso da interface de aplicativo. Geralmente:
/schemas/*schemaId*	</td>
</tr>
</table>  

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).
Neste cenário, a interface de aplicativo está associada ao tipo de item *RoomType*.

<!-- The following example shows how to use Python to add the thing application interface to the thing type *RoomType*:  
```python
result = api.addApplicationInterfaceToThingType(RoomType, "applicationInterfaceId", "roomSchemaId")
``` -->

## Etapa 8: Definir mapeamentos
{: #define_Thing_type_mappings}

Defina os mapeamentos para o tipo de item que descrevam como mapear propriedades do estado dos
dispositivos ou itens agregados para as propriedades que são definidas na interface de aplicativo tipo
de item.

Para mapear eventos, use a API a seguir:  
```
POST /thing/types/{thingtypeId}/mappings
```  

Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>	Parâmetro	</th><th>	Descrição	</th>
</tr>
<tr>
<td>	applicationInterfaceId	</td><td>	O ID criado para a interface de aplicativo.	</td>
</tr>
<tr>
<td>	propertyMappings	</td><td>	Uma estrutura JSON válida que mapeia propriedades definidas para a interface
de aplicativo com as propriedades da carga útil do evento do dispositivo.	</td>
</tr>
</table>  

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

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

O exemplo a seguir mostra uma entrada de parâmetro propertyMappings de amostra:

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

O *humiditySensor* é definido no esquema de item. O "$event.humidity" é definido no esquema
de interface de aplicativo com o identificador "58c135ea52faff0001678f06".
O *temperatureSensor*
é definido no esquema de item. O "$event.temperatureC" é definido no esquema de interface de aplicativo com o
identificador "58c135e352faff0001198a89".

## Etapa 9: Implementar a configuração que está associada ao tipo de item  
{: #deploy_Thing_config}   
Implemente a configuração que está relacionada à atualização do estado de item para cada tipo de item. Esta
configuração inclui esquemas, interfaces de aplicativo e mapeamentos.

Deve-se implementar a configuração do tipo de item antes de poder criar quaisquer instâncias do tipo
de item.

Para implementar sua configuração de tipo de item, use a API a seguir:

```
PATCH /thing/types/{thingtypeId}
```
Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Device_Types).

<!-- The following example shows how to use Python to deploy your configuration for thing type *Room*:

```python
result = api.deployThingTypeConfiguration(thingType)
``` -->

## Etapa 10: Criar uma instância de um tipo de item
{: #create_Thing_instances}

Um item é uma instância de um tipo de item. O item permite agregar uma ou mais instâncias de um
dispositivo ou item em um único objeto.

Para criar um item, use a API a seguir:

```
POST /thing/types/{thingTypeId}/things
```

Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>	Parâmetro	</th><th>	Descrição	</th>
</tr>
<tr>
<td>	typeId	</td><td>		O ID do tipo de item que foi criado anteriormente.</td>
</tr>
<tr>
<td>	thingId	</td><td>	Forneça um nome para a instância de item que você está criando.	</td>
</tr>
</table>

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Things).

Neste cenário, é necessário criar duas instâncias de item que sejam do tipo *RoomType*. Uma
instância de item é chamada *meetingroom1* e a outra instância de item é chamada
*meetingroom2*.

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

O identificador de item que é criado é usado na URL do método POST que é chamado para incluir um evento
de temperatura na interface de aplicativo de item.

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

## Etapa 11: Verificar se os eventos de dispositivo mapeados foram publicados na interface de aplicativo  
{: #publish_event}  
Publique os seguintes eventos para dispositivos que são agregados no item *meetingroom1*:  
 - um evento de temperatura no *temperatureSensor1* no tópico
`iot-2/evt/tevt/fmt/json`  
 - um evento de umidade no *humiditySensor1* no tópico
`iot-2/evt/hevt/fmt/json`  
Publique os seguintes eventos para dispositivos que são agregados no item *meetingroom2*:  
 - um evento de temperatura no *temperatureSensor2* no tópico
`iot-2/evt/tempevt/fmt/json`  
 - um evento de umidade no *humiditySensor2* no tópico
`iot-2/evt/humevt/fmt/json`  
Para obter informações sobre como publicar um evento de entrada por meio de um dispositivo, veja [Conectividade MQTT para aplicativos](../applications/mqtt.html#publishing_device_events).  

## Etapa 12: Verificar se o estado do item é mudado.  
{: #verify_Thing_state}  
Para verificar o estado do item, use a API a seguir:  
```
GET /thing/types/{thingTypeId}/things/{thingId}/state/{applicationInterfaceId}
```  

Os seguintes parâmetros são obrigatórios:  
<table>
<tr>
<th>Parâmetro	</th><th>	Descrição</th>
</tr>
<tr>
<td>thingtypeId	</td><td>O ID do tipo de item</td>
</tr>
<tr>
<td>thingId	</td><td>	O ID do item.</td>
</tr>
<tr>
<td>applicationInterfaceId</td><td>O ID criado para a interface de aplicativo.</td>
</tr>
</table>  

Para obter mais detalhes, consulte a documentação da
[API
de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/info-mgmt-beta.html#!/Thing_Types).

<!-- The following example shows how to use Python to retrieve the current state of *meetingroom1* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom1", applicationInterfaceId)
```  
The following example shows how to use Python to retrieve the current state of *meetingroom2* by referencing the identifier of the application interface that was created:  
```python
result = api.getThingStateForApplicationInterface("RoomType", "meetingroom2", applicationInterfaceId)
``` -->
