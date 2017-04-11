---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python para desenvolvedores de aplicativos
{: #python}


É possível usar Python para construir e desenvolver aplicativos que interagem com sua organização no {{site.data.keyword.iot_full}}. O cliente Python para o {{site.data.keyword.iot_short_notm}} fornece uma API (interface de programação de aplicativos) para facilitar interação simples com recursos do {{site.data.keyword.iot_short_notm}} abstraindo os protocolos subjacentes, como MQTT e HTTP (Protocolo de Transporte de Hipertexto).

{:shortdesc}

Use as informações e exemplos que são fornecidos para iniciar o desenvolvimento de seus aplicativos usando Python.

## Fazendo download de cliente e recursos do Python
{: #python_client_download}

Para acessar o cliente Python para o {{site.data.keyword.iot_short_notm}} e outros recursos disponíveis, acesse o repositório [iot-python ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-python){: new_window} no GitHub e conclua as instruções de instalação.

## Construtor
{: #constructor}

O dicionário de opções cria definições que são usadas para interagir com o módulo do {{site.data.keyword.iot_short_notm}}. O construtor cria a instância do cliente e aceita o dicionário de opções que contém as definições a seguir:

|Definição|Descrição |
|:-----|:-----|
|`orgId`|O ID de sua organização.|
|`appId`|O ID exclusivo de um aplicativo em sua organização.|
|`auth-method`|O método de autenticação. O único método que é suportado é `apikey`.|
|`auth-key`|Uma chave API opcional que se deve especificar ao configurar o valor de método de autenticação para `apikey`.|
|`auth-token`|Um token de chave API que também é necessário ao configurar o valor de método de autenticação para `apikey`.|
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao aplicativo no modo de assinatura durável. Por padrão, `clean-session` é configurado como true.|


Se nenhum dicionário de opções for fornecido, o cliente conecta-se ao serviço de iniciação rápida do {{site.data.keyword.iot_short_notm}} como um dispositivo não registrado.

```python

import ibmiotf.application
try:
  options = {
    "org": organization,
    "id": appId,
    "auth-method": authMethod,
    "auth-key": authKey,
    "auth-token": authToken,
    "clean-session": true
  }
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException  as e:
...
```

### Usando um arquivo de configuração


Se você não estiver usando um dicionário de opções, deve-se incluir um arquivo de configuração que contenha um dicionário de opções no formato de código a seguir:

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
O arquivo de configuração de aplicativo deve estar no seguinte formato:

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## Chamadas API
{: #api_calls}

Cada método no cliente da API (interface de programação de aplicativos) responde de uma das maneiras a seguir:

- Uma resposta JSON ou booleana válida, se bem-sucedido
- Uma exceção IoTFCReSTException, se mal sucedido

Para obter mais informações sobre por que uma chamada API (interface de programação de aplicativos) falhou ou para ver se a ação foi parcialmente bem-sucedida, um aplicativo pode analisar as propriedades de uma resposta excepcional. A resposta excepcional IoTFCReSTException contém as propriedades a seguir:

|Propriedade|Descrição|
|:---|:---|
|`httpcode`|O código de status de HTTP.|
|`message`|Uma mensagem de exceção que contém a razão da falha.|
|`response`|O elemento JSON que contém a resposta parcial. Se não existir nenhum, esse valor será configurado como nulo.|

## Assinando eventos de dispositivo
{: #subscribe_device_events}

Eventos são o mecanismo pelo qual os dispositivos publicam dados na instância do {{site.data.keyword.iot_short_notm}}. O dispositivo controla o conteúdo do evento e designa um nome para cada evento que ele envia.

Quando um evento é recebido pela instância do {{site.data.keyword.iot_short_notm}}, as credenciais do evento recebido identificam o dispositivo de envio, o que possibilita que um dispositivo personifique outro dispositivo.

Por padrão, os aplicativos assinam todos os eventos de todos os dispositivos conectados. Use os parâmetros deviceType, deviceId, event e msgFormat para controlar o escopo da assinatura. Um único cliente pode suportar várias assinaturas. As amostras de código a seguir mostram como é possível usar os parâmetros deviceType, deviceId, event e msgFormat para definir o escopo de uma assinatura:


### Assinando todos os eventos de todos os dispositivos


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Assinando todos os eventos de todos os dispositivos de um tipo específico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Assinando um evento específico de todos os dispositivos


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Assinando um evento específico de dois ou mais dispositivos diferentes

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Assinando todos os eventos publicados no formato JSON

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Manipulando eventos a partir de dispositivos
{: #handling_events_devices}

Para processar os eventos que são recebidos por suas assinaturas, você precisa registrar um método de retorno de chamada de evento. As mensagens são retornadas como uma instância na Classe de eventos:

|Propriedade|Tipo de Dados|Descrição|
|:---|:---|
|`event.device`|Seqüência de caracteres|Identifica o dispositivo de forma exclusiva entre todos os tipos de dispositivos na organização|
|`event.deviceType`|Seqüência de caracteres|Identifica o tipo de dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`event.deviceId`|Seqüência de caracteres|Representa o ID do dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`event.event`|Seqüência de caracteres|Normalmente usado para agrupar eventos específicos, por exemplo, "status", "warning" e "data".
|`event.format`|Seqüência de caracteres|O formato pode ser qualquer sequência, por exemplo, JSON.
|`event.data`|Dicionário|Os dados para a carga útil da mensagem. O comprimento máximo é 131072 bytes.
|`event.timestamp`|Date and time|A data e hora do evento|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  def myEventCallback(event):
      str = "%s event '%s' received from device [%s]: %s"
      print(str % (event.format, event.event, event.device, json.dumps(event.data)))

...
client.connect()
client.deviceEventCallback = myEventCallback
client.subscribeToDeviceEvents()
```


## Assinando status do dispositivo
{: #subscribe_device_status}


Por padrão, quando você assina status de dispositivo, atualizações de status são recebidas para todos os dispositivos conectados. Use os parâmetros tipo e ID para controlar o escopo da assinatura. Um único cliente pode suportar várias assinaturas.

### Assinando atualizações de status para todos os dispositivos


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Assinando atualizações de status para todos os dispositivos de um tipo específico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Assinando atualizações de status para dois dispositivos diferentes


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Manipulando atualizações de status a partir de dispositivos
{: #handling_device_updates}

Eventos de Status

Para processar as atualizações de status que são recebidas por suas assinaturas, você precisa registrar um método de retorno de chamada de evento. As mensagens são retornadas como uma instância da classe de status.

Há dois tipos de eventos de status, `Connect` e `Disconnect`. Todos os eventos de status incluem as propriedades a seguir:

|Propriedade|Tipo de Dados|
|:---|:---|
|`status.clientAddr`|Seqüência de caracteres|
|`status.protocol`|Seqüência de caracteres|
|`status.clientId`|Seqüência de caracteres|
|`status.user`|Seqüência de caracteres|
|`status.time`|Date and time|
|`status.action`|Seqüência de caracteres|
|`status.connectTime`|Date and time|
|`status.port`|Integer|


A propriedade `status.action` determina se um evento de status é do tipo `Connect` ou `Disconnect`.

Os eventos de status `Disconnect` incluem as propriedades adicionais a seguir:

|Propriedade|Tipo de Dados|
|:---|:---|
|`status.writeMsg`|Integer|
|`status.readMsg`|Integer|
|`status.reason`|Seqüência de caracteres|
|`status.readBytes`|Integer|
|`status.writeBytes`|Integer|

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

def myStatusCallback(status):

  if status.action == "Disconnect":
    str = "%s - device %s - %s (%s)"
    print(str % (status.time.isoformat(), status.device, status.action, status.reason))
    else:
      print("%s - %s - %s" % (status.time.isoformat(), status.device, status.action))
  ...
client.connect()
client.deviceStatusCallback = myStatusCallback
client.subscribeToDeviceStstus()
```


## Publicando eventos a partir de dispositivos
{: #publishing_device_events}

Os aplicativos podem publicar eventos como se eles tivessem originado de um dispositivo.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Publicando comandos para dispositivos
{: #publishing_commands_devices}


Os aplicativos podem publicar comandos para dispositivos conectados.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## Detalhes da organização
{: #org_details}

Os aplicativos podem usar o método `getOrganizationDetails()` para recuperar os detalhes sobre a configuração da organização.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

Para obter informações sobre o modelo de solicitação e de resposta e sobre os códigos de status HTTP, veja a seção Configuração da organização da API do [{{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


## Operações do dispositivo em massa
{: #bulk_device_ops}

Seus aplicativos podem usar operações em massa para obter, incluir ou remover diversos dispositivos simultaneamente.

Para obter informações sobre a lista de parâmetros de consulta, o modelo de solicitação e de resposta e os códigos de status HTTP, veja a seção 'Operações em massa' da API do [{{site.data.keyword.iot_short_notm}} API ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Bulk_Operations/){: new_window}.


### Recuperando Informações sobre o Dispositivo

Informações em massa sobre o dispositivo podem ser recuperadas usando o método `getAllDevices()`. Esse método recupera informações sobre todos os dispositivos registrados na organização. Cada solicitação pode conter no máximo 512 KB.

A resposta contém parâmetros que são necessários para o aplicativo. Use os resultados do dicionário que aparecem na resposta para obter a matriz de dispositivos que é retornada. Outros parâmetros na resposta são necessários para fazer mais chamadas, por exemplo, o elemento `_bookmark` pode ser usado para percorrer os resultados. Envie a primeira solicitação sem especificar um marcador, em seguida, pegue o marcador retornado na resposta e forneça-o na solicitação da próxima página. Repita até o final do conjunto de resultados, que é indicado pela ausência de um marcador. Cada solicitação deve usar os mesmos valores para os outros parâmetros, caso contrário, os resultados serão indefinidos.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Incluindo vários dispositivos


Use o método `addMultipleDevices()` para incluir um ou mais dispositivos em sua organização do {{site.data.keyword.iot_short_notm}}. Uma solicitação não pode ser maior que 512 KB. A resposta contém os tokens de autenticação que foram gerados para cada dispositivo. Assegure que seja feita uma cópia dos tokens de autenticação, pois se você perder os tokens de autenticação, eles não poderão ser recuperados.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
  deviceList = client.api.addMultipleDevices(listOfDevicesToAdd)
except IoTFCReSTException as e:
  print("ERROR [" + e.httpcode + "] " + e.message)
```

### Excluindo vários dispositivos


Use o método `deleteMultipleDevices()` para excluir diversos dispositivos de uma organização do {{site.data.keyword.iot_short_notm}}. Uma solicitação não pode ser maior que 512 KB.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  listOfDevicesToDelete = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
      deviceList = client.api.deleteMultipleDevices(listOfDevicesToDelete)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Operações do tipo de dispositivo
{: #device_type_ops}

Os tipos de dispositivo que você cria em sua organização podem ser usados para criar modelos para incluir dispositivos. Usando os recursos da API (interface de programação de aplicativos) do {{site.data.keyword.iot_short_notm}}, seus aplicativos podem listar, criar, excluir, visualizar ou atualizar tipos de dispositivo em sua organização.

Para obter informações sobre os parâmetros de consulta, o modelo de solicitação e de resposta e os códigos de status HTTP, veja a seção 'Tipos de dispositivo' da documentação da API do [{{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


### Recuperando todos os tipos de dispositivo

Use o método `getAllDeviceTypes()` para recuperar todos os tipos de dispositivo que estão em sua organização do {{site.data.keyword.iot_short_notm}}.
Use os resultados do dicionário que aparecem na resposta para obter a matriz de dispositivos que é retornada. Outros parâmetros na resposta são necessários para fazer mais chamadas, por exemplo, o elemento `_bookmark` pode ser usado para percorrer os resultados. Envie a primeira solicitação sem especificar um marcador, em seguida, pegue o marcador retornado na resposta e forneça-o na solicitação da próxima página. Repita esse processo até o final do conjunto de resultados, que é indicado pela ausência de um marcador. Cada solicitação deve usar os mesmos valores para os outros parâmetros, caso contrário, os resultados serão indefinidos.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

 listOfDevicesToAdd = [
      {'typeId' : "pi-model-a", 'deviceId' : '200020002004'},
      {'typeId' : "pi-model-b", 'deviceId' : '200020002005'}
  ]

try:
   options = {'_limit' : 2}
   deviceTypeList = client.api.getAllDeviceTypes(options)
except IoTFCReSTException as e:
   print("ERROR [" + e.httpcode + "] " + e.message)

```

### Incluindo um tipo de dispositivo

Use o método `addDeviceType()` para registrar um tipo de dispositivo para sua instância do {{site.data.keyword.iot_short_notm}}. Em cada solicitação, deve-se primeiro definir as informações sobre o dispositivo e os elementos de metadados do dispositivo que você deseja que sejam aplicados a todos os dispositivos desse tipo. O elemento de informações sobre o dispositivo consiste em várias variáveis, que incluem número de série, fabricante, modelo, classe, descrição, firmware, versões de hardware e localização descritiva. O elemento de metadados consiste em variáveis e valores customizados que podem ser definidos pelo usuário.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2"
  }

try:
      deviceType = client.api.addDeviceType(deviceType = "myDeviceType", description = "My first device type", deviceInfo = info, metadata = meta)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Excluindo um tipo de dispositivo


Use o método `deleteDeviceType()` para excluir um tipo de dispositivo de sua organização do{{site.data.keyword.iot_short_notm}}.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Recuperando informações de tipos de dispositivo específicos


Use o método `getDeviceType()` para recuperar informações para um tipo de dispositivo específico. O `typeId` do tipo de dispositivo que você deseja recuperar deve ser especificado como um parâmetro.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Atualizando um tipo de dispositivo


Use o método `updateDeviceType()` para modificar as propriedades de um tipo de dispositivo. Quando você usa o método `updateDeviceType()`, primeiro especifique o `typeId` do tipo de dispositivo a ser atualizado e, em seguida, especifique os elementos a seguir:

- `description`
- `deviceInfo`
- `metadata`

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

  info = {
      "serialNumber": "100087",
      "manufacturer": "ACME Co.",
      "model": "7865",
      "deviceClass": "A",
      "description": "My shiny device",
      "fwVersion": "1.0.0",
      "hwVersion": "1.0",
      "descriptiveLocation": "Office 5, D Block"
  }
  meta = {
      "customField1": "customValue1",
      "customField2": "customValue2",
      "customField3": "customValue3"
  }

try:
      updatedDeviceTypeInfo = client.api.updateDeviceType("myDeviceType", "New description", deviceInfo, metadata)
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```


## Operações do dispositivo
{: #device_ops}

As operações do dispositivo disponibilizadas na API (interface de programação de aplicativos) incluem listar, incluir, remover, visualizar, atualizar, visualizar localização e visualizar informações de gerenciamento do dispositivo em uma organização do {{site.data.keyword.iot_short_notm}}.

Para obter informações sobre os parâmetros de consulta, o modelo de solicitação e de resposta e os códigos de status HTTP, veja a 'Seção Dispositivo' da API do [{{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


### Recuperando dispositivos de um tipo de dispositivo específico

Use o método `retrieveDevices()` para recuperar todos os dispositivos de um tipo de dispositivo específico em uma organização em uma instância do {{site.data.keyword.iot_short_notm}}, o que é mostrado no exemplo a seguir:


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Use os resultados do dicionário que aparecem na resposta para obter a matriz de dispositivos que é retornada. Outros parâmetros na resposta são necessários para fazer mais chamadas, por exemplo, o elemento *_bookmark* pode ser usado para percorrer os resultados. Envie a primeira solicitação sem especificar um marcador, em seguida, pegue o marcador retornado na resposta e forneça-o na solicitação da próxima página. Repita até o final do conjunto de resultados, que é indicado pela ausência de um marcador. Cada solicitação deve usar os mesmos valores para os outros parâmetros, caso contrário, os resultados serão indefinidos.

Para passar *_bookmark* ou qualquer outra condição, o método sobrecarregado deve ser usado. O método sobrecarregado aceita os parâmetros no formato de dicionário, conforme mostrado no exemplo a seguir:

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

A amostra de código anterior classifica a resposta com base no ID do dispositivo e, em seguida, usa o marcador para percorrer os resultados.

### Incluindo um Dispositivo


Para incluir um dispositivo em uma organização do {{site.data.keyword.iot_short_notm}}, use o método `registerDevice()`. O método `registerDevice()` inclui um único dispositivo em sua organização do {{site.data.keyword.iot_short_notm}}. Ao incluir um dispositivo, é possível especificar os parâmetros a seguir:

|Parâmetro|Requirement|Descrição
|:---|:---|
|`deviceTypeId`|Optional|Atribui um tipo de dispositivo para o dispositivo. Se existir um conflito entre as variáveis definidas pelo tipo de dispositivo e as variáveis definidas pela variável `deviceInfo`, as variáveis específicas do dispositivo terão precedência.|
|`deviceId`|Mandatório||
|`authToken`|Optional|Se não fornecido, um token de autenticação será gerado e incluído na resposta.|
|`deviceInfo`|Optional|Contém diversas variáveis que incluem serialNumber, manufacturer, model, deviceClass, description, descriptiveLocation, firmware e versões de hardware.|
|`metadata`|Optional|Pares de sequência de valores de campo customizado, conforme esboçado em [Código de amostra para incluir um tipo de dispositivo](#sample_device_type).|
|`location`|Optional|Contém as variáveis longitude, latitude, elevation, accuracy e measuredDateTime.|

Para obter informações sobre esses parâmetros, o formato e os códigos de resposta, veja a documentação da API do [ ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window}.

Ao usar o método `registerDevice()`, defina o parâmetro deviceID obrigatório e os parâmetros opcionais necessários para seu dispositivo, em seguida, chame o método usando os parâmetros selecionados.

### Código de amostra para incluir um tipo de dispositivo
{: #sample_device_type}

Insira o código a seguir após o código do construtor no arquivo de script Python(.py). A amostra demonstra um método para incluir um tipo de dispositivo definindo os parâmetros deviceId, authToken, metadata, deviceInfo e location.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Excluindo um Dispositivo

Use o método `deleteDevice()` para remover um dispositivo de uma organização na organização do {{site.data.keyword.iot_short_notm}}. Ao excluir um dispositivo usando o método `deleteDevice()`, deve-se especificar os parâmetros deviceTypeId e deviceId.

A amostra de código a seguir esboça o formato necessário para esse método:

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Obtendo um dispositivo

Use o método `getDevice()` para recuperar um dispositivo de uma organização no {{site.data.keyword.iot_short_notm}}. Ao recuperar detalhes do dispositivo usando o método `getDevice()`, deve-se especificar os parâmetros deviceTypeId e deviceId

A amostra de código a seguir fornece um esboço do formato necessário para esse método.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Recuperando todos os dispositivos

Use o método `getAllDevices()` para recuperar todos os dispositivos de uma organização no {{site.data.keyword.iot_short_notm}}.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Atualizando um dispositivo

Para modificar uma ou mais propriedades de um dispositivo, use o método `updateDevice()`.

É possível atualizar qualquer propriedade nos parâmetros deviceInfo ou metadata. Para atualizar uma propriedade do dispositivo. defina o parâmetro deviceInfo antes de chamar o método `updateDevice()`. O parâmetro de status deve conter `alert`: True. A propriedade alert controla se um dispositivo exibe códigos de erro na interface com o usuário do {{site.data.keyword.iot_short_notm}} e deve estar configurada por padrão para `enabled`: True, conforme esboçado no exemplo de código a seguir:

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Código de amostra para atualizar as propriedades de deviceInfo

A amostra de código a seguir identifica um dispositivo específico e, em seguida, atualiza várias propriedades do parâmetro deviceInfo.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Recuperando informações de localização


Use o método `getDeviceLocation()` para recuperar as propriedades de localização de um dispositivo. Os parâmetros necessários para recuperar os dados da localização são deviceTypeId e deviceId.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

A resposta a este método contém as propriedades de longitude, latitude, elevação, precisão, measuredTimeStamp, e updatedTimeStamp.

### Atualizando informações de localização


Use o método `updateDeviceLocation()` para modificar as informações de localização de um dispositivo. Assim como na atualização de propriedades do dispositivo, o parâmetro deviceLocation deve ser definido com as mudanças que você gostaria de aplicar. A amostra de código a seguir demonstra a mudança dos dados da localização para um dispositivo específico:

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

Se uma data não for fornecida, a data e hora atuais serão usadas.


### Obter informações de gerenciamento


Use o método `getDeviceManagementInformation()` para obter as informações de gerenciamento de dispositivo de um dispositivo específico. A resposta contém a última data e hora de atividade, o status inativo do dispositivo (True/False), o suporte para ações de dispositivo e firmware e dados do firmware. Para obter uma lista abrangente de conteúdo de resposta, consulte a documentação da API (interface de programação de aplicativos) relevante.

A amostra de código a seguir retorna as informações de gerenciamento de dispositivo para um dispositivo com um deviceId configurado como "00aabbccde03" e um deviceTypeId configurado como "iotsample-arduino":

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Operações de diagnóstico do dispositivo
{: #device_diag_ops}

Use as operações de diagnóstico do dispositivo para implementar as tarefas de resolução de problemas e de gerenciamento de log a seguir:
- Limpando logs
- Recuperando todos os logs ou logs específicos para um dispositivo
- Incluindo informação de log
- Excluindo logs
- Limpando códigos de erro
- Recuperando códigos de erro do dispositivo
- Incluindo códigos de erro

Para obter mais informações sobre os modelos de consulta e de resposta, os códigos de resposta e os parâmetros de consulta, veja a [documentação da API ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window} documentação da API do {{site.data.keyword.iot_short_notm}}.

### Obter logs de diagnóstico


Use o método `getAllDiagnosticLogs()` para recuperar todos os logs de diagnóstico para um dispositivo específico. O método `getAllDiagnosticLogs()` requer os parâmetros deviceTypeId e deviceId.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

O modelo de resposta para esse método contém as propriedades ID do log, mensagem, gravidade, dados e registro de data e hora.

### Limpando os logs de diagnóstico para um dispositivo


Use o método `clearAllDiagnosticLogs()` para excluir todos os logs de diagnóstico de um dispositivo específico. Os parâmetros necessários são deviceTypeId e deviceId. Tome cuidado ao excluir arquivos de log, porque eles não podem ser recuperados após serem excluídos.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Incluindo um log de diagnóstico


Use o método `addDiagnosticLog()` para incluir uma entrada no log de diagnóstico do dispositivo. O log pode ser removido quando a nova entrada for incluída. Se nenhuma data for fornecida, a data e hora atuais serão incluídas na entrada. Para usar esse método, você precisa definir um parâmetro 'logs' com as variáveis a seguir:


|Variável|Requirement|Descrição|
|:---|:---|:---|
|`message`|Mandatório|Contém a mensagem de diagnóstico que você gostaria de incluir|
|`severity`|Optional|Corresponde à gravidade do log de diagnóstico e pode ser configurada como 0, 1 ou 2, o que corresponde às categorias de informação, aviso e erro|
|`data`|Optional|Contém dados de diagnóstico|
|`timestamp`|Optional|Contém a data e hora da entrada de log no formato ISO8601, mas se não especificada, a data e hora atuais serão usadas|


Os outros parâmetros necessários no método são os valores de deviceTypeId e deviceId para o dispositivo.

A amostra de código a seguir contém um exemplo do método `addDiagnosticLog()`:

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Recuperando um log de diagnóstico específico


Use o método `getDiagnosticLog()` para recuperar um log de diagnóstico específico para um dispositivo especificado com base no ID de log. Os parâmetros necessários para esse método são deviceTypeId, deviceId e logId.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Excluindo um log de diagnóstico


Use o método `deleteDiagnosticLog()` para excluir um log de diagnóstico específico. Para especificar um log de diagnóstico, os parâmetros deviceTypeId, deviceId e logID devem ser fornecidos.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Recuperando códigos de erro do dispositivo


Use o método `getAllDiagnosticErrorCodes()` para recuperar todos os códigos de erro de diagnóstico associados a um dispositivo específico.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Limpar códigos de erro de diagnóstico


Use o método `clearAllErrorCodes()` para limpar a lista de códigos de erro associados ao dispositivo. A lista é substituída com um único código de erro de zero.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Incluindo um código de erro de diagnóstico simples


Use o método `addErrorCode()` para incluir um usar na lista de códigos de erro associados ao dispositivo. A lista pode ser removida quando a nova entrada for incluída. Os parâmetros necessários no método são deviceTypeId, deviceId e errorCode. O parâmetro errorCode contém as seguintes variáveis:

- errorCode: Esta variável é obrigatória e deve ser configurada como inteiro. Essa variável configura o número do código de erro criado.
- timestamp: essa variável é opcional e contém a data e hora da entrada de log no formato ISO8601. Se esta variável não estiver incluída, ela é automaticamente incluída com a data e a hora atuais.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Determinação de problema de conexão
{: #connection_problem_determination}

Use o método `getDeviceConnectionLogs()` para listar os eventos de log de conexão para um dispositivo. Eventos de log de conexão podem ser usados para diagnosticar problemas de conectividade entre o dispositivo e o serviço do {{site.data.keyword.iot_short_notm}}. As entradas registram conexões bem-sucedidas, tentativas de conexão mal sucedidas, desconexões intencionais e eventos de desconexão iniciados pelo servidor.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

A resposta inclui uma lista de entradas de log, que contêm mensagens de log e registros de data e hora.
