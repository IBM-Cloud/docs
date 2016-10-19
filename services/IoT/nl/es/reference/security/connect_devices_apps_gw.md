---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Conexiones de aplicaciones, dispositivos y pasarelas a {{site.data.keyword.iot_short_notm}}
{: #connect_devices_apps_gw}
Última actualización: 08 de septiembre de 2016
{: .last-updated}

Las aplicaciones, los dispositivos y las pasarelas se pueden conectar a {{site.data.keyword.iot_full}} mediante el protocolo de MQTT. Los dispositivos también pueden conectarse y publicar sucesos en {{site.data.keyword.iot_short_notm}} a través de la API de HTTP.
{: shortdesc}


## URL de conexiones de clientes
{: #client_connect_url}

Para conectar clientes de dispositivos, aplicaciones y pasarelas a la instancia de {{site.data.keyword.iot_short_notm}}, utilice los siguientes URL de conexión:

### Dirección de mensajería

<pre class="pre"><var class="keyword varname">orgId</var>.messaging.internetofthings.ibmcloud.com</pre>
{: codeblock}

### URL de conexión de la API REST de HTTP

<pre class="pre">https://<var class="keyword varname">orgId</var>.internetofthings.ibmcloud.com/api/v0002/device/types/<var class="keyword varname">typeId</var>/devices/<var class="keyword varname">deviceId</var>/events/<var class="keyword varname">eventId</var></pre>
{: codeblock}

**Notas**
- *orgId* es el único ID de organización generado al registrar la instancia de servicio.
- Si está conectando un dispositivo o aplicación al servicio de Inicio rápido, especifique 'quickstart' como valor de *orgId*.

## Seguridad de puerto
{: #client_port_security}

Asegúrese de que los puertos requeridos estén abiertos y habilitados para la comunicación.

|Tipo de conexión |Número de puerto|
|:---|:---|
|No seguro|1883|
|Seguro|8883|
|Seguro|443|

Los clientes de MQTT se conectan utilizando las credenciales adecuadas, como por ejemplo las señales de autenticación de dispositivo para dispositivos y claves y señales de API para aplicaciones. Dado que la mensajería de MQTT al puerto no seguro 1883 envía estas credenciales en texto sin formato, utilice siempre las alternativas seguras 8883 o 443 en su lugar. Los puertos seguros fuerzan el cifrado de las credenciales de TLS. Tenga en cuenta que debe habilitar TLS en la aplicación mediante el método tls_set() en la biblioteca de MQTT de Python. De lo contrario, los datos se pueden enviar de forma no segura.

Cuando se utiliza la mensajería de MQTT segura en los puertos 8883 o 443, las bibliotecas de clientes más recientes confían automáticamente en el certificado presentado por {{site.data.keyword.iot_short_notm}}. Si este no es el caso para el entorno del cliente, puede descargar y utilizar la cadena de certificados completa desde [messaging.pem](https://github.com/ibm-messaging/iot-python/blob/master/src/ibmiotf/messaging.pem).


## Requisitos de TLS
{: #tls_requirements}
Algunas bibliotecas de cliente de Transport Layer Security (TLS) no dan soporte a dominios que incluyan un comodín. Si no puede cambiar satisfactoriamente las bibliotecas, inhabilite la comprobación de certificados.

{{site.data.keyword.iot_short_notm}} requiere TLS V1.2 y las siguientes suites de cifrado:
- ECDHE-RSA-AES256-GCM-SHA384
- AES256-GCM-SHA384
- ECDHE-RSA-AES128-GCM-SHA256
- AES128-GCM-SHA256

## Autenticación de cliente de MQTT
{: #mqtt_authentication}

**Importante:** Cada cliente de MQTT requiere un ID de cliente exclusivo. Si intenta conectar un cliente a la organización utilizando un ID de cliente que ya esté conectado, se desconectará la primera conexión.

Los dispositivos y pasarelas que están conectados directamente al {{site.data.keyword.iot_short_notm}} muestran un icono de estado en el panel de instrumentos para indicar que están conectados. Los dispositivos que están conectados de forma indirecta a través de una pasarela se muestran como desconectados porque el panel de instrumentos no sabe qué dispositivos están conectados a través de una pasarela.

### Identificadores de cliente de MQTT

Para que se autentiquen correctamente los dispositivos, aplicaciones y pasarelas, defina cada cliente de MQTT utilizando los siguientes identificadores de clientes y formato:

|Tipo de cliente |ID|Formato de ID de MQTT|
|:---|:---|:---|
|Aplicaciones|a|<pre class="pre">a:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Aplicaciones escalables|A|<pre class="pre">A:<var class="keyword varname">orgId</var>:<var class="keyword varname">appId</var></pre>
|Dispositivos|d|<pre class="pre">d:<var class="keyword varname">orgId</var>:<var class="keyword varname">deviceType</var>:<var class="keyword varname">deviceId</var></pre>|
|Pasarelas|g|<pre class="pre">g:<var class="keyword varname">orgId</var>:<var class="keyword varname">typeId</var>:<var class="keyword varname">deviceId</var></pre>|

Donde
- *orgId* es el ID de organización de seis caracteres exclusivo que se ha generado cuando se ha registrado el servicio.
- *appId* es un identificador de serie exclusivo definido por el usuario para el cliente. 
- *deviceId* identifica de forma exclusiva un dispositivo o pasarela en todos los tipos y es similar a un número de serie.
- *device_type* es el identificador para el tipo de dispositivo que se está conectando y es similar a un número de modelo.
- *typeId* es un identificador del tipo de pasarela que se está conectando y es similar a un número de modelo.

Los valores *appId*, *type_id*, *device_type* y *device_id* no deben tener más de 36 caracteres y sólo pueden contener:
- Caracteres alfanuméricos (a-z, A-Z, 0-9)
- Guiones ( - )
- Guiones bajos ( _ )
- Puntos ( . )

**Notas:**
- Cuando se conecta al servicio de Inicio rápido, no se necesita autenticación.
- No es necesario registrar una aplicación antes de establecer la conexión.


### Conexión de aplicaciones utilizando MQTT

Las aplicaciones de {{site.data.keyword.iot_short_notm}} requieren una clave de API para conectarse a una organización. Cuando se registra una clave de API, se genera una señal, que se debe utilizar con dicha clave de API.

El código siguiente proporciona un ejemplo de una clave de API:

<pre class="pre">a-<var class="keyword varname">orgId</var>-a84ps90Ajs</pre>
{: codeblock}

El ejemplo siguiente muestra una señal de autenticación típica:

```
 MP$08VKz!8rXwnR-Q*
```

Cuando se realiza una conexión de MQTT utilizando una clave de API, asegúrese de que cumple los siguientes requisitos:

- El ID de cliente de MQTT está en el siguiente formato: a:*orgId*:*appId*
- El nombre de usuario de MQTT es la clave de la API, por ejemplo, a-*orgId*-a84ps90Ajs
- La contraseña de MQTT es la señal de autenticación, por ejemplo, *MP$08VKz!8rXwnR-Q*

Para obtener más información, consulte [Conectividad de MQTT para las aplicaciones](../../applications/mqtt.html).

### Autenticación de dispositivo

#### Nombres de usuario
El servicio de {{site.data.keyword.iot_short_notm}} sólo da soporte a la autenticación basada en señales para dispositivos; por lo tanto, cada dispositivo sólo tiene un nombre de usuario válido.
Un valor de `use-token-auth` indica al servicio que la señal de autenticación para la pasarela o el dispositivo se utiliza como la contraseña para la conexión de MQTT.

Para obtener más información, consulte [Conectividad de MQTT para dispositivos](../../devices/mqtt.html)

#### Contraseñas
Si el cliente está utilizando la autenticación basada en señales, envíe la señal de autenticación de dispositivo como la contraseña para todas las conexiones de MQTT.
