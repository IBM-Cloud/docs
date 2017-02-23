---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-08-02"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Embedded C para desarrolladores de dispositivos
{: #embedded_c}

Puede utilizar Embedded C para crear y personalizar dispositivos que interactúan con su organización en {{site.data.keyword.iot_full}}. Utilice la información y los ejemplos que se proporcionan para empezar a desarrollar los dispositivos utilizando Embedded C.
{:shortdesc}

## Descarga del cliente y los recursos de Embedded C
{: #embeddedc_client_download}

Para acceder a las bibliotecas de clientes de Embedded C y a ejemplos para {{site.data.keyword.iot_short_notm}}, vaya al repositorio [iotf-embeddedc](https://github.com/ibm-messaging/iotf-embeddedc) en GitHub y complete las instrucciones de instalación.


## Dependencias
{: #dependencies}

|Dependencia |Descripción|
|:---|:---|
|[Biblioteca de Eclipse Paho Embedded C](http://git.eclipse.org/c/paho/org.eclipse.paho.mqtt.embedded-c.git) |Proporciona una biblioteca de cliente de MQTT C. Para obtener más información, consulte [Paquete de cliente de MQTT: C para dispositivos incorporados](http://www.eclipse.org/paho/clients/c/embedded/).|


## Instalación
{: #installation}

Para instalar la biblioteca de cliente de {{site.data.keyword.iot_short_notm}} para Embedded C, complete las instrucciones siguientes:

1. Para instalar la versión más reciente de la biblioteca, escriba el código siguiente en la línea de mandatos:
```
  [root@localhost ~]# git clone https://github.com/ibm-messaging/iotf-embeddedc.git
```
2. Copiar el archivo .tar de la biblioteca de Paho en el directorio *lib*.
```
    cd iotf-embeddedc
    cp ~/org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz lib/
```
3. Extraer el archivo de biblioteca
```  cd lib
    tar xvzf org.eclipse.paho.mqtt.embedded-c-1.0.0.tar.gz
```
El cliente descargado tiene la siguiente estructura de archivos:

```
 |-lib: contiene todos los archivos dependientes
 |-samples: contiene los ejemplos helloWorld y sampleDevice
   |-sampleDevice.c: implementación de dispositivos de ejemplo
   |-helloworld.c: aplicación de inicio rápido
   |-README.md
   |-Makefile
   |-build.sh
 |-iotfclient.c: Archivo del cliente principal
 |-iotfclient.h: Archivo de cabecera para el cliente
```

## Inicialización de la biblioteca de clientes
{: #initialize_client_library}

Una vez que se descargue la biblioteca del cliente, debe inicializarse y conectarse a la {{site.data.keyword.iot_short_notm}}. Puede inicializar la biblioteca de cliente de {{site.data.keyword.iot_short_notm}} para Embedded C pasando parámetros o utilizando un archivo de configuración.

### Cómo pasar parámetros

La función `initialize` utiliza los siguientes parámetros para conectar con el servicio de {{site.data.keyword.iot_short_notm}}:

|Definición |Descripción |
|:---|:---|
|`client`|Puntero al *iotfclient*.|
|`org`|El ID de la organización.|
|`type` |El tipo del dispositivo.|
|`id` |El ID de dispositivo.|
|`auth-method` |El método de autenticación que debe utilizarse. El único valor al que se da soporte actualmente es `token`.|
|`auth-token`|Una señal de autenticación para conectar de forma segura el dispositivo a Watson IoT Platform.|


```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	//quickstart
	rc = initialize(&client,"quickstart","iotsample","001122334455",NULL,NULL);
	//registered
	rc = initialize(&client,"org","type","id","auth-method","auth-token");
	....
```

### Utilización de un archivo de configuración

También puede utilizar un archivo de configuración para inicializar la biblioteca de cliente Embedded C. La función `initialize_configfile` toma la vía de acceso del archivo de configuración como un parámetro.

```
	#include "iotfclient.h"
	....
	....
	char *filePath = "./device.cfg";
	Iotfclient client;
	rc = initialize_configfile(&client, filePath);
	....
```

El archivo de configuración debe utilizar el formato siguiente:

```
	org=$orgId
	type=$myDeviceType
	id=$myDeviceId
	auth-method=token
	auth-token=$token
```

## Conexión al servicio
{: #connecting_service}

Después de inicializar la biblioteca de cliente de Embedded C de {{site.data.keyword.iot_short_notm}}, puede conectarse al {{site.data.keyword.iot_short_notm}} llamando a la función `connectiotf`.

```
	#include "iotfclient.h"
	....
	....
	Iotfclient client;
	char *configFilePath = "./device.cfg";

	rc = initialize_configfile(&client, configFilePath);

	if(rc != SUCCESS){
		printf("initialize failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}

	rc = connectiotf(&client);

	if(rc != SUCCESS){
		printf("Connection failed and returned rc = %d.\n Quitting..", rc);
		return 0;
	}
	....
```

## Manejo de mandatos
{: #handling_commands}

Cuando el cliente de dispositivo se conecta, se suscribe automáticamente a cualquier mandato para este dispositivo. Para procesar mandatos específicos, necesita registrar una función de devolución de llamada de mandatos llamando a la función `setCommandHandler`. La función de devolución de llamada tiene las siguientes propiedades:

|Propiedad |Descripción|
|:---|:---|
|`commandName`  |El nombre del mandato que se ha invocado. |  
|`format`  |El formato del suceso. El formato puede ser una serie, como por ejemplo JSON.|
|`payload`  |Los datos para la carga útil de mandatos. La longitud máxima es 131072 bytes. |


```
	#include "iotfclient.h"

	void myCallback (char* commandName, char* format, void* payload)
	{
	printf("The command received :: %s\n", commandName);
	printf("format : %s\n", format);
	printf("Payload is : %s\n", (char *)payload);
	}
	...
	...
	char *filePath = "./device.cfg";
	rc = connectiotfConfig(filePath);
	setCommandHandler(myCallback);

	yield(1000);
	....

```
**Nota:** La función `yield()` permite al dispositivo recibir mandatos desde la Watson IoT Platform y mantiene la conexión activa. Si la función `yield()` no se invoca dentro del intervalo de tiempo especificado por el intervalo de keepAlive, el dispositivo no recibirá ningún mandato enviado desde la plataforma. El valor que se asigna a la función `yield()` especifica la longitud de tiempo (en milisegundos) que se pueden leer los datos desde el socket antes de que se devuelva el control a la aplicación.

## Publicación de sucesos
{: #publishing_events}

Los sucesos se pueden publicar con las siguientes propiedades:

|Propiedad |Descripción|
|:---|:---|
|eventType  |El tipo de suceso que se publica, por ejemplo status o gps. |  
|eventFormat  |El formato puede ser cualquier cadena, por ejemplo `json`. |
|data  |Los datos para la carga útil. La longitud máxima es 131072 bytes. |
|QoS  |El nivel de Calidad de servicio para el suceso publicado. Los valores soportados son `0`, `1`, `2`.|


```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", "{\"d\" : {\"temp\" : 34 }}", QOS0);
	....
```

## Desconexión del cliente
{: #disconnect_client}

Para desconectar el cliente y lanzar las conexiones, ejecute el siguiente fragmento de código:

```
	#include "iotfclient.h"
	....
	rc = connectiotf (org, type, id , authmethod, authtoken);
	char *payload = {\"d\" : {\"temp\" : 34 }};

	rc= publishEvent("status","json", payload , QOS0);
	...
	rc = disconnect();
	....
```

## Ejemplos
{: #samples}

El dispositivo de ejemplo y el código de aplicaciones se proporcionan en [GitHub](https://github.com/ibm-messaging/iotf-embeddedc/tree/master/samples).
