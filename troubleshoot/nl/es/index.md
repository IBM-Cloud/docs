---

copyright:
  years: 2015, 2016

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 

# Resolución de problemas de acceso a {{site.data.keyword.Bluemix_notm}} 
{: #accessing}

*Última actualización: 16 de mayo de 2016*

Algunos de los problemas generales de acceso a {{site.data.keyword.Bluemix}} pueden ser que un usuario no pueda iniciar una sesión en {{site.data.keyword.Bluemix_notm}}, que una cuenta se haya bloqueado en estado pendiente, etc. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos. 
{:shortdesc}

## No se puede iniciar la sesión en {{site.data.keyword.Bluemix_notm}}
{: #ts_logintobm}

Debe tener un ID y contraseña de IBM válidos para poder iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.


Cuando intenta iniciar una sesión en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error: 
{: tsSymptoms} 

`El ID y/o la contraseña de IBM especificados a continuación son incorrectos. Inténtenlo de nuevo.`


El ID y contraseña de IBM que utiliza para iniciar una sesión en {{site.data.keyword.Bluemix_notm}} no son válidos.
{: tsCauses} 
 

Para obtener un ID y contraseña de IBM válidos, vaya a la página Mi perfil de IBM y siga los pasos siguientes:
{: tsResolve}
  * Si ya ha registrado un ID de IBM y desea comprobar si el ID y la contraseña son válidos, pulse **Iniciar sesión** y especifique la contraseña y el ID de IBM en la página Iniciar sesión. Si ha olvidado su contraseña, pulse **¿Ha olvidado su contraseña?** en la parte derecha de la página Iniciar sesión para restablecer la contraseña. Si ha olvidado el ID de IBM o sigue teniendo problemas con su contraseña, póngase en contacto con el centro de atención al cliente de registro de IBM a nivel mundial para obtener ayuda. 
  * Si no tiene un ID de IBM, pulse **Registrar** para registrar un ID y una contraseña de IBM. 
  
**Nota:** Para los empleados de IBM es posible que el ID de IBM no coincida con el ID de inicio de sesión en la intranet. 





## Hay cambios sin guardar
{: #ts_unsaved_changes}


Al navegar en la página de detalles de aplicaciones, es posible que no pueda realizar las acciones y es posible que se le solicite que guarde los cambios para poder continuar. 


Cuando intente comprobar la app o los servicios en la página de detalles de la app, seguirá recibiendo el siguiente mensaje de error:
{: tsSymptoms} 

`Hay cambios sin guardar en la página app_name. Guarde o cancele los cambios.`


Cuando desplace el ratón sobre el campo **INSTANCES** o **MEMORY QUOTA** del panel de tiempo de ejecución, los valores cambiarán. Este comportamiento es mediante diseño; sin embargo, el mensaje de error le solicitará que guarde los valores de instancia o de memoria para poder navegar fuera de la página. 
{: tsCauses}


Cierre la ventana de mensajes y, a continuación, pulse el botón **RESET** en el panel de tiempo de ejecución. 
{: tsResolve} 




    
    
## La migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}} no está disponible
{: #ts_failover}

No puede utilizar la migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}}. Sin embargo, puede utilizar un proveedor de DNS que dé soporte a la migración tras error entre varias direcciones IP como solución temporal.
 

Cuando una región de {{site.data.keyword.Bluemix_notm}} deja de estar disponible, las apps que se ejecutan en dicha región tampoco están disponibles, aunque las mismas apps se estén ejecutando en otra región de {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

 
{{site.data.keyword.Bluemix_notm}} aún no proporciona migración tras error automática entre una región y otra.
{: tsCauses}

 
Puede utilizar un proveedor de DNS que dé soporte a la migración tras error inteligente entre varias direcciones IP y configurar manualmente los valores de DNS para habilitar la migración tras error automática entre regiones de {{site.data.keyword.Bluemix_notm}}. Disponen de esta función los proveedores de DNS NSONE, Akamai, Dyn.
{: tsResolve}

Cuando configure los valores de DNS, debe especificar las direcciones IP públicas de las regiones de {{site.data.keyword.Bluemix_notm}} en la que se ejecutan sus apps. Para obtener la dirección IP pública de una región de {{site.data.keyword.Bluemix_notm}}, utilice el mandato `nslookup`. Por ejemplo, puede escribir el siguiente mandato en una ventana de línea de mandatos:
```
nslookup mybluemix.net
```



## La cuenta está pendiente
{: #ts_accntpding}

Si la cuenta está pendiente, no puede iniciar una sesión en {{site.data.keyword.Bluemix_notm}}.

 
Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, es posible que no pueda iniciar una sesión en {{site.data.keyword.Bluemix_notm}}. Verá en su lugar el siguiente mensaje:
{: tsSymptoms}

<code>Su cuenta está pendiente. Debe esperar hasta 24 horas a recibir una confirmación por correo electrónico y debe comprobar la carpeta spam. Si transcurrido este tiempo no ha recibido la confirmación por correo electrónico, póngase en contacto con el <a href="http://ibm.biz/bluemixsupport.com" target="_blank">soporte de Bluemix</a>.</code>


Después de registrarse para una cuenta de prueba de {{site.data.keyword.Bluemix_notm}}, recibirá un correo electrónico de confirmación. Debe pulsar el enlace del correo electrónico de confirmación para completar el proceso de registro.
{: tsCauses} 

El correo electrónico de confirmación se envía a la dirección de correo electrónico que ha especificado. Consulte la bandeja de entrada de la carpeta de correo basura. Si no ha recibido el correo electrónico de confirmación, póngase en contacto con el soporte de [{{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}.  
{: tsResolve}



## No se pueden añadir usuarios a una organización
{: #ts_adduser}

Puede invitar a más de un usuario a trabajar en la misma organización. Solo puede invitar a los usuarios a su organización si es el propietario de la cuenta o si es gestor y miembro de la organización.
 

No ve el enlace **Invitar a un nuevo usuario** en la sección **Gestionar organizaciones**. 
{: tsSymptoms}

 

Únicamente los siguientes usuarios de {{site.data.keyword.Bluemix_notm}}
pueden invitar a usuarios a una organización:
{: tsCauses}
  * El propietario de la cuenta de la organización
  * Gestores de la organización que también son miembros, no colaboradores,
de la organización
  
En {{site.data.keyword.Bluemix_notm}}
puede ser miembro o colaborador de una organización:

<dl><dt>Colaborador</dt>
<dd>Es colaborador de una organización si ya dispone de una
cuenta de {{site.data.keyword.Bluemix_notm}}
y alguien le ha invitado a la organización.</dd>
<dt>Miembro</dt>
<dd>Es miembro de una organización si no dispone de una cuenta de {{site.data.keyword.Bluemix_notm}}, pero alguien le invita a la organización y se registra en {{site.data.keyword.Bluemix_notm}} desde la invitación.</dd>
</dl>


No puede invitar a usuarios a su organización si es
colaborador, incluso si se le ha asignado
como gestor de la organización.

**Nota:** Todos los gestores de la organización, incluidos los que
son colaboradores, pueden añadir, modificar y
eliminar los usuarios que ya están en la organización.

 

Si no puede invitar usuarios a su organización
y necesita otro rol para hacerlo, póngase en contacto con el gestor de la organización
para cambiar el rol. Para identificar el gestor de la organización, siga estos pasos:
{: tsResolve}

  1. Vaya al Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el icono **Cuenta y soporte** ![Cuenta y soporte](images/account_support.svg) en la barra de menús superior y seleccione **Gestionar organizaciones**.
  2. Vaya a la organización y consulte la información sobre el gestor de la organización en el separador **USUARIOS**.  
  
Si no puede invitar usuarios porque es colaborador y no un miembro, debe suprimir la cuenta anterior de {{site.data.keyword.Bluemix_notm}} y luego se le debe invitar como un miembro de la organización. Para suprimir la cuenta anterior y unirse como miembro, complete los siguientes pasos: 

  1. Póngase en contacto con el [Soporte de {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} para abrir una incidencia de soporte y solicitar que se suprima la cuenta. Si tiene datos asociados con su antigua cuenta que desea guardar y moverlos a la nueva cuenta, incluya es información en el correo. 
  2. Cuando se suprima la cuenta, tendrá un usuario con el rol de gestor de la organización y le invitará a unirse como gestor. Luego, inicie sesión en {{site.data.keyword.Bluemix_notm}} desde la invitación. 




## No se da soporte al registro por lotes de usuarios
{: #ts_batchregistration}

Cuando registre usuarios para {{site.data.keyword.Bluemix_notm}},
debe registrar cada usuario por separado.
 

{{site.data.keyword.Bluemix_notm}} no ofrece la posibilidad de registrar varios usuarios a la vez.
{: tsSymptoms}
 

{{site.data.keyword.Bluemix_notm}} no da soporte al registro por lotes de usuarios. Para registrar usuarios para {{site.data.keyword.Bluemix_notm}}, debe registrar cada usuario por separado.
{: tsCauses}
 

Para registrar varios usuarios para {{site.data.keyword.Bluemix_notm}},
debe completar los pasos siguientes para cada usuario:
{: tsResolve}

  1. Pulse **REGISTRARSE** en la esquina superior derecha de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}.
  2. Complete los pasos siguiendo el asistente.

    

## No se puede cargar una página de {{site.data.keyword.Bluemix_notm}}
{: #ts_err}

Cuando utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, es posible que no pueda cargar una página de {{site.data.keyword.Bluemix_notm}}. En su lugar verá los mensajes de error BXNUI0001E o BXNUI0016E.
 

Es posible que vea uno de los siguientes mensajes de error cuando utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}:
{: tsSymptoms}

`BXNUI0001E: La página no se ha cargado porque Bluemix no ha detectado si existe una sesión.`


`BXNUI0016E: Las apps y servicios no se han recuperado porque no se ha cargado una página de Bluemix.`

 

Puede llevar a cabo una o varias de estas acciones si es necesario:
{: tsResolve}

  * Renueve o reinicie el navegador.
  * Finalice la sesión de {{site.data.keyword.Bluemix_notm}} y vuélvala a iniciar.
  * Utilice la modalidad de navegación privada del navegador. 
  * Borre las cookies y la memoria caché del navegador.
  * Utilice otro navegador. Para obtener información sobre las versiones de los navegadores a las que da soporte {{site.data.keyword.Bluemix_notm}}, consulte Requisitos previos de [{{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}.
  * Si ha instalado la interfaz de línea de mandatos cf, escriba el mandato `cf
apps` para ver si la app se está ejecutando.
  
  
  
  
  
## La barra de menús superior de {{site.data.keyword.Bluemix_notm}} desaparece
{: #ts_topmenubar}

Quizás no pueda ver la barra de menús superior de {{site.data.keyword.Bluemix_notm}} si cambia el tamaño de la ventana del navegador o si utiliza un dispositivo móvil.


Si reduce el tamaño de la ventana del navegador, o si utiliza un dispositivo móvil, la barra de menús superior de {{site.data.keyword.Bluemix_notm}} desaparece. Cuando la barra de menús superior desaparece, el menú lateral que se muestra como un icono de línea apilado aparece en la esquina superior izquierda. 
{: tsSymptoms}

 

La interfaz de usuario de {{site.data.keyword.Bluemix_notm}} tiene un diseño interactivo. Cuando la visualización del entorno cambia, el diseño de la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} también puede cambiar. 
{: tsCauses}
 

Utilice en su lugar el menú lateral de la esquina superior izquierda.
{: tsResolve}








# Resolución de problemas de gestión de apps
{: #managingapps}

Entre los problemas generales relacionados con la gestión de apps se pueden incluir
las aplicaciones que no se pueden actualizar y los caracteres de doble byte que no se visualizan. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}





## No se pueden conmutar apps en modalidad de depuración
{: #ts_debug}

Es posible que no pueda habilitar la modalidad de depuración si la versión de la máquina virtual Java (JVM) es 8 o inferior. 


Después de seleccionar **Habilitar depuración de aplicación**, las herramientas intentan conmutar la aplicación a la modalidad de depuración. A continuación, el entorno de trabajo de Eclipse empieza una sesión de depuración. Cuando las herramientas habilitan satisfactoriamente la modalidad de depuración, el estado de la aplicación web visualiza `Modalidad de actualización`, `Desarrollo` y `Depuración`. 
{: tsSymptoms}

Sin embargo, cuando has herramientas no pueden habilitar la modalidad de depuración, el estado de aplicación web visualiza solamente `Modalidad de actualización` y `Desarrollo`, pero no visualiza `Depuración`. Las herramientas también pueden visualizar el siguiente mensajes de error en la vista de consola.

```
bluemixMgmgClient - ???? [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at  org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at  com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
[2016-01-15 13:33:51.075] bluemixMgmgClient - ????  [pool-1-thread-1] .... ERROR --- ClientProxyImpl: Cannot create the  websocket connections for MyWebProj
com.ibm.ws.cloudoe.management.client.exception.ApplicationManagementException: javax.websocket.DeploymentException: The HTTP request to initiate the  WebSocket connection failed
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:161)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl$RunServerTask.run(ClientProxyImpl.java:267)
at java.util.concurrent.Executors$RunnableAdapter.call(Executors.java:522)
at java.util.concurrent.FutureTask.run(FutureTask.java:277)
at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1153)
at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:628)
at java.lang.Thread.run(Thread.java:785)
Caused by: javax.websocket.DeploymentException: The HTTP request to initiate the WebSocket connection failed
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:315)
at com.ibm.ws.cloudoe.management.client.impl.ClientProxyImpl.onNewClientSocket(ClientProxyImpl.java:158)
... 6 more
Caused by: java.util.concurrent.TimeoutException
at org.apache.tomcat.websocket.AsyncChannelWrapperSecure$WrapperFuture.get(AsyncChannelWrapperSecure.java:505)
at org.apache.tomcat.websocket.WsWebSocketContainer.processResponse(WsWebSocketContainer.java:542)
at org.apache.tomcat.websocket.WsWebSocketContainer.connectToServer(WsWebSocketContainer.java:296)
... 7 more
```
 

Las siguientes versiones de JVM (Java Virtual Machine) no pueden establecer una sesión de depuración:IBM JVM 7, IBM JVM 8 y versiones anteriores de Oracle JVM 8.
{: tsCauses}

Si la JVM del entorno de trabajo es de una de estas versiones, es posible que tenga problemas al crear una sesión de depuración. La versión de JVM del entorno de trabajo es normalmente la JVM del sistema local. La JVM del sistema no es la misma que la JVM de la aplicación Bluemix Java. La aplicación Bluemix Java casi siempre se ejecuta en IBM JVM, y algunas veces se ejecuta en OpenJDK JVM.
  

Para comprobar la versión de Java que IBM Eclipse Tools for Bluemix ejecuta, realice los siguientes pasos:
{: tsResolve}

  1. En IBM Eclipse Tools for Bluemix, seleccione **Ayuda** > **Acerca de Eclipse** > **Detalles de instalación** > **Configuración**.
  2. Busque la propiedad `eclipse.vm` en la lista. La siguiente línea muestra un ejemplo de una propiedad `eclipse.vm`:
	
	```
	eclipse.vm=C:\Archivos de programa\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. En la línea de mandatos, escriba `java -version` desde el directorio `bin` de la instalación Java. Se visualiza la información de la versión de IBM JVM.

Si la JVM del entorno de trabajos de IBM es IBM JVM 7 o 8, o una versión anterior de Oracle JVM 8, complete los siguientes pasos para conmutar a Oracle JVM 8:

  1. Descargue y, a continuación, vuelva a instalar Oracle JVM 8, consulte [Java SE Downloads](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} para obtener detalles.
  2. Reinicie Eclipse.
  3. Compruebe si la propiedad `eclipse.vm` apunta a la nueva instalación de Oracle JVM 8.







## No se pueden efectuar las acciones solicitadas
{: #ts_authority}

Es posible que no pueda efectuar acciones sin la autoridad de acceso adecuada.

 

Cuando intenta llevar a cabo acciones para una instancia de servicio o una instancia de app, no puede completar las acciones solicitadas y ve uno de los siguientes mensajes de error: 
{: tsSymptoms}

`BXNUI0514E: No es desarrollador de ningún espacio de la organización <NombreOrg>.`


`Error de servidor, código de estado: 403, código de error: 10003, mensaje: No tiene autorización para efectuar la acción solicitada.`

 

No tiene el nivel adecuado de autorización necesario para realizar las acciones. 
{: tsCauses}

  

Para obtener el nivel de autorización adecuado, utilice uno de estos métodos: 
{: tsResolve}
 * Seleccione otra organización y otro espacio de los que tenga el rol de desarrollador. 
 * Pida al gestor de la organización que le cambie el rol a desarrollador o que cree un espacio y le asigne un rol de desarrollador. Consulte [Gestión de organizaciones](../admin/orgs_spaces.html) para obtener detalles.
 

 


## No se puede acceder a los servicios de {{site.data.keyword.Bluemix_notm}} debido a errores de autorización
{: #ts_vcap}

Se pueden producir errores de autorización cuando la app accede a un servicio de {{site.data.keyword.Bluemix_notm}} y las credenciales del servicio están codificadas en la app. 

Después de configurar su app para comunicarse con un servicio de {{site.data.keyword.Bluemix_notm}}, despliega la app en {{site.data.keyword.Bluemix_notm}}. Sin embargo, no puede utilizar la app para acceder al servicio de {{site.data.keyword.Bluemix_notm}} y recibe un error de autorización.
{: tsSymptoms}

Las credenciales codificadas de la app podrían no ser correctas. Cada vez que el servicio se vuelve a crear, las credenciales para acceder a él cambian.
{: tsCauses}


En lugar de codificar las credenciales en la app, utilice parámetros de conexión de la variable de entorno VCAP_SERVICES. Los métodos para utilizar los parámetros de conexión de la variable de entorno VCAP_SERVICES varían en función de los lenguajes de programación. Por ejemplo, para las apps Node.js, puede utilizar el siguiente mandato: 
{: tsResolve}

```
process.env.VCAP_SERVICES
```
Para obtener más información sobre los mandatos que puede utilizar en otros lenguajes de programación, consulte [Java](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} y [Ruby](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}. 
 

 
 




## No se pueden desplegar apps utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}
{: #ts_bm_tools_facet}

Cuando se aplica una faceta no soportada en el proyecto de Eclipse,
no podrá desplegar las apps en {{site.data.keyword.Bluemix_notm}} utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}. 

 

Puede desplegar correctamente la app en {{site.data.keyword.Bluemix_notm}} con la CLI de Cloud Foundry. Sin embargo, no puede desplegar la app en {{site.data.keyword.Bluemix_notm}} utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} y verá el mensaje de error: `No se admite la faceta de proyecto <nombre_faceta>.` Por ejemplo, `No se da soporte a la Faceta de proyecto de la aplicación autónoma de Cloud Foundry versión 1.0.`
{: tsSymptoms}

 

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} asignan proyectos a los tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} mediante facetas de proyectos. Las facetas definen los requisitos de los proyectos de
Java EE en Eclipse y se utilizan como parte de la configuración de tiempo de ejecución de modo que los diferentes tiempos de ejecución estén asociados a diferentes proyectos. Si
IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} no da soporte a la faceta que se aplica al proyecto, no se podrá desplegar la app utilizando IBM Eclipse
Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}


Debe eliminar la faceta del proyecto de Eclipse para poder
desplegar la app utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsResolve} 

Para eliminar la faceta, en IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, pulse **Proyecto>Propiedades>Facetas de proyecto** del proyecto. Luego, desmarque el recuadro de selección de la faceta a la que no se da soporte. 



## Se han recibido errores 502 de pasarela errónea
{: #ts_502_error}

Si recibe errores 502 de pasarela errónea al interactuar con apps en {{site.data.keyword.Bluemix_notm}}, compruebe la página de estado de {{site.data.keyword.Bluemix_notm}} y, a continuación, tome las medidas apropiadas.

 

Recibe mensajes de error que empiezan por 502 Bad Gateway. Por ejemplo, puede que vea `502 Bad Gateway: Registered endpoint failed to handle the request.`
{: tsSymptoms}

 

Los errores de pasarela errónea suelen ocurrir al visitar un sitio web que utiliza un servidor proxy para almacenar y retransmitir los datos desde el servidor principal que aloja el sitio. Es posible que el servidor principal y el servidor proxy no se conecten correctamente, por eso ve el código de error de HTTP 502 en la ventana del navegador. Este código de estado indica que el servidor principal del sitio no ha recibido la implementación de HTTP que se esperaba del servidor proxy.
{: tsCauses}

Otras causas menos habituales de un error de pasarela errónea son caídas del ISP (proveedor de servicios de Internet), configuraciones erróneas de cortafuegos y errores de caché de navegador. 

 

Si cree que algún servicio de {{site.data.keyword.Bluemix_notm}} no está disponible, compruebe primero la página de estado de [{{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#status){: new_window}. Como método alternativo, es posible que desee utilizar el servicio en otra región de {{site.data.keyword.Bluemix_notm}}. Hay disponible información detallada en [Utilización de servicios en otra región](../services/reqnsi.html#cross_region_service){: new_window}. Si el estado del servicio es normal, pruebe los pasos siguientes para resolver el problema: 
{: tsResolve}

  * Reintente la acción:
    * Recargue la página pulsando F5 en el teclado o pulsando el botón de renovación. Si estos pasos no funcionan, borre las cookies y la memoria caché del navegador y recargue de nuevo.
	* Utilice otro navegador.
	* Rearranque el direccionador, el módem y el sistema. Rearrancar estos dispositivos puede borrar varios errores que provocan el error 502. 
  * Espere y vuelva a intentarlo más adelante. En algunas instancias, pueden ocurrir problemas temporales en el proveedor de servicios de Internet o en los servicios de {{site.data.keyword.Bluemix_notm}}. Puede esperar a que se resuelvan los problemas temporales.
  * Si el problema todavía existe, póngase en contacto con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}. Consulte [Cómo ponerse en contacto con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}](../support/index.html#contacting-bluemix-support){: new_window} para obtener más información. 




## Se ha excedido la cuota de disco
{: #ts_disk_quota}

Si se agota el espacio en disco, puede modificar manualmente la cuota de disco para obtener más espacio en disco.

  

Cuando se agota el espacio en disco, puede que vea un mensaje que indica que se ha superado la cuota de disco. Para resolver el problema, quizá haya intentado aumentar la escala de la instancia de la app para obtener más espacio de disco. Por ejemplo, cambiar la escala de 256 MB a 1256 MB modificando la cuota de memoria en la página de detalles de la app. Sin embargo, puesto que la cuota de disco no se ha modificado, no ha obtenido más espacio de disco. 
{: tsSymptoms}


La cuota de disco predeterminada que se asigna para una app es de 1 GB. Si necesita más espacio de disco, debe indicar manualmente la cuota de disco. 
{: tsCauses}

 
Utilice uno de estos métodos para especificar la cuota de disco. La cuota de disco máxima que puede especificar es de 2 GB. Si 2 GB todavía no es suficiente, pruebe un servicio externo, como [Object Store](../services/ObjectStorage/index.html){: new_window}.
{: tsResolve}

  * En el archivo manifest.yml, añada el elemento siguiente:
    ```
	disk_quota: <disk_quota>
	```
  * Utilice la opción **-k** con el mandato `cf push` cuando envíe la app por push a {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push appname -p app_path -k <cuota de disco>
	```

	
	
## No se puede añadir el repositorio Git
{: #ts_cannot_addgit}

Después de crear una app en el Panel de control. pulsa AÑADIR GIT para crear un repositorio Git, pero no puede continuar.



Cuando pulsa **AÑADIR GIT**, se abre una ventana y se produce uno de los siguientes problemas:
{: tsSymptoms} 

  * La ventana se cuelga con una pantalla en blanco.
  * Un mensaje indica que existe un problema con cookies de terceros.



Es posible que el navegador se haya configurado de modo que impida que se establezca una cookie. Dicha cookie se debe establecer desde el sitio de IBM® Bluemix DevOps Services en el dominio de Internet hub.jazz.net desde dentro del contexto de la consola de {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}  

 

Puede solucionar el problema de una de las siguientes formas:
{: tsResolve}

  * Siga las instrucciones de la ventana que se abre en la consola de {{site.data.keyword.Bluemix_notm}}. Pulse el botón. Se abre otra ventana del navegador temporalmente. En dicha ventana, DevOps Services establece la cookie de autenticación.
  * En otro separador del navegador, vaya a https://hub.jazz.net e inicie una sesión. Vuelva a la consola de {{site.data.keyword.Bluemix_notm}} y renueve la página. Vuelva a pulsar **AÑADIR GIT**.
  * Cambie la configuración del navegador para habilitar cookies de terceros y pulse AÑADIR GIT. Para obtener detalles sobre cómo configurar los valores, consulte la documentación del navegador:
    * [Mozilla Firefox](https://support.mozilla.org/en-US/kb/enable-and-disable-cookies-website-preferences#w_how-do-i-change-cookie-settings){: new_window}
	* [Google Chrome](https://support.google.com/chrome/answer/95647){: new_window}
	* [Apple Safari](https://support.apple.com/kb/PH17191){: new_window}
	* [Microsoft Internet Explorer](http://windows.microsoft.com/en-us/internet-explorer/delete-manage-cookies#ie=ie-11){: new_window}
Si estos métodos alternativos no solucionan el problema, envíe un correo electrónico a idslogin@jazz.net.



## Las apps de Android no pueden recibir notificaciones push
{: #ts_push}

En determinadas regiones en las que no se puede acceder a Google, las apps de Android no pueden recibir notificaciones enviadas a través del servicio IBM Push. En estos casos, se pueden utilizar servicios de terceros como método alternativo.

 

Enlaza un servicio Push con la app de Bluemix y envía un mensaje a los dispositivos registrados. No obstante, las apps que se desarrollan en la plataforma Android no pueden recibir notificaciones en determinadas regiones. 
{: tsSymptoms}

 
El servicio IBM Push utiliza Google Cloud Messaging (GCM) para enviar notificaciones a apps móviles desarrolladas en la plataforma Android. Para permitir que las apps de Android reciban notificaciones, se debe poder acceder al servicio Google Cloud Messaging (GCM) en las apps móviles. En las regiones en las que no se puede acceder al servicio GCM en las apps de Android, estas no pueden recibir notificaciones push.
{: tsCauses}

 
Como método alternativo, utilice servicios de terceros que no dependan del servicio GCM como, por ejemplo, [Pushy](https://pushy.me){: new_window}, [igetui](http://www.getui.com/){: new_window} y [jpush](https://www.jpush.cn/){: new_window}.
{: tsResolve}



## El límite de servicios de la organización se ha excedido
{: #ts_servicelimit}

Si es usuario de una cuenta de prueba, es posible que no pueda crear una app en {{site.data.keyword.Bluemix_notm}} si ha excedido el límite de servicios de su organización.
 

Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}},
ve el siguiente mensaje de error: 
{: tsSymptoms}

`BXNUI2032E: No se ha creado el recurso <instancias_servicio>. Mientras se estaba contactando con Cloud Foundry para crear el recurso, se ha producido un error. Mensaje de Cloud Foundry: "Ha excedido el límite de servicios de su organización."`



Este error se produce cuando se excede el límite de número de instancias del servicio que puede tener para su cuenta. El número máximo de número de instancias del servicio para una cuenta de prueba es 10.
{: tsCauses} 

 

Suprima las instancias del servicio que no sean necesarias, o elimine el límite de número de instancias del servicio que tiene.
{: tsResolve}
 
  * Para suprimir una instancia del servicio, puede utilizar la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o la interfaz de la línea de mandatos.
    Para utiliza la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} para suprimir una instancia de servicio, siga los siguientes pasos:
	  1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, pulse **SERVICIOS** en el panel de la izquierda. Se muestran los títulos de servicios. 
	  2. En el título de servicio que quiera suprimir, pulse en el icono **Menú**.
	  3. Pulse **Suprimir servicio**. Después de suprimir la instancia de servicio, se le solicitará que vuelva a transferir app a la cual estaba enlazada la instancia de servicio. 
    Para utilizar la interfaz de línea de mandatos para suprimir una instancia de servicio, siga los pasos siguientes:
	  1. Desenlace la instancia de servicio de la app escribiendo `cf
unbind-service <nombre_app> <nombre_instancia_servicio>`.
	  2. Suprima la instancia de servicio escribiendo `cf delete-service <nombre_instancia_servicio>`.
	  3. Después de suprimir la instancia de servicio, vuelva a transferir la app a la cual estaba enlazada la instancia de servicio escribiendo `cf
restage <nombre_app>`.
  * Para eliminar el límite del número de instancias de servicios que tiene, convierta su cuenta de prueba en una cuenta de pago. Para obtener más información sobre cómo convertir su cuenta de prueba en una cuenta de pago, consulte [Cómo cambiar su plan](../pricing/index.html#changing){: new_window}.

  
  
## No se pueden ejecutar archivos ejecutables en {{site.data.keyword.Bluemix_notm}}
{: #ts_executable}

Es posible que no pueda ejecutar archivos ejecutables en {{site.data.keyword.Bluemix_notm}} si estos se han desarrollado y compilado en un entorno diferente. 

 

No puede ejecutar archivos ejecutables en {{site.data.keyword.Bluemix_notm}} si estos se han desarrollado y compilado en un entorno diferente.
{: tsSymptoms}

 

Si el contenido que quiere enviar a {{site.data.keyword.Bluemix_notm}} ya es un ejecutable, el contenido ya se habrá compilado previamente y no será necesario compilarlo en {{site.data.keyword.Bluemix_notm}}. En este caso, no se requiere ningún paquete de compilación para ejecutar el archivo ejecutable en {{site.data.keyword.Bluemix_notm}}. Sin embargo, debe indicar explícitamente a {{site.data.keyword.Bluemix_notm}} que no se requiere ningún paquete de compilación.
{: tsCauses}

 

Cuando envíe el archivo ejecutable a {{site.data.keyword.Bluemix_notm}},
debe especificar un paquete de compilación nulo, que indica que no se requiere ningún paquete de compilación. Especifique un paquete de compilación nulo mediante la opción **-b** con el mandato `cf push`:
{: tsResolve}

```
cf push appname -p <vía_acceso_app> -c <mandato_inicio> -b <null-buildpack>
```
Por ejemplo:
```
cf push appname -p <vía_acceso_app> -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```


## El límite memoria de la organización se ha excedido
{: #ts_outofmemory}

Si es usuario de una cuenta de prueba, es posible que no pueda desplegar una app en {{site.data.keyword.Bluemix_notm}} si ha excedido el límite de memoria de su organización. Puede reducir la memoria que utilizan las apps o aumentar la cuota de memoria de su cuenta. 



Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, verá el siguiente mensaje de error:
{: tsSymptoms} 

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

 

Este error se produce cuando la cantidad de memoria que queda para la organización es menos que la cantidad de memoria que la app que quiere desplegar necesita. El máximo de cuota de memoria para una cuenta de prueba es de 2 GB.
{: tsCauses}



Puede aumentar la cuota de memoria de su cuenta o reducir la memoria que utilizan las apps.
{: tsResolve} 

  * Para aumentar la cuota de memoria de su cuenta, convierta su cuenta de prueba en una cuenta de pago. Para obtener más información sobre cómo convertir su cuenta de prueba en una cuenta de pago, consulte [Cuentas de pago](../pricing/index.html#pay-accounts){: new_window}. 
  * Para reducir la memoria que utilizan las apps, utilice la interfaz de usuario de {{site.data.keyword.Bluemix_notm}} o la interfaz de línea de mandatos cf.
    Si utiliza la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, siga estos pasos:
	  1. En el Panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione la app. Se abre la página de detalles de la app.
	  2. En el panel tiempo de ejecución, puede reducir el límite máximo de memoria o el número de instancias de la app, o ambos, para la app que desee. 
	Si utiliza la interfaz de línea de mandatos cf, siga estos pasos:
	  1. Compruebe cuánta memoria están utilizando las apps:
	  ```
	  cf apps
	  ```
	     El mandato cf apps lista todas las apps desplegadas en el espacio actual. También se visualiza el estado de cada app.
      2. Para reducir la cantidad de memoria que utiliza la app, puede reducir el número de instancias de la app, el límite máximo de memoria o ambos:
	  ```
	  cf push <nombre_app> -p <vía_acceso_app> -i <número_instancia> -m <límite_memoria>
      ```
	  3. Reinicie la app para que se apliquen los cambios.



	  
## Las apps no se reinician automáticamente
{: #ts_apps_not_auto_restarted}


Una app no se reinicia automáticamente si el servicio que ha enlazado a la app deja de funcionar.	  
	  
 

Si se bloquea un servicio enlazado con una app, se pueden producir problemas como paradas, excepciones o intentos de reconexión. {{site.data.keyword.Bluemix_notm}} no reinicia automáticamente la aplicación para solucionar los problemas.
{: tsSymptoms}



Este comportamiento se debe al diseño de Cloud Foundry.
{: tsCauses} 

 

Puede reiniciar la app manualmente si escribe el mandato siguiente en la interfaz de línea de mandatos:
{: tsResolve}

```
cf push <nombre_app> -p <vía_acceso_app>
```
Además, puede codificar la app para identificar y recuperarse de problemas como paradas, excepciones o intentos de reconexión. 

	  

## Se pierden las variables definidas por el usuario al enviar por push una app
{: #ts_varsnotretained}

Al enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, se restablecen las variables especificadas, a menos que las guarde
en el archivo de manifiesto.



Las variables especificadas se pierden tras enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms} 


Las variables especificadas solo se guardan si las guarda
en el archivo de manifiesto.
{: tsCauses} 

 

Al enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, seleccione el recuadro de verificación **Guardar en el archivo de manifiesto** en la página Detalles de aplicación del asistente Aplicación. Posteriormente,
las variables especificadas
en el asistente
se guardan en el archivo de manifiesto de su app. La próxima vez que abra el asistente, las variables se visualizarán automáticamente.
{: tsResolve}



## {{site.data.keyword.Bluemix_notm}} Los iconos de Live Sync no se muestran
{: #ts_llz_lkb_3r}

Ha creado una app en IBM Bluemix DevOps Services, pero los iconos de IBM Bluemix Live Sync no se muestran en la Web IDE.

 

Al editar una app Node.js en DevOps Services Web IDE, los iconos de {{site.data.keyword.Bluemix_notm}} Live de editar, reinicio rápido y depurar no se muestran.
{: tsSymptoms}

 

Los iconos no están disponibles en estas circunstancias:
{: tsCauses}

  * El archivo `manifest.yml` no está guardado en el nivel superior del proyecto.
  * La app está almacenada en un subdirectorio en lugar de en el nivel superior del proyecto, pero la vía de acceso al subdirectorio no está especificada en el archivo `manifest.yml`.
  * La app no contiene un archivo `package.json`.


Utilice uno de los métodos siguientes para resolver el problema: 
{: tsResolve} 

  * Si el archivo `manifest.yml` no está almacenado en el nivel superior del proyecto, guárdelo aquí.
  * Si la app está almacenada en un subdirectorio, especifique la vía de acceso al subdirectorio en el archivo `manifest.yml`.
  ```
   path: vía_acceso_a_app
   ```
  * Cree un archivo `package.json` que esté en el directorio de la app.

  
  
  

  
  

  
  
## No se encuentran las organizaciones en {{site.data.keyword.Bluemix_notm}}
{: #ts_orgs}

Es posible que no encuentre su organización en {{site.data.keyword.Bluemix_notm}} al
trabajar en una región de {{site.data.keyword.Bluemix_notm}}.
  
 

Puede iniciar sesión correctamente en la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, pero no puede enviar por push apps utilizando la interfaz de línea de mandatos cf o el plug-in de Eclipse.
{: tsSymptoms}

Al intentar enviar por push una app
a {{site.data.keyword.Bluemix_notm}} utilizando
la interfaz de línea de mandatos cf, ve uno de los siguientes mensajes de error con el nombre de la organización especificado en el mensaje: 

`Error al buscar la organización`

`No se ha encontrado la organización`


Al intentar enviar por push una app
a {{site.data.keyword.Bluemix_notm}} utilizando
el plug-in de Eclipse de Cloud Foundry, ve el siguiente mensaje de error:

`No se ha encontrado cloudspace.`



Este problema se produce porque no se ha especificado el punto final API de la región
con la que desea trabajar, y la organización que está buscando
puede encontrarse en otra región.
{: tsCauses} 

   
  
Si envía por push su app a {{site.data.keyword.Bluemix_notm}} utilizando la interfaz de línea de mandatos cf, introduzca el mandato cf api y especifique el punto final API de la región. Por ejemplo, escriba el siguiente mandato para conectarse a la región {{site.data.keyword.Bluemix_notm}} de Europa - Reino Unido:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Si
envía por push su app a {{site.data.keyword.Bluemix_notm}} utilizando
las herramientas de Eclipse, primero debe crear un servidor de {{site.data.keyword.Bluemix_notm}}
y especificar el punto final API de la región de {{site.data.keyword.Bluemix_notm}}
en la que se ha creado su organización. Para obtener más información
sobre el uso de las herramientas de Eclipse, consulte [Despliegue de apps con IBM Eclipse Tools for Bluemix](../manageapps/eclipsetools/eclipsetools.html){: new_window}.  
  
  


## No se puede crear una ruta de app
{: #ts_hostistaken}

Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, no se puede crear la ruta de la app si el nombre de host especificado ya está en uso.



Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, verá el siguiente mensaje de error: 
{: tsSymptoms} 

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`



Este problema se produce si el nombre de host especificado
ya está en uso.
{: tsCauses} 


  
El nombre de host especificado debe ser exclusivo en el dominio
que está utilizando. Para especificar otro nombre de host debe utilizar uno de los siguientes métodos:
{: tsResolve} 

  * Si despliega su app utilizando el archivo `manifest.yml`, especifique el nombre de host en la opción host.	 
    ```
    host: <hostname>	
	```
  * Si despliega su app desde el indicador de mandatos, utilice el mandato `cf
push` con la opción **-n**. 
    ```
    cf push <nombre_app> -p <vía_acceso_app> -n <nombreHost>
    ```


## Una app WAR no se puede enviar mediante el mandato cf push
{: #ts_cf_war}

Es posible que no pueda utilizar el mandato cf push para desplegar una app web archivada a {{site.data.keyword.Bluemix_notm}} si la ubicación de la app no se especifica correctamente.
	


Si carga una app WAR en {{site.data.keyword.Bluemix_notm}} mediante el mandato `cf push`, verá el mensaje de error `Error de transferencia: no se pueden obtener instancias porque la transferencia ha fallado.`
{: tsSymptoms} 

 

Este problema puede suceder si no se especifica el archivo WAR o si no se especifica la vía de acceso al archivo WAR. 
{: tsCauses}

 	
	
Utilice la opción **-p** para especificar un archivo
WAR o añada la vía de acceso al archivo WAR. Por ejemplo:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
Para obtener más información sobre el mandato `cf push`, escriba `cf
push -h`. 	





## Los caracteres de doble byte no se visualizan correctamente cuando se envían apps Liberty a {{site.data.keyword.Bluemix_notm}} aplicaciones
{: #ts_doublebytes}

Es posible que los caracteres de doble byte no se visualicen correctamente si el soporte de Unicode no está configurado correctamente para el servlet o los archivos JSP.

 

Cuando se envía una app Liberty a {{site.data.keyword.Bluemix_notm}}, los caracteres de doble byte especificados dentro de la app no se visualizan correctamente.
{: tsSymptoms}

 

El problema puede ocurrir si el soporte de Unicode no está configurado correctamente para el servlet o los archivos JSP.
{: tsCauses}


Puede utilizar el código siguiente en el servlet o archivo JSP:
{: tsResolve} 

  * En el archivo de origen del servlet 
    ```
	response.setContentType("text/html; charset=UTF-8");
	```
  * En el JSP 
    ```
	<meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
	```
	
	
	

## No se pueden desplegar las apps Node.js
{: #ts_nodejs_deploy}

Es posible que detecte problemas si actualiza una app Node.js o despliega una
app Node.js en {{site.data.keyword.Bluemix_notm}}.



Si actualiza una app Node.js o despliega una
app Node.js en {{site.data.keyword.Bluemix_notm}}, es posible que reciba uno de los siguientes mensajes de error:
{: tsSymptoms} 

`Ningún paquete de compilación disponible ha detectado correctamente una app.`


`La instancia (índice 0) no ha podido empezar a aceptar conexiones.`


`No se pueden obtener instancias debido a un error de transferencia. `


 

A continuación se muestran posibles causas del problema:
{: tsCauses}
 
  * No se ha especificado el mandato start.
  * Faltan archivos necesarios para desplegar una app Node.js o bien se han colocado en una carpeta que no es el directorio raíz.
  


	
Emprenda una de las siguientes acciones en función de la causa del problema:
{: tsResolve} 

  * Especifique el mandato start siguiendo uno de estos métodos: 
      * Utilice la interfaz de línea de mandatos cf. Por ejemplo: 
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
	  * Utilice el archivo [package.json](https://docs.npmjs.com/json){: new_window}. Por ejemplo:
	    ```
		{
      ...
  	   "scripts": {
	 		 "start": "node app.js"
 	   }
	}
	    ```
	  * Utilice el archivo `manifest.yml`. Por ejemplo: 
	    ```
		applications:
  name: MyUniqueNodejs01
  ...
  command: node app.js
  ...
        ```

  * Asegúrese de que el archivo `package.json` exista en la app
Node.js para permitir que el paquete de compilación Node.js reconozca la app. Además, debe colocar este archivo en el directorio raíz de la app.	
    El ejemplo siguiente muestra un archivo `package.json` sencillo:  
	```
	{
        "name": "MyUniqueNodejs01",
        "version": "0.0.1",
        "description": "A sample package.json file",
        "dependencies": {
                "express": "3.4.x",
                "jade": "1.1.x"
        },
        "engines": {
                "node": "0.10.x"
        },
        "scripts": {
                  "start": "node app.js"
        }
 }
    ```
	
Para ver más sugerencias sobre las apps Node.js, consulte [Consejos para las apps Node.js](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html){: new_window}.	




## Aparecen errores de configuración en el archivo `server.xml` después de importar una app {{site.data.keyword.Bluemix_notm}} Liberty de Bluemix DevOps Services en Eclipse
{: #ts_eclipse}

Si ve errores de configuración en el archivo `server.xml` después de importar una app {{site.data.keyword.Bluemix_notm}} Liberty de IBM Bluemix DevOps Services en Eclipse, es posible que tenga que eliminar el archivo `server.xml` del proyecto. 

 

Después de importar una app {{site.data.keyword.Bluemix_notm}} Liberty de {{site.data.keyword.Bluemix_notm}} DevOps Services en Eclipse, verá errores de configuración en el archivo `server.xml` en la vista Problemas de Eclipse. 
{: tsSymptoms}

 

El paquete de compilación de Liberty utiliza el archivo `server.xml` para configurar la app y genera un archivo `runtime-vars.xml` cuando la app Liberty se envía a {{site.data.keyword.Bluemix_notm}}. Cuando importa la app en Eclipse, el archivo `runtime-vars.xml` no existe en el entorno local.
{: tsCauses}

 

Puede resolver este problema eliminando el archivo server.xml del proyecto. El paquete de compilación crea el archivo `server.xml` de forma dinámica cuando se envía la app como una aplicación WAR. Para obtener más información, consulte [Liberty for Java](../runtimes/liberty/index.html){: new_window}.
{: tsResolve}
	
	
## No se puede transferir una app mediante un paquete de compilación personalizado
{: #ts_bp_compilation}

Es posible que no pueda desplegar una app en {{site.data.keyword.Bluemix_notm}} utilizando un paquete de compilación personalizado si los scripts del paquete de compilación no son ejecutables.



Si despliega una app en {{site.data.keyword.Bluemix_notm}} utilizando un paquete de compilación personalizado, verá el mensaje de error `La app no se ha podido transferir, por lo que no hay instancias que mostrar.`
{: tsSymptoms} 


Este problema puede suceder si los scripts, como el script de detección, el script de compilación y el script de liberación, no son ejecutables.
{: tsCauses}

 

Puede utilizar el mandato [git
update](http://git-scm.com/docs/git-update-index){: new_window} para cambiar el permiso de cada script por ejecutable. Por ejemplo, puede escribir git update --chmod=+x script.sh.
{: tsResolve}
	
	
	
## Una app no se puede desplegar desde DevOps Services a {{site.data.keyword.Bluemix_notm}}
{: #ts_devops_to_bm}

Es posible que no pueda enviar por push la app de IBM Bluemix DevOps Services a {{site.data.keyword.Bluemix_notm}} si la app no contiene el archivo `manifest.yml`.

 

Cuando se despliega una app desde DevOps Services en {{site.data.keyword.Bluemix_notm}}, es posible que se visualice el mensaje de error `No se ha detectado ningún tipo de app soportado`.
{: tsSymptoms}

 

Este problema puede deberse a que DevOps Services necesita un archivo `manifest.yml` para desplegar una app en {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

 

Para solucionar este problema, debe crear un archivo `manifest.yml`. Para obtener más información sobre cómo crear un archivo `manifest.yml`, consulte [Manifiesto de la app](../manageapps/depapps.html#appmanifest){: new_window}.
{: tsResolve}	
	




## No se pueden enviar por push las apps de Meteor
{: #ts_meteor}

Es posible que no pueda enviar por push una app de Meteor a {{site.data.keyword.Bluemix_notm}} si no se ha especificado correctamente el paquete de compilación.

 

Al desplegar una app de Meteor en {{site.data.keyword.Bluemix_notm}}, es posible que vea el mensaje de error `La app no se ha podido transferir, por lo que no hay instancias que mostrar.`
{: tsSymptoms}


Este problema se produce porque no se ha proporcionado ningún paquete de compilación incorporado para las apps de Meteor. Debe utilizar un paquete de compilación personalizado.
{: tsCauses} 


 

Para utilizar un paquete de compilación personalizado para las apps de Meteor, debe utilizar uno de los siguientes métodos:
{: tsResolve}

  * Si despliega su app mediante el archivo `manifest.yml`, especifique el URL o el nombre del paquete de compilación personalizado mediante la opción buildpack. Por ejemplo:
  ```
  buildpack: https://github.com/Sing-Li/bluemix-bp-meteor 
  ```
  * Si despliega su app desde un indicador de mandatos, utilice el mandato `cf
push` y especifique el paquete de compilación personalizado mediante la opción
**-b**. Por ejemplo:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor 
	```
	
  

    
## El botón Desplegar en {{site.data.keyword.Bluemix_notm}} no despliega la app
{: #deploytobluemixbuttondoesntdeployanapp}

Si pulsa el botón Desplegar en {{site.data.keyword.Bluemix_notm}} y se encuentra con que el repositorio Git no está clonado o que la app no se ha desplegado, pruebe la resolución de problemas de los siguientes problemas.
  * [El proyecto Bluemix DevOps Services no se puede crear](#project-cannot-be-created)
  * [El repositorio Git no se encuentra y no se puede clonar en DevOps Services](#repo-not-found)
  * [El repositorio Git está clonado en DevOps Services, pero la app no se despliega en {{site.data.keyword.Bluemix_notm}}](#repo-cloned-app-not-deployed)
Para obtener más información sobre cómo crear el botón, consulte Creación del botón Desplegar en {{site.data.keyword.Bluemix_notm}}.

### El proyecto Bluemix DevOps Services no se puede crear
{: #project-cannot-be-created}

Si no se puede crear el proyecto DevOps Services, es posible que su cuenta de IBM {{site.data.keyword.Bluemix_notm}} haya caducado.



Pulsa el botón **Desplegar en Bluemix**, pero el paso "Creando proyecto" no se completa correctamente.
{: tsSymptoms} 


Es posible que su cuenta de {{site.data.keyword.Bluemix_notm}} haya caducado.
{: tsCauses} 

Utilice uno de los métodos siguientes para arreglar el problema:
{: tsResolve}

  * Inicie sesión en {{site.data.keyword.Bluemix_notm}} y actualice la información de cuenta.
  * Pulse el botón **Desplegar en Bluemix** de nuevo.


### El repositorio Git no se encuentra y no se puede clonar en DevOps Services
{: #repo-not-found}

Si se encuentra con que el repositorio Git no está clonando, es posible que haya algún problema con el repositorio o con el fragmento de código del botón.



Pulsa el botón **Desplegar en Bluemix**, pero el repositorio Git no se encuentra y no se puede clonar en DevOps Services. El paso "Clonando repositorio" no se completa correctamente. Por lo tanto, la app no se puede desplegar en {{site.data.keyword.Bluemix_notm}}. 
{: tsSymptoms} 

Este problema se podría producir por las siguientes razones:
{: tsCauses} 

  * Es posible que el repositorio Git no exista o no se pueda acceder a él.
  * Es posible que haya un problema en el HTML o el markdown del fragmento de código del botón.
  * Es posible que haya un problema y que los caracteres especiales, los parámetros de consulta o fragmentos del URL impidan que se pueda acceder al repositorio Git.

Utilice uno de los métodos siguientes para arreglar el problema:
{: tsResolve}

  * Compruebe que el repositorio Git exista, se pueda acceder públicamente y que el URL sea correcto.
  * Compruebe que el fragmento de código no contenga errores de HTML ni markdown.
  * Si hay caracteres especiales, parámetros de consulta o fragmentos que causan algún problema con el URL del repositorio Git, codifique el URL del fragmento de código del botón.
  

  
  
### El repositorio Git está clonado en DevOps Services, pero la app no se despliega en {{site.data.keyword.Bluemix_notm}}
{: #repo-cloned-app-not-deployed}

Si detecta que la app no se ha desplegado, es posible que haya algún problema con el código del repositorio.
     


Pulsa el botón **Desplegar en Bluemix** y el repositorio Git se clona en DevOps Services, pero la app no se despliega en {{site.data.keyword.Bluemix_notm}}. El paso "Desplegando en Bluemix" no se completa correctamente.
{: tsSymptoms} 

Este problema se podría producir por las siguientes razones:
{: tsCauses}  

  * Puede que no haya suficiente espacio en el espacio de {{site.data.keyword.Bluemix_notm}} para desplegar una app. 
  * Puede que un servicio necesario no se haya declarado en el archivo `manifest.yml`.
  * Puede que un servicio necesario se haya declarado en el archivo `manifest.yml`, pero que el servicio ya exista en el espacio de destino.
  * Puede que haya algún problema con el código del repositorio.
Para diagnosticar el problema, revise los registros de compilación y despliegue del despliegue:
  1. Cuando el paso "Desplegando en Bluemix" no se complete correctamente, pulse el enlace del paso anterior "Configurando el conducto" para abrir Delivery Pipeline.
  2. Identifique la compilación o la etapa de despliegue anómala.
  3. En la etapa anómala, pulse **Ver registros e historial**.
  4. Localice el mensaje de error.
   
Utilice uno de los métodos siguientes para arreglar el problema:
{: tsResolve}

  * Si el mensaje de error indica que no hay suficiente espacio en el espacio de {{site.data.keyword.Bluemix_notm}} para desplegar la app, seleccione otro espacio.
  * Si el mensaje de error indica que un servicio necesario no se ha declarado en el archivo `manifest.yml`, notifique al propietario del repositorio que se debe añadir el servicio.
  * Si el mensaje de error indica que un servicio necesario ya existe en el espacio de destino, seleccione un espacio diferente.
  * Si el mensaje de error indica que existe un problema con la compilación, solucione los problemas con el código que impiden que la app se compile. Para verificar que el código no contiene ningún problema, compile el código utilizando mandatos Git:
    1. Clone el repositorio Git:
    ```
    git clone <URL_repositorio_git>
    ```
	2. Abra el directorio de la app:
	```
	cd <appname>
	```
	3. Cree la app:
	```
	<appname> create
	```
	4. Si es necesario, suministre los complementos.
	5. Añada las variables de configuración que sean necesarias.
	6. Envíe el código:
	```
	git push <appname> master
	```
	7. Compruebe que la app se compile correctamente.
	8. Si es necesario, ejecute el mandato posterior al despliegue:
	```
	<appname> run
	```
	9. Abra la app y compruebe que funcione correctamente:
	```
	<appname> open
	```
	



# Resolución de problemas de gestión de cuentas
{: #managingaccounts}

Puede experimentar problemas con la gestión de la cuenta; por ejemplo si distintas
apps comparten el mismo nombre de dominio, los administradores que no pueden ver
todas las organizaciones. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}


## La cuenta está inactiva
{: #ts_accnt_inactive}

No puede crear una app en {{site.data.keyword.Bluemix_notm}} si la cuenta está inactiva. Debe ponerse en contacto con el equipo de soporte para solucionar este problema.



Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error:
{: tsSymptoms} 

`BXNUI0096E: La app no se ha creado. La cuenta está inactiva porque se ha cancelado o suspendido.`


El estado de la cuenta de {{site.data.keyword.Bluemix_notm}} pasa a ser inactivo si la cuenta se cancela o se suspende.
{: tsCauses}

 

Para volver a activar la cuenta, póngase en contacto con el soporte de [{{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport.com){: new_window}. En el correo incluya la siguiente información:
{: tsResolve}

  * El ID de IBM que utiliza para iniciar la sesión en {{site.data.keyword.Bluemix_notm}}.
  * El nombre de la organización en la que se está creando la app. Esta información puede ayudar al equipo de soporte a determinar si se le han asignado los roles o pertenencia a grupos correctos en la organización.



## No hay espacio asociado a la organización actual
{: #ts_no_space}

No puede crear una app si no hay ningún espacio asociado a la organización actual.



Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error:
{: tsSymptoms} 


`BXNUI0097E: Para poder añadir una app, al menos un espacio debe estar asociado con la organización y la región. En el Panel de control, pulse **Crear un espacio**. Cuando se cree el espacio, vuélvalo a intentar.`



Las aplicaciones de {{site.data.keyword.Bluemix_notm}} se deben crear dentro de un espacio de la organización.
{: tsCauses} 

 

Para crear un espacio, utilice uno de estos métodos: 
{: tsResolve}
 
  * En el Panel de control de {{site.data.keyword.Bluemix_notm}}, seleccione la organización en la que desea crear el espacio y pulse **Crear un espacio**.
  * En la interfaz de línea de mandatos cf, escriba ```cf create-space <nombre_espacio> -o <nombre_organización>```.
  
  
  
  
## Los nombres de dominio de distintas apps coinciden
{: #ts_domain_diff}

Puede que observe que varias apps comparten el mismo URL en {{site.data.keyword.Bluemix_notm}}.

 

Este problema puede producirse cuando se asigna la misma ruta de URL a distintas apps de un espacio.
{: tsCauses}

Por ejemplo, supongamos que envía la app myApp1 a {{site.data.keyword.Bluemix_notm}} y establece el dominio en "mynewapp.mybluemix.net". Luego envía otra app myApp2 al mismo espacio y establece una de sus rutas de URL en "mynewapp.mybluemix.net". Ahora la ruta está correlacionada a ambas apps.

 

Este es el comportamiento soportado de {{site.data.keyword.Bluemix_notm}} y puede utilizar este procedimiento para conseguir un tiempo de inactividad cero para la actualización de la app. Para obtener más información, consulte Despliegues Blue-Green.
{: tsResolve}
  
	
	





## La tarjeta de crédito no se puede agregar
{: #ts_addcc}

No puede enviar información de su tarjeta de crédito para convertir la cuenta de prueba en una cuenta de pago según uso.

 

El botón Enviar en la página Añadir tarjeta de crédito está inhabilitado.
{: tsSymptoms}

 

El problema se produce cuando no se ha rellenado la página Añadir tarjeta de crédito con información correcta.
{: tsCauses}

 

Complete los siguientes pasos para resolver este problema:
{: tsResolve}

  1. En la página Añadir tarjeta de crédito, rellene los campos necesarios de las secciones: información de contacto, dirección de contacto y dirección de facturación.
  2. Seleccione **He leído y acepto los términos y condiciones de IBM**, luego pulse **Enviar**. Se muestra la sección **Seleccionar un método de pago**.
  3. Introduzca el número de tarjeta de crédito, la fecha de caducidad y el código de seguridad de su tarjeta. Luego, pulse **Enviar**.





# Resolución de problemas de tiempos de ejecución
{: #runtimes}

Puede tener problemas al utilizar los tiempos de ejecución de IBM® Bluemix™. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}


## Se carga un paquete de compilación obsoleto de la memoria cuando una app se envía por push
{: #ts_loading_bp}


Es posible que no pueda utilizar los últimos componentes de paquete de compilación al enviar por push una app. Puede utilizar paquetes de compilación que tengan mecanismos incorporados para evitar que se carguen componentes obsoletos, o puede suprimir el contenido del directorio de memoria caché de la app antes de enviar por push o volver a transferir la app. 

 

Cuando se envía por push o se vuelve a transferir una app después de que se actualice el paquete de compilación, los componentes del paquete de compilación no se cargan automáticamente. Como resultado, la app utiliza los componentes obsoletos del paquete de compilación. Las actualizaciones que se hayan aplicado al paquete de compilación desde la última vez que haya enviado por push la app no se implementan. 
{: tsSymptoms}



Algunos paquetes de compilación no están configurados para descargar automáticamente todos los componentes actualizados de Internet para asegurarse de utilizar siempre la última versión.
{: tsCauses} 

 

Puede utilizar paquetes de compilación que tengan mecanismos incorporados para evitar que se carguen componentes obsoletos. Los siguientes paquetes de compilación son dos ejemplos: 
{: tsResolve}

  * [Paquete de compilación Java de Cloud Foundry](https://github.com/cloudfoundry/java-buildpack){: new_window}. Este paquete de compilación tiene un mecanismo incorporado para garantizar que se utiliza la versión más reciente del paquete de compilación. Para obtener más información sobre el funcionamiento de este mecanismo, consulte [extending-caches.md](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Paquete de compilación Node.js de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Este paquete de compilación tiene una funcionalidad similar utilizando variables de entorno. Para habilitar el paquete de compilación Node.js para descargar módulos de nodo de Internet cada vez, escriba el siguiente mandato en la interfaz de línea de mandatos cf. 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Si el paquete de compilación que utiliza no ofrece un mecanismo para cargar los últimos componentes automáticamente, puede suprimir manualmente el contenido del directorio de memoria caché y volver a enviar por push la app efectuando los siguientes pasos:
  1. Extraiga una rama de un paquete de compilación nulo como, por ejemplo, https://github.com/ryandotsmith/null-buildpack. Para obtener información sobre cómo extraer una rama, consulte [Conceptos básicos de Git - Obtención de un repositorio Git](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Añada la siguiente línea al archivo `null-buildpack/bin/compile` y confirme los cambios. Para obtener información sobre cómo confirmar cambios, consulte [Conceptos básicos sobre - Grabación de cambios en el repositorio](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
  ```
  rm -rfv $2/*
  ```
  3. Envíe por push la app con el paquete de compilación nulo que ha sido modificado para suprimir la memoria caché utilizando el siguiente mandato. Después de completar este paso, se suprimirá todo el contenido del directorio de memoria caché de su app.
  ```
  cf push appname -p app_path -b <modified_null_buildpack>
  ```
  4. Envíe por push la app con el último paquete de compilación que desee utilizar mediante el mandato siguiente: 
  ```
  cf push appname -p app_path -b <latest_buildpack>
  ```
  
	


## AVISO mensajes del paquete de compilación PHP
{: #ts_phplog}

Puede que vea mensajes que contengan AVISOS procedentes de los registros. Puede detener el registro de estos mensajes cambiando el nivel de registro.	
	
 

Al enviar por push una app a Bluemix utilizando un paquete de compilación PHP, es posible que vea mensajes que contengan `AVISOS`:
{: tsSymptoms}

```
• 2015-01-26T15:00:59.70+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: [pool www] 'user' directive is ignored when FPM is not running as root
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: fpm is running, pid 93
• 2015-01-26T15:01:00.63+0100 [App/0] ERR [26-Jan-2015 14:00:59] NOTICE: ready to handle connections
```



En el paquete de compilación PHP, el parámetro error_log se utiliza para definir el nivel de registro. De forma predeterminad, el valor del parámetro `error_log` es **stderr notice**. El ejemplo siguiente muestra la configuración del nivel de registro predeterminado del archivo `nginx-defaults.conf` del paquete de compilación PHP que proporcionado por Cloud Foundry. Para obtener más información, consulte [cloudfoundry/php-buildpack](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
{: tsCauses} 

```
daemon off;
error_log stderr notice;
pid @{HOME}/nginx/logs/nginx.pid;
```

 	
	
Los mensajes tipo `AVISO` son informativos y no indican necesariamente que se haya producido un problema. Puede detener el registro de estos mensajes cambiando el nivel de registro de stderr notice a stderr
error en el archivo nginx-defaults.conf del paquete de compilación. Por ejemplo: 	
{: tsResolve}

```
daemon off;
error_log stderr error;
pid @{HOME}/nginx/logs/nginx.pid;
```
Para obtener más información sobre cómo cambiar la configuración de registro, consulte [error_log](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## No se puede importar una biblioteca Python de terceros en {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Es posible que no pueda importar una biblioteca Python de terceros en {{site.data.keyword.Bluemix_notm}}. Puede solucionar el problema añadiendo archivos de configuración al directorio raíz de su app Python.


Cuando intenta importar una biblioteca Python de terceros, como por ejemplo la biblioteca `web.py`, el mandato `cf push` falla.
{: tsSymptoms}


 

Este problema se produce cuando falta la información de configuración de la app Python.
{: tsCauses}


 

Para solucionar el problema, añada un archivo `requirements.txt` y un archivo `Procfile` al directorio raíz de la app Python. La información siguiente da por supuesto que está importando una biblioteca web.py:
{: tsResolve}

  1. Añada un archivo `requirements.txt` al directorio raíz de la app Python.
     El archivo `requirements.txt` especifica los paquetes de la biblioteca que la app Python requiere y la versión de los paquetes. El ejemplo siguiente muestra el contenido del archivo `requirements.txt`, donde `web.py==0.37` indica que la versión de la biblioteca `web.py` que se descargará es la 0.37, y `wsgiref==0.1.2` indica que la versión de la interfaz de la pasarela del servidor web que la biblioteca web.py requiere es la 0.1.2.
	 ```
	 web.py==0.37
     wsgiref==0.1.2
	 ```
	Para obtener más información sobre cómo configurar el archivo `requirements.txt`, consulte [Archivos de requisitos](https://pip.readthedocs.org/en/1.1/requirements.html). 
	 
  2. Añada un archivo `Procfile` al directorio raíz de la app Python.
	El archivo `Procfile` debe contener el mandato de inicio de la app Python. En el mandato siguiente, *nombreapp* es el nombre de la app Python, y *PUERTO* es el número de puerto que la app Python debe utilizar para recibir solicitudes de los usuarios de la app. *$PORT* es opcional. Si no especifica PUERTO en el mandato de inicio, se utilizará el número de puerto bajo la variable de entorno `VCAP_APP_PORT` de la app. 
	```
	web: python <nombreapp>.py $PORT
	```
Ahora puede importar una biblioteca Python de terceros en {{site.data.keyword.Bluemix_notm}}.	



## El botón Acciones de la página Detalles de la instancia está inhabilitado
{: #ts_actionsbutton}



El botón Acciones de la página Detalles de la instancia está inhabilitado.
{: tsSymptoms} 

 

Este problema se produce por las siguientes razones:
{: tsCauses}

  * La app no es una app web Java™. Runtime Management Utilities (RMU) solo da soporte a las apps web que se despliegan con paquetes de
compilación Liberty.
  * La app no se ha desplegada con el paquete de compilación Liberty integrado.
  * La app se ha desplegado con una versión anterior del paquete de compilación de Liberty.



Si el problema se debe a una versión anterior del paquete de compilación de Liberty, vuelva a desplegar la app en {{site.data.keyword.Bluemix_notm}}. De lo contrario, puede proporcionar los siguientes archivos de registro de la app del cliente al equipo de soporte:
{: tsResolve} 

  * logs/messages.log
  * logs/stdout.log
  * logs/stderr.log
  

  
  
## Se necesitan credenciales al abrir la ventana de rastreo o de volcado
{: #ts_username}


 

Se necesita un nombre de usuario y una contraseña al abrir la ventana de rastreo y volcado.
{: tsSymptoms}

 

Este problema se produce debido al tiempo de espera excedido de inicio de sesión.
{: tsCauses}

 

La solución es volver a especificar el nombre de usuario y la contraseña.
{: tsResolve}




## Los errores se producen al ejecutar operaciones de rastreo o de volcado
{: #ts_target}

 

Se muestra un mensaje de error mientras se están ejecutando las operaciones de rastreo o volcado. El mensaje indica que una instancia de destino de una app no está en ejecución:	
{: tsSymptoms}

```
Instancia 0: la especificación de rastreo se ha establecido correctamente
Instancia 2: la especificación de rastreo se ha establecido correctamente
Instancia 1: la instancia de destino 1 para la app abcd no se encuentra en el estado de ejecución.
Instancia 3: la especificación de rastreo se ha establecido correctamente
Instancia 4: la especificación de rastreo se ha establecido correctamente
```



Este problema se produce por las siguientes razones:
{: tsCauses} 

  * Las funciones de gestión de rastreo o de volcado son sólo para las instancias de apps que se están ejecutando. No se pueden utilizar operaciones de rastreo o de volcado en instancias de apps que se han detenido, se están iniciando o se han interrumpido.
  * El estado de la instancia de app cambia cuando se abre el diálogo de rastreo o de volcado. 
  


La solución consiste en cerrar la ventana y en volverla a abrir.
{: tsResolve} 



## Las instancias tienen distinta configuración de traceSpecification
{: #ts_different_config}

 

Para distintas instancias de una app, es posible que vea distinta configuración de traceSpecification.
{: tsSymptoms}

 

Este problema se produce por las siguientes razones:
{: tsCauses}

  * Es posible que haya cambiado anteriormente la configuración para una o varias de las instancias. Si cambia la configuración de traceSpecification para una instancia, no se aplica a otras instancias de la misma app. Por ejemplo, la app utiliza log4j y tiene 2 instancias para esta app. Puede cambiar el nivel de registro de la instancia 0 desde info para depurar, pero el nivel de registro de la instancia 1 permanece en info. 
  * La app escala y tiene nuevas instancias. RMU no aplica la configuración de traceSpecification de la instancia existente a la instancia nueva y escalada. La nueva instancia utiliza la configuración predeterminada. Por ejemplo, la app utiliza log4j y tiene una instancia. Puede cambiar el nivel de registro de esta instancia de info a debug. Una vez que realice este cambio, si escala la app en dos instancias, el nivel de registro de la nueva instancia es info, en lugar de debug (depurar).
  


Este comportamiento es el esperado.
{: tsResolve} 





## Cuota de disco excedida
{: #ts_diskquota}

Es posible que en el registro de app vea que se ha superado la cuota de disco.

 

Verá el mensaje de error `Cuota de disco excedida` en el registro de la app.
{: tsSymptoms}



Este problema se produce por una de las siguientes razones: 
{: tsCauses} 

  * Los archivos de volcado se generan con las instancias de la app que se está ejecutando y los archivos utilizan gran parte de la cuota de disco asignada. De forma predeterminada, la cuota de disco para una instancia de app es 1 GB. Puede comprobar el uso de disco
pulsando **Panel de control>Aplicación>Tiempo de ejecución de app**. En el siguiente ejemplo se muestra la información de tiempo de ejecución,
incluido el uso de disco, para dos instancias de una app:
    ```
    Instance	State	CPU	Memory Usage	Disk Usage

	0		Running	1.0%	344.8MB/512MB	236.8MB/1GB
	2		Running	2.3%	361.2MB/512MB	235.7MB/1GB
    ```
  * La cuota de disco está limitada por la cuota actual de la organización.
  
  


Puede solucionar este problema con uno de estos métodos:
{: tsResolve} 

  * Suprima los archivos de volcado después de descargarlos.
  * Vuelva a desplegar la app con una cuota de disco mayor, incluyendo la entrada siguiente en el manifiesto de despliegue:
    ```
	disk_quota: 2048
	```
	
	


