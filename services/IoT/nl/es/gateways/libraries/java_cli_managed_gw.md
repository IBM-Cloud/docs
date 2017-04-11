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

# Desarrollo de pasarelas gestionadas mediante Java
{: #java_cli_managed_gw}

Las pasarelas juegan un papel importante en la gestión de los dispositivos que estén conectados a ellas. Muchos dispositivos son muy básicos y no tienen funciones de gestión de dispositivos, por lo que estos dispositivos básicos se deben gestionar desde una pasarela. En {{site.data.keyword.iot_full}}, una pasarela gestionada es una pasarela que puede gestionar los dispositivos conectados a ella y proporcionar funciones de gestión de dispositivos, como por ejemplo actualizaciones de firmware, ubicación y diagnóstico.
{:shortdesc}

Mediante la biblioteca de cliente Java™ de {{site.data.keyword.iot_short}} y la información que se proporciona, puede desarrollar código Java para convertir su pasarela en una pasarela gestionada. También se proporcionan ejemplos para ayudarle a desarrollar código Java para conectar una pasarela al servicio de gestión de dispositivos y ejecutar operaciones de gestión de dispositivos.

## Servicio de gestión de dispositivos
{: #dm_service}

El servicio de gestión de dispositivos (DM) de {{site.data.keyword.iot_short}} proporciona funciones de gestión de dispositivos para que pasarelas gestionen los dispositivos que tienen conectados.

Una pasarela gestionada ejecuta un agente de gestión de dispositivos, que se ejecuta como un proxy para todos los dispositivos que se conectan a {{site.data.keyword.iot_short}} a través de la pasarela.

### Agente de gestión de dispositivo

Los dispositivos que se conectan a {{site.data.keyword.iot_short}} indirectamente a través de una pasarela pueden utilizar diversos protocolos de conexión, si reciben soporte del dispositivo de pasarela.

La instancia `ManagedGateway` es un agente de gestión de dispositivos que proporciona una lista de métodos para realizar una o varias acciones de gestión de dispositivos, como por ejemplo participar en la actividad de gestión de dispositivos, actualizar códigos de error y acciones sobre registros, ubicación y firmware o dispositivos.

El agente de gestión de dispositivos de la pasarela convierte y procesa el protocolo de conexión de los dispositivos de conexión, lo que garantiza que el dispositivo se puede gestionar mediante {{site.data.keyword.iot_short}}. A través del agente de gestión de dispositivos, la pasarela se convierte en más que un túnel transparente entre el dispositivo conectado y {{site.data.keyword.iot_short}}. Por ejemplo, si un dispositivo que está conectado a una pasarela no puede descargar firmware, el agente de gestión de dispositivos de la pasarela puede realizar las siguientes acciones:
- Interceptar una solicitud para que un dispositivo descargue firmware
- Descargar el firmware para el dispositivo
- Almacenar el firmware del dispositivo en la pasarela

Más adelante, cuando se solicite al dispositivo que realice la actualización, el agente de gestión de dispositivos de la pasarela puede enviar el firmware al dispositivo y actualizarlo.

## Creación del modelo de dispositivo
{: #create_device_model}

En {{site.data.keyword.iot_short}}, el modelo de dispositivo describe los metadatos y las características de gestión de dispositivos y pasarelas. La base de datos del dispositivo es el origen maestro de la información del dispositivo o de la pasarela. Las aplicaciones y los dispositivos gestionados pueden enviar actualizaciones de ubicación, actualizaciones del progreso de actualización de firmware y otros tipos de actualizaciones. Cuando {{site.data.keyword.iot_short}} recibe las actualizaciones, la base de datos del dispositivo se actualiza para que la información esté disponible para las aplicaciones que se conectan.

En la biblioteca cliente Java de {{site.data.keyword.iot_short}}, el modelo de dispositivo se representa mediante la clase Java `DeviceData`.

Para crear la clase `DeviceData`, cree los siguientes objetos:

- `DeviceInfo` (opcional)
- `DeviceLocation` (Opcional, solo es obligatorio si el dispositivo desea que se le notifique la ubicación definida por la aplicación mediante la API de {{site.data.keyword.iot_short}})
- `DeviceFirmware` (opcional)
- `DeviceMetadata` (opcional)

Para obtener más información, consulte [modelo de dispositivo](../../reference/device_model.html).

### DeviceInfo

El siguiente fragmento de código que contiene datos de ejemplo muestra cómo crear los objetos `DeviceInfo` y `DeviceMetadata`:

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
  * Crear un objeto DeviceMetadata
 **/
JsonObject data = new JsonObject();
data.addProperty("customField", "customValue");
DeviceMetadata metadata = new DeviceMetadata(data);

```

En el siguiente fragmento de código se describe cómo crear la clase `DeviceData` utilizando los objetos `DeviceInfo` y `DeviceMetadata` creados en el ejemplo anterior:

```java
DeviceData deviceData = new DeviceData.Builder().
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();
```

Cada pasarela y cada dispositivo conectado debe tener su propia definición de clase `DeviceData` para representarse a sí mismo en {{site.data.keyword.iot_short}}. Para pasarelas, la clase `DeviceData` se transfiere a la biblioteca como parte del proceso de creación de la instancia `ManagedGateway`. Para dispositivos conectados, la clase `DeviceData` se transfiere a la biblioteca como parte del objeto `sendDeviceManageRequest()`.

## Constructores ManagedGateway
{: #construct_managed_gateway}

`ManagedGateway` es una clase Java que conecta una pasarela con {{site.data.keyword.iot_short}} como pasarela gestionada que puede realizar al menos una operación de gestión de dispositivos para sí misma o para los dispositivos conectados. Una instancia `ManagedGateway` puede se puede utilizar para realizar operaciones normales de pasarela, como por ejemplo publicar sucesos de pasarela, adjuntar sucesos de dispositivo y escuchar mandatos procedentes de aplicaciones. La instancia `ManagedGateway` es un agente de gestión de dispositivos.

En la clase `ManagedGateway` dos constructores, Constructor One y Constructor Two, dan soporte a distintos patrones del usuario.

### Constructor One

Constructor One crea una instancia `ManagedGateway` aceptando una clase `DeviceData` que contiene todas las propiedades siguientes:

| Propiedad     |Descripción     |
|----------------|----------------|
|`Organization-ID` |El ID de la organización.|
|`Gateway-Type` |El tipo de dispositivo de pasarela.|
|`Gateway-ID` |El ID del dispositivo de pasarela.|
|`Authentication-Method`|El método de autenticación. El único método al que se da soporte es "token".|
|`Authentication-Token`|La señal de la clave de la API.|
|`auth-key`   |Una clave de API opcional, que debe especificar al establecer el valor de auth-method en `apikey`.|
|`auth-token`   |Una señal de clave API, que también es obligatoria al establecer el valor de auth-method en `apikey`. |
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la pasarela en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en `true`.|
|`Port`|El número de puerto al que conectarse. Especifique 8883 o 443. Si no especifica un número de puerto, el cliente se conectará a {{site.data.keyword.iot_short_notm}} en el número de puerto 8883 de forma predeterminada.|
|`WebSocket`|Un valor true o false que sólo es necesario si desea conectar la pasarela mediante websockets.|
|`MaxInflightMessages`  |Establece el número máximo de mensajes en vuelo para la conexión. El valor predeterminado es 100.|
|`Automatic-Reconnect`  |Un valor true o false que es necesario cuando desea que el dispositivo se conecte automáticamente a {{site.data.keyword.iot_short_notm}} mientras se encuentra en un estado desconectado. El valor predeterminado es false.|
|`Disconnected-Buffer-Size`|El número máximo de mensajes que se pueden almacenar en memoria mientras el cliente está desconectado. El valor predeterminado es 5000.|

**Nota:** Para conectar la pasarela en modalidad de suscripción duradera, establezca `clean-session` en `false`. Para obtener más información sobre la propiedad `clean-session`, consulte la sección 'Almacenamientos intermedios de suscripción y sesión limpia' de la [documentación de MQTT](../../reference/mqtt/index.html#subscription-buffers-and-clean-session).

El código siguiente describe cómo puede crear una instancia `ManagedGateway`:

```java
Properties options = new Properties();
options.setProperty("Organization-ID", "uguhsp");
options.setProperty("Gateway-Type", "iotsample-arduino");
options.setProperty("Gateway-ID", "00aabbccde03");
options.setProperty("Authentication-Method", "token");
options.setProperty("Authentication-Token", "AUTH TOKEN FOR DEVICE");

ManagedGateway ManagedGateway = new ManagedGateway(options, deviceData);
```

### Constructor Two

Constructor Two crea una instancia `ManagedGateway` aceptando un objeto `DeviceData` y la instancia de cliente de MQTT. Constructor Two también requiere que el objeto `DeviceData` de la instancia incluya el tipo de dispositivo y el ID de dispositivo, tal como se muestra en el ejemplo de código siguiente:

```java
// Código que crea una instancia de cliente MQTT síncrona o asíncrona de mqttClient.
.....

// Código que crea el objeto DeviceData
DeviceData deviceData = new DeviceData.Builder().
                         typeId("Gateway-Type").
                         deviceId("Gateway-ID").
                         deviceInfo(deviceInfo).
                         metadata(metadata).
                         build();

....
ManagedGateway ManagedGateway = new ManagedGateway(mqttClient, deviceData);

```

**Nota:** si está desarrollando para dispositivos personalizados, utilice Constructor Two, ya que este constructor crea una instancia de la pasarela gestionada utilizando la instancia del cliente MQTT existente y así puede aprovechar las operaciones de gestión de dispositivos. Utilice la biblioteca del cliente Java para todas las funciones del dispositivo.

## Solicitudes de gestión de dispositivos procedentes de una pasarela
{: #dm_requests}

### Envío de una solicitud de gestión procedente de una pasarela

Para indicar a una pasarela que participe en actividades de gestión de dispositivos, invoque el método `sendGatewayManageRequest()`, tal como se muestra en el ejemplo de código siguiente:

```java
managedGateway.sendGatewayManageRequest(0, true, true);
```
La solicitud de gestión inicia una solicitud de conexión internamente si el dispositivo aún no está conectado a {{site.data.keyword.iot_short}}.

El método `sendGatewayManageRequest()` acepta los parámetros siguientes:

| Parámetro     |Descripción     |
|----------------|----------------|
|`lifetime`|El periodo de tiempo en segundos en el que la pasarela debe enviar otra solicitud de gestión de tipo de dispositivo para evitar que se clasifique como inactiva y que se convierta en un dispositivo no gestionado. Si se omite el campo `lifetime` o se establece en 0, la pasarela gestionada no se convierte en inactiva. El valor mínimo admitido para el campo `lifetime` es 3600 segundos (1 hora).|
|`supportFirmwareActions`|Un valor true o false que determina si la pasarela da soporte a acciones de firmware. La pasarela también debe añadir un manejador de firmware para manejar las solicitudes de firmware.|
|`supportDeviceActions`|Un valor true o false que determina si la pasarela da soporte a acciones de dispositivo. La pasarela también debe añadir un manejador de acción de dispositivo para manejar las solicitudes de reinicio y restablecimiento de valores de fábrica.|


La instancia `ManagedGateway` es un agente de gestión de dispositivos que proporciona una lista de métodos para realizar una o varias acciones de gestión de dispositivos, como por ejemplo participar en la actividad de gestión de dispositivos, actualizar códigos de error y acciones sobre registros, ubicación y firmware o dispositivos.

### Envío de una solicitud de gestión procedente de dispositivos conectados

Para permitir que los dispositivos conectados detrás de una pasarela participen en actividades de gestión de dispositivos en la pasarela, invoque el método `sendDeviceManageRequest()`.

El método `sendDeviceManageRequest()` acepta los detalles de los dispositivos conectados y los parámetros `lifetime`, `supportFirmwareActions` y `supportDeviceActions`. Una pasarela también puede utilizar el método `sendDeviceManageRequest()` sobrecargado para definir el objeto `DeviceData` para el dispositivo conectado.

#### Ejemplo de envío de una solicitud de gestión procedente de dispositivos conectados

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, lifetime, true, true);
```

### Envío de una solicitud de no gestión procedente de una pasarela

Cuando ya no es necesario gestionar una pasarela, invoque el método `sendGatewayUnmanageRequet()` a fin de detener las actividades de gestión de dispositivos de la pasarela.  Cuando se invoca `sendGatewayUnmanageRequet()`, {{site.data.keyword.iot_short}} deja de enviar solicitudes de gestión de dispositivos para la pasarela, con la excepción de las solicitudes **Manage**. Las solicitudes procedentes de los dispositivos que están detrás de la pasarela no se rechazan.

#### Ejemplo de envío de una solicitud de no gestión procedente de una pasarela

```java
managedGateway.sendGatewayUnmanageRequet();
```

### Envío de una solicitud de no gestión procedente de dispositivos conectados

Cuando ya no es necesario gestionar un dispositivo situado detrás de una pasarela, a pasarela puede invocar el método `sendDeviceUnmanageRequet()` a fin de pasar el dispositivo del estado gestionado al estado no gestionado. Cuando se invoca `sendDeviceUnmanageRequet()`, {{site.data.keyword.iot_short}} deja de enviar nuevas solicitudes de gestión de dispositivos para el dispositivo y todas las solicitudes de gestión de dispositivos procedentes de la pasarela destinadas al dispositivo conectado se rechazan, con la excepción de las solicitudes **Manage**.

#### Ejemplo de envío de una solicitud de no gestión procedente de dispositivos conectados

```java
managedGateway.sendDeviceUnmanageRequet();
```

## Actualizaciones de ubicación
{: #location_updates}

### Envío de actualizaciones de ubicación de pasarela

Las pasarelas que pueden determinar su ubicación pueden optar por notificar a {{site.data.keyword.iot_short}} sobre los cambios de ubicación. La pasarela puede invocar uno de los métodos `updateLocation()` sobrecargados para actualizar la ubicación del dispositivo.

```java
    // actualizar la ubicación con latitud, longitud y elevación.
int rc = managedGateway.updateGatewayLocation(30.28565, -97.73921, 10);
if(rc == 200) {
    System.out.println("Location updated successfully!");
} else {
System.err.println("Failed to update the location!");
    }
```

### Envío de actualizaciones de ubicación de dispositivo conectado

La pasarela puede invocar el método de dispositivo `updateDeviceLocation()` correspondiente para actualizar la ubicación de los dispositivos conectados. El método sobrecargado se puede utilizar para especificar el método `measuredDateTime`.  

```java
// actualizar la ubicación del dispositivo conectado con latitud, longitud y elevación
int rc = managedGateway.updateDeviceLocation(typeId, deviceId, 30.28565, -97.73921, 10);
```
Para obtener más información sobre las actualizaciones de ubicación, consulte [Solicitudes de gestión de dispositivos](../../devices/device_mgmt/index.html#/update-location#update-location).

## Manejo de códigos de error
{: #errors}

### Creación y supresión de códigos de error

Una pasarela puede optar por notificar a {{site.data.keyword.iot_short}} sobre los cambios en su estado de error. La pasarela puede invocar el método `addErrorCode()` para añadir el código de error actual a {{site.data.keyword.iot_short}}.

```java
int rc = managedGateway.addGatewayErrorCode(300);
```

Los códigos de error correspondientes a una pasarela se pueden borrar de {{site.data.keyword.iot_short}} mediante una llamada al método `clearErrorCodes()`, tal como se muestra a continuación:

```java
int rc = managedGateway.clearGatewayErrorCodes();
```

### Creación y supresión de códigos de error correspondientes a dispositivos conectados

Una pasarela también puede invocar el método de dispositivo correspondiente para añadir o borrar códigos de error para los dispositivos conectados:

```java
int rc = managedGateway.addDeviceErrorCode(typeId, deviceId, 300);
rc = managedGateway.clearDeviceErrorCodes(typeId, deviceId);
```

### Creación y supresión de mensajes de registro de la pasarela

Una pasarela puede optar por notificar a {{site.data.keyword.iot_short}} sobre cambios mediante la adición de una nueva entrada de registro. Una entrada de registro incluye la información siguiente:

- Serie del mensaje
- Indicación de fecha y hora
- Gravedad
- De forma opcional, datos de diagnóstico binarios codificados en base64

Las pasarelas pueden invocar el método `addGatewayLog()` para enviar mensajes de registro, tal como se muestra en el ejemplo siguiente:

```java
// Ejemplo de suceso de registro
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addGatewayLog(message, timestamp, severity);
```

Los mensajes se pueden borrar de {{site.data.keyword.iot_short}} mediante una llamada al método `clearLogs()`:

```java
rc = managedGateway.clearGatewayLogs();
```

### Creación y supresión de registros correspondientes a dispositivos conectados

De forma similar, la pasarela puede invocar el método de dispositivo correspondiente para crear o borrar los registros para los dispositivos conectados, tal como se muestra en el ejemplo de código siguiente:

```java

// Ejemplo de suceso de registro:
String message = "Firmware Download Progress (%): " + 50;
Date timestamp = new Date();
LogSeverity severity = LogSeverity.informational;
int rc = managedGateway.addDeviceLog(typeId, deviceId, message, timestamp, severity);
```

Para borrar los registros de los dispositivos conectados, invoque el método `clearDeviceLogs()` especificando los detalles del dispositivo conectado, tal como se muestra en el ejemplo de código siguiente:

```java
int rc = managedGateway.clearDeviceLogs(typeId, deviceId);
```

Las operaciones de diagnóstico de dispositivo están pensadas para proporcionar información sobre errores de pasarela o de dispositivo. No proporcionan información de diagnóstico sobre la conexión de los dispositivos con {{site.data.keyword.iot_short}}.

Para obtener más información sobre la operación de diagnósticos, consulte [Solicitudes de gestión de dispositivos](../../devices/device_mgmt/index.html#/update-location#update-location).

## Actualizaciones y acciones de firmware
{: #firmware}

El proceso de actualización del firmware se divide en dos acciones distintas:

- Descarga de firmware
- Actualización de firmware

La pasarela debe realizar las siguientes actividades para dar soporte a las acciones de firmware tanto para sí misma como para sus dispositivos conectados:

1. Opcional: crear un objeto `DeviceFirmware`.
2. Informar al servidor sobre el soporte de acciones de firmware.
3. Crear el manejador de acciones de firmware.
4. Añadir el manejador a `ManagedGateway`.

### Paso 1: Creación de un objeto `DeviceFirmware`

Para realizar acciones de firmware, una pasarela puede opcionalmente crear un objeto `DeviceFirmware` para sí misma y para sus dispositivos conectados y luego añadirlo al objeto `DeviceData`, tal como se muestra en el ejemplo siguiente:

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

Para los dispositivos conectados, el objeto `DeviceData` creado se puede pasar a la biblioteca al enviar la solicitud de gestión, tal como se muestra en el ejemplo de código siguiente:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, lifetime, supportFirmwareActions, supportDeviceActions);
```

El objeto `DeviceFirmware` representa el firmware actual de la pasarela o del dispositivo y se utiliza para informar sobre el estado de la descarga de firmware y las acciones de actualización de firmware a {{site.data.keyword.iot_short}}. Si la pasarela no crea el objeto `DeviceFirmware`, la biblioteca crea un objeto vacío y notifica el estado a {{site.data.keyword.iot_short}}.

### Paso 2: Notificación al servidor sobre el soporte de la acción de firmware

La pasarela o sus dispositivos conectados deben establecer el distintivo de la acción de firmware en true para que el servidor inicie la solicitud de firmware. Este cambio se puede conseguir pasando el valor true para el parámetro `supportFirmwareActions` en la solicitud de gestión.

La pasarela puede invocar el método siguiente para informar al servidor sobre su soporte de firmware:
```java
managedGateway.sendGatewayManageRequest(3600, true, false);
```

De forma similar, la pasarela puede invocar el método de dispositivo correspondiente para informar sobre el soporte de firmware de los dispositivos conectados:

```java
managedGateway.sendDeviceManageRequest(typeId, deviceId, deviceData, 3600, true, false);
```

Cuando se notifica el soporte al servidor de gestión de dispositivos, el servidor reenvía las acciones de firmware a la pasarela para la propia pasarela o para los dispositivos situados detrás de la misma.

### Paso 3: Creación del manejador de acciones de firmware

Para dar soporte a la acción de firmware, la pasarela debe crear un manejador y añadirlo a `managedGateway`. El manejador debe ampliar una clase `DeviceFirmwareHandler` e implementar los métodos siguientes:

```java
public abstract void downloadFirmware(DeviceFirmware deviceFirmware);
public abstract void updateFirmware(DeviceFirmware deviceFirmware);
```

**Nota**: solo debe añadirse un manejador a la biblioteca para la pasarela y para los dispositivos conectados a los que se redirigen las solicitudes de descarga o actualización de firmware. La implementación debe crear una hebra o una agrupación de hebras para manejar varias solicitudes de firmware simultáneamente.

Encontrará una implementación de ejemplo de un manejador de agrupación de hebras en el [Repositorio GitHub de ejemplos de pasarela ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Una implementación de ejemplo de `downloadFirmware`

La implementación debe añadir lógica para descargar el firmware e informar sobre el estado de la descarga utilizando un objeto `DeviceFirmware`. Si la operación de descarga de firmware se ejecuta correctamente, el estado del firmware se debe establecer en 'DOWNLOADED' y la propiedad `UpdateStatus` en 'SUCCESS'.

Si se produce un error durante la descarga de firmware, estado se debe establecer en 'IDLE' y la propiedad `updateStatus` en uno de los siguientes valores de estado de error:

- OUT_OF_MEMORY
- CONNECTION_LOST
- INVALID_URI

En el ejemplo de código siguiente se muestra una implementación de descarga de firmware de ejemplo:

**Importante:** el código de ejemplo que se proporciona no incluye la sección de la agrupación de hebras. Encontrará un ejemplo de implementación completa de manejador de firmware en el [Repositorio GitHub de ejemplos de pasarela de IBM Java ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

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

Una pasarela gestionada puede comprobar la integridad de la imagen de firmware descargada utilizando el verificador e informando del estado a {{site.data.keyword.iot_short}}. La pasarela puede definir el verificador durante las fases siguientes:

- Durante el inicio cuando se crea el objeto 'DeviceFirmware'
- Cuando una aplicación envía una solicitud 'downloadFirmware'

#### Ejemplo

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

Encontrará el código completo en el ejemplo de gestión de pasarelas [GatewayFirmwareHandlerSample](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java).

### Una implementación de ejemplo de `updateFirmware`

La implementación debe crear una hebra separada y añadir lógica para instalar el firmware descargado e informar sobre el estado de la actualización mediante el objeto `DeviceFirmware`. Si la operación de actualización de firmware se ejecuta correctamente, el estado del firmware se debe establecer en 'IDLE' y el valor de `updateStatus` en 'SUCCESS'.

Si se produce un error durante la actualización de firmware, el valor de `updateStatus` se debe establecer en uno de los siguientes valores de estado de error:

* OUT_OF_MEMORY
* UNSUPPORTED_IMAGE

El ejemplo de código siguiente muestra cómo se puede implementar una actualización de firmware para un dispositivo Raspberry Pi:

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

Encontrará el código completo en el ejemplo `GatewayFirmwareHandlerSample` del [Repositorio de  GitHub de ejemplos de pasarela ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayFirmwareHandlerSample.java){: new_window}.

### Paso 4: Adición del manejador a `ManagedGateway`

Cuando se crea un manejador, se debe añadir a la instancia `ManagedGateway` para que la biblioteca de cliente Java invoque el método correspondiente cuando haya una solicitud de acción de firmware procedente de {{site.data.keyword.iot_short}}.

```java
GatewayFirmwareHandlerSample fwHandler = new GatewayFirmwareHandlerSample();
mgdGateway.addFirmwareHandler(fwHandler);
```

Para obtener más información sobre las acciones de firmware, consulte [Solicitudes de gestión de dispositivos ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/requests.html#/firmware-actions#firmware-actions){: new_window}.

## Acciones de dispositivos
{: #dev_actions}

{{site.data.keyword.iot_short}} da soporte a las siguientes acciones de dispositivo:

- Rearranque
- Restablecimiento de fábrica

La pasarela debe realizar las siguientes actividades para dar soporte a las acciones de dispositivo para sí misma y para los dispositivos que hay detrás:

1. Informar al servidor sobre el soporte de acciones de dispositivo.
2. Crear el manejador de acciones de dispositivo.
3. Añadir el manejador a `ManagedGateway`.

### Paso 1: Notificación al servidor sobre el soporte de acciones de dispositivo

Para realizar un rearranque o un restablecimiento de valores de fábrica para una pasarela y sus dispositivos conectados, primero la pasarela debe informar a {{site.data.keyword.iot_short}} sobre el soporte. Esta acción se puede realizar pasando el valor true para el parámetro `supportDeviceActions` al enviar la solicitud **Manage**.

Una pasarela puede invocar el método siguiente para informar al servidor sobre su soporte de dispositivo:

```java
// El último parámetro representa el soporte de la acción de dispositivo
managedGateway.sendGatewayManageRequest(3600, true, true);
```

Una pasarela puede invocar el método de dispositivo correspondiente para informar sobre el soporte de acción de dispositivo de los dispositivos conectados:

```java
// El último parámetro representa el soporte de la acción de dispositivo
managedGateway.sendDeviceManageRequest(typeId, deviceId, 0, true, true);
```

Cuando se notifica el soporte al servidor de gestión de dispositivos, el servidor reenvía las solicitudes de acción de dispositivo al dispositivo.

### Paso 2: Creación del manejador de acciones de dispositivo

Para dar soporte a la acción de dispositivo, la pasarela debe crear un manejador y añadirlo a la instancia `managedGateway`. El manejador debe ampliar una clase `DeviceActionHandler` e implementar los métodos siguientes:

```java
public abstract void handleReboot(DeviceAction action);
public abstract void handleFactoryReset(DeviceAction action);
```

**Nota:** solo debe añadirse un manejador a la biblioteca para la pasarela y para los dispositivos conectados a los que se redirigen las solicitudes de acción del dispositivo. La implementación debe crear una hebra o una agrupación de hebras para manejar varias solicitudes de acción de dispositivo simultáneamente. Encontrará una implementación de manejador de ejemplo que utiliza una agrupación de hebras en el [Repositorio de GitHub iot-gateway-samples ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.

### Una implementación de ejemplo de `handleReboot`

La implementación debe crear una hebra separada y añadir lógica para reiniciar la pasarela y el dispositivo conectado y notificar sobre el estado del reinicio mediante un objeto `DeviceAction`. Después de recibir la solicitud, primero la pasarela debe informar al servidor acerca del soporte o anomalía antes de continuar con el reinicio real. Si el ejemplo no puede reiniciar el dispositivo o si se produce algún otro error durante el reinicio, la pasarela puede actualizar el estado en un mensaje opcional. En el siguiente código de ejemplo se incluye una muestra de implementación de reinicio para un dispositivo Raspberry Pi:

```java
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

Encontrará la implementación completa de manejador de ejemplo que utiliza una agrupación de hebras en el [Repositorio de GitHub iot-gateway-samples ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/blob/master/java/advanced-gateway-sample/src/main/java/com/ibm/iotf/sample/gateway/GatewayActionHandlerSample.java){: new_window}.


### Una implementación de ejemplo de `handleFactoryReset`

La implementación debe crear una hebra separada y añadir lógica para restablecer la pasarela y el dispositivo conectado en los valores de fábrica y notificar sobre el estado del restablecimiento mediante un objeto DeviceAction. Cuando se recibe la solicitud, primero la pasarela debe informar al servidor acerca del soporte o anomalía antes de continuar con el restablecimiento real. En el ejemplo de código siguiente se muestra una implementación de restablecimiento de valores de fábrica:

```java
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

### Paso 3: Adición del manejador a `ManagedGateway`

Cuando se crea un manejador, se debe añadir a la instancia `ManagedGateway` para que la biblioteca de cliente Java invoque el método correspondiente cuando haya una solicitud de acción de dispositivo procedente de {{site.data.keyword.iot_short}} para la pasarela o los dispositivos conectados.

```java
GatewayActionHandlerSample actionHandler = new GatewayActionHandlerSample();
mgdGateway.addDeviceActionHandler(actionHandler);
```

Para obtener más información sobre las acciones de dispositivo, consulte [Solicitudes de gestión de dispositivos ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](../../devices/device_mgmt/requests.html#/device-actions-reboot#device-actions-reboot){: new_window}.

## Escucha de los cambios de atributos de dispositivos
{: #listen_device_attributes}

La biblioteca de cliente Java actualiza los objetos correspondientes cuando se recibe una solicitud de actualización procedente de {{site.data.keyword.iot_short}}. La aplicación inicia estas solicitudes de actualización directa o indirectamente a través de una actualización de firmware utilizando la API REST {{site.data.keyword.iot_short}}. Además de actualizar estos atributos, la biblioteca proporciona un mecanismo por el que se puede notificar a la pasarela cuando se actualiza un atributo del dispositivo.

Los atributos que se pueden actualizar mediante este tipo de operación son ubicación, metadatos, información de dispositivo y firmware de la pasarela o de los dispositivos conectados.

Para que se le notifique sobre cambios de atributos, la pasarela debe añadir un escucha de cambio de propiedades a los objetos en los que está interesada, lo que se muestra en el ejemplo de código siguiente:

```java
deviceLocation.addPropertyChangeListener(listener);
firmware.addPropertyChangeListener(listener);
deviceInfo.addPropertyChangeListener(listener);
metadata.addPropertyChangeListener(listener);
```

La pasarela también debe implementar el método `propertyChange()` donde reciba la notificación, lo que se muestra en la siguiente implementación de ejemplo:

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

Para obtener más información sobre la actualización de atributos de dispositivo, consulte [Solicitudes de gestión de dispositivos ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/devices/device_mgmt/index.html#/update-device-attributes#update-device-attributes){: new_window}.

## Ejemplos
{: #samples}

Dispone de varios ejemplos para ayudarle a conectar pasarelas y dispositivos situados detrás de pasarelas a su instancia de {{site.data.keyword.iot_short_notm}}. En los ejemplos se utiliza la biblioteca cliente Java de {{site.data.keyword.iot_short_notm}}y se encuentran en el [Repositorio GitHub de ejemplos de pasarela ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-gateway-samples/tree/master/java/gateway-samples){: new_window}.

## Recetas
{: #recipes}

Para ver una receta que muestra cómo conectar un dispositivo Raspberry Pi como pasarela gestionada a {{site.data.keyword.iot_short_notm}} y gestionar los dispositivos conectados, consulte el apartado sobre [Raspberry Pi como una pasarela gestionada en {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/recipes/tutorials/raspberry-pi-as-managed-gateway-in-watson-iot-platform-part-1/){: new_window}.

En la receta se explica cómo utilizar el protocolo de gestión de dispositivos de {{site.data.keyword.iot_short_notm}} para gestionar un dispositivo Arduino Uno desde un dispositivo Raspberry Pi que actúa como pasarela y realizar operaciones de gestión de dispositivos, como por ejemplo rearrancar el dispositivo o añadir un esbozo de programa.
