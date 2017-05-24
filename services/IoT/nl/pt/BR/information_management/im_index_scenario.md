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


# Cenário de interface de aplicativo 1 (Beta)
{: #scenario}

Use as informações a seguir para criar um cenário no qual dois sensores de temperatura publiquem eventos no {{site.data.keyword.iot_short_notm}}. Um sensor mede a temperatura em graus Celsius. O outro sensor mede a temperatura em graus Fahrenheit. Essas leituras são mapeadas para uma única leitura de temperatura que está em graus Celsius. Quando uma nova leitura de temperatura é publicada por esses dispositivos, o valor da propriedade associada ao estado do dispositivo muda.

## Pré-requisitos

Deve-se ter uma instância de organização do {{site.data.keyword.iot_short_notm}} e uma chave ou um token API para essa organização. Para obter mais informações sobre chaves e tokens API, veja [API de REST HTTP para aplicativos](../applications/api.html#authentication).

## Sobre essa Tarefa

Neste cenário, dois dispositivos estão configurados.

Um dispositivo chama-se *TemperatureSensor1*. Esse dispositivo publica eventos de temperatura que são medidos em graus Celsius. O evento de temperatura é publicado no tópico `iot-2/evt/tevt/fmt/json` e possui a carga útil de exemplo a seguir:
```
{
  “t” : 34.5
}
```

**Nota:** o identificador de evento é *tevt*. Esse identificador é necessário quando você inclui um evento de temperatura desse tipo na interface física e quando define mapeamentos para mapear uma propriedade associada a um evento de entrada desse tipo para uma propriedade em sua interface de aplicativo. Neste cenário, a propriedade definida na interface de aplicativo chama-se **temperatura**.

O outro dispositivo chama-se *TemperatureSensor2*. Esse dispositivo publica eventos de temperatura que são medidos em graus Fahrenheit. O evento de temperatura é publicado no tópico `iot-2/evt/tempevt/fmt/json` e possui a carga útil de exemplo a seguir:
```
{
  “temp” : 72.55
}
```

**Nota:** o identificador de evento é *tempevt*. Esse identificador é necessário quando você inclui um evento de temperatura desse tipo na interface física e quando define mapeamentos para mapear uma propriedade associada a um evento de entrada desse tipo para uma propriedade em sua interface de aplicativo. Neste cenário, a propriedade definida na interface de aplicativo chama-se **temperatura**.

Uma interface de aplicativo também é configurada. Essa interface de aplicativo representa o estado para dispositivos desse tipo na estrutura a seguir:
```
{
  “temperature” : <current temperature value in Celsius>
  }
```
Essa configuração significa que é possível configurar seu aplicativo para processar o valor que está associado a **temperatura**, em vez de configurar o aplicativo para processar o valor que está associado a **t** e processar o valor que está associado a **temp** depois de converter esse valor em graus Celsius.

![Mapeamento entre dispositivos de sensor de temperatura e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/Information "Mapeamento entre dispositivos de sensor de temperatura e um aplicativo no {{site.data.keyword.iot_short_notm}}")  

Use o cenário de exemplo a seguir para configurar seu próprio ambiente de interfaces.

## Se necessário, inclua um Tipo de dispositivo e um Dispositivo
{: #step14}

Neste cenário, são assumidos dois tipos de dispositivo e duas instâncias de dispositivo. A instância de dispositivo *TemperatureSensor1* é associada ao tipo de dispositivo *EnvSensor1*. A instância de dispositivo *TemperatureSensor2* é associada ao tipo de dispositivo *EnvSensor2*.

Para obter informações sobre como usar as APIs de REST para incluir um tipo de dispositivo, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

## Etapa 1: Criar um arquivo de esquema de evento
{: #step1}

Para este cenário, crie dois arquivos de esquema de evento para definir a estrutura de cada um dos eventos de temperatura de entrada.

**Importante:** para cargas úteis de evento [JSON ![ícone de Link externo](../../../icons/launch-glyph.svg "ícone de Link externo")](http://json-schema.org/){:new_window} estruturadas, certifique-se de que cada nível de aninhamento seja agrupado adequadamente em uma entrada `"properties"`. Por exemplo, se a carga útil for `{"d":{"t":<temp>}}`, será possível usar:
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

O exemplo a seguir mostra como criar um arquivo de esquema chamado *tEventSchema.json*. Esse arquivo define a estrutura de um evento de entrada de um sensor de temperatura que mede temperatura em graus Celsius:

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
**Dica:** use o parâmetro “required” para marcar uma ou mais propriedades conforme necessário. As propriedades necessárias devem ser incluídas em uma mensagem do dispositivo para o Watson IoT Platform para atualizar o estado do dispositivo com os dados do dispositivo. Uma mensagem que não inclui a propriedade necessária não é processada.   

O nome do arquivo de esquema *tEventSchema* é usado quando você cria um recurso de esquema de evento para seu tipo de evento.

O exemplo a seguir mostra como criar um arquivo de esquema chamado *tempEventSchema.json*. Esse arquivo define a estrutura de um evento de entrada de um sensor de temperatura que mede a temperatura em graus Fahrenheit:

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
O nome do arquivo de esquema *tempEventSchema* é usado quando você cria um recurso de esquema de evento para seu tipo de evento.   

## Etapa 2: Criar um recurso de esquema de evento para seu tipo de evento
{: #step2}

Para criar um recurso de esquema de evento, use a API a seguir:

```
POST /schemas
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição  
------	|	-----  
name	|	Forneça um nome para o esquema de evento que você está criando.  
schemaFile	|	Caminho para o arquivo JSON do esquema de evento local.  



Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

O exemplo a seguir mostra como usar cURL para criar o recurso de esquema de evento *tEventSchema.json*:

```curl
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=tEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tEventSchema.json'
```

O exemplo a seguir mostra uma resposta para o método POST:

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
O identificador de esquema *5846cd7c6522050001db0e0d* retornado em resposta ao método POST é necessário quando você inclui um esquema de evento em seu tipo de evento.

O exemplo a seguir mostra como usar cURL para criar o recurso de esquema de evento *tempEventSchema.json*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: multipart/form-data’ \
  --form name=tempEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/tempEventSchema.json"'
```

O exemplo a seguir mostra uma resposta para o método POST:

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
O identificador de esquema *5846cee36522050001db0e0e* retornado em resposta ao método POST é necessário quando você inclui um esquema de evento em seu tipo de evento.

## Etapa 3: Criar um tipo de evento que referencie o esquema de evento
{: #step3}

Cada tipo de evento referencia o esquema de evento relevante que foi criado no exemplo anterior usando o identificador de esquema retornado na resposta para o método POST usado para criar o recurso de esquema de evento.

Para criar um tipo de evento, use a API a seguir:

```
POST /event/types
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
name	|	Forneça um nome para o tipo de evento que você está criando.
schemaId	|	O ID criado para o recurso de
esquema de evento.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


O exemplo a seguir mostra como usar cURL para criar um tipo de evento para um evento de temperatura que é medido em graus Celsius:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d”}'
```

O identificador de esquema *5846cd7c6522050001db0e0d* é usado para incluir o esquema de evento no tipo de evento. Esse identificador foi retornado em resposta ao método POST usado para criar o recurso de esquema de evento *tEventSchema.json*

O exemplo a seguir mostra uma resposta para o método POST:

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

O identificador de tipo de evento *5846d0fd6522050001db0e0f* retornado em resposta ao método POST é usado para incluir um tipo de evento na interface física.

O exemplo a seguir mostra como usar cURL para criar um tipo de evento para um evento de temperatura que é medido em graus Fahrenheit:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tempEvent", "schemaId" : "5846cee36522050001db0e0e"}'
```
O identificador de esquema *5846cee36522050001db0e0e* é usado para incluir o esquema de evento no tipo de evento. Esse identificador foi retornado em resposta ao método POST usado para criar o recurso de esquema de evento *tempEventSchema.json*

O exemplo a seguir mostra uma resposta para o método POST:

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
O identificador de tipo de evento *5846d2846522050001db0e10* retornado em resposta ao método POST é usado para incluir um tipo de evento na interface física.

## Etapa 4: Criar uma interface física
{: #step7}

Para criar uma interface física, use a API a seguir:

```
POST /physicalinterfaces
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
name	|	Forneça um nome para a interface física que você está criando.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Neste cenário, precisamos de duas interfaces físicas, uma para cada tipo de evento.

O exemplo a seguir mostra como usar cURL para criar a primeira interface física:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 1"}'
```

O exemplo a seguir mostra uma resposta para o método POST:

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

O identificador de interface física *5847d1df6522050001db0e1a* retornado na resposta é usado na URL do método POST que é chamado para incluir um evento de temperatura que é medido em graus Celsius para a interface física.

O exemplo a seguir mostra como usar cURL para criar a segunda interface física:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=‘ \
  --header 'content-type: application/json’ \
  --data '{"name" : "Env sensor physical interface 2"}'
```

O exemplo a seguir mostra uma resposta para o método POST:

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

O identificador de interface física *5847d1df6522050001db0e1b* retornado na resposta é usado na URL do método POST que é chamado para incluir um evento de temperatura que é medido em graus Fahrenheit para a interface física.   

## Etapa 5: Incluir o tipo de evento na interface física
{: #step8}

Para incluir um tipo de evento na interface física, use a API a seguir:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
eventId	|	Insira o nome do evento da sua carga útil do evento de dispositivo.
eventTypeId	|	O ID criado para o
tipo de evento.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Physical_Interfaces).

Neste cenário, os tipos de eventos a seguir são incluídos nas interfaces físicas especificadas:
- o evento de temperatura Celsius *tevt* é incluído na interface física com o identificador *5847d1df6522050001db0e1a* usando o *eventId* do tópico e o *eventTypeId* da criação do recurso de esquema de evento.
- o evento de temperatura Fahrenheit *tempevt* é incluído na interface física com o identificador *5847d1df6522050001db0e1b* usando o *eventId* do tópico e o *eventTypeId* da criação do recurso de esquema de evento.


O exemplo a seguir mostra como usar cURL para incluir o evento de temperatura *tevt* na interface física com o identificador *5847d1df6522050001db0e1a*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1a/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : “tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
```

O exemplo a seguir mostra uma resposta para o método POST:

```
{
  "eventTypeId" : "5846d0fd6522050001db0e0f",
  "eventId" : "tevt"
}
```

O exemplo a seguir mostra como usar cURL para incluir o evento de temperatura *tempevt* na interface física com o identificador *5847d1df6522050001db0e1b*:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/5847d1df6522050001db0e1b/events \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"eventId" : "tempevt", "eventTypeId" : "5846d2846522050001db0e10"}'
```

O exemplo a seguir mostra uma resposta para o método POST:

```
{
  "eventTypeId" : "5846d2846522050001db0e10",
  "eventId" : “tempevt"
}
```

## Etapa 6: Atualizar o tipo de dispositivo para conectar a interface física
{: #step9}

Para atualizar um tipo de dispositivo, use a API a seguir:

```
PUT /device/types/{typeId}
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
physicalInterfaceId	|	O ID criado para a interface física.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, o tipo de dispositivo *EnvSensor1* é atualizado para se conectar à interface física *5847d1df6522050001db0e1a* e o tipo de dispositivo *EnvSensor2* é atualizado para se conectar à interface física *5847d1df6522050001db0e1b*.

O exemplo a seguir mostra como usar cURL para atualizar o tipo de dispositivo *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a”}’
```

O exemplo a seguir mostra uma resposta para o método POST:

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
O identificador de dispositivo *EnvSensor1* é necessário quando você inclui sua interface física e sua interface de aplicativo.

O exemplo a seguir mostra como usar cURL para atualizar o tipo de dispositivo *EnvSensor2*:

```
curl --request PUT \ --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" :
"5847d1df6522050001db0e1b”}’
```

O exemplo a seguir mostra uma resposta para o método POST:

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
O identificador de dispositivo *EnvSensor2* é necessário quando você inclui sua interface física e sua interface de aplicativo.



## Etapa 7: Criar um arquivo de esquema de interface de aplicativo
{: #step4}

O exemplo a seguir mostra como criar um arquivo de esquema de interface de aplicativo chamado *envSensor.json*.

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

## Etapa 8: Criar um recurso de esquema de interface de aplicativo.
{: #step5}

Para criar um recurso de esquema de interface de aplicativo, use a API a seguir:

```
POST /schemas
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
name	|	Forneça um nome para o esquema de interface de aplicativo que você está criando.
schemaFile	|	Caminho
para o arquivo JSON do esquema de interface de aplicativo local.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

O exemplo a seguir mostra como usar cURL para criar o esquema de interface de aplicativo:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/schemas \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: multipart/form-data' \
  --form name=temperatureEventSchema \
  --form 'schemaFile=@"/Users/ANOther/Documents/IoT/DeviceState/deviceStateDemo/setup/schemas/envSensor.json"'
```

O exemplo a seguir mostra uma resposta para o método POST:

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
Use o identificador de esquema *5846ec826522050001db0e11* retornado na resposta ao método POST para incluir o esquema de interface de aplicativo na interface de aplicativo.

## Etapa 9: Criar uma interface de aplicativo que referencie um esquema de interface de aplicativo
{: #step6}

Para criar uma interface de aplicativo, use a API a seguir:

```
POST /applicationinterfaces
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
name	|	Forneça um nome para a interface de aplicativo que você está criando.
schemaId	|	O ID criado para o
recurso de esquema de interface de aplicativo.


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Application_Interfaces).

Neste cenário, use o identificador de esquema *5846ec826522050001db0e11* que foi retornado na resposta anterior para incluir o esquema de interface de aplicativo na interface de aplicativo.

O exemplo a seguir mostra como usar cURL para criar uma interface de aplicativo:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "environment sensor interface", "schemaId" : "5846ec826522050001db0e11"}'
```

O exemplo a seguir mostra uma resposta para o método POST:

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
Neste cenário, use o identificador de interface de aplicativo *5846ed076522050001db0e12* retornado na resposta ao método POST para incluir sua interface de aplicativo no tipo de dispositivo. Esse identificador também é usado para mapear um evento de dispositivo de entrada para uma propriedade que é definida pela interface de aplicativo.

## Etapa 10: Incluir a interface de aplicativo em um tipo de dispositivo
{: #step10}

Para incluir uma interface de aplicativo em um tipo de dispositivo, use a API a seguir:

```
POST /device/types/{typeId}/applicationinterfaces
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
id	|	O ID criado para a interface de aplicativo.
name	|	O nome do tipo de dispositivo.
schemaId	|	O ID criado
para o recurso da interface de aplicativo.
refs/schema	|	O caminho para o recurso da interface de aplicativo. Geralmente: /schemas/*schemaId*


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, a interface de aplicativo está associada ao tipo de dispositivo *EnvSensor1* e ao tipo de dispositivo *EnvSensor2*.

O exemplo a seguir mostra como usar cURL para incluir a interface de aplicativo *5846ed076522050001db0e12* que referencia o identificador de esquema de aplicativo *5846ec826522050001db0e11* no tipo de dispositivo *EnvSensor1*:

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

O exemplo a seguir mostra uma resposta para o método POST:

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

O exemplo a seguir mostra como usar cURL para incluir a interface de aplicativo *5846ed076522050001db0e12* associada ao identificador de esquema de aplicativo *5846ec826522050001db0e11* no tipo de dispositivo *EnvSensor2*:

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


O exemplo a seguir mostra uma resposta para o método POST:

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

## Etapa 11: definir mapeamentos para mapear propriedades no evento de entrada para propriedades na
interface de aplicativo
{: #step11}

Para mapear eventos, use a API a seguir:

```
POST /device/types/{typeId}/mappings
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
applicationInterfaceId	|	O ID criado para a interface de aplicativo.
propertyMappings	|	Uma estrutura JSON válida que mapeia propriedades definidas para a interface de aplicativo com as propriedades da carga útil do evento do dispositivo. Consulte os seguintes exemplos:


Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, definimos mapeamentos para o tipo de dispositivo *EnvSensor1* mapear a propriedade **t** no evento de entrada *tevt* para a propriedade **temperatura** na interface de aplicativo. Também definimos mapeamentos para o tipo de dispositivo *EnvSensor2* mapear a propriedade **temp** no evento de entrada *tempevt* para a propriedade **temperatura** na interface de aplicativo.

O exemplo a seguir mostra como usar cURL para incluir um mapeamento no tipo de dispositivo *EnvSensor1*:

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

**Importante:** para cargas úteis de evento [JSON ![ícone de Link externo](../../../icons/launch-glyph.svg "ícone de Link externo")](http://json-schema.org/){:new_window}, assegure-se de que a entrada $event.*property* corresponda corretamente à estrutura JSON de suas propriedades. Por exemplo, se a carga útil for `{"d":{"t":<temp>}}`, use `$event.d.t`

Especifique o identificador de interface de aplicativo *5846ed076522050001db0e12* retornado na resposta ao método POST usado para criar a interface de aplicativo e o tipo de dispositivo *EnvSensor1*.

O exemplo a seguir mostra uma resposta para o método POST:

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
O exemplo a seguir mostra como usar cURL para incluir um mapeamento no tipo de dispositivo *EnvSensor2*:

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

Especifique o identificador de interface de aplicativo *5846ed076522050001db0e12* retornado na resposta ao método POST usado para criar a interface de aplicativo e o tipo de dispositivo *EnvSensor2*.
É aplicada uma conversão para mudar o valor de uma medida em graus Fahrenheit para uma medida em graus Celsius.


O exemplo a seguir mostra uma resposta para o método POST:

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

## Etapa 12: Implementar a configuração
{: #step15}

Implemente a configuração que está relacionada à atualização do estado do dispositivo para cada tipo de
dispositivo. Essa configuração inclui seus esquemas, tipos de eventos, interfaces físicas, interfaces de aplicativo e mapeamentos.

Para implementar sua configuração de tipo de dispositivo, use a API a seguir:

```
PATCH /device/types/{typeId}
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
typeId	|	O ID do tipo de dispositivo

Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, precisamos implementar a configuração para dois tipos de dispositivos.

O exemplo a seguir mostra como usar cURL para implementar sua configuração para o tipo de dispositivo *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy-configuration"
          }'
```

O exemplo a seguir mostra uma resposta para o método PATCH:

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

O exemplo a seguir mostra como usar cURL para implementar sua configuração para o tipo de dispositivo *EnvSensor2*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
          }'
```

O exemplo a seguir mostra uma resposta para o método PATCH:

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

## Etapa 13: Publicar um evento de dispositivo de entrada
{: #step12}

Publique um evento de temperatura de *TemperatureSensor1* no tópico `iot-2/evt/tevt/fmt/json` e um evento de temperatura de *TemperatureSensor2* no tópico `iot-2/evt/tempevt/fmt/json`.

Para obter informações sobre como publicar um evento de entrada por meio de um dispositivo, veja [Conectividade MQTT para aplicativos](../applications/mqtt.html#publishing_device_events).


## Etapa 14: Verificar se o estado do dispositivo é mudado
{: #step13}

Para verificar o estado do dispositivo, use a API a seguir:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```

Os seguintes parâmetros são obrigatórios:  

Parâmetro	|	Descrição
------	|	-----
typeId	|	O ID do tipo de dispositivo deviceId	|	O ID do dispositivo.
applicationInterfaceId	|	O ID criado para a interface de aplicativo.

Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

O exemplo a seguir mostra como usar cURL para recuperar o estado atual de *TemperatureSensor1* referenciando o identificador da interface de aplicativo que foi criada:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

O identificador de interface de aplicativo *5846ed076522050001db0e12* é usado no método GET. Esse identificador é retornado na resposta ao método POST que foi usado para criar a interface de aplicativo.
O exemplo a seguir mostra uma resposta para o método GET:
```
{
  "temperature":34.5
}
```
O exemplo a seguir mostra como usar cURL para recuperar o estado atual de *TemperatureSensor2* referenciando o identificador da interface de aplicativo que foi criada:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2/devices/TemperatureSensor2/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

O identificador de interface de aplicativo *5846ed076522050001db0e12* é usado no método GET. Esse identificador é retornado na resposta ao método POST que foi usado para criar a interface de aplicativo.
O exemplo a seguir mostra uma resposta para o método GET:
```
{
  "temperature":22.5
}
```
Observe que a leitura de temperatura retornada está em graus Celsius e não em graus Fahrenheit.

Seu aplicativo pode processar esses dados normalizados sem requerer configuração para entender ou converter as diferentes escalas de temperatura.


**Nota:** para recuperar a configuração mais recente implementada, use a API a
seguir:

```
GET /device/types/<typeId>/deployedconfiguration
```
Use esta API para recuperar a configuração que foi implementada na última vez em que a operação de
implementação PATCH foi concluída com sucesso. Para recuperar a configuração de um recurso que foi mudado,
mas não implementado, utilize o método GET regular que está associado ao recurso que você deseja consultar.

Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

O exemplo a seguir mostra como usar cURL para recuperar a configuração mais recente implementada:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/deployedconfiguration \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```
O exemplo a seguir mostra uma resposta para o método GET:

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
