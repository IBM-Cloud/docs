---

copyright:
 years: 2015, 2016

---

# Acerca de {{site.data.keyword.mobilepushshort}}
{: #overview-push}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Las {{site.data.keyword.mobilepushshort}} de IBM son un servicio que puede utilizar para enviar notificaciones a dispositivos iOS y Android. Las notificaciones se pueden destinar a todos los usuarios de la aplicación o a un conjunto específico de usuarios y dispositivos mediante etiquetas. Puede
        administrar dispositivos, etiquetas y suscripciones. También puede utilizar un SDK (software development kit, kit de desarrollo de software) y API (application program interface, interfaz de programa de aplicaciones) REST (Representational State Transfer) para desarrollar más las aplicaciones de cliente. 

La {{site.data.keyword.mobilepushshort}} también está disponible como servicio dedicado de Bluemix. Para obtener información sobre la {{site.data.keyword.mobilepushshort}} como servicio dedicado, consulte [Servicios dedicados](../../dedicated/index.html). Tenga en cuenta que el separador de supervisión de {{site.data.keyword.mobilepushshort}} no muestra los datos analíticos.

El servicio {{site.data.keyword.mobilepushshort}} ahora está habilitado para OpenWhisk. Para obtener más información, consulte [OpenWhisk](../../openwhisk/index.html).


## Proceso del servicio {{site.data.keyword.mobilepushshort}}
{: #overview_push_process}

Los clientes móviles pueden suscribirse y registrarse al servicio {{site.data.keyword.mobilepushshort}}. Al arrancar, las aplicaciones móviles se registrarán y se suscribirán al servicio {{site.data.keyword.mobilepushshort}}. Las notificaciones se asignan
                al servicio de APN (Apple Push Notification Service) o al servidor de GCM (Google Cloud Messaging)
                y, a continuación, se enviarán a los clientes móviles registrados.

![Visión general de push](images/overview.jpg)


###Aplicaciones móviles
{: mobile-applications}

Al arrancar, las aplicaciones móviles se registrarán y se suscribirán al servicio {{site.data.keyword.mobilepushshort}} para recibir notificaciones.

###Aplicaciones de fondo
{: backend-applications}

Las aplicaciones de fondo pueden ser locales o pueden estar en una nube pública. Las aplicaciones de fondo utilizan el servicio {{site.data.keyword.mobilepushshort}} para enviar notificaciones según el contexto a usuarios móviles. No es necesario que las aplicaciones de fondo mantengan ni gestionen dispositivos móviles ni información de usuarios para enviar notificaciones push. En lugar de ello, pueden utilizar el servicio {{site.data.keyword.mobilepushshort}}.

###Propietario de back-end de app
{: app-backend-owner}

El propietario de back-end de app crea la aplicación móvil de fondo, que agrupa una instancia del servicio {{site.data.keyword.mobilepushshort}}. El propietario también configura el servicio {{site.data.keyword.mobilepushshort}} para adaptar las aplicaciones de fondo utilizando el servicio junto con las aplicaciones móviles destinadas para {{site.data.keyword.mobilepushshort}}.

###Servicio {{site.data.keyword.mobilepushshort}}
{: push-notification-service}

El servicio {{site.data.keyword.mobilepushshort}} gestiona toda la información relacionada con los dispositivos registrados para las notificaciones. El servicio mantiene sus aplicaciones transparentes a los detalles tecnológicos de enviar notificaciones a plataformas móviles heterogéneas y lo maneja todo.

###Pasarelas
{: gateways}

Los servicios de nube específicos de plataformas de dispositivos móviles, como Google Cloud Messaging (GCM) o Apple Push Notification Service (APNs), utilizan el servicio {{site.data.keyword.mobilepushshort}} para asignar notificaciones a las aplicaciones móviles.

###Seguridad push
{: push-security}

Las API de las {{site.data.keyword.mobilepushshort}} están protegidas por dos tipos de secretos: i) appSecret ii) clientSecret.  'appSecret' protege las API que suelen invocar las aplicaciones de fondo, como por ejemplo la API para enviar {{site.data.keyword.mobilepushshort}}, la API para configurar las opciones, etc. 'clientSecret' protege las API que suelen invocar las aplicaciones de clientes móviles. Actualmente solo hay una API relacionada con el registro de dispositivos con un UserId asociado que necesite este 'clientSecret'. El resto de las API invocadas desde clientes móviles no necesitan dicho 'clientSecret'. 'appSecret' y 'clientSecret' se asignan a todas las instancias de servicio en el momento de enlazar una aplicación con el servicio {{site.data.keyword.mobilepushshort}}. Consulte la documentación de la API REST para obtener más información sobre cómo se deben pasar los secretos y para qué API.

## Tipos de {{site.data.keyword.mobilepushshort}}
{: #overview-push-types}

###Difusión
{: broadcast}

Cuando una aplicación móvil se registra en el servicio {{site.data.keyword.mobilepushshort}}, puede comenzar a recibir difusiones. Las notificaciones de difusión son mensajes destinados a todos los dispositivos que cuentan con una aplicación instalada y configurada para el servicio {{site.data.keyword.mobilepushshort}}. Las notificaciones de difusión están habilitadas de forma predeterminada para cualquier aplicación habilitada para {{site.data.keyword.mobilepushshort}}. Las aplicaciones habilitadas para el servicio {{site.data.keyword.mobilepushshort}} tienen una suscripción predefinida en la etiqueta Push.ALL, que utiliza el servidor para transmitir mensajes de notificación a todos los dispositivos. Para enviar una notificación de difusión
                        que utiliza la API Push REST, asegúrese de que el "destino" sea un archivo JSON vacío
                        al publicar en recursos de mensajes.

###Notificaciones basadas en etiquetas
{: tag-based-notifications}

Las notificaciones basadas en etiquetas son mensajes que están pensados para todos los dispositivos suscritos a una etiqueta determinada. Las notificaciones basadas en código
                        permiten la segmentación de notificaciones en función de los temas o de las áreas de temas. Los destinatarios de la notificación pueden elegir recibir notificaciones sólo si es sobre
                        un asunto o tema de su interés. Por lo tanto, la notificación basada en etiquetas
                        proporciona un medio de segmentar destinatarios. Esta característica habilita
                        la función de definir etiquetas y, a continuación, enviar y recibir mensajes por etiquetas. Un
                        mensaje sólo se ha dirigido a los dispositivos que están suscritos a una etiqueta. Primero debe crear las etiquetas para la aplicación, configurar las suscripciones de etiquetas y, a continuación, iniciar las notificaciones basadas en etiquetas. Para enviar una notificación basada en etiquetas que utiliza la API REST, asegúrese de que los "tagNames" se proporcionen al publicarse en el recurso de mensajes. 

###Notificaciones de difusión única
{: unicast-notifications}

Las notificaciones de difusión única son mensajes destinados a un dispositivo o usuario específico. Dichas notificaciones destinadas a dispositivos no necesitan ninguna configuración adicional y están habilitadas de forma predeterminada cuando se habilita la aplicación para {{site.data.keyword.mobilepushshort}}.

No obstante, las notificaciones de difusión única destinadas a usuarios necesitan lo siguiente:

- Se debe asociar un ID de usuario a un dispositivo en el momento de registrar el dispositivo móvil a las notificaciones push.  

- Se debe autorizar dicho registro del ID de usuario pasando un 'clientSecret', que se asigna al enlazar una aplicación de fondo al servicio {{site.data.keyword.mobilepushshort}}. 

Normalmente, las aplicaciones móviles primero ejecutan un ciclo de autenticación en el que el usuario de la aplicación se autentica en un servicio de autenticación, como por ejemplo [Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Si la autenticación es correcta, el ID de usuario autenticado se pasa a la API de registro del dispositivo push, junto con un 'clientSecret'. La presencia de un 'clientSecret' aplica únicamente la asociación autorizada de ID de usuario con registros de dispositivos móviles. Para enviar una notificación de difusión única mediante la API REST, asegúrese de que se proporcionan los deviceId o los userId al publicarse en un recurso de mensajes.

###Notificaciones basadas en plataforma
{: platform-based-notifications}

Las notificaciones se pueden definir para alcanzar una plataforma de dispositivo determinada. Por
                            ejemplo, se puede enviar una notificación únicamente a todos usuarios de Android. Para
                            enviar una notificación basada en plataforma que utilice la API REST, asegúrese
                            de que se proporcionan plataformas de destino al publicar en un recurso de
                            mensajes. Especifique las plataformas como una matriz. Las plataformas
                            soportadas son las siguientes:
* A (Apple)
* G (Google)

## Tamaño de los mensajes de {{site.data.keyword.mobilepushshort}}
{: #push-message-size}

El tamaño de carga útil de los mensajes de {{site.data.keyword.mobilepushshort}} depende de los mediadores. 

###iOS
{: ios-message-size}

Para iOS 8 y posterior, el tamaño máximo permitido es de 2 kilobytes. El Servicio de notificaciones Push de Apple no envía notificaciones que superen este límite.

###Android
{: android-message-size}

No hay limitaciones en la plataforma Android.
