
{:shortdesc: .shortdesc}

# Servicios VCAP

*Última actualización: 9 de noviembre de 2015*


La variable de entorno VCAP_SERVICES es un objeto JSON que contiene
información que puede utilizar para interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}.
{:shortdesc}


## Recuperación del valor de la variable de entorno VCAP_SERVICES
{:retrieving}

La variable de entorno VCAP_SERVICES es un objeto JSON que contiene
información que puede utilizar para interactuar con una instancia de servicio en
{{site.data.keyword.Bluemix_notm}}. La información incluye el nombre de instancia de servicio, la credencial y el URL de conexión a la instancia de servicio. Estos valores se llenan en la variable de entorno VCAP_SERVICES cuando se enlaza la aplicación a una instancia de servicio en {{site.data.keyword.Bluemix_notm}}.

El valor de la variable de entorno VCAP_SERVICES está disponible solo cuando se enlaza una instancia de servicio a la aplicación. Puede visualizar las variables de entorno de la aplicación mediante el controlador de consola de WebSocket. En el ejemplo siguiente se muestra cómo utilizar el controlador de consola de WebSocket para visualizar las variables de entorno de una aplicación
Node.js.

En primer lugar, ejecute el mandato para volver a enviar por push la aplicación Node.js.
```
cf push -c "curl -s https://raw.githubusercontent.com/dmikusa-pivotal/cf-debug-tools/master/debug-console.sh | bash" yourapp
```
A continuación, introduzca el URL siguiente:
```
https://yourapp.{APPDomain}/bash.sh
```
En la página que se muestra, pulse la marca de verificación para conectar la herramienta y, a continuación, emita el mandato env para ver las variables de entorno de su aplicación. Para obtener más información sobre cf-debug-tools,
consulte [Debug
Tools for Cloud Foundry](https://github.com/dmikusa-pivotal/cf-debug-tools).


## Visualización de las capas de la infraestructura de Bluemix
{:viewinfra}


{{site.data.keyword.Bluemix_notm}} abstrae y oculta las capas de sistema operativo y de infraestructura para que el usuario no tenga que gestionarlas. Sin embargo, es posible que en alguna ocasión desee obtener más información sobre el sistema operativo y el middleware de la app.

Puede ejecutar el mandato cf stacks para mostrar las pilas disponibles o los sistemas de archivo raíz en los que están desplegadas las apps. También puede especificar la pila cuando utilice el mandato cf push con la opción *-s* y el *nombre_pila*, donde el nombre_pila es el sistema de archivos raíz, como `lucid64` o `cflinuxfs2`:
```
cf push nombreApp -s nombre_pila
```
Puede utilizar el mandato `cf buildpacks` para mostrar los componentes de middleware, como Perfil de WebSphere Liberty y SDK para Node.js, disponibles como tiempos de ejecución en los que se puede ejecutar la app. También puede especificar el entorno de tiempo de ejecución de la app con el siguiente mandato:
```
cf push nombreApp -b nombre_paquete_compilación
```
