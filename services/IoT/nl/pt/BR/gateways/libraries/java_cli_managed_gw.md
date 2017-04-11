---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desenvolvendo gateways gerenciados usando Java
{: #java_cli_managed_gw}

Os gateways executam uma função importante no gerenciamento dos dispositivos conectados a eles. Vários dispositivos são muito básicos e não possuem recursos de gerenciamento de dispositivo, portanto, esses dispositivos básicos precisam ser gerenciados por meio de um gateway. No {{site.data.keyword.iot_full}}, um gateway gerenciado é aquele que pode gerenciar os dispositivos que estão conectados a ele e fornecer recursos de gerenciamento de dispositivo, como atualizações de firmware, de local e de diagnóstico.
{:shortdesc}

Ao usar a biblioteca do cliente Java™ do {{site.data.keyword.iot_short}} e as informações fornecidas, é possível desenvolver código Java para transformar o gateway em um gateway gerenciado. Também são fornecidas amostras para ajudá-lo a desenvolver código Java para conectar um gateway ao serviço Device Management e executar operações de gerenciamento de dispositivo.

## Serviço de gerenciamento de dispositivo
{: #dm_service}

O serviço Device Management (DM) do {{site.data.keyword.iot_short}} fornece recursos de gerenciamento de dispositivo para que os gateways gerenciem os dispositivos conectados a eles.

Um gateway gerenciado executa um agente de gerenciamento de dispositivo, que é executado como um proxy para todos os dispositivos que se conectam ao {{site.data.keyword.iot_short}} por meio do gateway.

### Agente de gerenciamento de dispositivo

Os dispositivos que se conectam ao {{site.data.keyword.iot_short}} indiretamente por meio de um gateway poderão usar vários protocolos de conexão, se forem suportados pelo dispositivo de gateway.

A instância `ManagedGateway` é um agente de gerenciamento de dispositivo que fornece uma lista de métodos para executar uma ou mais ações de gerenciamento de dispositivo, por exemplo, participar na atividade de gerenciamento de dispositivo, atualizar códigos de erro, logs, local e ações de firmware ou de dispositivo.

O agente de gerenciamento de dispositivo no gateway converte e processa o protocolo de conexão dos dispositivos de conexão, que asseguram que o dispositivo possa ser gerenciado pelo {{site.data.keyword.iot_short}}. Por meio do agente de gerenciamento de dispositivo, o gateway torna-se mais do que um túnel transparente entre o dispositivo conectado e o {{site.data.keyword.iot_short}}. Por exemplo, se um dispositivo que estiver conectado a um gateway não puder fazer download do firmware, o agente de gerenciamento de dispositivo no gateway poderá executar as ações a seguir:
- Interceptar uma solicitação para um dispositivo fazer download do firmware
- Fazer download do firmware para o dispositivo
- Armazenar o firmware do dispositivo no gateway

Em um momento posterior, quando o dispositivo for instruído a fazer upgrade, o agente de gerenciamento de dispositivo no gateway poderá enviar o firmware por push para o dispositivo e atualizá-lo.

## Criando o modelo de dispositivo
{: #create_device_model}

No {{site.data.keyword.iot_short}}, o modelo de dispositivo descreve as características de metadados e de gerenciamento de dispositivos e gateways. O banco de dados de dispositivo é a principal fonte de informações de dispositivo ou de gateway. Aplicativos e dispositivos gerenciados podem enviar atualizações de local, atualizações de progresso de upgrade de firmware e outros tipos de atualizações. Quando as atualizações são recebidas pelo {{site.data.keyword.iot_short}}, o banco de dados de dispositivo é atualizado para que as informações fiquem disponíveis para conectar aplicativos.

Na biblioteca do cliente Java do {{site.data.keyword.iot_short}}, o modelo de dispositivo é representado pela classe Java `DeviceData`.

Para criar a classe `DeviceData`, crie os objetos a seguir:

- `DeviceInfo` (Opcional)
- `DeviceLocation` (Opcional, necessário apenas se o dispositivo desejar ser notificado sobre o local que está configurado pelo aplicativo por meio da API do {{site.data.keyword.iot_short}})
- `DeviceFirmware` (Opcional)
- `DeviceMetadata` (opcional)

Para obter mais informações, veja [modelo de dispositivo](../../reference/device_model.html).

### DeviceInfo

O fragmento de código a seguir que contém dados de amostra mostra como criar os objetos `DeviceInfo` e `DeviceMetadata`:

```java
DeviceInfo deviceInfo = new DeviceInfo.Builder().
                           serialNumber("10087").
                           manufacturer("IBM").
                           model("7865").
                           deviceClass("A").
                           description("My RasPi Device").
                           fwVersion("1.0.0").
                           hwVersion("1.0").
                           descriptiveLocation("EGL C").
                           build();

/**
  * Create a DeviceMetadata object
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

O fragmento de código a seguir descreve como criar a classe `DeviceData` usando os objetos `DeviceInfo` e `DeviceMetadata` que foram criados na amostra anterior:

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Cada gateway e cada dispositivo conectado devem ter suas próprias definições de classe `DeviceData` para representarem a si mesmos no {{site.data.keyword.iot_short}}. Para gateways, a classe `DeviceData` é passada para a biblioteca como parte da construção da instância `ManagedGateway`. Para dispositivos conectados, a classe `DeviceData` é passada para a biblioteca como parte do objeto `sendDeviceManageRequest()`.

## Construtores ManagedGateway
{: #construct_managed_gateway}

`ManagedGateway` é uma classe Java que conecta um gateway ao {{site.data.keyword.iot_short}} como um gateway gerenciado que pode executar pelo menos uma operação de gerenciamento de dispositivo para si mesmo ou para os dispositivos conectados. Uma instância `ManagedGateway` também pode ser usada para executar operações normais de gateway, como publicar eventos de gateway, conectar eventos de dispositivo e receber comandos por meio de aplicativos. A instância `ManagedGateway` é um agente de gerenciamento de dispositivo.

Na classe `ManagedGateway`, dois construtores diferentes, Construtor um e Construtor dois, suportam diferentes padrões de usuário.

### Construtor um

O Construtor um constrói uma instância `ManagedGateway` aceitando uma classe `DeviceData` que contém todas as propriedades a seguir:

| Propriedade     |Descrição     |
|----------------|----------------|
|`Organization-ID` |O ID de sua organização.|
|`Gateway-Type` |O tipo de seu dispositivo de gateway.|
|`Gateway-ID` |O ID do dispositivo de gateway.|
|`Authentication-Method`|O método de autenticação. O único método suportado é "token".|
|`Authentication-Token`|O token da chave API.|
|`auth-key`   |Uma chave API opcional que se deve especificar ao configurar o valor de método de autenticação para `apikey`.|
|`auth-token`   |Um token de chave API que também é necessário ao configurar o valor de método de autenticação para `apikey`. |
|`clean-session`|Um valor true ou false necessário somente se você desejar se conectar ao gateway no modo de assinatura durável. Por padrão, `clean-session` está configurado como `true`.|
|`Porta`|O número da porta a qual se conectar. Especifique 8883 ou 443. Se você não especificar um número de porta, o cliente se conectará ao {{site.data.keyword.iot_short_notm}} no número de porta 8883 por padrão.|
|`WebSocket`|Um valor true ou false necessário somente se você desejar se conectar ao gateway usando websockets.|
|`MaxInflightMessages`  |Configura o número máximo de mensagens em andamento para a conexão. O valor padrão é 100.|
|`Automatic-Reconnect`  |Um valor true ou false que é necessário quando você deseja reconectar automaticamente o dispositivo ao {{site.data.keyword.iot_short_notm}} enquanto ele está em um estado desconectado. O valor-padrão é false.|
|`Disconnected-Buffer-Size`|O número máximo de mensagens que podem ser armazenadas na memória enquanto o cliente está desconectado. O valor-padrão é
5000.|

**Nota:** para conectar o gateway no modo de assinatura durável, configure `clean-session` como `false`. Para obter mais informações sobre a propriedade `clean-session`, veja a seção 'Buffers de assinatura e sessão limpa' da [documentação do MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

O código a seguir descreve como criar uma instância `ManagedGateway`:

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Construtor dois

O Construtor dois constrói uma instância `ManagedGateway` aceitando um objeto `DeviceData` e a instância do cliente MQTT. O Construtor dois também requer que o objeto `DeviceData` na instância inclua o tipo de dispositivo e o ID do dispositivo, conforme descrito na amostra de código a seguir:

```java
// Code that constructs either a synchronous or asynchronous MQTT client instance of mqttClient.
.....

// Code that constructs the DeviceData object
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Nota:** se você estiver desenvolvendo para dispositivos customizados, use o Construtor dois, porque esse construtor cria uma instância de gateway gerenciado usando a instância de cliente MQTT conectado existente para que seja possível alavancar operações de gerenciamento de dispositivo. Use a biblioteca do cliente Java para todas as funções do dispositivo.

## Solicitações de gerenciamento de dispositivo de um gateway
{: #dm_requests}

### Enviando uma solicitação de gerenciamento de um gateway

Para instruir um gateway a participar de atividades de gerenciamento de dispositivo, chame o método `sendGatewayManageRequest()`, que é descrito na amostra de código a seguir:

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
A solicitação de gerenciamento iniciará uma solicitação de conexão internamente se o dispositivo ainda não estiver conectado ao {{site.data.keyword.iot_short}}.

O método `sendGatewayManageRequest()` aceita os parâmetros a seguir:

| Parâmetro     |Descrição     |
|----------------|----------------|
|`lifetime`|O período de tempo em segundos em que o gateway deve enviar outra solicitação de tipo de dispositivo de gerenciamento para evitar que seja classificado como inativo e se torne um dispositivo não gerenciado. Se o campo `lifetime` for omitido ou configurado como 0, o gateway gerenciado não se tornará inativo. A configuração mínima suportada para o campo `lifetime` é 3.600 segundos (uma hora).|
|`supportFirmwareActions`|Um valor true ou false que determina se o gateway suporta ações do firmware. O gateway também deve incluir um manipulador de firmware para manipular as solicitações de firmware.|
|`supportDeviceActions`|Um valor true ou false que determina se o gateway suporta ações do dispositivo. O gateway também deve incluir um manipulador de ações de dispositivo para manipular as solicitações de reinicialização e de reconfiguração de fábrica.|


A instância `ManagedGateway` é um agente de gerenciamento de dispositivo que fornece uma lista de métodos para executar uma ou mais ações de gerenciamento de dispositivo, por exemplo, participar na atividade de gerenciamento de dispositivo, atualizar códigos de erro, logs, local e ações de firmware ou de dispositivo.

### Enviando uma solicitação de gerenciamento de dispositivos conectados

Para permitir que dispositivos que estejam conectados protegidos por um gateway participem de atividades de gerenciamento de dispositivo no gateway, chame o método `sendDeviceManageRequest()`.

O método `sendDeviceManageRequest()` aceita os detalhes dos dispositivos conectados e os parâmetros `lifetime`, `supportFirmwareActions` e `supportDeviceActions`. Um gateway também pode usar o método `sendDeviceManageRequest()` sobrecarregado para definir o objeto `DeviceData` para o dispositivo conectado.

#### Exemplo de envio de uma solicitação de gerenciamento de dispositivos conectados

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Enviando uma solicitação de cancelamento de gerenciamento de um gateway

Quando um gateway não precisar mais ser gerenciado, para parar as atividades de gerenciamento de dispositivo no gateway, chame o método `sendGatewayUnmanageRequet()`.  Quando `sendGatewayUnmanageRequet()` for chamado, o {{site.data.keyword.iot_short}} não mais enviará novas solicitações de gerenciamento de dispositivo para o gateway e todas as solicitações de gerenciamento de dispositivo do gateway serão rejeitadas, exceto para solicitações de **Gerenciamento**. As solicitações de dispositivos protegidos pelo gateway não são rejeitadas.

#### Exemplo de envio de uma solicitação de cancelamento de gerenciamento de um gateway

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Enviando uma solicitação de cancelamento de gerenciamento de dispositivos conectados

Quando um dispositivo protegido por um gateway não precisar mais ser gerenciado, para mover um dispositivo conectado de um estado gerenciado para um estado não gerenciado, o gateway poderá chamar o método `sendDeviceUnmanageRequet()`. Quando `sendDeviceUnmanageRequet()` for chamado, o {{site.data.keyword.iot_short}} não mais enviará novas solicitações de gerenciamento de dispositivo para o dispositivo e todas as solicitações de gerenciamento de dispositivo do gateway que forem para o dispositivo conectado serão rejeitadas, exceto para solicitações de **Gerenciamento**.

#### Exemplo de envio de uma solicitação de cancelamento de gerenciamento de dispositivos conectados

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Atualizações de locais
{: #location_updates}

### Enviando atualizações de local do gateway

Os gateways que podem determinar sua localização podem optar por notificar o {{site.data.keyword.iot_short}} sobre mudanças de local. O gateway pode chamar um dos métodos `updateLocation()` sobrecarregados para atualizar o local do dispositivo.

```java
    // update the location with latitude, longitude, and elevation.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Enviando atualizações de local do dispositivo conectado

O gateway pode chamar o método de dispositivo `updateDeviceLocation()` correspondente para atualizar o local dos dispositivos conectados. O método sobrecarregado pode ser usado para especificar o método `measuredDateTime`.  

```java
// update the location of the attached device with latitude, longitude, and elevation
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
Para obter mais informações sobre atualizações de local, veja [Solicitações de gerenciamento de dispositivo](../../devices/device_mgmt/index.html#/update-location#update-location).

## Manipulação de código de erro
{: #errors}

### Criando e excluindo códigos de erro do gateway

Um gateway pode optar por notificar o {{site.data.keyword.iot_short}} sobre mudanças em seu status de erro. O gateway pode chamar o método `addErrorCode()` para incluir o código de erro atual no {{site.data.keyword.iot_short}}.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

Os códigos de erro para um gateway podem ser limpos do {{site.data.keyword.iot_short}} chamando o método `clearErrorCodes()`, conforme mostrado:

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Criando e excluindo códigos de erro de dispositivos conectados

Um gateway também pode chamar o método de dispositivo correspondente para incluir ou limpar códigos de erro dos dispositivos conectados:

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Criando e excluindo mensagens de log do gateway

Um gateway pode optar por notificar o {{site.data.keyword.iot_short}} sobre mudanças, incluindo uma nova entrada de log. Uma entrada de log inclui os itens a seguir:

- Sequência de mensagem
- Carimbo de data/hora
- Severity
- Opcionalmente, dados diagnósticos binários codificados por base64

Os gateways podem chamar o método `addGatewayLog()` para enviar mensagens de log, que está descrito na amostra a seguir:

```java
// An example Log event
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

As mensagens de log podem ser limpas do {{site.data.keyword.iot_short}} chamando o método `clearLogs()`:

```java
rc = managedGateway.clearGatewayLogs();
```

### Criando e excluindo logs de dispositivos conectados

Da mesma forma, o gateway pode chamar o método de dispositivo correspondente para criar ou limpar os logs dos dispositivos conectados, que é descrito na amostra de código a seguir:

```java

// An example log event:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

Para limpar os logs de dispositivos conectados, chame o método `clearDeviceLogs()` especificando os detalhes do dispositivo conectado, que é descrito na amostra de código a seguir:

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

As operações de diagnósticos de dispositivo são destinadas a fornecer informações sobre erros de gateway ou de dispositivo. Elas não fornecem informações de diagnóstico sobre uma conexão de dispositivo para o {{site.data.keyword.iot_short}}.

Para obter mais informações sobre a operação de diagnósticos, veja [Solicitações de gerenciamento de dispositivo](../../devices/device_mgmt/index.html#/update-location#update-location).

## Atualizações de firmware e ações
{: #firmware}

O processo de atualização de firmware é separado em duas ações distintas:

- Fazendo download de firmware
- Atualizando o Firmware

O gateway precisa executar as atividades a seguir para suportar ações de firmware para si mesmo e para seus dispositivos conectados:

1. Opcional: construir um objeto `DeviceFirmware`.
2. Informar o servidor sobre o suporte à ação de firmware.
3. Criar o manipulador de ações do firmware.
4. Incluir o manipulador em `ManagedGateway`.

### Etapa 1: construindo um objeto `DeviceFirmware`

Para executar ações de firmware, um gateway pode opcionalmente construir um objeto `DeviceFirmware` para si mesmo e para seus dispositivos conectados e, em seguida, incluí-lo no objeto `DeviceData`, que é descrito na amostra a seguir:

```java
DeviceFirmware firmware = new DeviceFirmware.Builder().
			version("Firmware.version").
			name("Firmware.name").
			url("Firmware.url").
			verifier("Firmware.verifier").
			state(FirmwareState.IDLE).				
			build();

DeviceData deviceData = new DeviceData.Builder().
			deviceInfo(deviceInfo).
			deviceFirmware(firmware).
			metadata(metadata).
			build();

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
managedGateway.connect();
```

Para dispositivos conectados, o objeto construído `DeviceData` pode ser passado para a biblioteca ao enviar a solicitação de gerenciamento, conforme descrito na amostra de código a seguir:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

O objeto `DeviceFirmware` representa o firmware atual do gateway ou do dispositivo conectado e é usado para relatar o status das ações de download de firmware e de atualização de firmware para o {{site.data.keyword.iot_short}}. Se o objeto `DeviceFirmware` não for construído pelo gateway, a biblioteca criará um objeto vazio e relatará o status para o {{site.data.keyword.iot_short}}.

### Etapa 2: informar o servidor sobre o suporte à ação de firmware

O gateway ou seus dispositivos conectados precisam configurar a sinalização de ação de firmware como true para que o servidor inicie a solicitação de firmware. Essa mudança pode ser obtida passando um valor true para o parâmetro `supportFirmwareActions` na solicitação de gerenciamento.

O gateway pode chamar o método a seguir para informar o servidor sobre seu suporte de firmware:
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

Da mesma forma, o gateway pode chamar o método de dispositivo correspondente para informar o suporte de firmware de dispositivos conectados:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

Quando o suporte for informado ao servidor de gerenciamento de dispositivo, o servidor encaminhará então as ações de firmware para o gateway, para o próprio gateway ou para os dispositivos protegidos por ele.

### Etapa 3: criando o manipulador de ações do firmware

Para suportar a ação de firmware, o gateway precisará criar um manipulador e incluí-lo em `managedGateway`. O manipulador deve estender uma classe `DeviceFirmwareHandler` e implementar os métodos a seguir:

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Nota**: deve haver a inclusão de apenas um manipulador na biblioteca para o gateway e os dispositivos conectados nos quais as solicitações de download ou de atualização de firmware são redirecionadas. A implementação deve criar um encadeamento ou um conjunto de encadeamentos para manipular múltiplas solicitações de firmware ao mesmo tempo.

É possível localizar uma implementação de amostra de um manipulador de conjunto de encadeamentos no [Repositório do GitHub de amostras do gateway ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Uma implementação de amostra de `downloadFirmware`

A implementação deve incluir lógica para fazer download do firmware e relatar o status do download usando o objeto `DeviceFirmware`. Se a operação de download de firmware for bem-sucedida, o estado do firmware deverá ser configurado como 'DOWNLOADED' e a propriedade `UpdateStatus` deverá ser configurada como 'SUCCESS'.

Se ocorrer um erro durante um download de firmware, o estado deverá ser configurado como "IDLE" e a propriedade `updateStatus` deverá ser configurada como um dos valores de status de erro a seguir:

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

Uma implementação de download de firmware de amostra é mostrada na amostra de código a seguir:

**Importante:** a amostra de código fornecida não inclui a seção de conjunto de encadeamentos. Para obter a implementação completa do manipulador de firmware, há uma amostra disponível no [Repositório do GitHub de amostras de gateway do IBM Java ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

```java
public void downloadFirmware(DeviceFirmware deviceFirmware) {
	boolean success = false;
    URL firmwareURL = null;
    URLConnection urlConnection = null;

	try {
		firmwareURL = new URL(deviceFirmware.getUrl());
        urlConnection = firmwareURL.openConnection();
        if(deviceFirmware.getName() != null) {
			downloadedFirmwareName = deviceFirmware.getName();
        } else {
			// use the time stamp as the name
			downloadedFirmwareName = "firmware_" +new Date().getTime()+".deb";
		}

		File file = new File(downloadedFirmwareName);
		BufferedInputStream bis = new BufferedInputStream(urlConnection.getInputStream());
		BufferedOutputStream bos = new BufferedOutputStream(new FileOutputStream(file.getName()));

		int data = bis.read();
        if(data != -1) {
			bos.write(data);
            byte[] block = new byte[1024];
            while (true) {
				int len = bis.read(block, 0, block.length);
                if(len != -1) {
					bos.write(block, 0, len);
                } else {
					break;
                }
			}
            bos.close();
            bis.close();
            success = true;
        } else {
			//There is no data to read, so set an error
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
	} catch(MalformedURLException me) {
		// Invalid URL, so set the status to reflect the same,
        deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
    } catch (IOException e) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.CONNECTION_LOST);
    } catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }

    if(success == true) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
        deviceFirmware.setState(FirmwareState.DOWNLOADED);
    } else {
		deviceFirmware.setState(FirmwareState.IDLE);
    }
}
```

Um gateway gerenciado pode verificar a integridade da imagem de firmware transferida por download usando o verificador e, em seguida, relatar o status de volta para o {{site.data.keyword.iot_short}}. O verificador pode ser configurado pelo gateway durante os estágios a seguir:

- Durante a inicialização quando o objeto 'DeviceFirmware' é criado
- Quando um aplicativo envia uma solicitação 'downloadFirmware'

#### Exemplo

```java
private boolean verifyFirmware(File file, String verifier) throws IOException {
	FileInputStream fis = null;
    String md5 = null;
    try {
		fis = new FileInputStream(file);
        md5 = org.apache.commons.codec.digest.DigestUtils.md5Hex(fis);
        System.out.println("Downloaded Firmware MD5 sum:: "+ md5);
    } catch (FileNotFoundException e) {
		e.printStackTrace();
    } catch (IOException e) {
		e.printStackTrace();
    } finally {
		fis.close();
    }
    if(verifier.equals(md5)) {
		System.out.println("Firmware verification successful");
		return true;
	}
	System.out.println("Download firmware checksum verification failed."
			+ "Expected "+verifier + " found "+md5);
    return false;
}
```

O código completo pode ser localizado na amostra de gerenciamento de gateway [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Uma implementação de amostra de `updateFirmware`

A implementação deve criar um encadeamento separado, incluir lógica para instalar o firmware transferido por download e relatar o status da atualização usando o objeto `DeviceFirmware`. Se a operação de atualização de firmware for bem-sucedida, o estado do firmware deverá ser configurado como 'IDLE' e o valor `updateStatus` deverá ser configurado como 'SUCCESS'.

Se ocorrer um erro durante uma atualização de firmware, o valor `updateStatus` deverá ser configurado como um dos valores de status de erro a seguir:

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

A amostra de código a seguir descreve como é possível implementar uma atualização de firmware para um dispositivo Raspberry Pi:

```java
public void updateFirmware(DeviceFirmware deviceFirmware) {
	try {
		ProcessBuilder pkgInstaller = null;
        Process p = null;
        pkgInstaller = new ProcessBuilder("sudo", "dpkg", "-i", downloadedFirmwareName);
        boolean success = false;
        try {
			p = pkgInstaller.start();
            boolean status = waitForCompletion(p, 5);
            if(status == false) {
				p.destroy();
                deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
                return;
            }
            System.out.println("Firmware Update command "+status);
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.SUCCESS);
            deviceFirmware.setState(FirmwareState.IDLE);
        } catch (IOException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        } catch (InterruptedException e) {
			e.printStackTrace();
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.UNSUPPORTED_IMAGE);
        }
	} catch (OutOfMemoryError oom) {
		deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.OUT_OF_MEMORY);
    }
}
```

O código completo pode ser localizado na amostra `GatewayFirmwareHandlerSample` que está no [Repositório do GitHub de amostras do gateway ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Etapa 4: incluindo o manipulador em `ManagedGateway`

Quando um manipulador for criado, ele deverá ser incluído na instância `ManagedGateway` para que a biblioteca do cliente Java chame o método correspondente quando houver uma solicitação de ação de firmware do {{site.data.keyword.iot_short}}.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

Para obter mais informações sobre ações de firmware, veja [Solicitações de gerenciamento de dispositivo ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}.

## Ações do Dispositivo
{: #dev_actions}

O {{site.data.keyword.iot_short}} suporta as ações de dispositivo a seguir:

- Reinicalização
- Reconfiguração de fábrica

O gateway deverá executar as atividades a seguir para suportar ações do dispositivo para si mesmo e também para os dispositivos protegidos por ele.

1. Informar o servidor sobre o suporte a ações do dispositivo.
2. Criar o manipulador de ação do dispositivo.
3. Incluir o manipulador em `ManagedGateway`.

### Etapa 1: informando o servidor sobre o suporte a ações do dispositivo

Para executar uma ação de reinicialização ou de reconfiguração de fábrica para um gateway e seus dispositivos conectados, o gateway deve primeiro informar o {{site.data.keyword.iot_short}} sobre o suporte. Essa ação pode ser executada passando um valor true para o parâmetro `supportDeviceActions` ao enviar a solicitação de **Gerenciamento**.

Um gateway pode chamar o método a seguir para informar o servidor sobre seu suporte à ação de dispositivo:

```java
// Last parameter represents the device action support
managedGateway.sendGatewayManageRequest(3600, true, true);
```

Um gateway pode chamar o método de dispositivo correspondente para informar o suporte à ação de dispositivo de dispositivos conectados:

```java
// Last parameter represents the device action support
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

Quando o suporte for informado ao servidor de gerenciamento de dispositivo, o servidor encaminhará então as solicitações de ação de dispositivo para o dispositivo.

### Etapa 2: criando o manipulador de ações do dispositivo

Para suportar a ação do dispositivo, o gateway precisará criar um manipulador e incluí-lo na instância `managedGateway`. O manipulador deve ampliar uma classe `DeviceActionHandler` e fornecer implementação para os métodos a seguir:

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Nota:** deve haver a inclusão de apenas um manipulador na biblioteca para o gateway e os dispositivos conectados nos quais as solicitações de ação de dispositivo são redirecionadas. A implementação deve criar um encadeamento ou um conjunto de encadeamentos para manipular múltiplas solicitações de ação de dispositivo ao mesmo tempo. Uma implementação de manipulador de amostra que usa um conjunto de encadeamentos é demonstrada no [Repositório do GitHub iot-gateway-samples ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.

### Uma implementação de amostra de `handleReboot`

A implementação deve criar um encadeamento separado, incluir lógica para reinicializar o gateway e o dispositivo conectado e relatar o status da reinicialização usando um objeto `DeviceAction`. Depois de receber a solicitação, o gateway deve primeiro informar o servidor sobre o suporte ou a falha antes de continuar com a reinicialização real. Se a amostra não puder reinicializar o dispositivo ou ocorrer qualquer outro erro durante a reinicialização, o gateway poderá atualizar o status em uma mensagem opcional. Uma implementação de reinicialização de amostra para um dispositivo Raspberry Pi é fornecida na amostra de código a seguir:

```java
public void handleReboot(DeviceAction action) {
	ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
		p = processBuilder.start();
        // wait for say 2 minutes before giving it up
        status = waitForCompletion(p, 2);
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    } catch (InterruptedException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

A implementação de manipulador de amostra completa que usa um conjunto de encadeamentos é demonstrada no [Repositório do GitHub iot-gateway-samples ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.


### Uma implementação de amostra de `handleFactoryReset`

A implementação deve criar um encadeamento separado, incluir lógica para reconfigurar o gateway e o dispositivo conectado para as configurações de fábrica e relatar o status da reconfiguração usando o objeto DeviceAction. Quando a solicitação for recebida, o gateway precisará primeiro informar o servidor sobre o suporte ou a falha antes de continuar com a reconfiguração real. A estrutura de tópicos básica da implementação da reconfiguração de fábrica é mostrada na amostra de código a seguir:

```java
public void handleFactoryReset(DeviceAction action) {
	try {
		// code to perform Factory reset
    } catch (IOException e) {
		action.setMessage(e.getMessage());
    }
    if(status == false) {
		action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

### Etapa 3: incluindo o manipulador em `ManagedGateway`

Quando um manipulador for criado, ele deverá ser incluído na instância `ManagedGateway` para que a biblioteca do Cliente Java chame o método correspondente quando houver uma solicitação de ação de dispositivo do {{site.data.keyword.iot_short}} para o gateway ou os dispositivos conectados.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

Para obter mais informações sobre ações de dispositivo, veja [Solicitações de gerenciamento de dispositivo ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}.

## Recebendo mudanças de atributos de dispositivo
{: #listen_device_attributes}

A biblioteca do cliente Java atualizará os objetos correspondentes sempre que houver uma solicitação de atualização do {{site.data.keyword.iot_short}}. Essas solicitações de atualização serão iniciadas pelo aplicativo direta ou indiretamente por meio de uma atualização de firmware usando a API de REST do {{site.data.keyword.iot_short}}. Além de atualizar esses atributos, a biblioteca fornece um mecanismo por meio do qual o gateway poderá ser notificado sempre que um atributo de dispositivo for atualizado.

Os atributos que podem ser atualizados por esse tipo de operação são location, metadata, device information e firmware do gateway ou dos dispositivos conectados.

Para ser notificado sobre mudanças de atributos, o gateway deverá incluir um listener de mudança de propriedade nos objetos em que estiver interessado, que é descrito na amostra de código a seguir:

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

O gateway também deve implementar o método `propertyChange()` no qual recebe a notificação, que está descrito na implementação de amostra a seguir:

```java
public void propertyChange(PropertyChangeEvent evt) {
	if(evt.getNewValue() == null) {
		return;
	}
	Object value = (Object) evt.getNewValue();
		switch(evt.getPropertyName()) {
		case "metadata":
            DeviceMetadata metadata = (DeviceMetadata) value;
            System.out.println("Received an updated metadata -- "+ metadata);
            break;

			case "location":
            DeviceLocation location = (DeviceLocation) value;
            System.out.println("Received an updated location -- "+ location);
            break;

			case "deviceInfo":
            DeviceInfo info = (DeviceInfo) value;
            System.out.println("Received an updated device info -- "+ info);
            break;

			case "mgmt.firmware":
            DeviceFirmware firmware = (DeviceFirmware) value;
            System.out.println("Received an updated device firmware -- "+ firmware);
            break;
    }
}
```

Para obter mais informações sobre como atualizar os atributos de dispositivo, veja [Solicitações de gerenciamento de dispositivo ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}.

## Amostras
{: #samples}

Há várias amostras disponíveis para ajudá-lo a conectar gateways e dispositivos que estão protegidos por gateways à instância do {{site.data.keyword.iot_short_notm}}. As amostras usam a biblioteca do cliente Java do {{site.data.keyword.iot_short_notm}} e estão localizadas no [Repositório do GitHub de amostras do gateway ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Receitas
{: #recipes}

Para obter uma orientação que mostre como conectar um dispositivo Raspberry Pi como um gateway gerenciado ao {{site.data.keyword.iot_short_notm}} e gerenciar os dispositivos conectados, veja [Raspberry Pi como um gateway gerenciado no {{site.data.keyword.iot_short_notm}} ![Ícone de link externo](../../../../icons/launch-glyph.svg "Ícone de link externo")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}.

A orientação explica como é possível usar o protocolo Device Management do {{site.data.keyword.iot_short_notm}} para gerenciar um dispositivo Arduino Uno por meio de um dispositivo Raspberry Pi que age como um gateway e executa operações de gerenciamento de dispositivo, como a reinicialização do dispositivo ou a inclusão de um programa de rascunho.
