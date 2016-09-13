---

Título: Habilitación de notificaciones push basadas en usuarios

Palabras clave: notificaciones push basadas en usuarios, userId
copyright:
 years: 2015, 2016

---

# Habilitación de notificaciones basadas en usuarios
{: #user_based_notifications}
Última actualización: 16 de agosto de 2016
{: .last-updated}

Las {{site.data.keyword.mobilepushshort}} basadas en ID de usuario están pensadas para los usuarios de aplicaciones móviles con mensajes personalizados. Las notificaciones basadas en usuarios hacen que determinadas personas aprovechen sus preferencias y elecciones personales.  

## Dispositivo de registro con ID de usuario
Para habilitar las notificaciones push destinadas por ID de usuario, asegúrese de registrar el dispositivo con un ID de usuario y de pasar el 'clientSecret' que se asigna al suministrar el servicio {{site.data.keyword.mobilepushshort}}. El registro del dispositivo no funcionará si no se proporciona un 'clientSecret' válido.  

El ID de usuario puede ser cualquier serie que proporcione la aplicación a la API de registro del dispositivo. Normalmente, las aplicaciones móviles primero ejecutan un ciclo de autenticación en el que el usuario de la aplicación se autentica en un servicio de autenticación, como por ejemplo [{{site.data.keyword.amafull}}](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html). Si la autenticación es correcta, el ID de usuario autenticado se pasa a la API de registro del dispositivo push, junto con un 'clientSecret'. La presencia de un 'clientSecret' aplica únicamente la asociación autorizada de ID de usuario con registros de dispositivos móviles.

No muestre nunca el 'clientSecret' ni lo codifique en la aplicación. Hay distintos patrones de inicialización de aplicaciones que se pueden utilizar para obtener dinámicamente el 'clientSecret' durante el tiempo de ejecución de la aplicación. El diagrama de secuencia sigue este patrón.

![Enable_Push](images/init_client_secret.jpg) 

También puede registrar un dispositivo para asociarlo a un usuario 'anónimo'. Para ello, debe utilizar una variante de la API de registro de dispositivos que no precisa los argumentos de ID de usuario ni 'clientSecret'.   

## Sincronización el inicio y el cierre de sesión de usuario y habilitación de las notificaciones push 

Puede elegir el envío de notificaciones únicamente si el usuario ha iniciado la sesión. 

Por ejemplo, si un dispositivo está compartido por una familia o por un equipo de trabajo y necesita dirigirse a determinados usuarios de la familia o del equipo. En tal caso práctico, habría una secuencia de inicio y cierre de sesión de usuario que protege la aplicación para efectuar un seguimiento de la identidad del usuario de la aplicación en cuestión. Para garantizar que las notificaciones destinadas a un determinado usuario lleguen siempre únicamente a dicho usuario, después de iniciar la sesión, invoque la API de registro de dispositivos pasando el ID de usuario del usuario conectado. De la misma manera, antes de cerrar la sesión, invoque la API de eliminación de registro de dispositivos. La secuenciación de estas API push con el inicio y el cierre de sesión garantizará que las notificaciones push destinadas a un determinado usuario se envíen únicamente a dicho usuario.
