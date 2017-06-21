---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-10"

---

{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}





# Resolución de problemas de gestión de apps
{: #managingapps}


Entre los problemas generales relacionados con la gestión de apps se pueden incluir las apps que no se pueden actualizar y los caracteres de doble byte que no se visualizan. En muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}


## Hay cambios sin guardar
{: #ts_unsaved_changes}

Al navegar en la página de detalles de apps, es posible que no pueda realizar las acciones y es posible que se le solicite que guarde los cambios para poder continuar.

Cuando intente comprobar la app o los servicios en la página de detalles de la app, seguirá recibiendo el siguiente mensaje de error:
{: tsSymptoms}

`Hay cambios sin guardar en la página app_name. Guarde o cancele los cambios.`

Cuando desplace el ratón sobre el campo **INSTANCIAS** o **CUOTA DE MEMORIA** del panel de tiempo de ejecución, los valores cambiarán. Este comportamiento es mediante diseño; sin embargo, el mensaje de error le solicitará que guarde los valores de instancia o de memoria para poder navegar fuera de la página.
{: tsCauses}

Cierre la ventana de mensajes y, a continuación, pulse el botón **RESTABLECER** en el panel de tiempo de ejecución.
{: tsResolve}

## La migración tras error automática entre regiones de Bluemix no está disponible
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
nslookup stage1.mybluemix.net
```

## No se pueden conmutar apps a la modalidad de depuración
{: #ts_debug}

Es posible que no pueda habilitar la modalidad de depuración si la versión de la máquina virtual Java (JVM) es 8 o inferior.

Después de seleccionar **Habilitar depuración de aplicación**, las herramientas intentan conmutar la app a la modalidad de depuración. A continuación, el entorno de trabajo de Eclipse empieza una sesión de depuración. Cuando las herramientas habilitan satisfactoriamente la modalidad de depuración, el estado de la aplicación web visualiza `Modalidad de actualización`, `Desarrollo` y `Depuración`.
{: tsSymptoms}

Sin embargo, cuando las herramientas no pueden habilitar la modalidad de depuración, el estado de aplicación web visualiza solamente `Modalidad de actualización` y `Desarrollo`, pero no muestra `Depuración`. Las herramientas también pueden visualizar el siguiente mensaje de error en la vista de consola:

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

Las siguientes versiones de JVM (Java Virtual Machine) no pueden establecer una sesión de depuración: IBM JVM 7, IBM JVM 8 y versiones anteriores de Oracle JVM 8.
{: tsCauses}

Si la JVM del entorno de trabajo es de una de estas versiones, es posible que tenga problemas al crear una sesión de depuración. La versión de JVM del entorno de trabajo es normalmente la JVM del sistema local. La JVM del sistema no es la misma que la JVM de la aplicación {{site.data.keyword.Bluemix_notm}} Java&trade;. La aplicación {{site.data.keyword.Bluemix_notm}} Java casi siempre se ejecuta en IBM JVM, y algunas veces se ejecuta en OpenJDK JVM.

Para comprobar la versión de Java que ejecuta {{site.data.keyword.eclipsetoolsfull}}, siga los siguientes pasos:
{: tsResolve}

  1. En IBM Eclipse Tools for Bluemix, seleccione **Ayuda** > **Acerca de Eclipse** > **Detalles de instalación** > **Configuración**.
  2. Busque la propiedad `eclipse.vm` en la lista. La siguiente línea muestra un ejemplo de una propiedad `eclipse.vm`:

	```
	eclipse.vm=C:\Archivos de programa\IBM\ibm-java-sdk-80-win-x86_64\bin\..\jre\bin\j9vm\jvm.dll
	```

  3. En la línea de mandatos, escriba `java -version` desde el directorio `bin` de la instalación Java. Se visualiza la información de la versión de IBM JVM.

Si la JVM del entorno de trabajos de IBM es IBM JVM 7 u 8, o una versión anterior de Oracle JVM 8, complete los siguientes pasos para conmutar a Oracle JVM 8:

  1. Descargue y, a continuación, vuelva a instalar Oracle JVM 8, consulte [Java SE Downloads ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://www.oracle.com/technetwork/java/javase/downloads/index.html){: new_window} para obtener detalles.
  2. Reinicie Eclipse.
  3. Compruebe si la propiedad `eclipse.vm` apunta a la nueva instalación de Oracle JVM 8.


## No se pueden reutilizar los nombres de apps suprimidas
{: #ts_reuse_appname}

Tras suprimir una app, puede reutilizar el nombre de la app solo después de suprimir la ruta de la app.

Al intentar reutilizar el nombre de la app, recibirá el mensaje siguiente:
{: tsSymptoms}

`El nombre ya está siendo utilizado por otra app.`

Cuando se suprime una app, su ruta, que es el URL de la app, no se suprime automáticamente. Por lo tanto, no está disponible para su reutilización. Debe acceder al espacio donde se ha creado la app para suprimir la ruta, de manera que se pueda reutilizar.
{: tsCauses}

Siga los pasos siguientes para suprimir una ruta no utilizada:
{: tsResolve}

  1. Compruebe si la ruta pertenece al espacio actual especificando el mandato siguiente:
     ```
	 cf routes
	 ```
  2. Si la ruta no pertenece al espacio actual, cambie al espacio u organización a la que pertenezca especificando el mandato siguiente:
     ```
	 cf target -o nombre_org -s nombre_espacio
	 ```
  3. Suprima la ruta de la app especificando el mandato siguiente:
     ```
	 cf delete-route nombre_dominio -n nombre_host
	 ```
	 Por ejemplo:
	 ```
	 cf delete-route mybluemix.net -n app001
	 ```

## No se pueden recuperar espacios en la organización
{: #ts_retrieve_space}

No puede crear una app o un servicio si la organización actual no tiene un espacio asociado al mismo.

Cuando intenta crear una app en Bluemix, ve el siguiente mensaje de error:
{: tsSymptoms}

`BXNUI0515E: Los espacios de la organización no se han recuperado. Se ha producido un problema de conexión de red, o la organización actual no tiene un espacio asociado al mismo.`

Este error se suele producir la primera vez que se intenta crear una app o un servicio desde el catálogo cuando aún no se ha creado un espacio.
{: tsCauses}

Asegúrese de haber creado un espacio en la organización actual. Para crear un espacio, utilice uno de estos métodos:
{: tsResolve}

  * Desde la barra de menús, pulse **Gestionar > Cuenta > Organizaciones**. Seleccione la organización en la que desea crear el espacio y pulse **Crear un espacio**.
  * En la interfaz de línea de mandatos cf, escriba `cf create-space <nombre_espacio> -o <nombre_organización>`.

Inténtelo de nuevo. Si vuelve a ver este mensaje, vaya a la página [Estado de Bluemix ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://ibm.biz/bluemixstatus){: new_window} para comprobar si el servicio o el componente tienen algún problema.


## No se pueden realizar las acciones solicitadas
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
 * Pida al gestor de la organización que le cambie el rol a desarrollador o que cree un espacio y le asigne un rol de desarrollador. Consulte [Gestión de organizaciones y espacios](/docs/admin/orgs_spaces.html) para obtener detalles.

## No se puede acceder a los servicios de Bluemix debido a errores de autorización
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
Para obtener más información sobre los mandatos que puede utilizar en otros lenguajes de programación, consulte [Java ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://docs.run.pivotal.io/buildpacks/java/java-tips.html#env-var){: new_window} y [Ruby ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://docs.run.pivotal.io/buildpacks/ruby/ruby-tips.html#env-var){: new_window}.


## No se pueden desplegar apps utilizando IBM Eclipse Tools for Bluemix
{: #ts_bm_tools_facet}

Cuando se aplica una faceta no soportada en el proyecto de Eclipse, no podrá desplegar las apps en {{site.data.keyword.Bluemix_notm}} utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.

Puede desplegar correctamente la app en {{site.data.keyword.Bluemix_notm}} con la CLI de Cloud Foundry. Sin embargo, no puede desplegar la app en {{site.data.keyword.Bluemix_notm}} utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} y verá el mensaje de error: `No se admite la faceta de proyecto <nombre_faceta>.` Por ejemplo:
{: tsSymptoms}
`No se da soporte a la faceta de proyecto de la aplicación autónoma de Cloud Foundry versión 1.0.`

IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} asignan proyectos a los tiempos de ejecución de {{site.data.keyword.Bluemix_notm}} mediante facetas de proyectos. Las facetas definen los requisitos de los proyectos de Java EE en Eclipse y se utilizan como parte de la configuración de tiempo de ejecución de modo que los diferentes tiempos de ejecución estén asociados a diferentes proyectos. Si IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}} no da soporte a la faceta que se aplica al proyecto, no se podrá desplegar la app utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsCauses}

Debe eliminar la faceta del proyecto de Eclipse para poder desplegar la app utilizando IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
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

Si cree que algún servicio de {{site.data.keyword.Bluemix_notm}} no está disponible, compruebe primero la página [Estado de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://ibm.biz/bluemixstatus){: new_window}. Como método alternativo puede utilizar el servicio en otra región de {{site.data.keyword.Bluemix_notm}}. Encontrará información detallada en [Utilización de servicios en otra región![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/services/reqnsi.html#cross_region_service){: new_window}. Si el estado del servicio es normal, pruebe los pasos siguientes para resolver el problema:
{: tsResolve}

  * Reintente la acción:
    * Recargue la página pulsando F5 en el teclado o pulsando el botón de renovación. Si este paso no funciona, borre las cookies y la memoria caché del navegador y recargue de nuevo.
    * Utilice otro navegador.
    * Rearranque el direccionador, el módem y el sistema. Rearrancar estos dispositivos puede borrar varios errores que provocan el error 502.
  * Espere y vuelva a intentarlo más adelante. En algunas instancias, pueden ocurrir problemas temporales en el proveedor de servicios de Internet o en los servicios de {{site.data.keyword.Bluemix_notm}}. Puede esperar a que se resuelvan los problemas temporales.
  * Si el problema todavía existe, póngase en contacto con el equipo de soporte de {{site.data.keyword.Bluemix_notm}}. Consulte [Cómo ponerse en contacto con el equipo de soporte de {{site.data.keyword.Bluemix_notm}} ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](/docs/support/index.html#contacting-bluemix-support){: new_window} para obtener más información.

## Se ha excedido la cuota de disco
{: #ts_disk_quota}

Si se agota el espacio en disco, puede modificar manualmente la cuota de disco para obtener más espacio en disco.

Cuando se agota el espacio en disco, puede que vea un mensaje que indica que se ha superado la cuota de disco. Para resolver el problema, quizá haya intentado aumentar la escala de la instancia de la app para obtener más espacio de disco. Por ejemplo, cambiar la escala de 256 MB a 1256 MB modificando la cuota de memoria en la página de detalles de la app. Sin embargo, puesto que la cuota de disco no se ha modificado, no ha obtenido más espacio de disco.
{: tsSymptoms}

La cuota de disco predeterminada que se asigna para una app es de 1 GB. Si necesita más espacio de disco, debe indicar manualmente la cuota de disco.
{: tsCauses}

Utilice uno de estos métodos para especificar la cuota de disco. La cuota de disco máxima que puede especificar es de 2 GB. Si 2 GB todavía no es suficiente, pruebe un servicio externo, como [Object Store](/docs/services/ObjectStorage/index.html).
{: tsResolve}

  * En el archivo manifest.yml, añada el elemento siguiente:
    ```
	disk_quota: <disk_quota>
	```
  * Utilice la opción **-k** con el mandato `cf push` cuando envíe la app por push a {{site.data.keyword.Bluemix_notm}}:
    ```
	cf push appname -p app_path -k <cuota de disco>
	```


## Las apps de Android no pueden recibir {{site.data.keyword.mobilepushshort}}
{: #ts_push}

En determinadas regiones en las que no se puede acceder a Google, las apps de Android no pueden recibir notificaciones enviadas a través del servicio IBM {{site.data.keyword.mobilepushshort}}. En este caso, un método alternativo consiste en utilizar servicios de terceros.

Enlaza un servicio {{site.data.keyword.mobilepushshort}} con la app de Bluemix y envía un mensaje a los dispositivos registrados. No obstante, las apps que se desarrollan en la plataforma Android no pueden recibir notificaciones en determinadas regiones.
{: tsSymptoms}

El servicio IBM {{site.data.keyword.mobilepushshort}} utiliza Google Cloud Messaging (GCM) para enviar notificaciones a apps móviles desarrolladas en la plataforma Android. Para permitir que las apps de Android reciban notificaciones, se debe poder acceder al servicio Google Cloud Messaging (GCM) en las apps móviles. En regiones en las que las apps Android no pueden acceder al servicio GCM, las apps Android no pueden recibir {{site.data.keyword.mobilepushshort}}.
{: tsCauses}

Como método alternativo, utilice servicios de tercero que no se basen en el servicio GCM, como por ejemplo [Pushy ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://pushy.me){: new_window}, [igetui ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://www.getui.com/){: new_window} y [jpush ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://www.jpush.cn/){: new_window}.
{: tsResolve}


## El límite de servicios de la organización se ha excedido
{: #ts_servicelimit}

Si es usuario de una cuenta de prueba, es posible que no pueda crear una app en {{site.data.keyword.Bluemix_notm}} si ha excedido el límite de servicios de su organización.

Cuando intenta crear una app en {{site.data.keyword.Bluemix_notm}}, ve el siguiente mensaje de error:
{: tsSymptoms}

`BXNUI2032E: No se ha creado el recurso <instancias_servicio>. Mientras se estaba contactando con Cloud Foundry para crear el recurso, se ha producido un error. Mensaje de Cloud Foundry: "Ha excedido el límite de servicios de su organización."`

Este error se produce cuando se excede el límite de número de instancias del servicio que puede tener para su cuenta. El número máximo de número de instancias del servicio para una cuenta de prueba es 10.
{: tsCauses}

Suprima las instancias del servicio que no sean necesarias o elimine el límite de número de instancias del servicio que tiene.
{: tsResolve}

  * Para suprimir una instancia del servicio, puede utilizar la consola de {{site.data.keyword.Bluemix_notm}} o la interfaz de la línea de mandatos.

    Para utilizar la consola de {{site.data.keyword.Bluemix_notm}} para suprimir una instancia de servicio, siga estos pasos:
	  1. En el panel de control Servicios, pulse el menú **Acciones** para el servicio que desea suprimir.
	  2. Pulse **Suprimir servicio**. Se le solicitará que cambie las etapas de la app a la que está vinculada la instancia de servicio.

    Para utilizar la interfaz de línea de mandatos para suprimir una instancia de servicio, siga los pasos siguientes:
	  1. Desenlace la instancia de servicio de la app escribiendo `cf unbind-service <nombre_app> <nombre_instancia_servicio>`.
	  2. Suprima la instancia de servicio escribiendo `cf delete-service <nombre_instancia_servicio>`.
	  3. Después de suprimir la instancia de servicio, vuelva a transferir la app a la cual estaba enlazada la instancia de servicio escribiendo `cf restage <nombre_app>`.

  * Para eliminar el límite del número de instancias de servicios que tiene, convierta su cuenta de prueba en una cuenta de pago. Para obtener más información sobre cómo convertir su cuenta de prueba en una cuenta de pago, consulte [Cómo cambiar su plan](/docs/pricing/index.html#changing).

## Los ejecutables no se pueden ejecutar en Bluemix
{: #ts_executable}

Es posible que no pueda ejecutar archivos ejecutables en {{site.data.keyword.Bluemix_notm}} si estos se han desarrollado y compilado en un entorno diferente.

No puede ejecutar archivos ejecutables en {{site.data.keyword.Bluemix_notm}} si se han desarrollado y compilado en otro entorno.
{: tsSymptoms}

Si el contenido que quiere enviar a {{site.data.keyword.Bluemix_notm}} ya es un ejecutable, el contenido ya se habrá compilado previamente y no será necesario compilarlo en {{site.data.keyword.Bluemix_notm}}. En este caso, no se requiere ningún paquete de compilación para ejecutar el archivo ejecutable en {{site.data.keyword.Bluemix_notm}}. Sin embargo, debe indicar explícitamente a {{site.data.keyword.Bluemix_notm}} que no se requiere ningún paquete de compilación.
{: tsCauses}

Cuando envíe el archivo ejecutable a {{site.data.keyword.Bluemix_notm}}, debe especificar un paquete de compilación nulo, que indica que no se requiere ningún paquete de compilación. Especifique un paquete de compilación nulo mediante la opción **-b** con el mandato `cf push`:
{: tsResolve}

```
cf push appname -p app_path -c <start_command> -b <null-buildpack>
```
Por ejemplo:
```
cf push appname -p app_path -c ./RunMeNow -b https://github.com/ryandotsmith/null-buildpack
```

## El límite memoria de la organización se ha excedido
{: #ts_outofmemory}

Si es usuario de una cuenta de prueba, es posible que no pueda desplegar una app en {{site.data.keyword.Bluemix_notm}} si ha excedido el límite de memoria de su organización. Puede reducir la memoria que utilizan las apps o aumentar la cuota de memoria de su cuenta. El máximo de cuota de memoria para una cuenta de prueba es de 2 GB y únicamente se puede incrementar pasando a una cuenta de pago.

Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, verá el siguiente mensaje de error:
{: tsSymptoms}

`FAILED Server error, status code: 400, error code: 100005, message: You have exceeded your organization's memory limit.`

Este error se produce cuando la cantidad de memoria que queda para la organización es menos que la cantidad de memoria que la app que quiere desplegar necesita. El máximo de cuota de memoria para una cuenta de prueba es de 2 GB.
{: tsCauses}

Puede aumentar la cuota de memoria de su cuenta o reducir la memoria que utilizan las apps.
{: tsResolve}

  * Para aumentar la cuota de memoria de su cuenta, convierta su cuenta de prueba en una cuenta de pago. Para obtener más información sobre cómo convertir su cuenta de prueba en una cuenta de pago, consulte [Cuentas de pago](/docs/pricing/index.html#pay-accounts).
  * Para reducir la memoria que utilizan las apps, utilice la consola de {{site.data.keyword.Bluemix_notm}} o la interfaz de línea de mandatos cf.

    Si utiliza la consola de {{site.data.keyword.Bluemix_notm}}, siga estos pasos:

    1. En el panel de control Apps, seleccione su app. Se abre la página de detalles de la app.
    2. En el panel tiempo de ejecución, puede reducir el límite máximo de memoria o el número de instancias de la app, o ambos, para la app que desee.

    Si utiliza la interfaz de línea de mandatos cf, siga estos pasos:

    1. Compruebe cuánta memoria están utilizando las apps:

	  ```
	  cf apps
	  ```

	  El mandato cf apps lista todas las apps desplegadas en el espacio actual. También se visualiza el estado de cada app.

    2. Para reducir la cantidad de memoria que utiliza la app, puede reducir el número de instancias de la app, el límite máximo de memoria o ambos:

	  ```
	  cf push appname -p vía_acceso_app -i número_instancia -m límite_memoria
      ```

    3. Reinicie la app para que se apliquen los cambios.


## Las apps no se reinician automáticamente
{: #ts_apps_not_auto_restarted}

Una app no se reinicia automáticamente si el servicio que ha enlazado a la app deja de funcionar.	  

Si se bloquea un servicio enlazado con una app, se pueden producir problemas en la app como paradas, excepciones o intentos de reconexión. {{site.data.keyword.Bluemix_notm}} no reinicia automáticamente la app para solucionar los problemas.
{: tsSymptoms}

Este comportamiento se debe al diseño de Cloud Foundry.
{: tsCauses}

Puede reiniciar la app manualmente si escribe el mandato siguiente en la interfaz de línea de mandatos:
{: tsResolve}

```
cf push appname -p app_path
```
Además, puede codificar la app para identificar y recuperarse de problemas como paradas, excepciones o intentos de reconexión.

## Se pierden las variables definidas por el usuario al enviar por push una app
{: #ts_varsnotretained}

Al enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, se restablecen las variables especificadas, a menos que las guarde en el archivo de manifiesto.

Las variables especificadas se pierden tras enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}.
{: tsSymptoms}

Las variables especificadas solo se guardan si las guarda en el archivo de manifiesto.
{: tsCauses}

Al enviar por push una app a {{site.data.keyword.Bluemix_notm}} desde IBM Eclipse Tools for {{site.data.keyword.Bluemix_notm}}, seleccione el recuadro de verificación **Guardar en el archivo de manifiesto** en la página Detalles de aplicación del asistente Aplicación. Posteriormente, las variables especificadas en el asistente se guardan en el archivo de manifiesto de su app. La próxima vez que abra el asistente, las variables se visualizarán automáticamente.
{: tsResolve}

<!-- begin STAGING ONLY -->

## Bluemix Live Sync Debug no se inicia desde la línea de mandatos
{: #ts_no_debug}

Ha habilitado la característica IBM Bluemix Live Sync Debug para su app utilizando la línea de mandatos, pero no puede acceder a la interfaz de Debug.  

Debería habilitar la característica de depuración de su app configurando la variable de entono **BLUEMIX_APP_MGMT_ENABLE**. No obstante, no puede acceder a la interfaz de usuario de Debug en `app_url/bluemix-debug/manage`.
{: tsSymptoms}

La característica Debug no se puede habilitar en estas situaciones:
{: tsCauses}

  * Cuando `manifest.yml` contiene el atributo command.
  * Cuando utiliza la opción **-c** para enviar por push la app a {{site.data.keyword.Bluemix_notm}}

Utilice una de las siguientes opciones para resolver este problema:
{: tsResolve}

  * La práctica recomendada es utilizar el paquete de compilación IBM Node.js para iniciar la app. Para obtener más información, consulte la sección del mandato Startup del tema [Desplegar una aplicación Node.js en {{site.data.keyword.Bluemix_notm}}](/docs/runtimes/nodejs/index.html#nodejs_runtime).
  * Inhabilite el mandato para su app existente revisando el atributo command en su archivo `manifest.yml` para command: nulo o editándolo para que el mandato push incluya `-c null`.
  * Elimine el atributo **command** de `manifest.yml`. A continuación suprima la app actual de {{site.data.keyword.Bluemix_notm}} y envíe por push la app de nuevo.

<!-- end STAGING ONLY -->  


## No se pueden encontrar organizaciones en Bluemix
{: #ts_orgs}

Es posible que no encuentre su organización en {{site.data.keyword.Bluemix_notm}} al trabajar en una región de {{site.data.keyword.Bluemix_notm}}.

Puede iniciar sesión correctamente en la consola de {{site.data.keyword.Bluemix_notm}}, pero no puede enviar por push apps utilizando la interfaz de línea de mandatos cf o el plug-in de Eclipse.
{: tsSymptoms}

Al intentar enviar por push una app a {{site.data.keyword.Bluemix_notm}} utilizando la interfaz de línea de mandatos cf, ve uno de los siguientes mensajes de error con el nombre de la organización especificado en el mensaje:

`Error al buscar la organización`

`No se ha encontrado la organización`

Al intentar enviar por push una app a {{site.data.keyword.Bluemix_notm}} utilizando el plug-in de Eclipse de Cloud Foundry, ve el siguiente mensaje de error:

`No se ha encontrado cloudspace.`

Este problema se produce porque no se ha especificado el punto final de la API de la región con la que desea trabajar, y la organización que está buscando puede encontrarse en otra región.
{: tsCauses}

Si envía por push su app a {{site.data.keyword.Bluemix_notm}} utilizando la interfaz de línea de mandatos cf, introduzca el mandato cf api y especifique el punto final API de la región. Por ejemplo, escriba el siguiente mandato para conectarse a la región {{site.data.keyword.Bluemix_notm}} de Europa - Reino Unido:
{: tsResolve}

```
cf api https://api.eu-gb.bluemix.net
```
Si envía por push su app a {{site.data.keyword.Bluemix_notm}} utilizando las herramientas de Eclipse, primero debe crear un servidor de {{site.data.keyword.Bluemix_notm}} y especificar el punto final API de la región de {{site.data.keyword.Bluemix_notm}} en la que se ha creado su organización. Para obtener más información sobre el uso de las herramientas de Eclipse, consulte [Despliegue de apps con IBM Eclipse Tools for Bluemix](/docs/manageapps/eclipsetools/eclipsetools.html).  

## No se pueden crear rutas de app
{: #ts_hostistaken}

Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, no se puede crear la ruta de la app si el nombre de host especificado ya está en uso.

Al desplegar una app en {{site.data.keyword.Bluemix_notm}}, verá el siguiente mensaje de error:
{: tsSymptoms}

`Creating route hostname.domainname ... FAILED Server error, status code: 400, error code: 210003, message: The host is taken: hostname`

Este problema se produce si el nombre de host especificado ya está en uso.
{: tsCauses}

El nombre de host especificado debe ser exclusivo en el dominio que está utilizando. Para especificar otro nombre de host debe utilizar uno de los siguientes métodos:
{: tsResolve}

  * Si despliega su app utilizando el archivo `manifest.yml`, especifique el nombre de host en la opción host.	 
    ```
    host: nombre_host
	```
  * Si despliega su app desde el indicador de mandatos, utilice el mandato `cf push` con la opción **-n**.
    ```
    cf push nombre_app -p vía_acceso_app -n nombre_host
    ```


## Las apps WAR no se pueden enviar utilizando el mandato cf push
{: #ts_cf_war}

Es posible que no pueda utilizar el mandato cf push para desplegar una app web archivada a {{site.data.keyword.Bluemix_notm}} si la ubicación de la app no se especifica correctamente.

Si carga una app WAR en {{site.data.keyword.Bluemix_notm}} mediante el mandato `cf push`, verá el mensaje de error:
{: tsSymptoms}
`Error de transferencia: no se pueden obtener instancias debido a un error de transferencia. `

Este problema puede suceder si no se especifica el archivo WAR o si no se especifica la vía de acceso al archivo WAR.
{: tsCauses}

Utilice la opción **-p** para especificar un archivo WAR o añada la vía de acceso al archivo WAR. Por ejemplo:
{: tsResolve}

```
cf push MyUniqueAppName01 -p app.war
```

```
cf push MyUniqueAppName02 -p "./app.war"
```
Para obtener más información sobre el mandato `cf push`, escriba `cf push -h`. 	


## Los caracteres de doble byte no se visualizan correctamente cuando se envían por push apps Liberty a Bluemix 
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

Es posible que tenga problemas si actualiza una app Node.js o despliega una app Node.js en {{site.data.keyword.Bluemix_notm}}.

Si actualiza una app Node.js o despliega una app Node.js en {{site.data.keyword.Bluemix_notm}}, es posible que reciba uno de los siguientes mensajes de error:
{: tsSymptoms}

`Ningún paquete de compilación disponible ha detectado correctamente una app.`

`La instancia (índice 0) no ha podido empezar a aceptar conexiones.`

`No se pueden obtener instancias debido a un error de transferencia. `

A continuación se detallan las causas posibles:
{: tsCauses}

  * No se ha especificado el mandato start.
  * Faltan archivos necesarios para desplegar una app Node.js o bien se encuentran en una carpeta que no es el directorio raíz.

Utilice uno de los métodos siguientes en función de la causa del problema:
{: tsResolve}

  * Especifique el mandato start siguiendo uno de estos métodos:
     * Utilice la interfaz de línea de mandatos cf. Por ejemplo:
        ```
		cf push MyUniqueNodejs01 -p app_path -c "node app.js"
		```
    * Utilice el archivo [package.json ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](https://docs.npmjs.com/json){: new_window}. Por ejemplo:
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

  * Asegúrese de que el archivo `package.json` exista en la app Node.js para que el paquete de compilación de Node.js pueda reconocer la app. Asegúrese de que dicho archivo esté en el directorio raíz de la app.
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

Para ver más sugerencias sobre las apps Node.js, consulte [Consejos para las aplicaciones Node.js](http://docs.cloudfoundry.org/buildpacks/node/node-tips.html ![External link icon](../icons/launch-glyph.svg "icono de enlace externo"){: new_window}.


## Aparecen errores de configuración en el archivo `server.xml` después de importar una app Bluemix Liberty en Eclipse
{: #ts_eclipse}

Si ve errores de configuración en el archivo `server.xml` después de importar una app {{site.data.keyword.Bluemix_notm}} Liberty en Eclipse, es posible que tenga que eliminar el archivo `server.xml` del proyecto.

Después de importar una app {{site.data.keyword.Bluemix_notm}} Liberty en Eclipse, verá errores de configuración en el archivo `server.xml` en la vista Problemas de Eclipse.
{: tsSymptoms}

El paquete de compilación de Liberty utiliza el archivo `server.xml` para configurar la app y genera un archivo `runtime-vars.xml` cuando la app Liberty se envía a {{site.data.keyword.Bluemix_notm}}. Cuando importa la app en Eclipse, el archivo `runtime-vars.xml` no existe en el entorno local.
{: tsCauses}

Puede resolver este problema eliminando el archivo server.xml del proyecto. El paquete de compilación crea el archivo `server.xml` de forma dinámica cuando se envía la app como una app WAR. Para obtener más información, consulte el apartado [Liberty for Java](/docs/runtimes/liberty/index.html).
{: tsResolve}


## No se pueden transferir las apps utilizando paquetes de compilación personalizados
{: #ts_bp_compilation}

Es posible que no pueda desplegar una app en {{site.data.keyword.Bluemix_notm}} utilizando un paquete de compilación personalizado si los scripts del paquete de compilación no son ejecutables.

Si despliega una app en {{site.data.keyword.Bluemix_notm}} utilizando un paquete de compilación personalizado, verá el mensaje de error `La app no se ha podido transferir, por lo que no hay instancias que mostrar.`
{: tsSymptoms}

Este problema puede suceder si los scripts, como el script de detección, el script de compilación y el script de liberación, no son ejecutables.
{: tsCauses}

Puede utilizar el mandato [git update ![icono de enlace externo](../icons/launch-glyph.svg "icono de enlace externo")](http://git-scm.com/docs/git-update-index){: new_window} para cambiar el permiso de cada script por ejecutable. Por ejemplo, puede escribir `git update --chmod=+x script.sh`.
{: tsResolve}

## No puede desplegar una app desde Delivery Pipeline en IBM Bluemix Continuous Delivery
 {: #ts_devops_to_bm}

 Podría no poder desplegar su app utilizando {{site.data.keyword.deliverypipeline}} en {{site.data.keyword.contdelivery_short}} si el archivo `manifest.yml` no está presente en su app. 

 Cuando se despliega una app utilizando {{site.data.keyword.deliverypipeline}} en {{site.data.keyword.contdelivery_short}}, podría visualizarse el mensaje de error `No es posible detectar un tipo de aplicación soportada`.
 {: tsSymptoms}

 Este problema podría deberse a que el conducto necesita un archivo `manifest.yml` para desplegar una app en {{site.data.keyword.Bluemix_notm}}.
 {: tsCauses}

 Para solucionar este problema, debe crear un archivo `manifest.yml`. Para obtener más información sobre cómo crear un archivo `manifest.yml`, consulte [Manifiesto de la app](/docs/manageapps/depapps.html#appmanifest).
 {: tsResolve}

## No se pueden enviar por push las apps de Meteor
{: #ts_meteor}

Es posible que no pueda enviar por push una aplicación de Meteor a {{site.data.keyword.Bluemix_notm}} si no se ha especificado correctamente el paquete de compilación.

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
  * Si despliega su app desde un indicador de mandatos, utilice el mandato `cf push` y especifique el paquete de compilación personalizado mediante la opción **-b**. Por ejemplo:
    ```
	cf push appname -p app_path -b https://github.com/Sing-Li/bluemix-bp-meteor
	```
