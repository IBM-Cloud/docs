{:new_window: target="_blank"}
{:codeblock: .codeblock}

*Última actualización: 18 de enero de 2016*

# Últimas actualizaciones del paquete de compilación Node.js
{: #latest_updates}

Lista de las últimas actualizaciones en el paquete de compilación Node.js.

## 16 de diciembre de 2015: actualización del paquete de compilación de Node.js v2.8-20151209-1403 y v3.0beta-20151211-2041

Este release del paquete de compilación de Node.js incluye dos versiones,
v2.8 y v3.0beta. Ambas versiones incluyen los siguientes cambios:

Una corrección al servicio de Monitoring and Analytics
La inclusión de un tiempo de ejecución almacenado en memoria caché para IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 y v1.2.0.7 (basado en la comunidad Node.js v4.2.3, v4.2.2, v0.12.9 y v0.12.8, respectivamente)
Además, en v3.0beta, el tiempo de ejecución Node.js predeterminado se modificará a v4.2.3.

El paquete de compilación de IBM Node.js v3.0beta se ha publicado como paquete de compilación no predeterminado en Bluemix con Node.js v4.2.3 como tiempo de ejecución predeterminado. Para asegurarse de que las apps y servicios sigan funcionando en Bluemix, envíe su aplicación por push con la versión beta del paquete de compilación. Después de 30 días o más, v3 se convertirá en el paquete de compilación predeterminado.

Para enviar por push su aplicación con v3.0beta:
* Utilice la opción "-b" en el mandato 'cf push':
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* O bien, utilice la opción "buildpack" en el archivo manifest.yml:
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

Este cambio en el tiempo de ejecución predeterminado no afectará a su aplicación si ha configurado una versión específica de Node.js en el archivo package.json de la aplicación. Tenga en cuenta que siempre puede especificar la versión de Node.js para ejecutar su aplicación utilizando la entrada engines.node en package.json como se describe en [Versiones disponibles](index.html#available_versions).

## 23 de noviembre de 2015: actualización del paquete de compilación de Node.js v2.7-20151118-1003

Con la versión 2.7, hemos incluido la versión 4.2.1.0 de IBM SDK for Node.js (basado en Node v4.2.1 LTS). Todavía no es la versión predeterminada, pero se puede especificar para ser utilizada. Tenga en cuenta que sustituye a la compilación de código abierto que antes estaba disponible. También hemos realizado algunas pequeñas correcciones de errores a nuestra infraestructura de extensión de servicio.

## 19 de octubre de 2015: actualización del paquete de compilación de Node.js v2.6.1-20151015-1326

Node.js v2.6.1 presenta una corrección de errores para el [manejador de gestión de la app StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) y una versión de NPM más coherente.

## 15 de octubre de 2015: actualización del paquete de compilación Node.js v2.6-20151006-1309

Este release del paquete de compilación de Node.js incluye la integración de [Gestor de procesos de StrongLoop](https://strong-pm.io) a la característica App Management. Para obtener más información, consulte el artículo del blog [StrongLoop DevOps para aplicaciones de Node.js en Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 de junio de 2015: actualización del paquete de compilación Node.js v2.0-20150608-1503

En esta versión, hemos sincronizado nuestro paquete de compilación Node.js con el último [paquete de compilación Node.js de CF community](https://github.com/cloudfoundry/nodejs-buildpack), que incluye varias características nuevas de la comunidad.
Además, hemos reformado la característica de gestión de aplicaciones del paquete de compilación Node.js, que habilita funciones tales como el shell, node-inspector y Bluemix Live Sync, entre otras. Consulte [App Management](../../manageapps/app_mng.html) para obtener más detalles.

## 5 de mayo de 2015: actualización del paquete de compilación Node.js v1.17-20150429-1033

* El paquete de compilación Node.js ahora incluye [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Si la aplicación no especifica un tiempo de ejecución en su paquete package.json, la aplicación ahora se iniciará con v0.12.1, en lugar de v0.10.x. Si necesita utilizar la versión anterior, especifique v0.10.x en package.json como se muestra a continuación
```
   "engines": {
        "node": "0.10.x"
    }
```
{: codeblock}
* La versión v0.12.1 presenta algunos problemas conocidos:
   * Al utilizar la función de Herramientas de depuración proporcionada por Bluemix Live Sync, la función "Suspender" se bloquea.
   * El módulo mqlight utilizado para el servicio MQ Light no recibe soporte en v0.12.x

* Se han resuelto varias vulnerabilidades de seguridad:
  * Vulnerabilidades corregidas en OpenSSL que afectan a IBM SDK for Node.js. Encontrará información más detallada en el [boletín sobre seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnerabilidad corregida en el cifrado de secuencia RC4 que afecta a IBM SDK for Node.js. Encontrará información más detallada en el [boletín sobre seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 de abril de 2015: actualización del paquete de compilación Node.js v1.15-20150331-2231

* El paquete de compilación Node.js ahora incluye tres nuevas funciones para ayudar a desarrollar en Bluemix con la misma rapidez con la que desarrollaría en el escritorio, sin necesidad de volver a implementar.
  * Sincronización del escritorio: sincronice cualquier árbol de escritorio (Windows) en un espacio de trabajo de proyectos basado en la nube
  * Edición en directo: puede realizar cambios en una aplicación Node.js que se ejecute en Bluemix y probarlos directamente en el navegador.
  * Depuración: conéctese mediante shell a su entorno e inicie la depuración. Con el depurador de node Inspector puede, de manera dinámica, editar el código, insertar puntos de interrupción, recorrer el código, reiniciar el tiempo de ejecución, entre otras características.
  * Consulte [App Management](../../manageapps/app_mng.html#Utilities) para obtener más información.
* Hemos integrado los últimos cambios del [paquete de compilación Node.jgs de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Esto incluye varias correcciones y mejoras realizadas por la comunidad.
* El paquete de compilación Node.js ahora incluye [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 de enero de 2015: actualización del paquete de compilación Node.js v1.9.1-20141208-1221

* El paquete de compilación Node.js ahora incluye soporte para la configuración dinámica de registros. Con esto, los desarrolladores pueden cambiar el nivel de registro de su aplicación al momento si la aplicación utiliza módulos log4js, bunyan o
ibmbluemix para el registro.
* El paquete de compilación Node.js ahora incluye [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Incluye arreglos para el problema de POODLE.

## 23 de octubre de 2014: Actualizado el paquete de compilación Node.js v1.6-20141013-1736

* El paquete de compilación Node.js ahora incluye [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Esto significa que obtiene un soporte completo al tiempo de ejecución de IBM Node.js cuando especifique el tiempo de ejecución Node.js más estable para la aplicación, v0.10.32. Este último SDK incluye un arreglo de un problema con el módulo qs incorporado que provocaba un a denegación de servicio. También contiene una versión actualizada del módulo npm y otras mejoras en los módulos http y url. Para obtener detalles adicionales, consulte el [registro de cambios de v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* El paquete de compilación también contiene un arreglo de un error que provocaba la adición de un archivo index.html incorrecto en la aplicación del cliente durante el despliegue.

## 30 de septiembre de 2014: Actualizado el paquete de compilación Node.js v1.4-20140908-1746

* El paquete de compilación Node.js ahora incluye [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Esto significa que obtendrá un soporte completo al tiempo de ejecución de IBM Node.js cuando especifique el tiempo de ejecución Node.js latest más estable para la aplicación, v0.10.31. Con soporte completo para el tiempo de ejecución Node.js, los clientes pueden crear sobre él sabiendo que pueden confiar en el mismo soporte integral que siempre han obtenido de los productos de IBM.
* El paquete de compilación contiene una infraestructura de servicio mejorada. En concreto, funciona mejor al enlazar el servicio Monitoring and Analytics y proporciona información adicional de diagnóstico en caso de errores.

## 28 de agosto de 2014: Actualizado el paquete de compilación Node.js v1.3-20140821-1143

* El paquete de compilación Node.js más reciente se suministra ahora con IBM SDK for Node.js v1.1.0.6. Esto significa que tendrá un soporte completo al tiempo de ejecución de IBM Node.js al especificar el tiempo de ejecución Node.js más estable, v0.10.30, para la aplicación. Este tiempo de ejecución soluciona la [Vulnerabilidad de daños en la memoria de V8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* El paquete de compilación también incluye mejoras y correcciones de errores de la extensión de servicio Monitoring and Analytics, lo que le permite diagnosticar el rendimiento y condiciones de error a través del servicio.

## 29 de julio de 2014: Actualizado el paquete de compilación Node.js v1.1-20140717-1447

El paquete de compilación Node.js se suministra ahora con IBM SDK for Node.js v1.1.0.5. Esto significa que tendrá un soporte completo al tiempo de ejecución de IBM Node.js al especificar el tiempo de ejecución Node.js más estable para la aplicación, v0.10.29. Consulte más información sobre los SDK IBM Node.js [aquí](https://developer.ibm.com/node/sdk/).
