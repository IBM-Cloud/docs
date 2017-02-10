---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-01-11"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 





# Resolución de problemas de tiempos de ejecución
{: #runtimes}



Puede tener problemas al utilizar los tiempos de ejecución de IBM® Bluemix™. Sin embargo, en muchos de los casos, puede solucionar estos problemas siguiendo unos sencillos pasos.
{:shortdesc}


## Se utiliza un paquete de compilación obsoleto cuando se envía una app por push
{: #ts_loading_bp}


Es posible que no pueda utilizar los últimos componentes de paquete de compilación al enviar por push una app. Puede utilizar paquetes de compilación que tengan mecanismos incorporados para evitar que se carguen componentes obsoletos, o puede suprimir el contenido del directorio de memoria caché de la app antes de enviar por push o volver a transferir la app. 

 

Cuando se envía por push o se vuelve a transferir una app después de que se actualice el paquete de compilación, los componentes del paquete de compilación no se cargan automáticamente. Como resultado, la app utiliza los componentes obsoletos del paquete de compilación de la memoria caché. Las actualizaciones que se hayan aplicado al paquete de compilación desde la última vez que haya enviado por push la app no se implementan. 
{: tsSymptoms}



Algunos paquetes de compilación no están configurados para descargar automáticamente todos los componentes actualizados de Internet para asegurarse de utilizar siempre la última versión.
{: tsCauses} 

 

Puede utilizar paquetes de compilación que tengan mecanismos incorporados para evitar que se carguen componentes obsoletos. Los siguientes paquetes de compilación son dos ejemplos: 
{: tsResolve}

  * [Paquete de compilación Java de Cloud Foundry ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack){: new_window}. Este paquete de compilación tiene un mecanismo incorporado para garantizar que se utiliza la versión más reciente del paquete de compilación. Para obtener más información sobre el funcionamiento de este mecanismo, consulte [extending-caches.md ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/java-buildpack/blob/master/docs/extending-caches.md){: new_window}. 
  * [Paquete de compilación Node.js de Cloud Foundry ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/nodejs-buildpack){: new_window}. Este paquete de compilación tiene una funcionalidad similar utilizando variables de entorno. Para habilitar el paquete de compilación Node.js para descargar módulos de nodo de Internet cada vez, escriba el siguiente mandato en la interfaz de línea de mandatos cf: 	
  ```
  set NODE_MODULES_CACHE=false
  ```
Si el paquete de compilación que utiliza no ofrece un mecanismo para cargar los últimos componentes automáticamente, puede suprimir manualmente el contenido del directorio de memoria caché y volver a enviar por push la app efectuando los siguientes pasos:
  1. Extraiga una rama de un paquete de compilación nulo como, por ejemplo, https://github.com/ryandotsmith/null-buildpack. Para obtener información sobre cómo extraer una rama, consulte [Conceptos básicos de Git - Obtención de un repositorio Git ![icono de enlace externo](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Getting-a-Git-Repository){: new_window}.  
  2. Añada la siguiente línea al archivo `null-buildpack/bin/compile` y confirme los cambios. Para obtener información sobre cómo confirmar cambios, consulte [Conceptos básicos sobre Git - Grabación de cambios en el repositorio ![icono de enlace externo](../icons/launch-glyph.svg)](http://www.git-scm.com/book/en/v2/Git-Basics-Recording-Changes-to-the-Repository){: new_window}.
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



En el paquete de compilación PHP, el parámetro error_log se utiliza para definir el nivel de registro. De forma predeterminada, el valor del parámetro `error_log` es **stderr notice**. El ejemplo siguiente muestra la configuración del nivel de registro predeterminado del archivo `nginx-defaults.conf` del paquete de compilación PHP que proporcionado por Cloud Foundry. Para obtener más información, consulte [cloudfoundry/php-buildpack ![icono de enlace externo](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/php-buildpack/blob/ff71ea41d00c1226d339e83cf2c7d6dda6c590ef/defaults/config/nginx/1.5.x/nginx-defaults.conf){: new_window}.
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
Para obtener más información sobre cómo cambiar la configuración de registro, consulte [error_log ![icono de enlace externo](../icons/launch-glyph.svg)](http://nginx.org/en/docs/ngx_core_module.html#error_log){: new_window}.
	

## No se puede importar una biblioteca Python de terceros en {{site.data.keyword.Bluemix_notm}}
{: #ts_importpylib}

Es posible que no pueda importar una biblioteca Python de terceros en {{site.data.keyword.Bluemix_notm}}. Puede solucionar el problema añadiendo archivos de configuración al directorio raíz de su app Python.


Cuando intenta importar una biblioteca Python de terceros, como por ejemplo la biblioteca `web.py`, el mandato `cf push` falla.
{: tsSymptoms}


 

Este problema se produce cuando falta la información de configuración de la app Python.
{: tsCauses}


 

Para solucionar el problema, añada un archivo `requirements.txt` y un archivo `Procfile` al directorio raíz de la app Python. La información siguiente da por supuesto que está importando una biblioteca web.py:
{: tsResolve}

  1. Añada un archivo `requirements.txt` al directorio raíz de la app Python. El archivo `requirements.txt` especifica los paquetes de la biblioteca que la app Python requiere y la versión de los paquetes. El ejemplo siguiente muestra el contenido del archivo `requirements.txt`, donde `web.py==0.37` indica que la versión de la biblioteca `web.py` que se descargará es la 0.37, y `wsgiref==0.1.2` indica que la versión de la interfaz de la pasarela del servidor web que la biblioteca web.py requiere es la 0.1.2.
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
	
	
<!-- begin STAGING ONLY --> 

	
## Los objetos de registrador Log4js no se muestran en la ventana emergente de rastreo de Node.js
{: #ts_logger}

Los objetos de registrador log4js no se muestran en la ventana emergente de rastreo de Node.js cuando se utilizan los módulos log4js e ibmbluemix en la app. 	

 
Los objetos de registrador log4js no se muestran en la ventana emergente de rastreo de Node.js cuando se utilizan los módulos log4js, winston e ibmbluemix en la app.
{: tsSymptoms}


Debido a que el módulo ibmbluemix proporciona una API unificada para operaciones de registro que utilizan los módulos log4js y winston, únicamente se muestran los objetos de registrador ibmbluemix en la ventana emergente de rastreo de Node.js. El objetivo de esto es impedir que los valores de nivel de registro de los objetos de registrador ibmbluemix, log4js y winston se sobrescriban los unos a los otros.
{: tsCauses}


Este comportamiento es el esperado.
{: tsResolve}

<!-- end STAGING ONLY -->




<!-- begin STAGING ONLY -->


## El recuadro de selección Aplicar valor de rastreo a todas las instancias de la aplicación está inhabilitado
{: #ts_bunyan}

El recuadro de selección **Aplicar valor de rastreo a todas las instancias de la aplicación** está deseleccionado e inhabilitado en la ventana emergente de rastreo de Node.js cuando se modifican los niveles de rastreo de Bunyan.



Al modificar los niveles de los objetos de registrador Bunyan, el recuadro de selección **Aplicar valor de rastreo a todas las instancias de la aplicación** está deseleccionado e inhabilitado en la ventana emergente de rastreo de Node.js.
{: tsSymptoms} 

 

Cuando se modifican los niveles de registro de Bunyan, el valor de rastreo no se puede aplicar a todas las instancias de una aplicación. Esto se debe a que la biblioteca de Bunyan no requiere que los nombres o identificadores de los objetos de registrador Bunyan sean exclusivos. Es posible que dos o más objetos de registrador Bunyan sutilizado para especificar niveles en los mensajes de registro de la aplicación tengan el mismo nombre o identificador. Por lo tanto, si el valor de rastreo está habilitado para una aplicación, los niveles de registro especificados en los mensajes de registro de la aplicación podrían ser imprecisos.
{: tsCauses}




Este comportamiento es el esperado.
{: tsResolve} 

<!-- end STAGING ONLY -->

