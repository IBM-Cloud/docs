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

# Usando interfaces para mapear dados do dispositivo (Beta)
{: #im_index}

Use o recurso de mapeamento de interface do {{site.data.keyword.iot_full}} para organizar e integrar dados de dispositivo recebidos e de saída.
{:shortdesc}

**Importante:** o recurso de mapeamento de interface está disponível no momento presente apenas como um recurso Beta. Antes da liberação final, é provável que as atualizações Beta incluirão mudanças incompatíveis com a versão atual. É altamente recomendável que os recursos Beta não sejam usados em aplicativos de produção até a liberação final. Para receber informações adicionais e fornecer feedback sobre esse Beta, [registre-se para o programa IM Beta](https://www.ibm.com/software/support/trial/cst/forms/nomination.wss?id=7050) e diga-nos o que pensa.

## Visão geral
{: #overview}

É possível usar o recurso de mapeamento de interface para desenvolver interfaces para seus aplicativos. Talvez você tenha tipos, criações ou modelos diferentes de dispositivos ou sensores que deseja conectar ao {{site.data.keyword.iot_short_notm}} e esses dispositivos podem publicar dados em formatos diferentes. Use o recurso de mapeamento de interface para normalizar dados recebidos e para simplificar seus aplicativos desacoplando-os das complexidades de como seus dispositivos específicos são conectados.

Por exemplo, é possível que você tenha dois sensores de temperatura. Um sensor mede a temperatura em graus Celsius e um sensor mede a temperatura em graus Fahrenheit.

![Mapeamento entre dispositivos de sensor de temperatura e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/Information "Mapeamento entre dispositivos de sensor de temperatura e um aplicativo no {{site.data.keyword.iot_short_notm}}")

O sensor de temperatura 1 publica uma leitura de temperatura de `{ "t" : 34.5 }` no {{site.data.keyword.iot_short_notm}}. Essa é uma leitura de temperatura com um valor em Celsius. O sensor de temperatura 2 publica uma leitura de temperatura de `{ "temp" : 72.55 }` no {{site.data.keyword.iot_short_notm}}. Esse é um tipo diferente de sensor de temperatura que tem uma leitura com um valor em Fahrenheit. As leituras de temperatura são publicadas como eventos separados no {{site.data.keyword.iot_short_notm}}.

Ao usar o recurso de mapeamento de interface, é possível normalizar essas leituras em um formato consistente para processamento. Não é necessário gravar seu aplicativo para entender ou converter escalas de temperatura diferentes. O aplicativo recebe uma visualização normalizada única e pode se conectar à **temperatura** em vez de se conectar a **t** e **temp**.

## Fluxo de dados entre dispositivos e aplicativos
{: #mapping}

O fluxograma a seguir mostra como os diferentes recursos no recurso de mapeamento de interface são usados:

![O fluxo entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/Information "O fluxo entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}")

O diagrama a seguir ilustra como os esquemas são usados neste fluxo:

![O fluxo entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/Information "O fluxo entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}")

Os esquemas JSON são usados para definir e validar o formato de eventos recebidos e o [estado do dispositivo](#key_concepts). Para obter mais informações sobre esses esquemas, veja [Esquemas](#resources).

## Conceitos-chave
{: #key_concepts}

O recurso de mapeamento de interface amplia o conceito atual de [tipo de dispositivo](#resources) incluindo um recurso de interface física e um recurso de interface de aplicativo para controlar melhor os dados que fluem pelo {{site.data.keyword.iot_short_notm}}.

O diagrama a seguir ilustra o mapeamento lógico entre dispositivos e aplicativos no {{site.data.keyword.iot_short_notm}} usando [recursos](#resources):

![O mapeamento lógico entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}.](images/im_mapping.svg "O mapeamento lógico entre um dispositivo e um aplicativo no {{site.data.keyword.iot_short_notm}}")

Mapeamento de interface refere-se ao conceito de um estado do dispositivo. O estado do dispositivo consiste em um conjunto de propriedades que são definidas pela interface de aplicativo. Os valores mais recentes dessas propriedades são armazenados no {{site.data.keyword.iot_short_notm}} e disponibilizados para o aplicativo por meio de solicitação usando uma API de HTTP.

Para processar dados de eventos de entrada e mapear propriedades no evento de entrada para as propriedades na interface de aplicativo, as informações a seguir devem ser configuradas:

- A estrutura de um ou mais eventos de entrada. O esquema de evento define essas informações. Cada esquema de evento define a estrutura de um evento de entrada e está associado a um tipo de evento. A interface física agrupa um ou mais tipos de eventos.

    A estrutura e o formato de dados contidos em um evento de dispositivo de entrada são definidos por um arquivo de esquema de evento que está no formato de esquema JSON. É possível fazer upload do arquivo de esquema de evento para o {{site.data.keyword.iot_short_notm}} usando um método POST para criar um recurso de esquema nomeado. Para Beta, todos os eventos de entrada devem estar no formato JSON.

- A estrutura do estado do dispositivo desejado. O esquema de interface de aplicativo define essas informações.

    O estado do dispositivo é uma representação da estrutura de dados e dos dados que seu aplicativo está configurado para receber como dados do dispositivo. Os valores de propriedade que são armazenados no estado do dispositivo são atualizados em resposta a um evento de dispositivo de entrada. Os valores de estado de dispositivo mais recentes são fornecidos para um aplicativo por meio de solicitação usando uma API de HTTP.

- Informações sobre como mapear os eventos de entrada para o estado de dispositivo preferencial. Os mapeamentos definem essas informações.

    Para mapear os dados contidos nas propriedades de um evento de entrada para as propriedades adequadas na interface de aplicativo, é necessário criar um mapeamento. O mapeamento descreve como atualizar as propriedades que são definidas por uma interface de aplicativo específica em resposta a um evento de entrada de um dispositivo.


## Recursos
{: #resources}

É possível gerenciar os recursos ilustrados nos diagramas anteriores usando APIs de REST. Para obter informações sobre as APIs de REST, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).

Recurso                        | Descrição       
------------- | ------------- | -------------  
Esquemas                         | Os esquemas JSON são usados para definir a estrutura de eventos de entrada que são publicados no {{site.data.keyword.iot_short_notm}} por meio de dispositivos e o estado do dispositivo desejado. Para obter mais informações sobre o Esquema JSON, veja [Esquema JSON](http://json-schema.org/). No mapeamento de interface, dois esquemas JSON são referenciados - esquemas de evento e esquemas de interface de aplicativo. Os esquemas de evento são usados para definir a estrutura dos eventos que são publicados no {{site.data.keyword.iot_short_notm}} por um dispositivo. Os esquemas de interface de aplicativo são referenciados pela interface do aplicativo e são usados para definir a estrutura do [estado do dispositivo](#key_concepts) que é armazenado no {{site.data.keyword.iot_short_notm}}.
Tipo de evento                         | Deve-se criar um tipo de evento dentro de sua organização para que o {{site.data.keyword.iot_short_notm}} possa processar os dados que estão contidos em um evento específico. Todos os tipos de eventos devem referenciar um esquema de evento. Para o beta, todos os eventos de entrada devem estar no formato JSON.   
Interface física                         | A interface física pode ser associada a um ou mais tipos de eventos e define quais tipos de eventos são associados a um tipo de dispositivo.  
Tipo de dispositivo                         | Cada dispositivo conectado ao Watson IoT Platform está associado a um tipo de dispositivo. Tipos de dispositivos são grupos de dispositivos que compartilham características ou comportamentos. No mapeamento de interface, o tipo de dispositivo é estendido para incluir uma interface física para um dispositivo e uma interface de aplicativo que pode ser usada para recuperar o estado do dispositivo. Um tipo de dispositivo pode ser configurado com múltiplas interfaces de aplicativo. Para obter mais informações sobre tipos de dispositivo, veja a seção "Identificadores e tipos de dispositivo" em [Modelo de dispositivo](../reference/device_model.html#id_and_device_types).
Interface de aplicativo                         | A interface de aplicativo deve referenciar um esquema de interface de aplicativo. Em sua interface de aplicativo, é possível definir a estrutura dos dados que são armazenados como o estado do dispositivo. O estado do dispositivo é uma representação da estrutura de dados e dos dados que um aplicativo está configurado para receber como dados do dispositivo. Pelo menos uma interface de aplicativo deve estar associada a um tipo de dispositivo antes que os mapeamentos possam ser definidos.
Mapeamentos                         | Os mapeamentos definem como as propriedades que estão associadas a eventos de entrada são mapeadas para propriedades definidas em uma interface de aplicativo específica. Um mapeamento deve especificar o identificador de interface de aplicativo ao qual se aplica e essa interface de aplicativo deve ser associada ao tipo de dispositivo em que o mapeamento está sendo incluído.


## Fluxo de trabalho de alto nível
{: #workflow}



### Sobre essa Tarefa

Use as etapas a seguir para ajudá-lo a configurar os recursos que você precisa para começar a mapear seus dados de dispositivo usando interfaces.

Para obter detalhes sobre a API, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html).
Para obter informações mais detalhadas sobre cada uma das etapas, veja o [Cenário de exemplo](#scenario) ou use os links para ir diretamente para uma etapa específica no cenário de exemplo.

### Configurar seu ambiente para começar a usar interfaces para mapear dados do dispositivo

1.  Se necessário, inclua um Tipo de dispositivo e um Dispositivo

  1. Crie um tipo de dispositivo usando o método POST de API de REST com o URI a seguir:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types
      ```
  2.  Inclua um dispositivo, se necessário.  
Para obter mais informações sobre como incluir um tipo de dispositivo e um dispositivo, veja [Conectando dispositivos](../iotplatform_task.html#devices)

2. Crie uma Interface física

  1. [Criar um arquivo de esquema de evento](#step1). O arquivo de esquema de evento é um arquivo .JSON local que define a estrutura e o formato de um evento de entrada.

  2. [Criar um recurso de esquema de evento para seu tipo de evento](#step2) usando o método POST de API de REST com o URI a seguir:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
      ```  

  3. [Criar um tipo de evento que referencia o esquema de evento](#step3) usando o método POST de API de REST com o URI a seguir:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/event/types
      ```
      Inclua o tipo de evento em seu esquema de evento usando o identificador de esquema que foi retornado em resposta ao método POST usado para criar o recurso de esquema de evento.

  4. [Criar uma interface física](#step7) usando o método POST de API de REST com o URI a seguir:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces
        ```

   5. [Incluir o tipo de evento na interface física](#step8) usando o método POST de API de REST com o URI a seguir:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/physicalinterfaces/{physicalInterfaceId}/events
        ```

       Inclua o tipo de evento em sua interface física usando o *eventId* do tópico e o identificador de tipo de evento *eventTypeId* que foi retornado em resposta ao método POST usado para criar o tipo de evento.       

3. Inclua sua interface física em seu tipo de dispositivo       

      [Atualizar o tipo de dispositivo para conectar a interface física](#step9) usando o método PUT de API de REST com o URI a seguir:
     ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
     ```

4. Crie uma Interface de aplicativo

  1. [Criar um arquivo de esquema de interface de aplicativo](#step4). O arquivo de esquema de interface de aplicativo é um arquivo .JSON local que define o estado do dispositivo.

  2. [Criar um recurso de esquema de interface de aplicativo](#step5) usando o método POST de API de REST com o URI a seguir:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/schemas
        ```     

  3. [Criar uma interface de aplicativo que referencia um esquema de interface de aplicativo](#step6) usando o método POST de API de REST com o URI a seguir:
         ```
         https://**orgId**.internetofthings.ibmcloud.com/api/v0002/applicationinterfaces
         ```  

        A interface de aplicativo referencia o esquema de interface de aplicativo usando o identificador de esquema que foi retornado em resposta ao método POST usado para criar o recurso de esquema de interface de aplicativo.

  4. [Incluir a interface de aplicativo em um tipo de dispositivo](#step10) usando o método POST de API de REST com o URI a seguir:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/types/{typeId}/applicationinterfaces
        ```

        Inclua sua interface de aplicativo no tipo de dispositivo usando a resposta para o método POST que foi usado para criar a interface de aplicativo.

5. Defina os mapeamentos para o tipo de dispositivo

  [Definir mapeamentos para mapear propriedades no evento de entrada para propriedades na interface de aplicativo](#step11) usando o método POST de API de REST com o URI a seguir:       
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/mappings/{applicationInterfaceId}
      ```

6. Implemente a configuração que está associada ao tipo de dispositivo

  [Implementar a configuração](#step15) no {{site.data.keyword.iot_short_notm}} usando o método PATCH de API de REST com o URI a seguir:
      ```
      https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}
      ```

7. Verifique se os eventos de dispositivo mapeados foram publicados na interface de aplicativo

  1. [Publicar um evento de dispositivo de entrada](#step12).

  2. [Verificar se o estado do dispositivo mudou](#step13) usando o método GET de API de REST com o URI a seguir:
        ```
        https://**orgId**.internetofthings.ibmcloud.com/api/v0002/device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
        ```

## Cenário de exemplo
{: #scenario}

Use as informações a seguir para criar um cenário no qual dois sensores de temperatura publiquem eventos no {{site.data.keyword.iot_short_notm}}. Um sensor mede a temperatura em graus Celsius. O outro sensor mede a temperatura em graus Fahrenheit. Essas leituras são mapeadas para uma única leitura de temperatura que está em graus Celsius. Quando uma nova leitura de temperatura é publicada por esses dispositivos, o valor da propriedade associada ao estado do dispositivo muda.

### Pré-requisitos

Deve-se ter uma instância de organização do {{site.data.keyword.iot_short_notm}} e uma chave ou um token API para essa organização. Para obter mais informações sobre chaves e tokens API, veja [API de REST HTTP para aplicativos](../applications/api.html#authentication).

### Sobre este cenário

Neste cenário, dois dispositivos estão configurados.

Um dispositivo chama-se *TemperatureSensor1*. Esse dispositivo publica eventos de temperatura que são medidos em graus Celsius. O evento de temperatura é publicado no tópico `iot-2/evt/tevt/fmt/json` e possui a carga útil de exemplo a seguir:
```
{
  "t" : 34.5
}
```

**Nota:** o identificador de evento é *tevt*. Esse identificador é necessário quando você inclui um evento de temperatura desse tipo na interface física e quando define mapeamentos para mapear uma propriedade associada a um evento de entrada desse tipo para uma propriedade em sua interface de aplicativo. Neste cenário, a propriedade definida na interface de aplicativo chama-se **temperatura**.

O outro dispositivo chama-se *TemperatureSensor2*. Esse dispositivo publica eventos de temperatura que são medidos em graus Fahrenheit. O evento de temperatura é publicado no tópico `iot-2/evt/tempevt/fmt/json` e possui a carga útil de exemplo a seguir:
```
{
  "temp" : 72.55
}
```

**Nota:** o identificador de evento é *tempevt*. Esse identificador é necessário quando você inclui um evento de temperatura desse tipo na interface física e quando define mapeamentos para mapear uma propriedade associada a um evento de entrada desse tipo para uma propriedade em sua interface de aplicativo. Neste cenário, a propriedade definida na interface de aplicativo chama-se **temperatura**.

Uma interface de aplicativo também é configurada. Essa interface de aplicativo representa o estado para dispositivos desse tipo na estrutura a seguir:
```
{
  "temperature" : <current temperature value in Celsius>
  }
```
Essa configuração significa que é possível configurar seu aplicativo para processar o valor que está associado a **temperatura**, em vez de configurar o aplicativo para processar o valor que está associado a **t** e processar o valor que está associado a **temp** depois de converter esse valor em graus Celsius.

## Etapas

Use as informações a seguir para configurar o cenário de exemplo usando interfaces.

### Se necessário, inclua um Tipo de dispositivo e um Dispositivo
{: #step14}

Neste cenário, são assumidos dois tipos de dispositivo e duas instâncias de dispositivo. A instância de dispositivo *TemperatureSensor1* é associada ao tipo de dispositivo *EnvSensor1*. A instância de dispositivo *TemperatureSensor2* é associada ao tipo de dispositivo *EnvSensor2*.

Para obter informações sobre como usar as APIs de REST para incluir um tipo de dispositivo, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Types).

### Criar um arquivo de esquema de evento
{: #step1}

Para este cenário, crie dois arquivos de esquema de evento para definir a estrutura de cada um dos eventos de temperatura de entrada.

O exemplo a seguir mostra como criar um arquivo de esquema chamado *tEventSchema.json*. Esse arquivo define a estrutura de um evento de entrada de um sensor de temperatura que mede temperatura em graus Celsius:

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

O nome do arquivo de esquema *tEventSchema* é usado quando você cria um recurso de esquema de evento para seu tipo de evento.

O exemplo a seguir mostra como criar um arquivo de esquema chamado *tempEventSchema.json*. Esse arquivo define a estrutura de um evento de entrada de um sensor de temperatura que mede a temperatura em graus Fahrenheit:

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
O nome do arquivo de esquema *tempEventSchema* é usado quando você cria um recurso de esquema de evento para seu tipo de evento.   

### Criar um recurso de esquema de evento para seu tipo de evento
{: #step2}

Para criar um recurso de esquema de evento, use a API a seguir:

```
POST /schemas
```
Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Schemas).

O exemplo a seguir mostra como usar cURL para criar o recurso de esquema de evento *tEventSchema.json*:

```
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

### Criar um tipo de evento que referencia o esquema de evento
{: #step3}

Cada tipo de evento referencia o esquema de evento relevante que foi criado no exemplo anterior usando o identificador de esquema retornado na resposta para o método POST usado para criar o recurso de esquema de evento.



Para criar um tipo de evento, use a API a seguir:

```
POST /event/types
```

Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Event_Types).


O exemplo a seguir mostra como usar cURL para criar um tipo de evento para um evento de temperatura que é medido em graus Celsius:

```
curl --request POST \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/event/types \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"name" : "tEvent", "schemaId" : "5846cd7c6522050001db0e0d"}'
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
  "name" : "tempEvent",
  "refs" : {
    "schema" : "/schemas/5846cee36522050001db0e0e"
  },
  "updatedBy" : "a-8x7nmj-9iqt56kfil"
}
```
O identificador de tipo de evento *5846d2846522050001db0e10* retornado em resposta ao método POST é usado para incluir um tipo de evento na interface física.

### Criar uma interface física
{: #step7}

Para criar uma interface física, use a API a seguir:

```
POST /physicalinterfaces
```
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

### Incluir o tipo de evento na interface física
{: #step8}

Para incluir um tipo de evento na interface física, use a API a seguir:

```
POST /physicalinterfaces/{physicalInterfaceId}/events
```
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
  --data '{"eventId" : "tevt", "eventTypeId" : "5846d0fd6522050001db0e0f"}'
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
  "eventId" : "tempevt"
}
```

### Atualizar o tipo de dispositivo para conectar a interface física
{: #step9}

Para atualizar um tipo de dispositivo, use a API a seguir:

```
PUT /device/types/{typeId}
```

Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, o tipo de dispositivo *EnvSensor1* é atualizado para se conectar à interface física *5847d1df6522050001db0e1a* e o tipo de dispositivo *EnvSensor2* é atualizado para se conectar à interface física *5847d1df6522050001db0e1b*.

O exemplo a seguir mostra como usar cURL para atualizar o tipo de dispositivo *EnvSensor1*:

```
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an environment sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1a"}’
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
curl --request PUT \
--url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor2 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{"description" : "an env sensor","deviceInfo" : {},"metadata" : {}, "physicalInterfaceId" : "5847d1df6522050001db0e1b"}’
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



### Criar um arquivo de esquema de interface de aplicativo
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

### Criar um recurso de esquema de interface de aplicativo
{: #step5}

Para criar um recurso de esquema de interface de aplicativo, use a API a seguir:

```
POST /schemas
```
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

### Criar uma interface de aplicativo que referencia um esquema de interface de aplicativo
{: #step6}

Para criar uma interface de aplicativo, use a API a seguir:

```
POST /applicationinterfaces
```
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

### Incluir a interface de aplicativo em um tipo de dispositivo
{: #step10}

Para incluir uma interface de aplicativo em um tipo de dispositivo, use a API a seguir:

```
POST /device/types/{typeId}/applicationinterfaces
```
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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
          "updatedBy" : "a-8x7nmj-9iqt56kfil","id" : "5846ed076522050001db0e12","updated" : "2016-12-06T16:53:27Z","name" : "environment sensor interface"
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

### Definir mapeamentos para mapear propriedades no evento de entrada para propriedades na interface de aplicativo
{: #step11}

Para mapear eventos, use a API a seguir:

```
POST /device/types/{typeId}/mappings
```
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

### Implementar a configuração
{: #step15}

Implemente a configuração que está relacionada à atualização do estado do dispositivo para cada tipo de dispositivo. Essa configuração inclui seus esquemas, tipos de eventos, interfaces físicas, interfaces de aplicativo e mapeamentos.

Para implementar sua configuração de tipo de dispositivo, use a API a seguir:

```
PATCH /device/types/{typeId}
```
Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

Neste cenário, precisamos implementar a configuração para dois tipos de dispositivos.

O exemplo a seguir mostra como usar cURL para implementar sua configuração para o tipo de dispositivo *EnvSensor1*:

```
curl --request PATCH \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1 \
  --header 'authorization: Basic MK2fdJpobP6tOWlhgTR2a4Hklss2eXC7AZIxZWxPL9B8XlVwSZL=' \
  --header 'content-type: application/json' \
  --data '{
            "operation" : "deploy"
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

### Publicar um evento de dispositivo de entrada
{: #step12}

Publique um evento de temperatura de *TemperatureSensor1* no tópico `iot-2/evt/tevt/fmt/json` e um evento de temperatura de *TemperatureSensor2* no tópico `iot-2/evt/tempevt/fmt/json`.

Para obter informações sobre como publicar um evento de entrada por meio de um dispositivo, veja [Conectividade MQTT para aplicativos](../applications/mqtt.html#publishing_device_events).


### Verificar se o estado do dispositivo mudou
{: #step13}

Para verificar o estado do dispositivo, use a API a seguir:
```
GET /device/types/{typeId}/devices/{deviceId}/state/{applicationInterfaceId}
```
Para obter mais detalhes, veja a documentação da [API de REST HTTP do {{site.data.keyword.iot_short_notm}}](https://docs.internetofthings.ibmcloud.com/swagger/info-mgmt-beta.html#!/Device_Types).

O exemplo a seguir mostra como usar cURL para recuperar o estado atual de *TemperatureSensor1* referenciando o identificador da interface de aplicativo que foi criada:
```
curl --request GET \
  --url https://yourOrgID.internetofthings.ibmcloud.com/api/v0002/device/types/EnvSensor1/devices/TemperatureSensor1/state/5846ed076522050001db0e12 \
  --header 'authorization: Basic TGS04NXg5dHotKNBzbGZ5eWdiaToxX543S0lKOmE3Tk5Mc0xMu6n='
```

O identificador de interface de aplicativo *5846ed076522050001db0e12* é usado no método GET. Esse identificador é retornado na resposta ao método POST que foi usado para criar a interface de aplicativo. O exemplo a seguir mostra uma resposta para o método GET:
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

O identificador de interface de aplicativo *5846ed076522050001db0e12* é usado no método GET. Esse identificador é retornado na resposta ao método POST que foi usado para criar a interface de aplicativo. O exemplo a seguir mostra uma resposta para o método GET:
```
{
  "temperature":22.5
}
```
Observe que a leitura de temperatura retornada está em graus Celsius e não em graus Fahrenheit.

Seu aplicativo pode processar esses dados normalizados sem requerer configuração para entender ou converter as diferentes escalas de temperatura.
