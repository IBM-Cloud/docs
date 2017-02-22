---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Acerca de {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Última actualización: 18 de enero de 2017
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} es un servicio que puede utilizar para enviar notificaciones a dispositivos y plataformas. Las notificaciones se pueden destinar a todos los usuarios de la aplicación o a un conjunto específico de usuarios y dispositivos mediante etiquetas. Puede administrar dispositivos, etiquetas y suscripciones.   

Puede utilizar cualquiera de las siguientes opciones para crear un servicio enlazado o sin enlazar: 

- Creando una aplicación Bluemix mediante el contenedor modelo del iniciador de servicios MobileFirst desde el catálogo. Se creará un servicio de notificaciones Push enlazado a una aplicación de fondo de Bluemix. 
- Creando un servicio de notificaciones Push sin enlazar directamente desde el catálogo de Mobile. Luego puede enlazar una aplicación o incluso utilizarlo sin enlazar.  
- Utilizando el [panel de control de Mobile ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://console.ng.bluemix.net/docs/mobile/services.html "icono de enlace externo"){: new_window}.

Tenga en cuenta que el separador de supervisión de {{site.data.keyword.mobilepushshort}} no muestra los datos analíticos.

El servicio {{site.data.keyword.mobilepushshort}} ahora está habilitado para OpenWhisk. Para obtener más información, consulte [OpenWhisk](/docs/openwhisk/index.html).


## Proceso del servicio {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

Los clientes de navegadores web y móviles y las aplicaciones y extensiones de Google Chrome pueden suscribirse y registrarse para el servicio de {{site.data.keyword.mobilepushshort}}. Al arrancar, las aplicaciones móviles y de navegador se registrarán y se suscribirán al servicio {{site.data.keyword.mobilepushshort}}. Las notificaciones se asignan al servicio de APN (Apple Push Notification Service) o al servidor de Firebase Cloud Messaging (FCM)/Google Cloud Messaging (GCM) y, a continuación, se enviarán a los clientes móviles y de navegador registrados.

![Visión general de push](images/overview.jpg)


###Aplicaciones móviles y de navegador
{: mobile-applications}

Al arrancar, las aplicaciones cliente se registrarán y se suscribirán al servicio {{site.data.keyword.mobilepushshort}} para recibir notificaciones.

###Aplicaciones de fondo
{: backend-applications}

Las aplicaciones de fondo pueden ser locales o pueden estar en una nube pública. Las aplicaciones de fondo utilizarán el servicio {{site.data.keyword.mobilepushshort}} para enviar notificaciones según el contexto a usuarios de aplicaciones móviles y de navegador. No es necesario que las aplicaciones de fondo mantengan ni gestionen dispositivos móviles, agentes de navegador ni información de usuarios para enviar notificaciones push. En lugar de ello, pueden utilizar el servicio {{site.data.keyword.mobilepushshort}}, que los gestionará y mantendrá.

###Propietario de back-end de app
{: app-backend-owner}

El propietario de back-end de app crea la aplicación móvil de fondo, que agrupa una instancia del servicio {{site.data.keyword.mobilepushshort}}. El propietario también configura el servicio {{site.data.keyword.mobilepushshort}} para adaptar las aplicaciones de fondo utilizando el servicio junto con las aplicaciones móviles y de navegador destinadas para {{site.data.keyword.mobilepushshort}}.

###Servicio {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

El servicio {{site.data.keyword.mobilepushshort}} gestiona toda la información relacionada con los dispositivos móviles y clientes de navegadores web registrados para las notificaciones. El servicio mantiene sus aplicaciones transparentes a los detalles tecnológicos del envío de notificaciones a plataformas móviles y navegadores web heterogéneas y lo maneja todo.

###Pasarelas
{: gateways}

Los servicios de nube específicos de plataformas para las notificaciones push, como FCM/GCM o Apple Push Notification Service (APN), que utilizan el servicio IBM {{site.data.keyword.mobilepushshort}} para asignar notificaciones a las aplicaciones móviles y de navegador.

###Seguridad push
{: push-security}

Las API de {{site.data.keyword.mobilepushshort}} se protegen mediante dos tipos de secretos: 

- **appSecret**: 'appSecret' protege las API que suelen invocar las aplicaciones de fondo, como por ejemplo la API para enviar {{site.data.keyword.mobilepushshort}} y la API para configurar las opciones.   
- **clientSecret**:  'clientSecret' protege las API que suelen invocar las aplicaciones de clientes móviles. Sólo hay una API relacionada con el registro de un dispositivo con un ID de usuario asociado que requiere este 'clientSecret'. Ninguna del resto de las API invocadas desde los clientes móviles requiere el clientSecret.  

'appSecret' y 'clientSecret' se asignan a todas las instancias de servicio en el momento de enlazar una aplicación con el servicio {{site.data.keyword.mobilepushshort}}. Consulte la documentación de las [API REST ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://mobile.{DomainName}/imfpush/ "icono de enlace externo") para obtener información sobre cómo se pasan los secretos y a qué API. 

**Nota**: Las aplicaciones anteriores requerían que se pasara clientSecret solo al registrar o actualizar dispositivos con el campo userID. Todas las otras API invocadas con clientes móviles y de navegador no necesitaban clientSecret. Estas aplicaciones antiguas pueden seguir utilizando el clientSecret de forma opcional para los registros de dispositivos o las llamadas de actualización. Sin embargo, se recomienda encarecidamente realizar la comprobación de clientSecret en todas las llamadas de API de cliente. Para imponer esto en las aplicaciones existentes, se ha publicado una nueva API 'verifyClientSecret'.  En las aplicaciones nuevas, la comprobación de clientSecret se efectuará en todas las llamadas de API de cliente. Este comportamiento no puede modificarse con la API 'verfiyClientSecret'.

De forma predeterminada, la verificación del secreto de cliente se impone sólo en las nuevas aplicaciones. Está permitido que tanto las aplicaciones existentes como las nuevas habiliten o inhabiliten la verificación del secreto de cliente mediante la API REST verifyClientSecret. Se recomienda que imponga la verificación del secreto de cliente para evitar exponer los dispositivos a los usuarios que puedan conocer el applicationId y el deviceId.

Asegúrese de que el 'clientSecret' no se muestre nunca ni lo codifique en la aplicación. Hay varios patrones de inicialización de aplicaciones que se pueden utilizar para obtener dinámicamente el 'clientSecret' durante el tiempo de ejecución de la aplicación. El diagrama de secuencia sigue el posible patrón.
![Enable_Push](images/init_client_secret.jpg) 

## Tipos de {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

###Difusión
{: broadcast}

Cuando una aplicación cliente se registra en el servicio {{site.data.keyword.mobilepushshort}}, puede comenzar a recibir difusiones. Las notificaciones de difusión son mensajes destinados a todas las instancias de una aplicación instalada en dispositivos móviles, navegadores o implementadas como instancias de aplicaciones o extensiones de Chrome y configuradas para el servicio {{site.data.keyword.mobilepushshort}}. Las notificaciones de difusión están habilitadas de forma predeterminada para cualquier aplicación habilitada para {{site.data.keyword.mobilepushshort}}. Las aplicaciones habilitadas para el servicio {{site.data.keyword.mobilepushshort}} tienen una suscripción predefinida en la etiqueta Push.ALL, que utiliza el servidor para transmitir mensajes de notificación a todos los dispositivos. Para enviar una notificación de difusión que utiliza la API Push REST, asegúrese de que el "destino" sea un archivo JSON vacío al publicar en recursos de mensajes.

###Notificaciones basadas en etiquetas
{: tag-based-notifications}

Las notificaciones basadas en etiquetas son mensajes que están pensados para todos los dispositivos suscritos a una etiqueta determinada. Las notificaciones basadas en código permiten la segmentación de notificaciones en función de los temas o de las áreas de temas. Los destinatarios de la notificación pueden elegir recibir notificaciones sólo si es sobre un asunto o tema de su interés. Por lo tanto, la notificación basada en etiquetas proporciona un medio de segmentar destinatarios. Esta característica habilita la función de definir etiquetas y, a continuación, enviar y recibir mensajes por etiquetas. Un mensaje sólo se ha dirigido a las instancias de aplicación cliente (en móvil, navegador o como una aplicación o extensión) que están suscritas a la etiqueta. Primero debe crear las etiquetas para la aplicación, configurar las suscripciones de etiquetas y, a continuación, iniciar las notificaciones basadas en etiquetas. Para enviar una notificación basada en etiquetas que utiliza la API REST, asegúrese de que los "tagNames" se proporcionen al publicarse en el recurso de mensajes.

###Notificaciones de difusión única
{: unicast-notifications}

Las notificaciones de difusión única son mensajes destinados a un dispositivo o usuario específico. Dichas notificaciones destinadas a dispositivos no necesitan ninguna configuración adicional y están habilitadas de forma predeterminada cuando se habilita la aplicación para {{site.data.keyword.mobilepushshort}}.

Sin embargo, las notificaciones de difusión única destinadas a usuarios necesitan que se asocie un ID de usuario a un dispositivo en el momento de registrar el dispositivo móvil cliente o el navegador web o las aplicaciones y extensiones de Chrome a {{site.data.keyword.mobilepushshort}}.   

Normalmente, las aplicaciones cliente primero ejecutan un ciclo de autenticación en el que el usuario de la aplicación móvil se autentica en un servicio de autenticación, como por ejemplo [Mobile Client Access](docs/services/mobileaccess/index.html). Si la autenticación es correcta, el ID de usuario autenticado se pasa a la API de registro del dispositivo push. 
Para enviar una notificación de difusión única mediante la API REST, asegúrese de que se proporcionan los deviceId o los userId al publicarse en un recurso de mensajes.

###Notificaciones basadas en plataforma
{: platform-based-notifications}

Las notificaciones se pueden definir para alcanzar una plataforma de dispositivo determinada. Por ejemplo, se puede enviar una notificación únicamente a todos los usuarios de Android o Google Chrome. Para enviar una notificación basada en plataforma que utilice la API REST, asegúrese de que se proporcionan plataformas de destino al publicar en un recurso de mensajes. Especifique las plataformas como una matriz. Las plataformas soportadas son las siguientes:
* A (Apple)
* G (Google)
* WEB_CHROME (push web del navegador Google Chrome)
* WEB_FIREFOX (push web del navegador Mozilla Firefox)
* WEB_SAFARI (push web del navegador Safari)
* APPEXT_CHROME (aplicaciones y extensiones de Google Chrome)

## Tamaño de los mensajes de {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

El tamaño de carga útil de los mensajes de {{site.data.keyword.mobilepushshort}} depende de las restricciones diseñadas por las pasarelas (FCM/GCM, APN) y las plataformas cliente. 

### iOS y Safari
{: ios-message-size}

Para iOS 8 y posterior, el tamaño máximo permitido es de 2 kilobytes. El Servicio de notificaciones Push de Apple no envía notificaciones que superen este límite.

###Android, navegador Firefox, navegador Chrome y aplicaciones y extensiones de Chrome
{: android-message-size}

Existe una limitación de 4 kilobytes en el tamaño máximo permitido de la carga útil de mensajes.  
