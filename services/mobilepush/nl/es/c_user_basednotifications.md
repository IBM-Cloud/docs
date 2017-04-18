---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Habilitación de notificaciones basadas en usuarios
{: #user_based_notifications}
Última actualización: 16 de enero de 2017
{: .last-updated}

Las {{site.data.keyword.mobilepushshort}} basadas en ID de usuario están pensadas para los usuarios de aplicaciones móviles con mensajes personalizados. Con las notificaciones basadas en usuarios, puede elegir notificar a individuos específicos según sus preferencias.

## Dispositivo de registro con ID de usuario
Para habilitar las notificaciones push destinadas por ID de usuario, asegúrese de registrar el dispositivo con un campo de ID de usuario definido.     

El ID de usuario puede ser cualquier serie que proporcione la aplicación a la API de registro del dispositivo. Normalmente, las aplicaciones móviles primero ejecutan un ciclo de autenticación en el que el usuario de la aplicación se autentica en un servicio de autenticación, como por ejemplo [{{site.data.keyword.amafull}} ![icono de enlace externo](../../icons/launch-glyph.svg "icono de enlace externo")](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html){: new_window}. Si la autenticación es correcta, el ID de usuario autenticado se pasa a la API de registro del dispositivo push. 

## Sincronización del inicio y cierre de sesión de un usuario 

Puede elegir el envío de notificaciones únicamente si el usuario ha iniciado la sesión. 

Por ejemplo, piense en un dispositivo compartido por los miembros de una familia o por un equipo de trabajo, y habrá necesidad de dirigirse a determinados usuarios. En tal caso práctico, habría una secuencia de inicio y cierre de sesión de usuario. Este mecanismo de autenticación permite que la aplicación efectúe un seguimiento de la identidad del usuario de la aplicación en cuestión. De esta manera, se garantiza que las notificaciones destinadas a un usuario específico lleguen siempre únicamente a dicho usuario. Después de iniciar sesión, invoque la API de registro de dispositivos pasando el ID de usuario del usuario conectado. De la misma manera, antes de cerrar la sesión, invoque la API de eliminación de registro de dispositivos. La secuenciación de estas API push con el inicio y el cierre de sesión garantizará que las notificaciones destinadas a un determinado usuario se envíen únicamente a dicho usuario.
