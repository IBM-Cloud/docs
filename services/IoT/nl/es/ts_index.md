---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Resolución de problemas de {{site.data.keyword.iot_short_notm}}
{: #ts}

A continuación se muestran las respuestas a preguntas de resolución de problemas comunes sobre cómo utilizar {{site.data.keyword.iot_full}} en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema al acceder a la organización de {{site.data.keyword.iot_short_notm}}
{: #access-expiry-problem}

No puede iniciar una sesión en una organización de {{site.data.keyword.iot_short_notm}} de la que es propietario.
{:shortdesc}

No puede iniciar una sesión en su organización de {{site.data.keyword.iot_short_notm}} directamente mediante el URL o mediante `https://internetofthings.ibmcloud.com`.
{: tsSymptoms}

Es posible que su acceso a la organización de {{site.data.keyword.iot_short_notm}} haya caducado. Las organizaciones de {{site.data.keyword.iot_short_notm}} creadas mediante {{site.data.keyword.Bluemix}} utilizan de forma predeterminada perfiles de usuario temporales.
{: tsCauses}

Puede solucionar este problema accediendo a su organización de {{site.data.keyword.iot_short_notm}} mediante {{site.data.keyword.Bluemix_notm}} y modificando el valor de caducidad de su perfil de usuario. Para cambiar los valores de caducidad de usuario:

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, abra el servicio {{site.data.keyword.iot_short_notm}}.
2. Pulse **Miembros** en la barra de navegación.
3. Pulse el icono **Editar**.
4. Desmarque el recuadro **El acceso caduca** y pulse **Guardar**.
{: tsResolve}

## Problema de conexión al {{site.data.keyword.iot_short_notm}}
{: #connection_problem}

Su conexión al {{site.data.keyword.iot_short_notm}} se descarta o se desconecta de forma inesperada.
{:shortdesc}

Cuando intente conectarse al {{site.data.keyword.iot_short_notm}}, su dispositivo o aplicación recibirá un error.
{: tsSymptoms}

Es posible que tenga dos dispositivos que intenten conectarse con el mismo clientID y credenciales. Sólo se permite una conexión por clientID. No puede tener dos conexiones simultáneas utilizando el mismo ID. Las aplicaciones pueden compartir la misma clave de API, pero MQTT requiere que el ID de cliente sea siempre exclusivo.
{: tsCauses}

Puede resolver este problema confirmando que no tiene dos dispositivos intentando conectarse mediante las mismas credenciales.
{: tsResolve}

## El dispositivo se desconecta de forma intermitente de {{site.data.keyword.iot_short_notm}}
{: #disconnection_problem}

La conexión del dispositivo al {{site.data.keyword.iot_short_notm}} se descarta intermitentemente de forma inesperada.
{:shortdesc}

Un dispositivo que está conectado al servicio de {{site.data.keyword.iot_short_notm}} está desconectado de forma intermitente. El dispositivo vuelve a conectarse, pero se desconecta de forma inesperada de nuevo después de unos minutos.
{: tsSymptoms}

Es posible que cuando se conecte esté utilizando un valor para una opción de ping de MQTT que es demasiado bajo, lo que hace que tenga el aspecto de que la conexión ha excedido el tiempo de espera. Por ejemplo, si el MQTT del cliente se ha establecido de forma incorrecta, no se reciben los pings de forma puntual, y se cierra la conexión.
{: tsCauses}

Puede solucionar este problema confirmando que ha establecido correctamente los parámetros ping y KeepAlive para la conexión.   
{: tsResolve}


## Obtención de ayuda y soporte para {{site.data.keyword.iot_short_notm}}
{: #gettinghelp}

Si tiene problemas o preguntas al utilizar {{site.data.keyword.iot_short_notm}}, puede obtener ayuda buscando información o planteando preguntas a través de un foro. También puede abrir una incidencia de soporte.

Al utilizar los foros para formular una pregunta, etiquete la pregunta para que la vean los equipos de desarrollo de {{site.data.keyword.Bluemix_notm}}.

* Si tiene preguntas técnicas sobre el desarrollo o el despliegue de una app con {{site.data.keyword.iot_short_notm}}, publique su pregunta en [Stack Overflow ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://stackoverflow.com/search?q=watson-iot+ibm-bluemix){:new_window} y etiquete la pregunta con "ibm-bluemix" y "watson-iot".
<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
* Para formular preguntas sobre las instrucciones del servicio y cómo empezar, utilice el foro [dW Answers de IBM developerWorks ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://developer.ibm.com/answers/topics/watson-iot/?smartspace=bluemix){:new_window}. Incluya las etiquetas "watson-iot" y "bluemix".

Consulte [Obtención de ayuda](https://www.{DomainName}/docs/support/index.html#getting-help) para obtener más detalles sobre cómo utilizar los foros.

Para obtener información sobre la apertura de una incidencia de soporte de IBM, o sobre los niveles de soporte y la gravedad de las incidencias, [Cómo ponerse en contacto con el soporte ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.{DomainName}/docs/support/index.html#contacting-support).
