---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Mandatos de Cloud Foundry (cf)

*Última actualización: 29 de enero de 2016*

Puede utilizar mandatos de Cloud Foundry (cf) para gestionar apps.
{:shortdesc}

La información siguiente muestra los mandatos cf más utilizados para gestionar apps. Para ver una lista de todos los mandatos cf y su información de ayuda, utilice `cf help`. Utilice `cf nombre_mandato -h` para ver información de ayuda detallada sobre un determinado mandato.

*Nota:* Si la red contiene un servidor proxy HTTP entre el host que ejecuta los mandatos cf y el punto final de la API de
Cloud Foundry, debe especificar el nombre de host o la dirección IP del servidor proxy mediante la variable de entorno `HTTP_PROXY`. Para ver detalles, consulte el apartado [Utilización de la CLI cf con un servidor proxy HTTP](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Visualiza o
especifica el URL del punto final API de {{site.data.keyword.Bluemix_notm}}.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>El URL del punto final API de Bluemix que debe especificar al conectarse a {{site.data.keyword.Bluemix_notm}}. Normalmente, este URL es https://api.{DomainName}.
Si desea visualizar el URL del punto final API que está utilizando actualmente
no tiene que especificar este parámetro para el mandato cf api.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Inhabilita el proceso de validación de SSL. El uso de este parámetro puede ocasionar problemas de seguridad.</dd>
<dt>*--unset*</dt>
<dd>Elimina información de conexión para todos los puntos finales de la API.</dd>
</dl>

## cf apps

Lista todas las
apps desplegadas en el espacio actual. También se visualiza el estado
de cada app.

Suponga que tiene una instancia para una app, en la columna instancias de la respuesta desde el mandato cf apps, verá 1/1 si la app está activa y 0/1 si la app está desactivada. Si ve ?/1, indicará que el estado de la instancia de la app es desconocido; puede copiar el URL de la app en su navegador para comprobar si la app responde, o puede poner el registro en cola mediante el mandato `cf logs nombre_app` para ver si la app está generando contenido de registro.

## cf bind-service

Enlaza
una instancia de servicio existente a su app.
```
cf bind-service nombre_app instancia_servicio
```

Por ejemplo, si tiene una instancia de servicio llamada `my_dataworks` en la organización y espacio actuales, puede utilizar `cf bind-service my_app
my_dataworks` para enlazar esta instancia del servicio a la app.

<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
<dt>instancia_servicio</dt>
<dd>El nombre de la instancia de servicio existente.</dd>
</dl>

## cf create-service

Crea una instancia de servicio.
```
cf create-service nombre_servicio plan_servicio instancia_servicio
```
Por ejemplo, puede utilizar `cf create-service DataWorks free my_dataworks` para crear una instancia del servicio {{site.data.keyword.dataworks_short}} con un plan free.

<dl>
<dt>nombre_servicio</dt>
<dd>El nombre del servicio.</dd>
<dt>plan_servicio</dt>
<dd>El nombre del plan del servicio.</dd>
<dt>instancia_servicio</dt>
<dd>El nombre que desea utilizar para la nueva instancia del servicio que cree.</dd>
</dl>

## cf create-space

Crea un espacio.
```
cf create-space nombre_espacio
```
<dl>
<dt>nombre_espacio</dt>
<dd>El nombre del espacio.</dd>
<dt>*-o*</dt>
<dd>El nombre de la organización en la que desea crear un espacio.</dd>
<dt>*-q*</dt>
<dd>La cuota para asignar al espacio recién creado. Si no se especifica, se asignará automáticamente una cuota predeterminada.</dd>
</dl>

## cf delete

Suprima una app existente.
```
cf delete nombre_app
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.<dd>
<dt>*-f*</dt>
<dd>Fuerza la supresión de la app sin ninguna confirmación. Este
parámetro es opcional.</dd>
<dt>*-r*</dt>
<dd>Suprime todos los nombres de dominio asociados a la app . Este
parámetro es opcional.</dd>
</dl>

## cf delete-space

Suprime un espacio.
```
cf delete-space nombre_espacio
```
<dl>
<dt>nombre_espacio</dt>
<dd>El nombre del espacio.</dd>
<dt>*-f*</dt>
<dd>Fuerza la supresión del espacio sin ninguna confirmación. Este
parámetro es opcional.</dd>
*Nota:* La supresión de un espacio en una operación irreversible.
</dl>

## cf events

Muestra los sucesos de tiempo de ejecución relacionados con una app.
```
cf events nombre_app
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
</dl>

## cf help

Muestra información de ayuda
para todos los mandatos cf o para un mandato cf específico
si se utiliza el parámetro nombre_mandato.
```
cf help nombre_mandato
```
<dl>
<dt>nombre_mandato</dt>
<dd>El nombre de un mandato. Puede utilizar este parámetro si desea obtener información de ayuda específica
de un mandato.</dd>
<dd>Si no especifica este parámetro se visualizará la información de ayuda de todos los mandatos cf.</dd>
</dl>


## cf login

Se inicia la sesión
en {{site.data.keyword.Bluemix_notm}}.
```
cf login
```
Puede utilizar uno o varios de los siguientes parámetros con el mandato cf
login:
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>El URL del punto final API de {{site.data.keyword.Bluemix_notm}}. Este
parámetro es opcional.</dd>
<dt>*-u*nombre_usuario</dt>
<dd>Su nombre de usuario. Este
parámetro es opcional.</dd>
<dt>*-p* contraseña</dt>
<dd>Su contraseña.</dd>
<dd>*Importante:* Si especifica la contraseña con el parámetro *-p* en la interfaz de línea de mandatos, es posible que la contraseña quede registrada en el historial de línea de mandatos. Por motivos de seguridad, evite especificar la contraseña con el parámetro -p. Escriba en su lugar la contraseña cuando se lo solicite la interfaz de línea de mandatos.</dd>
<dt>*-o*nombre_organización</dt>
<dd>El nombre de la organización en la que desea iniciar sesión.</dd>
<dt>*-s*nombre_espacios</dt>
<dd>El nombre del espacio en el que desea iniciar sesión.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Inhabilita el proceso de validación de SSL. El uso de este parámetro puede ocasionar problemas de seguridad.</dd>
</dl>

*Nota:* Si proporciona la contraseña en el parámetro *-p* de este mandato, es posible que quede registrada en el archivo histórico del mandato de shell
y lo vean otros usuarios del sistema operativo local.


## cf logs

Visualiza las
corrientes de anotaciones cronológicas STDOUT y STDERR de una app.
```
cf logs nombre_app
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
<dt>*--recent*</dt>
<dd>Recupera los registros recientes.</dd>
</dl>

## cf marketplace

Lista todos los
servicios disponibles en el mercado. Los servicios que muestra este mandato también se pueden ver en el catálogo de {{site.data.keyword.Bluemix_notm}}.
```
cf marketplace
```

## cf push

Despliega una app nueva en Bluemix, o actualiza una app existente en Bluemix.
```
cf push nombre_app 
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
<dt>*-b*nombre_paquete_compilación</dt>
<dd>El nombre del paquete de compilación. El nombre_paquete_compilación puede
ser un paquete de compilación personalizado por nombre o URL Git, por ejemplo, `my-buildpack` o `https://github.com/heroku/heroku-buildpack-play.git`.</dd>
<dt>*-c*mandato_inicio</dt>
<dd>El mandato de inicio de la app. Para utilizar el mandato de inicio predeterminado
debe especificar un valor null para esta opción. Por ejemplo:</dd>
<dd>```
cf push nombre_app -c null
```</dd>
<dd>También puede utilizar esta opción para ejecutar archivos script. Por ejemplo:
```
cf push nombre_app -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>La vía de acceso al archivo de manifiesto. El archivo de manifiesto predeterminado es manifest.yml y se encuentra en el directorio raíz de la app.</dd>
<dt>*-i*número_instancia</dt>
<dd>El número de instancias.</dd>
<dt>*-k*límite_disco</dt>
<dd>El límite de disco de la app, como por ejemplo *256M*, *1024M*
o *1G*.</dd>
<dt>*-m*límite_memoria</dt>
<dd>El límite de memoria de la app, como por ejemplo *256M*, *1024M*
o *1G*.</dd>
<dt>*-n*nombre_host</dt>
<dd>El nombre de host de la app, como por ejemplo *mi-subdominio*.</dd>
<dt>*-p*vía_acceso_app</dt>
<dd>La vía de acceso al directorio de la app o el archivo de archivado de la app.</dd>
<dt>*-t*tiempo_espera</dt>
<dd>Tiempo máximo en segundos para que se inicie la app. Es posible que otros tiempos de espera de lado del servidor
sustituyan este valor.</dd>
<dt>*-s* nombrepila</dt>
<dd>La pila para ejecutar las apps. Una pila es un sistema de archivos preconstruido, incluido el sistema operativo. Utilice `cf stacks` para ver las pilas disponibles en {{site.data.keyword.Bluemix_notm}}.</dd>
<dt>*--no-hostname*</dt>
<dd>Correlaciona el dominio de sistema de Bluemix a esta app.</dd>
<dt>*--no-manifest*</dt>
<dd>Ignora el archivo de manifiesto predeterminado.</dd>
<dt>*--no-route*</dt>
<dd>No correlaciona ninguna ruta a esta app.</dd>
<dt>*--no-start*</dt>
<dd>No inicia la app tras desplegarse.</dd>
<dt>*--random-route*</dt>
<dd>Crea una ruta aleatoria para la app.</dd>
</dl>

## cf scale

Muestra o cambia el número de instancia, el límite de espacio de disco y el límite de memoria de una app.
```
cf scale nombre_app -i número_instancia -k límite_disco -m límite_memoria
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
<dt>*-i*número_instancia</dt>
<dd>El número de instancias</dd>
<dt>*-k*límite_disco</dt>
<dd>El límite de disco de la app, como por ejemplo *256M*, *1024M*
o *1G*.</dd>
<dt>*-m*límite_memoria</dt>
<dd>El límite de memoria de la app, como por ejemplo *256M*, *1024M*
o *1G*.</dd>
<dt>*-f*</dt>
<dd>Fuerza el reinicio de la app sin ninguna solicitud.</dd>
</dl>

## cf services

Lista todos los
servicios disponibles en el espacio actual.
```
cf services
```

## cf set-env

Establece una variable de entorno para una app.
```
cf set-env nombre_app nombre_variable valor_variable
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
<dt>nombre_variable</dt>
<dd>El nombre de la variable de entorno.</dd>
<dt>valor_variable</dt>
<dd>El valor de la variable de entorno.</dd>
</dl>

## cf stacks

Lista todas las pilas. Una pila es un sistema de archivos predefinido, incluido un sistema operativo que pueda ejecutar apps.
```
cf stacks
```

## cf stop

Detiene una app.
```
cf stop nombre_app
```
<dl>
<dt>nombre_app</dt>
<dd>El nombre de la app.</dd>
</dl>

## cf -v

Muestra
la versión de la interfaz de línea de mandatos cf.
```
cf -v
```

# rellinks
{: #rellinks}
## general 
{: #general}
* [Tarjeta de referencia rápida: mandatos cf](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
