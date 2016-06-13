---

copyright:
 years: 2015, 2016

---

# Acerca de las notificaciones push
{: #overview-push}

Las notificaciones push son un servicio que puede utilizar para enviar notificaciones al dispositivo iOS y Android. Las notificaciones se pueden destinar a todos los usuarios de la aplicación o a un conjunto específico de usuarios y dispositivos mediante etiquetas. Puede
        administrar dispositivos, etiquetas y suscripciones. También puede utilizar un SDK (software development kit, kit de desarrollo de software) y API (application program interface, interfaz de programa de aplicaciones) REST (Representational State Transfer) para desarrollar más las aplicaciones de cliente. Para obtener información sobre el servicio push dedicado, consulte [Servicios dedicados](../../dedicated/index.html). 


## Proceso de servicio de notificaciones push
{: #overview_push_process}

Los clientes móviles pueden suscribirse y registrarse para el servicio de notificaciones Push. Al
                arrancar, las aplicaciones móviles se registrarán y se suscribirán al servicio de notificaciones
                Push. Las notificaciones se asignan
                al servicio de APN (Apple Push Notification Service) o al servidor de GCM (Google Cloud Messaging)
                y, a continuación, se enviarán a los clientes móviles registrados.

![Visión general de push](images/overview.jpg)


###Aplicaciones móviles

Al arrancar, las aplicaciones móviles se registrarán
                        y se suscribirán al servicio de notificaciones Push para recibir
                        notificaciones.

###Aplicaciones de fondo

Las aplicaciones de fondo pueden estar de forma local o en una nube pública. Las aplicaciones de fondo utilizan el Servicio de notificaciones Push
                        para enviar notificaciones según el contexto a usuarios
                        móviles. No es necesario que las aplicaciones de fondo mantengan ni gestionen
                        dispositivos móviles ni información de usuarios para enviar notificaciones push. En su lugar,
                        las aplicaciones de fondo pueden utilizar el Servicio de notificaciones Push.

###Propietario de back-end de app

El rol que ha creado la aplicación de fondo móvil que empaqueta una
                        instancia del Servicio de notificaciones Push. Esta persona configura
                        el Servicio de notificaciones Push para que se ajuste a las aplicaciones de fondo que utilizan
                        el Servicio de notificaciones Push y las aplicaciones móviles que son el destino de notificaciones
                        push.

###Servicio de notificaciones Push

El servicio de notificaciones Push gestiona toda la información relacionada con los dispositivos que se registran para notificaciones. El servicio mantiene sus aplicaciones transparentes a los detalles tecnológicos de enviar notificaciones a estas plataformas móviles heterogéneas y lo maneja todo.

###Pasarelas

Los servicios de nube específicos de plataformas de dispositivos móviles tales como Google Cloud Messaging (GCM) o Apple Push Notification Service(APNs) utilizan el Servicio de notificaciones Push
                        para asignar notificaciones a las aplicaciones móviles.

## Tipos de notificación de envío
{: #overview-push-types}

###Difusión

Cuando una aplicación móvil se registra con el servicio de notificaciones Push, puede comenzar a recibir notificaciones. Las notificaciones de difusión son mensajes de notificación destinados a todos
                        los dispositivos que tienen la aplicación instalada y configurada para el Servicio de
                        notificaciones Push. Las notificaciones de difusión están
                        habilitadas de forma predeterminada con cualquier aplicación que está habilitada para las notificaciones
                        push. Cualquier aplicación que esté habilitada para el Servicio de notificaciones push tiene una suscripción predefinida a la etiqueta Push.ALL, que utiliza el servidor para difundir mensajes de notificación a todos los dispositivos. Para enviar una notificación de difusión
                        que utiliza la API Push REST, asegúrese de que el "destino" sea un archivo JSON vacío
                        al publicar en recursos de mensajes.

###Notificaciones basadas en etiquetas

Las notificaciones de código son mensajes de notificación que están pensados para todos los
                        dispositivos suscritos a un código determinado. Las notificaciones basadas en código
                        permiten la segmentación de notificaciones en función de los temas o de las áreas de temas. Los destinatarios de la notificación pueden elegir recibir notificaciones sólo si es sobre
                        un asunto o tema de su interés. Por lo tanto, la notificación basada en etiquetas
                        proporciona un medio de segmentar destinatarios. Esta característica habilita
                        la función de definir etiquetas y, a continuación, enviar y recibir mensajes por etiquetas. Un
                        mensaje sólo se ha dirigido a los dispositivos que están suscritos a una etiqueta. Primero debe
                        crear las etiquetas para la aplicación, configurar las suscripciones de etiquetas
                        y, a continuación, iniciar las notificaciones basadas en etiquetas. Para enviar una notificación basada en código
                        que utiliza la API REST, asegúrese de que los "tagNames" se proporcionen
                        al publicar en el recurso de mensajes.

###Notificaciones de difusión única

Las notificaciones de difusión única son mensajes de notificación que están pensados para un dispositivo concreto. Las notificaciones de difusión única no requieren ninguna configuración adicional y están habilitadas de forma predeterminada cuando se habilita la aplicación para notificaciones push. Para enviar una notificación de difusión única que utilice la API REST, asegúrese de que se proporcionan ID de dispositivo al publicar en un recurso de mensajes.

###Notificaciones basadas en plataforma

Las notificaciones se pueden definir para alcanzar una plataforma de dispositivo determinada. Por
                            ejemplo, se puede enviar una notificación únicamente a todos usuarios de Android. Para
                            enviar una notificación basada en plataforma que utilice la API REST, asegúrese
                            de que se proporcionan plataformas de destino al publicar en un recurso de
                            mensajes. Especifique las plataformas como una matriz. Las plataformas
                            soportadas son las siguientes:
* A (Apple)
* G (Google)
