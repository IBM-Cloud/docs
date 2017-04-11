---

copyright:
  years: 2015, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desenvolvendo dispositivos gerenciados usando Java
{: #java_deviceManagement}

##Introdução
{: #introduction}

No {{site.data.keyword.iot_full}}, um dispositivo gerenciado é aquele que pode fazer operações de gerenciamento de dispositivo, como atualizações de firmware, de local e de diagnóstico.
Ao usar a biblioteca do cliente Java™ do {{site.data.keyword.iot_short}} e as informações fornecidas, é possível desenvolver código Java para transformar seus dispositivos conectados em dispositivos gerenciados. Também são fornecidas amostras para ajudá-lo a desenvolver código Java para conectar um dispositivo ao serviço Device Management e executar operações de gerenciamento de dispositivo.

Para obter mais informações sobre como os aplicativos podem usar a biblioteca do cliente Java para interagir com dispositivos, veja [Java para desenvolvedores de aplicativos](../../applications/libraries/java.html).

## Device Management
{: #device_management}

O recurso [gerenciamento de dispositivo](../reference/device_mgmt.html) aprimora o serviço do {{site.data.keyword.iot_short_notm}} com mais capacidades para gerenciar dispositivos. O gerenciamento de dispositivos faz uma distinção entre dispositivos gerenciados e não gerenciados:

-   **Dispositivos gerenciados** são definidos como dispositivos que têm um agente de gerenciamento instalado. O agente de gerenciamento envia e recebe metadados do dispositivo e responde a comandos de gerenciamento de dispositivo do {{site.data.keyword.iot_short_notm}}.
-   **Dispositivos não gerenciados** são quaisquer dispositivos que não têm um agente de gerenciamento de dispositivo. Todos os dispositivos iniciam seu ciclo de vida como dispositivos não gerenciados e podem fazer a transição para dispositivos gerenciados enviando uma mensagem de um agente de gerenciamento de dispositivo para o {{site.data.keyword.iot_short_notm}}.

## Conectando-se ao serviço de Gerenciamento de dispositivo do {{site.data.keyword.iot_short_notm}}
{: #connecting_dm_service}

## Criando dados do dispositivo
{: #creating_device_data}

O [modelo de dispositivo](../reference/device_model.html) descreve as características de metadados e de gerenciamento de um dispositivo. O banco de dados de dispositivos no {{site.data.keyword.iot_short_notm}} é a principal fonte de informações dos dispositivos. Aplicativos e dispositivos gerenciados são capazes de enviar atualizações para o banco de dados, como uma localização ou o progresso de uma atualização de firmware. Quando essas atualizações forem recebidas pelo {{site.data.keyword.iot_short_notm}}, o banco de dados de dispositivos será atualizado, disponibilizando as informações para os aplicativos.

`DeviceData` é um modelo de dispositivo na biblioteca do cliente ibmiotf e inclui os objetos a seguir:

-   DeviceInfo (obrigatório)
-   DeviceLocation (necessário se o dispositivo suportar atualização de local)
-   DiagnosticErrorCode (necessário se o dispositivo desejar atualizar o ErrorCode)
-   DiagnosticLog (necessário se o dispositivo desejar atualizar as informações de log)
-   DeviceFirmware (necessário se o dispositivo suportar ações de firmware)
-   DeviceMetadata (opcional)

A amostra de código a seguir demonstra como criar o objeto obrigatório `DeviceInfo` juntamente com um objeto `DeviceMetadata` opcional com dados de amostra:

```
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

Use a amostra de código a seguir para criar um objeto `DeviceData` que inclui os objetos `DeviceInfo` e `DeviceMetadata` criados na amostra anterior.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## Construa ManagedDevice
{: #construct_managed_device}

`ManagedDevice` é uma classe de dispositivo que conecta o dispositivo como um dispositivo gerenciado ao {{site.data.keyword.iot_short_notm}} e ativa o dispositivo para executar uma ou mais operações de gerenciamento de dispositivo. Também é possível usar uma instância de `ManagedDevice` para executar operações de dispositivo normais, como publicar eventos de dispositivo e receber comandos de um aplicativo.

`ManagedDevice` expõe os construtores a seguir, que suportam os diferentes padrões de usuário:

**Construtor um**

O Constructor um constrói uma instância de `ManagedDevice` no {{site.data.keyword.iot_short_notm}} aceitando `DeviceData` e todas as propriedades necessárias a seguir:

|Propriedade |Descrição |
|:---|:---|
|`Organization-ID` |O ID de sua organização|
|`Device-Type` |O tipo de seu dispositivo. Normalmente, o deviceType é um agrupamento de dispositivos que executam uma tarefa específica, por exemplo, "weatherballoon".|
|`Device-ID` |O ID de seu dispositivo. Normalmente, para um tipo de dispositivo especificado, o deviceId é um identificador exclusivo desse dispositivo, por exemplo, um número de série ou um endereço de Controle de Acesso à Mídia.|
|`Authentication-Method` |O método de autenticação a ser usado. O único valor atualmente suportado é `token`.|
|`Authentication-Token` |Um token de autenticação para conectar seu dispositivo de forma segura ao Watson IoT Platform.|


O código a seguir descreve como é possível criar uma instância de `ManagedDevice`:

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

Se você já estiver usando uma instância de `DeviceClient`, observará que os nomes das propriedades são ligeiramente diferentes e espelham os nomes do painel do {{site.data.keyword.iot_short_notm}}. Para migrar de `DeviceClient` para `ManagedDevice`, é possível continuar a usar o formato anterior construindo a instância de `ManagedDevice` conforme esboçado na amostra a seguir:

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Construtor dois**

Construa uma instância de `ManagedDevice` aceitando as instâncias de `DeviceData` e `MqttClient`. Esse construtor requer que o `DeviceData` seja criada com atributos de dispositivo adicionais, como Tipo de dispositivo e ID do dispositivo, conforme descrito na amostra a seguir:

```
// Code that constructs the MqttClient (either Synchronous or Asynchronous MqttClient)
.....

// Code that constructs the DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Nota:** este construtor ajuda os usuários de dispositivos customizados a criar uma instância de `ManagedDevice` com a instância de `MqttClient` já criada e conectada para tirar proveito das operações de gerenciamento de dispositivo. Mas nós recomendamos que os usuários utilizem a biblioteca para todas as funcionalidades do dispositivo.

## Gerenciar

O dispositivo `Manage` pode chamar o método manage() para participar das atividades de gerenciamento de dispositivo. A solicitação de gerenciamento inicia uma solicitação de conexão internamente se o dispositivo ainda não estiver conectado ao {{site.data.keyword.iot_short_notm}}.

```
managedDevice.manage();
```

O dispositivo pode usar o método de gerenciamento sobrecarregado (tempo de vida) para registrar o dispositivo por um determinado prazo. O prazo especifica a duração em que o dispositivo deve enviar outra solicitação **Gerenciar dispositivo** para evitar a reversão para um dispositivo não gerenciado e marcado como inativo.

```
managedDevice.manage(3600);
```

Para obter mais informações sobre a operação `Manage`, consulte a [documentação].

  [documentation]:../device_mgmt/operations/manage.html

## Cancelar Gerenciamento

Um dispositivo pode chamar o método unmanage() quando não precisar mais ser gerenciado. O {{site.data.keyword.iot_short_notm}} deixará de enviar novas solicitações de gerenciamento de dispositivo a este dispositivo e todas as solicitações de gerenciamento de dispositivo deste dispositivo serão rejeitadas, exceto uma solicitação **Gerenciar dispositivo**.

```
managedDevice.unmanage();
```

Para obter mais informações sobre a operação `Unmanage`, consulte a [documentação].

  [documentation]:../device_mgmt/operations/manage.html

## Atualização de localização
{: #construct_location_update}
Os dispositivos que podem determinar sua localização podem optar por notificar o {{site.data.keyword.iot_short_notm}} sobre mudanças de localização. Para atualizar a localização, o dispositivo precisa criar uma instância de `DeviceData` com o objeto `DeviceLocation` primeiro.

```
// Construct the location object with latitude, longitude and elevation
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

Quando o dispositivo estiver conectado ao {{site.data.keyword.iot_short_notm}}, será possível atualizar a localização usando o método a seguir:

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

Atualizações subsequentes da localização do dispositivo podem ser realizadas modificando-se as propriedades do objeto `DeviceLocation`, conforme descrito na amostra a seguir:

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

O método update() informa o {{site.data.keyword.iot_short_notm}} sobre a nova localização.

Para obter mais informações sobre a atualização de localizações, consulte a [documentação](../device_mgmt/operations/update.html) vinculada.



## Anexando e limpando códigos de erro
{: #appending_error_codes}

Os dispositivos podem optar por notificar o {{site.data.keyword.iot_short_notm}} sobre as mudanças em seu status de erro. Para enviar códigos de erro, o dispositivo precisa construir um objeto `DiagnosticErrorCode` conforme esboçado na amostra a seguir:

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

Assim que o dispositivo estiver conectado ao {{site.data.keyword.iot_short_notm}}, o `ErrorCode` poderá ser enviado chamando o método send() da seguinte forma:

```
errorCode.send();
```

Posteriormente, quaisquer `ErrorCodes` novos poderão ser facilmente incluídos no {{site.data.keyword.iot_short_notm}} chamando o método append, da seguinte forma:

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

Além disso, os `ErrorCodes` podem ser limpos do {{site.data.keyword.iot_short_notm}} chamando o método clear() da seguinte forma:

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Anexando e limpando mensagens de log

Os dispositivos podem optar por notificar o {{site.data.keyword.iot_short_notm}} sobre mudanças incluindo uma nova entrada de log. Uma entrada de log inclui as informações a seguir:
- Mensagem do Log
- Carimbo de data/hora
- Severity
- Dados diagnósticos binários codificados por base64 (opcional)

Para enviar mensagens de log, o dispositivo precisa construir um objeto `DiagnosticLog` conforme esboçado na amostra a seguir:

```
DiagnosticLog log = new DiagnosticLog(
            "Simple Log Message",
            new Date(),
            DiagnosticLog.LogSeverity.informational);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLog(log).
             metadata(metadata).
             build();
```

Assim que o dispositivo estiver conectado ao {{site.data.keyword.iot_short_notm}}, a mensagem de log poderá ser enviada chamando o método send() conforme esboçado na amostra a seguir:

```
log.send();
```

Posteriormente, quaisquer mensagens de log novas poderão ser facilmente incluídas no {{site.data.keyword.iot_short_notm}} chamando o método append conforme esboçado na amostra a seguir:

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Além disso, as mensagens de log podem ser limpas do {{site.data.keyword.iot_short_notm}} chamando o método clear, conforme descrito na amostra a seguir:

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

As operações de diagnósticos de dispositivos são destinadas a fornecer informações sobre erros de dispositivo e não fornecem informações de diagnóstico relacionadas à conexão de dispositivos com o {{site.data.keyword.iot_short_notm}}.

Para obter mais informações sobre a operação de Diagnósticos, consulte a [documentação](../device_mgmt/operations/diagnostics.html).

## Ações de firmware
{: #firmware_actions}

O processo de atualização de firmware é separado em duas ações distintas:

* Fazendo download de firmware
* Atualizando o Firmware

O dispositivo precisa executar as atividades a seguir para suportar ações de firmware:

**1. Construir o objeto DeviceFirmware**

Para executar ações de firmware, o dispositivo precisa construir o objeto `DeviceFirmware` e incluí-lo em `DeviceData` da seguinte forma:

```
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

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
managedDevice.connect();
```

O objeto `DeviceFirmware` representa o firmware atual do dispositivo e será usado para relatar o status das ações de download de firmware e de atualização de firmware para o {{site.data.keyword.iot_short_notm}}.

**2. Informar o servidor sobre o suporte à ação de firmware**

O dispositivo precisa configurar a sinalização de ação de firmware como true para que o servidor inicie a solicitação de firmware. Isso pode ser feito chamando o método a seguir com um valor booleano:

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

Como a solicitação de gerenciamento informa o {{site.data.keyword.iot_short_notm}} sobre o suporte à ação de firmware, o método manage() precisa ser chamado imediatamente após a configuração do suporte à ação de firmware.

**3. Criar o manipulador de ações de firmware**

Para suportar a ação de firmware, o dispositivo precisa criar um manipulador e incluí-lo em `ManagedDevice`. O manipulador deve estender uma classe `DeviceFirmwareHandler` e implementar os métodos a seguir:

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Implementação de amostra de downloadFirmware**

A implementação deve incluir lógica para fazer download do firmware e relatar o status do download usando um objeto `DeviceFirmware`. Se a operação de download de firmware for bem-sucedida, então, o status será configurado como `DOWNLOADED` e, em seguida, `UpdateStatus` será configurado como `SUCCESS`.

Se ocorrer um erro durante download do firmware, o estado será configurado como `IDLE` e, em seguida, `updateStatus` será configurado como um dos valores de status de erro a seguir:

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

A amostra a seguir esboça uma implementação de download de firmware para um dispositivo Raspberry Pi:

```
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
            // use the timestamp as the name
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

Um dispositivo pode verificar a integridade da imagem do firmware transferido por download usando o verificador e relatar o status de volta ao {{site.data.keyword.iot_short_notm}}. O verificador pode ser configurado pelo dispositivo durante a inicialização (ao criar o objeto DeviceFirmware) ou como parte da solicitação de download de firmware feita pelo aplicativo. A seguir é mostrado um código de amostra para fazer essa verificação:

```
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
    System.out.println("Download firmware checksum verification failed.. "
            + "Expected "+verifier + " found "+md5);
    return false;
}
```

Para o código inteiro, consulte a amostra de gerenciamento de dispositivo [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).



**3.2 Implementação de amostra de updateFirmware**

A implementação deve incluir lógica para instalar o firmware transferido por download e relatar o status da atualização por meio do objeto `DeviceFirmware`. Se a operação de atualização de firmware for bem-sucedida, então, o estado do firmware deverá ser configurado como IDLE e `updateStatus` deve ser configurado como `SUCCESS`.

Se ocorrer um erro durante a atualização de firmware, `updateStatus` deve ser configurado como um dos valores de status de erro:

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

Uma amostra da implementação de atualização de firmware para um dispositivo Raspberry Pi é mostrada abaixo:

```
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

O código completo pode ser localizado na amostra de gerenciamento de dispositivo [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Incluir o manipulador em ManagedDevice**

O manipulador criado precisa ser incluído na instância de ManagedDevice para que a biblioteca do cliente ibmiotf chame o método correspondente quando houver uma solicitação de ação de firmware do {{site.data.keyword.iot_short_notm}}.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Consulte [esta página](../device_mgmt/operations/firmware_actions.html) para obter mais informações sobre a ação de firmware.

## Ações do Dispositivo

O {{site.data.keyword.iot_short_notm}} suporta as ações de dispositivo a seguir:

* Reinicalização
* Reconfiguração de Fábrica

O dispositivo precisa executar as seguintes atividades para suportar ações do dispositivo:

**1. Informar o servidor sobre o suporte a ações do dispositivo**

Para executar reinicialização e reconfiguração de fábrica, o dispositivo precisa informar o {{site.data.keyword.iot_short_notm}} sobre seu suporte primeiro. Isso pode ser feito chamando o método a seguir com um valor booleano:

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

Como a solicitação de gerenciamento informa o {{site.data.keyword.iot_short_notm}} sobre o suporte à ação do dispositivo, o método manage() precisa ser chamado imediatamente após a configuração do suporte à ação do dispositivo.

**2. Criar o manipulador de ações do dispositivo**

Para suportar a ação de dispositivo, o dispositivo precisa criar um manipulador e incluí-lo em ManagedDevice. O manipulador deve ampliar uma classe DeviceActionHandler e fornecer a implementação dos seguintes métodos:

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Implementação de amostra de handleReboot**

A implementação deve incluir uma lógica para reinicializar o dispositivo e relatar o status da reinicialização por meio do objeto DeviceAction. O dispositivo precisa atualizar o status juntamente com uma mensagem opcional apenas quando houver uma falha (porque a operação bem-sucedida reinicializa o dispositivo e o código do dispositivo não terá um controle para atualizar o {{site.data.keyword.iot_short_notm}}). Uma amostra da implementação de reinicialização para um dispositivo Raspberry Pi é mostrada abaixo:

```
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

O código completo pode ser localizado na amostra de gerenciamento de dispositivo [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Implementação de amostra de handleFactoryReset**

A implementação deve incluir uma lógica para reconfigurar o dispositivo para as configurações de fábrica e relatar o status por meio do objeto DeviceAction. O dispositivo precisa atualizar o status juntamente com uma mensagem opcional apenas quando houver uma falha (porque como parte deste processo, o dispositivo é reinicializado e o dispositivo não terá um controle para atualizar o status no {{site.data.keyword.iot_short_notm}}). A estrutura básica da implementação da reconfiguração de fábrica é mostrada abaixo:

```
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

**3. Incluir o manipulador em ManagedDevice**

O manipulador criado precisa ser incluído na instância de ManagedDevice para que a biblioteca do cliente ibmiotf chame o método correspondente quando houver uma solicitação de ação do dispositivo do {{site.data.keyword.iot_short_notm}}.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Consulte [esta página](../device_mgmt/operations/device_actions.html) para obter mais informações sobre a ação do dispositivo.



## Receber mudanças de atributos de dispositivos
{: #listen_device_attribute}

Esta biblioteca do cliente ibmiotf atualiza os objetos correspondentes sempre que houver uma solicitação de atualização do {{site.data.keyword.iot_short_notm}}. Essas solicitações de atualização são iniciadas pelo aplicativo direta ou indiretamente (atualização de firmware) por meio da API (interface de programação de aplicativos) REST do {{site.data.keyword.iot_short_notm}}. Além de atualizar esses atributos, a biblioteca fornece um mecanismo que permite que o dispositivo seja notificado sempre que um atributo do dispositivo for atualizado.

Os atributos que podem ser atualizados por esta operação são `location`, `metadata`, `device information` e `firmware`.

Para ser notificado, o dispositivo deve incluir um listener de mudança de propriedade nos objetos de interesse.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Além disso, o dispositivo precisa implementar o método `propertyChange()` no qual ele recebe a notificação. A amostra a seguir esboça como isso pode ser implementado:

```
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

Para obter mais informações sobre como atualizar os atributos do dispositivo, consulte [esta página](../device_mgmt/operations/update.html).

## Exemplos
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java) - Um código do agente de amostra que demonstra como executar várias operações de gerenciamento de dispositivo no Raspberry Pi.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java) - Um código de amostra que demonstra como é possível executar operações do dispositivo e operações de gerenciamento.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java) - Um código do agente de amostra com MqttAsyncClient customizado.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java) - Um código do agente de amostra com MqttClient customizado.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java) - Uma implementação de amostra de FirmwareHandler para o Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java) - Uma implementação de amostra de DeviceActionHandler
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java) - Uma amostra que demonstra como enviar solicitação de gerenciamento regular com tempo de vida especificado.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java) - Um código de listener de amostra que demonstra como receber diversas mudanças de atributos de dispositivo.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java) - Uma amostra quer demonstra como incluir ErrorCode sem esperar pela resposta do servidor.

##Receitas s
{: #Recipes}

Consulte [a receita](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/) que mostra como conectar o dispositivo Raspberry Pi como dispositivo gerenciado ao {{site.data.keyword.iot_short_notm}} para executar várias operações de gerenciamento de dispositivo passo a passo usando esta biblioteca do cliente.
