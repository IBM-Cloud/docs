---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-22"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Desarrollo de dispositivos gestionados mediante Java
{: #java_deviceManagement}

##Introducción
{: #introduction}

En {{site.data.keyword.iot_full}}, un dispositivo gestionado es un dispositivo que puede realizar operaciones de gestión de dispositivos, como por ejemplo actualizaciones de firmware, ubicación y diagnóstico.
Mediante la biblioteca de cliente Java™ de {{site.data.keyword.iot_short}} y la información que se proporciona, puede desarrollar código Java para convertir sus dispositivos conectados en dispositivos gestionados. También se proporcionan ejemplos para ayudarle a desarrollar código Java para conectar un dispositivo al servicio de gestión de dispositivos y ejecutar operaciones de gestión de dispositivos.

Para obtener más información sobre cómo pueden sus aplicaciones utilizar la biblioteca de cliente Java para interactuar con dispositivos, consulte [Java para desarrolladores de aplicaciones](../../applications/libraries/java.html).

## Gestión de dispositivos
{: #device_management}

La característica [gestión de dispositivos](../reference/device_mgmt.html) mejora el servicio de {{site.data.keyword.iot_short_notm}} con más posibilidades para la gestión de dispositivos. La gestión de dispositivos establece una diferencia entre dispositivos gestionados y no gestionados:

-   **Dispositivos gestionados** se definen como los dispositivos que tienen un agente de gestión instalado. El agente de gestión envía y recibe metadatos de dispositivos y responde a los mandatos de gestión de dispositivos desde {{site.data.keyword.iot_short_notm}}.
-   **Dispositivos no gestionados** son cualquier dispositivo que no tenga un agente de gestión de dispositivos. Todos los dispositivos inician su ciclo vital como dispositivos no gestionados, y pueden transicionar a dispositivos gestionados enviando un mensaje desde un agente de gestión de dispositivos a {{site.data.keyword.iot_short_notm}}.

## Conexión al servicio de Gestión de dispositivos de {{site.data.keyword.iot_short_notm}}
{: #connecting_dm_service}

## Creación de datos de dispositivos
{: #creating_device_data}

El [modelo de dispositivo](../reference/device_model.html) describe los metadatos y las características de gestión de un dispositivo. La base de datos del dispositivo del {{site.data.keyword.iot_short_notm}} es el origen maestro de la información del dispositivo. Las aplicaciones y los dispositivos gestionados pueden enviar actualizaciones a la base de datos como una ubicación o el progreso de una Actualización de firmware. Una vez que {{site.data.keyword.iot_short_notm}} reciba estas actualizaciones, se actualizará la base de datos de dispositivos, convirtiendo en disponible la información para las aplicaciones.

`DeviceData` es el modelo de dispositivo de la biblioteca de clientes de ibmiotf e incluye los siguientes objetos:

-   DeviceInfo (necesario)
-   DeviceLocation (necesario si el dispositivo soporta la actualización de ubicaciones)
-   DiagnosticErrorCode (necesario si el dispositivo quiere actualizar el ErrorCode)
-   DiagnosticLog (necesario si el dispositivo quiere actualizar la información de registro)
-   DeviceFirmware (necesario si el dispositivo soporta acciones de firmware)
-   DeviceMetadata (opcional)

El ejemplo de código siguiente muestra cómo crear el objeto obligatorio `DeviceInfo` junto con un objeto `DeviceMetadata` opcional con datos de ejemplo:

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
  * Crear un objeto DeviceMetadata
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);
```

Utilice el ejemplo de código siguiente para crear un objeto `DeviceData` que incluya los objetos `DeviceInfo` y `DeviceMetadata` que ha creado en el ejemplo anterior.

  ```
  DeviceData deviceData = new DeviceData.Builder().
               deviceInfo(deviceInfo).
               metadata(metadata).
               build();
  ```

## Construir ManagedDevice
{: #construct_managed_device}

`ManagedDevice` es una clase de dispositivo que conecta el dispositivo como un dispositivo gestionado a {{site.data.keyword.iot_short_notm}} y permite que el dispositivo realice una o varias operaciones de gestión de dispositivo. También puede utilizar una instancia `ManagedDevice` para realizar operaciones de dispositivos normales como la publicación de sucesos de dispositivos y la escucha de mandatos desde una aplicación.

`ManagedDevice` expone los siguientes constructores, que dan soporte a los distintos patrones del usuario:

**Constructor One**

Constructor One construye una instancia `ManagedDevice` en {{site.data.keyword.iot_short_notm}} aceptando los `DeviceData` y todas las propiedades necesarias siguientes:

|Propiedad |Descripción |
|:---|:---|
|`Organization-ID` |El ID de la organización|
|`Device-Type` |El tipo del dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`Device-ID` |El ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`Authentication-Method` |El método de autenticación que debe utilizarse. El único valor al que se da soporte actualmente es `token`.|
|`Authentication-Token` |Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform.|


El código siguiente describe cómo puede crear una instancia `ManagedDevice`:

```
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Device-Type", "iotsample-arduino");
options.setProperty("Device-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

Si ya está utilizando una instancia `DeviceClient`, observará que los nombres de las propiedades son ligeramente diferentes, y que duplica los nombres del panel de instrumentos de {{site.data.keyword.iot_short_notm}}. Para migrar desde `DeviceClient` a `ManagedDevice`, puede seguir utilizando el formato anterior creando la instancia de `ManagedDevice`, tal como se describe en el ejemplo siguiente:

```
Properties options = new Properties();
options.setProperty("org", "uguhsp");
options.setProperty("type", "iotsample-arduino");
options.setProperty("id", "00aabbccde03");
options.setProperty("auth-method", "token");
options.setProperty("auth-token", "AUTH TOKEN FOR DEVICE");
ManagedDevice managedDevice = new ManagedDevice(options, deviceData);
```

**Constructor Two**

Construya una instancia `ManagedDevice` aceptando las instancias `DeviceData` y `MqttClient`. Este constructor requiere que `DeviceData` se cree con atributos de dispositivos adicionales como Tipo de dispositivo e ID de dispositivo, tal como se describe en el ejemplo siguiente:

```
// Código que construye el MqttClient (MqttClient Síncrono o Asíncrono)
.....

// Código que construye los DeviceData
DeviceData deviceData = new DeviceData.Builder().
             typeId("Device-Type").
             deviceId("Device-ID").
             deviceInfo(deviceInfo).
             metadata(metadata).
             build();

....
ManagedDevice managedDevice = new ManagedDevice(mqttClient, deviceData);
```

**Nota:** Este constructor ayuda a los usuarios de dispositivos personalizados a crear una instancia de `ManagedDevice` con la instancia de `MqttClient` ya creada y conectada para aprovechar las operaciones de gestión de dispositivos. No obstante, recomendamos a los usuarios utilizar la biblioteca para todas las funcionalidades de dispositivos.

## Gestionar

El dispositivo `Gestionar` puede invocar el método manage() para participar en actividades de gestión de dispositivos. La solicitud de gestión inicia una solicitud de conexión internamente si el dispositivo aún no está conectado a la {{site.data.keyword.iot_short_notm}}.

```
managedDevice.manage();
```

El dispositivo puede utilizar el método overloaded manage (lifetime) para registrar el dispositivo para un período de tiempo determinado. El intervalo de tiempo especifica el período de tiempo en el que el dispositivo debe enviar otra solicitud **Gestionar dispositivo** para evitar que se revierta a un dispositivo no gestionado y se marque como inactivo.

```
managedDevice.manage(3600);
```

Para obtener más información sobre la operación `Gestionar`, consulte la [documentación].

  [documentation]:../device_mgmt/operations/manage.html

## No gestionar

Un dispositivo puede solicitar el método unmanage() cuando ya no necesite ser gestionado. El {{site.data.keyword.iot_short_notm}} ya no enviará nuevas solicitudes de gestión de dispositivos a este dispositivo y se rechazarán todas las solicitudes de gestión de dispositivos de este dispositivo que no sean una solicitud **Gestionar dispositivo**.

```
managedDevice.unmanage();
```

Para obtener más información sobre la operación `Eliminar gestión`, consulte la [documentación].

  [documentation]:../device_mgmt/operations/manage.html

## Actualización de la ubicación
{: #construct_location_update}
Los dispositivos que pueden determinar su ubicación pueden elegir notificar al {{site.data.keyword.iot_short_notm}} sobre los cambios de ubicación. Para actualizar la ubicación, el dispositivo necesita crear una instancia `DeviceData` con el objeto `DeviceLocation` en primer lugar.

```
// Construir el objeto de ubicación con latitud, longitud y elevación
DeviceLocation deviceLocation = new DeviceLocation.Builder(30.28565, -97.73921).
                            elevation(10).
                            build();
DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceLocation(deviceLocation).
             metadata(metadata).
             build();
```

Cuando el dispositivo está conectado a {{site.data.keyword.iot_short_notm}}, puede actualizar la ubicación utilizando el siguiente método:

```
int rc = deviceLocation.sendLocation();
if(rc == 200) {
        System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
            System.err.println("Failed to update the location");
}
```

Las actualizaciones posteriores a la ubicación del dispositivo se pueden actualizar modificando las propiedades del objeto `DeviceLocation`, tal como se describe en el ejemplo siguiente:

```
int rc = deviceLocation.update(40.28, -98.33, 11);
if(rc == 200) {
    System.out.println("Current location (" + deviceLocation.toString() + ")");
} else {
    System.err.println("Failed to update the location");
}
```

El método update() informa al {{site.data.keyword.iot_short_notm}} sobre la nueva ubicación.

Para obtener más información sobre las ubicaciones de actualización, consulte la [documentación](../device_mgmt/operations/update.html) enlazada.



## Adición y borrado de códigos de error
{: #appending_error_codes}

Los dispositivos pueden elegir notificar al {{site.data.keyword.iot_short_notm}} sobre los cambios realizados en su estado de error. Para enviar códigos de error, el dispositivo necesita construir un objeto `DiagnosticErrorCode`, tal como se describe en el ejemplo siguiente:

```
DiagnosticErrorCode errorCode = new DiagnosticErrorCode(0);

DeviceData deviceData = new DeviceData.Builder().
             deviceInfo(deviceInfo).
             deviceErrorCode(errorCode).
             metadata(metadata).
             build();
```

Tan pronto como el dispositivo se conecte a {{site.data.keyword.iot_short_notm}}, el `ErrorCode` se puede enviar llamando al método send() como se indica a continuación:

```
errorCode.send();
```

Posteriormente, los nuevos `ErrorCodes` se pueden añadir fácilmente al {{site.data.keyword.iot_short_notm}} llamando al método de adición como se indica a continuación:

```
int rc = errorCode.append(500);
if(rc == 200) {
    System.out.println("Current Errorcode (" + errorCode + ")");
} else {
    System.out.println("Errorcode addition failed!");
}
```

Además, los `ErrorCodes` se pueden borrar de {{site.data.keyword.iot_short_notm}} llamando al método clear() como se indica a continuación:

```
int rc = errorCode.clear();
if(rc == 200) {
    System.out.println("ErrorCodes are cleared successfully!");
} else {
    System.out.println("Failed to clear the ErrorCodes!");
}
```

## Adición y borrado de mensajes de registro

Los dispositivos pueden elegir notificar al {{site.data.keyword.iot_short_notm}} sobre los cambios añadiendo una nueva entrada de registro. Una entrada de registro incluye la información siguiente:
- Mensaje de registro
- Indicación de fecha y hora
- Gravedad
- Datos de diagnóstico binarios con código Base64 (opcional)

Para enviar mensajes de registro, el dispositivo debe construir un objeto `DiagnosticLog`, tal como se describe en el ejemplo siguiente:

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

Tan pronto como el dispositivo se conecte a {{site.data.keyword.iot_short_notm}}, el mensaje de registro se puede enviar llamando al método send(), tal como se describe en el ejemplo siguiente:

```
log.send();
```

Posteriormente, los nuevos mensajes de registro se pueden añadir fácilmente al {{site.data.keyword.iot_short_notm}} invocando el método append, tal como se describe en el ejemplo siguiente:

```
int rc = log.append("sample log", new Date(), DiagnosticLog.LogSeverity.informational);

if(rc == 200) {
    System.out.println("Current Log (" + log + ")");
} else {
    System.out.println("Log Addition failed");
}
```

Además, los mensajes de registro se pueden borrar de {{site.data.keyword.iot_short_notm}} llamando al método clear, tal como se describe en el ejemplo siguiente:

```
rc = log.clear();
if(rc == 200) {
    System.out.println("Logs are cleared successfully");
} else {
    System.out.println("Failed to clear the Logs")
}
```

Las operaciones de diagnóstico de dispositivo están pensadas para proporcionar información sobre errores de dispositivo, y no proporcionan información de diagnóstico relacionada con la conexión de dispositivos con el {{site.data.keyword.iot_short_notm}}.

Para obtener más información sobre la operación de Diagnóstico, consulte la [documentación](../device_mgmt/operations/diagnostics.html).

## Acciones de firmware
{: #firmware_actions}

El proceso de actualización del firmware se divide en dos acciones distintas:

* Descarga de firmware
* Actualización de firmware

El dispositivo necesita realizar las siguientes actividades para dar soporte a las acciones de firmware:

**1. Construir el Objeto de DeviceFirmware**

Para realizar las acciones de firmware, el dispositivo necesita construir el objeto `DeviceFirmware` y añadirlo a `DeviceData` tal como se indica a continuación:

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

El objeto `DeviceFirmware` representa el firmware actual del dispositivo y se utilizará para informar sobre el estado de la descarga de firmware y las acciones de Actualización de firmware para {{site.data.keyword.iot_short_notm}}.

**2. Informar al servidor sobre el soporte de acciones de Firmware**

Para que el servidor inicie la solicitud de firmware, el dispositivo debe definir el distintivo de la acción de firmware en true. Para ello se puede invocar el siguiente método con un valor booleano:

```
managedDevice.supportsFirmwareActions(true);
managedDevice.manage();
```

A medida que la solicitud de gestión informe al {{site.data.keyword.iot_short_notm}} sobre el soporte de la acción de firmware, el método manage() debe llamarse después de establecer el soporte de la acción de firmware.

**3. Crear el Manejador de acciones de firmware**

Para dar soporte a la acción de Firmware, el dispositivo debe crear un manejador y añadirlo a `ManagedDevice`. El manejador debe ampliar una clase `DeviceFirmwareHandler` e implementar los métodos siguientes:

```
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**3.1 Implementación de ejemplo de downloadFirmware**

La implementación debe añadir una lógica para descargar el firmware e informar sobre el estado de la descarga utilizando un objeto `DeviceFirmware`. Si la operación de descarga de firmware es satisfactoria, el estado se establece en `DOWNLOADED` y, a continuación, `UpdateStatus` se establece en `SUCCESS`.

Si se produce un error durante la descarga de firmware, el estado se establece en `IDLE` y, a continuación, el `updateStatus` se debe establecer en uno de los valores de estado de error siguientes:

* `OUT_OF_MEMORY
* CONNECTION_LOST
* INVALID_URI`

El ejemplo siguiente describe una implementación de descarga de firmware para un dispositivo Raspberry Pi:

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
            // utilizar la indicación de fecha y hora como nombre
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
            //No hay datos para leer, por lo que se establece un error
            deviceFirmware.setUpdateStatus(FirmwareUpdateStatus.INVALID_URI);
        }
    } catch(MalformedURLException me) {
        // URL no válido, por lo que establezca el estado para reflejar el mismo,
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

Un dispositivo puede comprobar la integridad de la imagen de firmware descargada utilizando el verificador e informando del estado a {{site.data.keyword.iot_short_notm}}. El verificador puede ser definido por el dispositivo durante el inicio (al crear el objeto DeviceFirmware) o como parte de la solicitud de Descarga de firmware de la aplicación. A continuación de indica un código de muestra para realizar la verificación:

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

Para todo el código, consulte el ejemplo de gestión de dispositivos de [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).



**3.2 Implementación de ejemplo de updateFirmware**

La implementación debe añadir una lógica para instalar el firmware descargado e informar sobre el estado de la actualización mediante el objeto `DeviceFirmware`. Si la operación de Actualización de firmware es satisfactoria, el estado del firmware debería establecerse en IDLE y `updateStatus` debería establecerse en `SUCCESS`.

Si se produce un error durante la Actualización de firmware, `updateStatus` debería establecerse en uno de los valores de estado de error:

`* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE`

A continuación se incluye una muestra de implementación de la Actualización de firmware del dispositivo Raspberry Pi:

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

El código completo se puede encontrar en el ejemplo de gestión de dispositivos [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java).


**4. Añadir el manejador a ManagedDevice**

El manejador creado debe añadirse a la instancia de ManagedDevice para que la biblioteca de cliente ibmiotf invoque el método correspondiente cuando haya una solicitud de acción de Firmware de {{site.data.keyword.iot_short_notm}}.

```
DeviceFirmwareHandlerSample fwHandler = new DeviceFirmwareHandlerSample();
deviceData.addFirmwareHandler(fwHandler);
```

Consulte [esta página](../device_mgmt/operations/firmware_actions.html) para obtener más información sobre la acción de Firmware.

## Acciones de dispositivos

El {{site.data.keyword.iot_short_notm}} da soporte a las siguientes acciones de dispositivos:

* Rearranque
* Restablecimiento de fábrica

Para soportar las acciones del dispositivo, el dispositivo debe llevar a cabo las siguientes actividades:

**1. Informar al servidor sobre el soporte de Acciones de dispositivos**

Para realizar el Rearranque y el Restablecimiento de fábrica, el dispositivo debe informar primero al {{site.data.keyword.iot_short_notm}} sobre su soporte. Para ello se puede invocar el siguiente método con un valor booleano:

```
managedDevice.supportsDeviceActions(true);
    managedDevice.manage();
```

A medida que la solicitud de gestión informa al {{site.data.keyword.iot_short_notm}} sobre el soporte de acciones de dispositivos, el método manage() necesita invocarse después de establecer el soporte de acción de dispositivos.

**2. Crear el Manejador de acciones de dispositivos**

Para soportar la acción del dispositivo, el dispositivo debe crear un manejador y añadirlo a ManagedDevice. El manejador debe ampliar una clase DeviceActionHandler e implementar los métodos siguientes:

```
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**2.1 Implementación de ejemplo de handleReboot**

La implementación debe añadir una lógica para rearrancar el dispositivo e informar sobre el estado del rearranque a través del objeto DeviceAction. El dispositivo debe actualizar el estado junto con un mensaje opcional sólo cuando se produzca una anomalía (dado que la operación satisfactoria rearranca el dispositivo y el código de dispositivo no tendrá control para actualizar el {{site.data.keyword.iot_short_notm}}). A continuación se incluye una muestra de implementación de rearranque para el dispositivo Raspberry Pi:

```
public void handleReboot(DeviceAction action) {
    ProcessBuilder processBuilder = null;
    Process p = null;
    processBuilder = new ProcessBuilder("sudo", "shutdown", "-r", "now");
    boolean status = false;
    try {
        p = processBuilder.start();
        // espere unos 2 minutos antes de abandonar
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

El código completo se puede encontrar en el ejemplo de gestión de dispositivos [DeviceActionHandlerSample].

  [DeviceActionHandlerSample]: https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java

**2.2 Implementación de ejemplo de handleFactoryReset**

La implementación debe añadir una lógica para restablecer los valores de fábrica del dispositivo e informar sobre el estado a través del objeto DeviceAction. El dispositivo debe actualizar el estado junto con un mensaje opcional sólo cuando se produzca una anomalía (porque como parte de este proceso, el dispositivo se reinicia y el dispositivo no tendrá un control para actualizar el estado a {{site.data.keyword.iot_short_notm}}). A continuación se muestra un resumen de la implementación del restablecimiento de los valores de fábrica:

```
public void handleFactoryReset(DeviceAction action) {
    try {
        // código para realizar el Restablecimiento de fábrica
    } catch (IOException e) {
        action.setMessage(e.getMessage());
    }
    if(status == false) {
        action.setStatus(DeviceAction.Status.FAILED);
    }
}
```

**3. Añadir el manejador a ManagedDevice**

El manejador creado debe añadirse a la instancia de ManagedDevice para que la biblioteca de cliente ibmiotf invoque el método correspondiente cuando haya una solicitud de acción de dispositivos de {{site.data.keyword.iot_short_notm}}.

```
DeviceActionHandlerSample actionHandler = new DeviceActionHandlerSample();
deviceData.addDeviceActionHandler(actionHandler);
```

Consulte [esta página](../device_mgmt/operations/device_actions.html) para obtener más información sobre la Acción de dispositivos.



## Escuchar los cambios de atributos de dispositivos
{: #listen_device_attribute}

Esta biblioteca de cliente ibmiotf actualiza los objetos correspondientes siempre que haya una solicitud de actualización de la {{site.data.keyword.iot_short_notm}}, estas solicitudes de actualización las inicia la aplicación ya sea directamente o indirectamente (Actualización de firmware) a través de la API REST de {{site.data.keyword.iot_short_notm}}. Además de actualizar estos atributos, la biblioteca proporciona un mecanismo mediante el que se puede notificar al dispositivo cuando se actualiza un atributo del dispositivo.

Los atributos que se pueden actualizar mediante esta operación son `location`, `metadata`, `device information` y `firmware`.

Para que se le notifique, el dispositivo debe añadir una escucha de cambio de propiedad en los objetos de interés.

```
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

Además, el dispositivo debe implementar el método `propertyChange()` donde reciba la notificación. El siguiente ejemplo describe cómo se puede implementar esto:

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

Para obtener más información sobre cómo actualizar los atributos de dispositivos, consulte [esta página](../device_mgmt/operations/update.html).

## Ejemplos
{: #examples}

-   [SampleRasPiDMAgent](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgent.java): Un código de agente de ejemplo que muestra cómo realizar varias operaciones de gestión de dispositivos en Raspberry Pi.
-   [SampleRasPiManagedDevice](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiManagedDevice.java): Un código de ejemplo que muestra cómo se pueden realizar las dos operaciones de dispositivos y las operaciones de gestión.
-   [SampleRasPiDMAgentWithCustomMqttAsyncClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttAsyncClient.java): Un código de agente de ejemplo con MqttAsyncClient personalizado.
-   [SampleRasPiDMAgentWithCustomMqttClient](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/SampleRasPiDMAgentWithCustomMqttClient.java): Un código de agente de ejemplo con MqttClient personalizado.
-   [RasPiFirmwareHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/RasPiFirmwareHandlerSample.java): Una implementación de ejemplo de FirmwareHandler for Raspberry Pi.
-   [DeviceActionHandlerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceActionHandlerSample.java): Una implementación de ejemplo de DeviceActionHandler
-   [ManagedDeviceWithLifetimeSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/ManagedDeviceWithLifetimeSample.java): Un ejemplo que muestra cómo enviar la solicitud de gestión regular con el tiempo de vida especificado.
-   [DeviceAttributesUpdateListenerSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/DeviceAttributesUpdateListenerSample.java): Un código de escucha de ejemplo que muestra cómo escuchar varios cambios de atributo de dispositivo.
-   [NonBlockingDiagnosticsErrorCodeUpdateSample](https://github.com/ibm-messaging/iot-java/blob/master/samples/iotfdevicemanagement/src/com/ibm/iotf/sample/devicemgmt/device/NonBlockingDiagnosticsErrorCodeUpdateSample.java): Un ejemplo que muestra cómo añadir ErrorCode sin esperar la respuesta del servidor.

##s Recipes
{: #Recipes}

Consulte [la receta](https://developer.ibm.com/recipes/tutorials/connect-raspberry-pi-as-managed-device-to-ibm-iot-foundation/) que muestra cómo conectar el dispositivo Raspberry Pi como un dispositivo gestionado a {{site.data.keyword.iot_short_notm}} para realizar varias operaciones de gestión de dispositivos paso a paso utilizando esta biblioteca de cliente.
