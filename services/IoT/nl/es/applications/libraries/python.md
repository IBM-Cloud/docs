---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-04"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Python para desarrolladores de aplicaciones
{: #python}


Puede utilizar Python para crear y desarrollar aplicaciones que interactúan con su organización en {{site.data.keyword.iot_full}}. El cliente Python para {{site.data.keyword.iot_short_notm}} proporciona una API para facilitar la interacción simple con las características de {{site.data.keyword.iot_short_notm}} abstrayendo los protocolos subyacentes como MQTT y HTTP.

{:shortdesc}

Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar las aplicaciones por medio de Python.

## Descarga del cliente y los recursos de Python
{: #python_client_download}

Para acceder al cliente Python para {{site.data.keyword.iot_short_notm}} y otros recursos disponibles, vaya al repositorio [iot-python ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://github.com/ibm-messaging/iot-python){: new_window} en GitHub y complete las instrucciones de instalación.

## Constructor
{: #constructor}

El diccionario de opciones crea definiciones que se utilizan para interactuar con el módulo de {{site.data.keyword.iot_short_notm}}. El constructor compila la instancia de cliente y acepta un diccionario de opciones que contiene las siguientes definiciones:

|Definición|Descripción |
|:-----|:-----|
|`orgId`|El ID de la organización.|
|`appId`|El ID exclusivo de una aplicación en su organización.|
|`auth-method`|El método de autenticación. El único método al que se da soporte es `apikey`.|
|`auth-key`|Una clave de API opcional, que debe especificar al establecer el valor de auth-method en `apikey`.|
|`auth-token`|Una señal de clave API, que también es obligatoria al establecer el valor de auth-method en `apikey`.|
|`clean-session`|Un valor true o false que sólo es necesario si desea conectar la aplicación en modalidad de suscripción duradera. De forma predeterminada, `clean-session` se establece en true.|


Si no se proporciona el diccionario de opciones, el cliente se conecta al servicio Inicio rápido de {{site.data.keyword.iot_short_notm}} como un dispositivo no registrado.

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

### Utilización de un archivo de configuración


Si no utiliza un diccionario de opciones, debe incluir un archivo de configuración que contenga un diccionario de opciones en el siguiente formato de código:

```python

import ibmiotf.application
try:
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)
except ibmiotf.ConnectionException as e:
...
```
El archivo de configuración de aplicación debe estar en el formato siguiente:

```python

[application]
org=orgId
id=myApplication
auth-method=apikey
auth-key=key
auth-token=token
clean-session=true/false

```

## Llamadas de la API
{: #api_calls}

Cada método del cliente de API responde con:

- Una respuesta JSON o Booleana válida si es satisfactorio
- Una excepción IoTFCReSTException si no es satisfactorio

Para obtener más información sobre el motivo del fallo de una llamada a API, o para ver si la acción es parcialmente satisfactoria, una aplicación puede analizar las propiedades de una respuesta de excepciones. La respuesta de la excepción IoTFCReSTException contiene las siguientes propiedades:

|Propiedad|Descripción|
|:---|:---|
|`httpcode`|Código de estado HTTP.|
|`message`|Un mensaje de excepción que contiene el motivo de la anomalía.|
|`response`|El elemento JSON que contiene la respuesta parcial. Si no existe ninguna, este valor se establece en null.|

## Suscripción a sucesos de dispositivos
{: #subscribe_device_events}

Los sucesos son el mecanismo por el que los dispositivos publican datos en la instancia de {{site.data.keyword.iot_short_notm}}. El dispositivo controla el contenido del suceso y asigna un nombre a cada suceso que envía.

Cuando la instancia de {{site.data.keyword.iot_short_notm}} recibe un suceso, las credenciales del suceso recibido identifican el dispositivo de envío, lo que hace que sea imposible que un dispositivo suplante a otro dispositivo.

De forma predeterminada, las aplicaciones se suscriben a todos los sucesos desde todos los dispositivos conectados. Utilice los parámetros deviceType, deviceId, event y msgFormat para controlar el ámbito de la suscripción. Un cliente individual puede admitir varias suscripciones. Los siguientes ejemplos de código muestran cómo puede utilizar los parámetros deviceType, deviceId, event y msgFormat para definir el ámbito de una suscripción:


### Suscripción a todos los sucesos de todos los dispositivos


```python

import ibmiotf.application
  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents()
```

### Suscripción a todos los sucesos de todos los dispositivos de un tipo específico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType)
```

### Suscripción a un suceso específico de todos los dispositivos


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(event=myEvent)
```

### Suscripción a un suceso específico de dos o más dispositivos distintos

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, event=myEvent)
client.subscribeToDeviceEvents(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId, event=myEvent)
```

### Suscripción a todos los sucesos que se publican en formato JSON

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceEvents(deviceType=myDeviceType, deviceId=myDeviceId, msgFormat="json")
```

## Manejo de sucesos desde dispositivos
{: #handling_events_devices}

Para procesar los sucesos recibidos por las suscripciones, tiene que registrar un método callback de sucesos. Los mensajes se devuelven como una instancia de la clase de suceso:

|Propiedad|Tipos de datos|Descripción|
|:---|:---|
|`event.device`|Serie|Identifica de forma exclusiva el dispositivo a través de todos los tipos de dispositivos de la organización|
|`event.deviceType`|Serie|Identifica el tipo de dispositivo. Normalmente, el deviceType es una agrupación para los dispositivos que realizan una tarea específica, como por ejemplo "weatherballoon".|
|`event.deviceId`|Serie|Representa el ID del dispositivo. Normalmente, para un determinado tipo de dispositivo, el deviceId es un identificador exclusivo de dicho dispositivo, por ejemplo un número de serie o una dirección MAC.|
|`event.event`|Serie|Normalmente se utiliza para agrupar sucesos específicos, como por ejemplo "status", "warning" y "data".
|`event.format`|Serie|El formato puede ser una serie, como por ejemplo JSON.
|`event.data`|Diccionario|Los datos para la carga útil de mensaje. La longitud máxima es 131072 bytes.
|`event.timestamp`|Fecha y hora|La fecha y hora del suceso|

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


## Suscripción a estado de dispositivos
{: #subscribe_device_status}


De forma predeterminada, al suscribirse al estado del dispositivo, se recibirán actualizaciones de estado para todos los dispositivos conectados. Utilice los parámetros type e ID para controlar el ámbito de la suscripción. Un cliente individual puede admitir varias suscripciones.

### Suscripción a actualizaciones de estado para todos los dispositivos


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus()
```

### Suscripción a actualizaciones de estado para todos los dispositivos de un tipo específico


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType)
```

### Suscripción a actualizaciones de estado para dos dispositivos distintos


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
client.subscribeToDeviceStatus(deviceType=myDeviceType, deviceId=myDeviceId)
client.subscribeToDeviceStatus(deviceType=myOtherDeviceType, deviceId=myOtherDeviceId)
```

## Manejo de actualizaciones de estado desde dispositivos
{: #handling_device_updates}

Sucesos de estado

Para procesar las actualizaciones de estado recibidas por las suscripciones, tiene que registrar un método callback de sucesos. Los mensajes se devuelven como una instancia de la clase Estado.

Hay dos tipos de sucesos de estado: sucesos `Connect` y sucesos `Disconnect`. Todos los sucesos de estado incluyen las siguientes propiedades:

|Propiedad|Tipos de datos|
|:---|:---|
|`status.clientAddr`|Serie|
|`status.protocol`|Serie|
|`status.clientId`|Serie|
|`status.user`|Serie|
|`status.time`|Fecha y hora|
|`status.action`|Serie|
|`status.connectTime`|Fecha y hora|
|`status.port`|Entero|


La propiedad `status.action` determina si un suceso de estado es de tipo `Connect` o `Disconnect`.

Los sucesos de estado `Disconnect` incluyen las siguientes propiedades adicionales:

|Propiedad|Tipos de datos|
|:---|:---|
|`status.writeMsg`|Entero|
|`status.readMsg`|Entero|
|`status.reason`|Serie|
|`status.readBytes`|Entero|
|`status.writeBytes`|Entero|

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


## Publicación de sucesos desde dispositivos
{: #publishing_device_events}

Las aplicaciones pueden publicar sucesos como si se originaran a partir de un dispositivo.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
myData={'name' : 'foo', 'cpu' : 60, 'mem' : 50}
client.publishEvent(myDeviceType, myDeviceId, "status", "json", myData)
```


## Publicación de mandatos en dispositivos
{: #publishing_commands_devices}


Las aplicaciones pueden publicar mandatos en dispositivos conectados.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

client.connect()
commandData={'rebootDelay' : 50}
client.publishCommand(myDeviceType, myDeviceId, "reboot", "json", commandData)
```


## Detalles de la organización
{: #org_details}

Las aplicaciones pueden utilizar el método `getOrganizationDetails()` para recuperar los detalles sobre la configuración de la organización.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    orgDetail = client.api.getOrganizationDetails()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

Para obtener información sobre el modelo de solicitud y de respuesta y códigos de estado HTTP, consulte la sección Configuración de la organización de la [{{site.data.keyword.iot_short_notm}} API ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window}.


## Operaciones masivas de dispositivos
{: #bulk_device_ops}

Sus aplicaciones pueden utilizar operaciones masivas para obtener, añadir o eliminar varios dispositivos simultáneamente.

Para obtener información sobre la lista de parámetros de consulta, el modelo de solicitud y respuesta y códigos de estado HTTP, consulte la sección 'Operaciones masivas' de la [{{site.data.keyword.iot_short_notm}} API ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html){: new_window}.


### Recuperación de información de dispositivo

La información de dispositivos masiva se puede recuperar mediante el método `getAllDevices()`. Este método recupera información en todos los dispositivos registrados de la organización. Cada solicitud puede contener un máximo de 512 KB.

La respuesta contiene parámetros necesarios para la aplicación. Utilice los resultados del diccionario de la respuesta para obtener la matriz de dispositivos que se devuelven. Son necesarios otros parámetros de la respuesta para realizar más llamadas, como por ejemplo, el elemento `_bookmark` se puede utilizar para pasar por las páginas de resultados. Envíe la primera solicitud sin especificar un marcador y, a continuación, tome el marcador que se devuelve en la respuesta y proporciónelo en la solicitud para la página siguiente. Repita hasta el final del conjunto de resultados, que se indica mediante la ausencia de un marcador. Cada solicitud debe utilizar los mismos valores para el resto de los parámetros, o de lo contrario los resultados no estarán definidos.


```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceList = client.api.getAllDevices()
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```
### Adición de varios dispositivos


Utilice el método `addMultipleDevices()` para añadir uno o varios dispositivos a la organización de {{site.data.keyword.iot_short_notm}}. Una solicitud no puede tener más de 512 KB. La respuesta contiene las señales de autenticación generadas para cada dispositivo. Asegúrese de que realice una copia de las señales de autenticación porque, si pierde las señales de autenticación, no se pueden recuperar.


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

### Supresión de varios dispositivos


Utilice el método `deleteMultipleDevices()` para suprimir varios dispositivos desde una organización de {{site.data.keyword.iot_short_notm}}. Una solicitud no puede tener más de 512 KB.

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


## Operaciones de tipos de dispositivos
{: #device_type_ops}

Los tipos de dispositivos que se crean en su organización se pueden utilizar para crear plantillas para añadir dispositivos. Al utilizar las características de la API de {{site.data.keyword.iot_short_notm}}, las aplicaciones pueden listar, crear, suprimir, ver o actualizar tipos de dispositivos en su organización.

Para obtener información sobre los parámetros de consulta, el modelo de solicitud y de respuesta y los códigos de estado HTTP, consulte la sección 'Tipos de dispositivos' de la documentación de la [{{site.data.keyword.iot_short_notm}} API ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


### Recuperación de todos los tipos de dispositivos

Utilice el método `getAllDeviceTypes()` para recuperar todos los tipos de dispositivos que se encuentran en la organización de {{site.data.keyword.iot_short_notm}}.
Utilice los resultados del diccionario de la respuesta para obtener la matriz de dispositivos que se devuelven. Son necesarios otros parámetros de la respuesta para realizar más llamadas, como por ejemplo, el elemento `_bookmark` se puede utilizar para pasar por las páginas de resultados. Envíe la primera solicitud sin especificar un marcador y, a continuación, tome el marcador que se devuelve en la respuesta y proporciónelo en la solicitud para la página siguiente. Repita este proceso hasta el final del conjunto de resultados, que se indica mediante la ausencia de un marcador. Cada solicitud debe utilizar los mismos valores para el resto de los parámetros, o de lo contrario los resultados no estarán definidos.

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

### Adición de un tipo de dispositivo

Utilice el método `addDeviceType()` para registrar un tipo de dispositivo en la instancia de {{site.data.keyword.iot_short_notm}}. En cada solicitud, debe definir en primer lugar los elementos device information y device metadata que desea que se apliquen a todos los dispositivos de este tipo. El elemento device information consta de varias variables, entre las que se incluyen serial number, manufacturer, model, class, description, firmware, hardware versions y descriptive location. El elemento metadata consta de variables y valores personalizados, que puede definir el usuario.


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

### Supresión de un tipo de dispositivo


Utilice el método `deleteDeviceType()` para suprimir un tipo de dispositivo de la organización de {{site.data.keyword.iot_short_notm}}.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
      success = client.api.deleteDeviceType("myDeviceType")
except IoTFCReSTException as e:
      print("ERROR [" + e.httpcode + "] " + e.message)
```

### Recuperación de información para tipos de dispositivos específicos


Utilice el método `getDeviceType()` para recuperar información para un tipo de dispositivo específico. El `typeId` del tipo de dispositivo que desea recuperar debe especificarse como un parámetro.

```python

import ibmiotf.application

  options = ibmiotf.application.ParseConfigFile(configFilePath)
  client = ibmiotf.application.Client(options)

try:
    deviceTypeInfo = client.api.getDeviceType("myDeviceType")
except IoTFCReSTException as e:
    print("ERROR [" + e.httpcode + "] " + e.message)
```

### Actualización de un tipo de dispositivo


Utilice el método `updateDeviceType()` para modificar las propiedades de un tipo de dispositivo. Al utilizar el método `updateDeviceType()`, especifique en primer lugar el `typeId` del tipo de dispositivo a actualizar y, a continuación, especifique los elementos siguientes:

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


## Operaciones de dispositivo
{: #device_ops}

Las operaciones de dispositivo que están disponibles en la API incluyen el listado, la adición, la eliminación, la visualización, la actualización, la visualización de ubicación y la visualización de información de gestión de dispositivos en una organización
de {{site.data.keyword.iot_short_notm}}.

Para obtener información sobre los parámetros de consulta, el modelo de solicitud y de respuesta y los códigos de estado HTTP, consulte la sección 'Tipos de dispositivos' de la [documentación de la API de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.


### Recuperación de dispositivos de un determinado tipo de dispositivo

Utilice el método `retrieveDevices()` para recuperar todos los dispositivos de un determinado tipo de dispositivo de una organización en una instancia de {{site.data.keyword.iot_short_notm}}, que se muestra en el ejemplo siguiente:


```python

   print("\nRetrieving All existing devices")
   print("Retrieved Devices = ", apiCli.retrieveDevices(deviceTypeId))
```

Utilice los resultados del diccionario de la respuesta para obtener la matriz de dispositivos que se devuelven. Son necesarios otros parámetros de la respuesta para realizar más llamadas, por ejemplo, el elemento *_bookmark* se puede utilizar para pasar por las páginas de resultados. Envíe la primera solicitud sin especificar un marcador y, a continuación, tome el marcador que se devuelve en la respuesta y proporciónelo en la solicitud para la página siguiente. Repita hasta el final del conjunto de resultados, que se indica mediante la ausencia de un marcador. Cada solicitud debe utilizar los mismos valores para el resto de los parámetros, o de lo contrario los resultados no estarán definidos.

Para pasar el *_bookmark* o cualquier otra condición, debe utilizarse el método sobrecargado. El método sobrecargado toma los parámetros en la forma de diccionario, tal como se muestra en el ejemplo siguiente:

```python
response = apiClient.retrieveDevices("iotsample-arduino", parameters);
```

El ejemplo de código anterior clasifica la respuesta en función del ID de dispositivo y, a continuación, utiliza el marcador para pasar por las páginas de resultados.

### Adición de un dispositivo


Para añadir un dispositivo en una organización de {{site.data.keyword.iot_short_notm}}, utilice el método `registerDevice()`. El método `registerDevice()` añade un único dispositivo a su organización de {{site.data.keyword.iot_short_notm}}. Al añadir un dispositivo, puede especificar los parámetros siguientes:

|Parámetro|Requisito|Descripción
|:---|:---|
|`deviceTypeId`|Opcional|Asigna un tipo de dispositivo al dispositivo. Si existe un conflicto entre las variables que se definen mediante el tipo de dispositivo y las variables definidas por la variable `deviceInfo`, tendrán prioridad las variables específicas del dispositivo.|
|`deviceId`|Obligatorio||
|`authToken`|Opcional|Si no se proporciona, se generará una señal de autenticación y se incluirá en la respuesta.|
|`deviceInfo`|Opcional|Contiene varias variables entre las que se incluyen serialNumber, manufacturer, model, deviceClass, description, descriptiveLocation, firmware y hardware versions.|
|`metadata`|Opcional|Pares de series de valor de campo personalizado, tal como se describe en [Código de ejemplo para añadir un tipo de dispositivo](#sample_device_type).|
|`location`|Opcional|Contiene las variables longitude, latitude, elevation, accuracy, y measuredDateTime.|

Para obtener más información sobre estos parámetros y el formato de respuesta y códigos, consulte la documentación de la API [ ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Devices/post_device_types_typeId_devices){: new_window}.

Al utilizar el método `registerDevice()`, defina el parámetro deviceID obligatorio y los parámetros opcionales que necesite para su dispositivo y, a continuación, invoque el método mediante los parámetros que ha seleccionado.

### Código de ejemplo para añadir un tipo de dispositivo
{: #sample_device_type}

Inserte el código siguiente tras el código del constructor en un archivo de script Python(.py). El ejemplo hace una demostración de un método para añadir un tipo de dispositivo definiendo los parámetros deviceId, authToken, metadata, deviceInfo, y location.

```python

deviceId = "200020002000"
authToken = "password"
metadata = {"customField1": "customValue1", "customField2": "customValue2"}
deviceInfo = {"serialNumber": "001", "manufacturer": "Blueberry", "model": "abc1", "deviceClass": "A", "descriptiveLocation" : "Bangalore", "fwVersion" : "1.0.1", "hwVersion" : "12.01"}
location = {"longitude" : "12.78", "latitude" : "45.90", "elevation" : "2000", "accuracy" : "0", "measuredDateTime" : "2015-10-28T08:45:11.662Z"}

apiCli.registerDevice(deviceTypeId, deviceId, metadata, deviceInfo, location)
```
### Supresión de un dispositivo

Utilice el método `deleteDevice()` para eliminar un dispositivo de una organización en la organización {{site.data.keyword.iot_short_notm}}. Al suprimir un dispositivo utilizando el método `deleteDevice()`, debe especificar los parámetros deviceTypeId y deviceId.

El siguiente ejemplo de código describe el formato necesario para este método:

```python
apiCli.deleteDevice(deviceTypeId, deviceId)
```

### Obtención de un dispositivo

Utilice el método `getDevice()` para recuperar un dispositivo de una organización en el {{site.data.keyword.iot_short_notm}}. Al recuperar los detalles del dispositivo utilizando el método `getDevice()`, debe especificar los parámetros deviceTypeId y deviceId

El ejemplo de código siguiente proporciona un esquema del formato necesario para este método.

```python
apiCli.getDevice(deviceTypeId, deviceId)
```

### Recuperación de todos los dispositivos

Utilice el método `getAllDevices()` para recuperar todos los dispositivos de una organización en el {{site.data.keyword.iot_short_notm}}.

```python
apiCli.getAllDevices({'typeId' : deviceTypeId})
```

### Actualización de un dispositivo

Para modificar una o más propiedades de un dispositivo, utilice el método `updateDevice()`.

Puede actualizar cualquier propiedad de los parámetros deviceInfo o metadata. Para actualizar una propiedad de dispositivo, defina el parámetro deviceInfo antes de invocar el método `updateDevice()`. El parámetro status debe contener `alert`: True. La propiedad alert controla si un dispositivo muestra códigos de error en la interfaz de usuario de {{site.data.keyword.iot_short_notm}} y debe establecerse de forma predeterminada en `enabled`: True, tal como se describe en el siguiente ejemplo de código:

```python
status = { "alert": { "enabled": True }  }
apiCli.updateDevice(deviceTypeId, deviceId, metadata2, deviceInfo, status)
```

### Código de ejemplo para actualizar propiedades de deviceInfo

El ejemplo de código siguiente identifica un dispositivo específico y, a continuación, actualiza varias propiedades del parámetro deviceInfo.

```python
status = { "alert": { "enabled": True } }
deviceInfo = {descriptiveLocation: "London", hwVersion: "2.0.1", fwVersion: "2.5.1"}
apiCli.updateDevice("MyDeviceType", "200020002000", deviceInfo, status)
```

### Recuperación de la información de ubicación


Utilice el método `getDeviceLocation()` para recuperar la información de ubicación de un dispositivo. Los parámetros que son necesarios para recuperar los datos de ubicación son deviceTypeId y deviceId.

```python
apiClient.getDeviceLocation("iotsample-arduino", "arduino01")
```  

La respuesta a este método contiene las propiedades longitude, latitude, elevation, accuracy, measuredTimeStamp y updatedTimeStamp.

### Actualización de información de ubicación


Utilice el método `updateDeviceLocation()` para modificar la información de ubicación para un dispositivo. Como con la actualización de las propiedades del dispositivo, el parámetro deviceLocation debe estar definido con los cambios que desea aplicar. El ejemplo de código siguiente muestra cómo cambiar los datos de ubicación para un dispositivo específico:

```python
deviceLocation = { "longitude": 0, "latitude": 0, "elevation": 0, "accuracy": 0, "measuredDateTime": "2015-10-28T08:45:11.673Z"}
apiCli.updateDeviceLocation(deviceTypeId, deviceId, deviceLocation)
```

Si no se proporciona una fecha, se utilizará la fecha y hora actuales.


### Obtener información de gestión


Utilice el método `getDeviceManagementInformation()` para obtener la información de gestión de dispositivos para un dispositivo. La respuesta contiene la fecha y hora de la última actividad, el estado inactivo del dispositivo (True/False), el soporte para acciones de dispositivos y de firmware, y datos de firmware. Para obtener una lista completa del contenido de la respuesta, consulte la documentación de la API relevante.

El ejemplo de código siguiente devuelve la información de gestión de dispositivos para un dispositivo con un deviceId que se establece en "00aabbccde03" y un deviceTypeId que se establece en "iotsample-arduino":

```
apiCli.getDeviceManagementInformation("iotsample-arduino", "00aabbccde03")
```

## Operaciones de diagnóstico de dispositivos
{: #device_diag_ops}

Utilice las operaciones de diagnóstico de dispositivos para implementar las siguientes tareas de resolución de problemas y de gestión de registro:
- Borrado de registros
- Recuperación de todos o de registros específicos para un dispositivo
- Adición de información de registro
- Supresión de registros
- Borrador de códigos de error
- Recuperación de códigos de error de dispositivos
- Adición de códigos de error

Para obtener más información sobre los modelos de consulta y de respuesta, los códigos de respuesta y los parámetros de consulta, consulte la [documentación de la API de {{site.data.keyword.iot_short_notm}} ![Icono de enlace externo](../../../../icons/launch-glyph.svg "Icono de enlace externo")](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html){: new_window}.

### Obtener los registros de diagnóstico


Utilice el método `getAllDiagnosticLogs()` para recuperar todos los registros de diagnóstico para un dispositivo específico. El método `getAllDiagnosticLogs()` requiere los parámetros deviceTypeId y deviceId.

```python
apiCli.getAllDiagnosticLogs(deviceTypeId, deviceId)
```

El modelo de respuesta para este método contiene las propiedades log ID, message, severity, data y time stamp.

### Borrado de los registros de diagnóstico para un dispositivo


Utilice el método `clearAllDiagnosticLogs()` para suprimir todos los registros de diagnóstico para un dispositivo específico. Los parámetros necesarios son deviceTypeId y deviceId. Tenga cuidado al suprimir los archivos de registro, porque no se pueden recuperar una vez que se han suprimido.

```python
apiCli.clearAllDiagnosticLogs(deviceTypeId, deviceId)
```

### Adición de un registro de diagnóstico


Utilice el método `addDiagnosticLog()` para añadir una entrada al registro de diagnóstico del dispositivo. El registro se puede podar al añadir la nueva entrada. Si no se proporciona ninguna fecha, se añadirán a la entrada la fecha y hora actuales. Para utilizar este método, tiene que definir un parámetro 'logs' con las siguientes variables:


|Variable|Requisito|Descripción|
|:---|:---|:---|
|`message`|Obligatorio|Contiene el mensaje de diagnóstico que desea añadir|
|`severity`|Opcional|Se corresponde con la gravedad del registro de diagnóstico y se puede establecer en 0, 1, o 2, que se corresponde con las categorías información, aviso y error|
|`data`|Opcional|Contiene datos de diagnóstico|
|`timestamp`|Opcional|Contiene la fecha y hora de la entrada de registro en formato ISO8601 pero, si no se especifica, se utilizará la fecha y hora actuales|


El resto de los parámetros necesarios en el método son los valores deviceTypeId y deviceId para el dispositivo.

El siguiente ejemplo de código contiene un ejemplo del método `addDiagnosticLog()`:

```python
logs = { "message": "MessageContent", "severity": 0, "data": "LogData"}
apiCli.addDiagnosticLog(deviceTypeId, deviceId, logs)
```

### Recuperación de un registro de diagnóstico específico


Utilice el método `getDiagnosticLog()` para recuperar un registro de diagnóstico específico para un dispositivo determinado basado en el ID de registro. Los parámetros necesarios para este método son deviceTypeId, deviceId y logId.

```python
apiCli.getDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Supresión de un registro de diagnóstico


Utilice el método `deleteDiagnosticLog()` para suprimir un registro de diagnóstico específico. Para especificar un registro de diagnóstico, se deben facilitar los parámetros deviceTypeId, deviceId y logID.

```python
apiCli.deleteDiagnosticLog(deviceTypeId, deviceId, logId)
```

### Recuperación de códigos de error de dispositivos


Utilice el método `getAllDiagnosticErrorCodes()` para recuperar todos los códigos de error de diagnóstico asociados con un dispositivo específico.

```python
apiCli.getAllDiagnosticErrorCodes(deviceTypeId, deviceId)
```

### Borrar códigos de error de diagnóstico


Utilice el método `clearAllErrorCodes()` para borrar la lista de códigos de error asociados con el dispositivo. La lista se sustituye por un código de error individual igual a cero.

```python
apiCli.clearAllErrorCodes(deviceTypeId, deviceId)
```

### Adición de un único código de error de diagnóstico


Utilice el método `addErrorCode()` para añadir un código de error a la lista de códigos de error asociados con el dispositivo. La lista se puede podar cuando se añada la nueva entrada. Los parámetros necesarios en el método son deviceTypeId, deviceId y errorCode. El parámetro errorCode contiene las siguientes variables:

- errorCode: esta variable es obligatoria y debe establecerse como un entero. Esta variable establece el número del código de error que se ha creado.
- timestamp: esta variable es opcional y contiene la fecha y la hora de la entrada de registro en formato ISO8601. Si esta variable no se incluye, se añade automáticamente con la fecha y hora actuales.

```python
errorCode = { "errorCode": 1234, "timestamp": "2015-10-29T05:43:57.112Z" }
apiCli.addErrorCode(deviceTypeId, deviceId, errorCode)
```

## Determinación de problemas de conexión
{: #connection_problem_determination}

Utilice el método `getDeviceConnectionLogs()` para listar sucesos de registro de conexión para un dispositivo. Los sucesos de registro de conexión se pueden utilizar para ayudar a diagnosticar problemas de conectividad entre el dispositivo y el servicio de {{site.data.keyword.iot_short_notm}}. Las entradas registran sucesos de conexión satisfactoria, intentos de conexión no satisfactoria, desconexión intencional y desconexión iniciada por el servidor.

```
apiCli.getDeviceConnectionLogs(deviceTypeId, deviceId)
```

La respuesta incluye una lista de entradas de registro, que contiene mensajes de registro e indicaciones de fecha y hora.
