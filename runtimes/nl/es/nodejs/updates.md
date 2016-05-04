---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Últimas actualizaciones del paquete de compilación sdk-for-nodejs
{: #latest_updates}

*Última actualización: 22 de marzo de 2016*

Una lista de las últimas actualizaciones del paquete de compilación sdk-for-nodejs.
## 29 de abril de 2016: se ha actualizado el paquete de compilación Node.js v3.3-20160418-1749

Este release del paquete de compilación añade el tiempo de ejecución de IBM SDK for Node.js versiones 0.10.44, 0.12.13, 4.4.1 y 4.4.2. El valor predeterminado es ahora 4.4.2. También se han eliminado varias versiones anteriores del tiempo de ejecución de IBM SDK for Node.js. El paquete de compilación ahora solo incluye las dos versiones más recientes de 0.10.x, 0.12.x y 4.x que en este momento son 0.10.43, 0.10.44, 0.12.12, 0.12.13, 4.4.1 y 4.4.2.

Para 4.4.1 y 4.4.2, ahora es posible utilizar una versión compatible de FIPS del tiempo de ejecución estableciendo la variable de entorno de `FIPS_MODE=true` para la app. A continuación, busque `FIPS_MODE` en la salida de transferencia para confirmar que lo ha reconocido el paquete de compilación.

El paquete de compilación actualizado y las nuevas versiones de tiempo de ejecución también contienen arreglos para vulnerabilidades de seguridad:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

El paquete de compilación actualizado también contiene arreglos para dos errores:
* Ahora las compilaciones de IBM SDK for Node.js se utilizarán siempre si hay una disponible que coincida con el rango solicitado. Anteriormente, esto solo era true para versiones de tiempo de ejecución 4.x.
* Ahora, la utilidad del inspector de App Management funcionará con versiones de tiempo de ejecución 4.x.

## 18 de marzo de 2016: se ha actualizado el paquete de compilación Node.js v3.2-20160315-1257

Este release del paquete de compilación mueve el tiempo de ejecución de IBM SDK for Node.js predeterminado desde la versión 4.3.0 a 4.3.2. También incluye IBM SDK for Node.js versiones 0.10.43, 0.12.12 y 4.3.1. Los usuarios deben utilizar estas versiones recientes de Node.js para recoger arreglos para varias vulnerabilidades de seguridad.

## 4 de marzo de 2016: se ha actualizado el paquete de compilación Node.js v3.1-20160222-1123

Este release del paquete de compilación mueve el tiempo de ejecución de IBM SDK for Node.js predeterminado de la versión 4.2.4 a 4.3.0. También incluye IBM SDK for Node.js versiones 0.10.42, 0.12.10 y 4.2.6. Los usuarios deben utilizar estas versiones recientes de Node.js para recoger arreglos para varias vulnerabilidades de seguridad.

## 4 de febrero de 2016: se ha actualizado el paquete de compilación Node.js v3.0-20160125-1224

Este release está totalmente sincronizado con el paquete de compilación de [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). Además de los cambios de comunidad, se han realizado cambios en determinados valores predeterminados, optimizaciones para reducir el momento de la transferencia y actualizaciones a la característica de App Management.

* Actualizaciones del paquete de compilación:

  * Node.js v4.2.4 (IBM SDK for Node.js Versión 4) es ahora el tiempo de ejecución predeterminado en Bluemix, que sustituye a v0.12.9. Esto puede provocar que su aplicación se comporte de forma diferente si no ha especificado una determinada versión para la aplicación. Para obtener más información sobre cómo especificar una versión de Node.js para su aplicación Bluemix, consulte la documentación de [tiempo de ejecución de Node.js](index.html).

  * NODE_ENV ahora está establecido en *producción* de forma predeterminada. Esto hará que algunas dependencias de nodos se comporten de forma distinta. Por ejemplo, la infraestructura de Express ya no devolverá stacktraces en el navegador web para puntos finales defectuosos, pero en lugar de ello, mostrará *Error de servidor interno*. Cuando NPM_CONFIG_PRODUCTION se establece en *true*, NPM establecerá NODE_ENV en *producción* para scripts de subshell solo en la fase de instalación de npm. Esto permitirá a los usuarios establecer NODE_ENV en otro valor como por ejemplo *desarrollo* para el tiempo de ejecución de la aplicación. Por razones de claridad, los scripts de npm verán el mensaje **NODE_ENV=production**.

  * Se incluye un arreglo de errores en el servicio Monitoring and Analytics.

* Actualizaciones de memoria caché:

  * Si se inhabilita la memoria caché (NODE_MODULES_CACHE=false), el paquete de compilación no intentará almacenar en la memoria caché ningún módulo/componente. Anteriormente, este valor hizo que la memoria caché no emergiera, pero aún puede almacenar en memoria caché los módulos instalados para despliegues futuros. Ahora no hará emerger la memoria caché ni intenta almacenar ninguna memoria caché.

  * Bower_components se almacenan en la memoria caché de forma predeterminada además de node_modules.

* Otras actualizaciones:

  * Se han añadido avisos útiles para dependencias que faltan, como por ejemplo gulp, bower y angular.

  * El script de detección se actualiza con la información de la versión del paquete de compilación.

  * La recomendación de agrupación en clúster (WEB_CONCURRENCY) introducida inicialmente por la comunidad se eliminará, ya que la determinación de la memoria no era precisa en Bluemix.


## 16 de diciembre de 2015: actualización del paquete de compilación Node.js v2.8-20151209-1403 y v3.0beta-20151211-2041

Este release del paquete de compilación de Node.js incluye dos versiones, v2.8 y v3.0beta. Ambas versiones incluyen los siguientes cambios:

Una corrección de errores para el servicio de Monitoring and Analytics
La inclusión de un tiempo de ejecución almacenado en memoria caché para IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 y v1.2.0.7 (según el Node.js de la comunidad v4.2.3, v4.2.2, v0.12.9 y v0.12.8, respectivamente)
Además, en v3.0beta el tiempo de ejecución de Node.js predeterminado se cambia a v4.2.3.

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

Este cambio en el tiempo de ejecución predeterminado no afectará a su aplicación si ha configurado una versión específica de Node.js en el archivo package.json de la aplicación. Tenga en cuenta que siempre puede especificar la versión de Node.js para ejecutar la aplicación utilizando la entrada engines.node en el package.json, como se explica en [Versiones disponibles](index.html#available_versions).

## 23 de noviembre de 2015: actualización del paquete de compilación de Node.js v2.7-20151118-1003

Con la versión 2.7, hemos incluido la versión 4.2.1.0 de IBM SDK para Node.js (basado en Node v4.2.1 LTS). Todavía no es la versión predeterminada, pero se puede especificar para ser utilizada. Tenga en cuenta que sustituye a la compilación de código abierto que antes estaba disponible. También hemos realizado algunas pequeñas correcciones de errores a nuestra infraestructura de extensión de servicio.

## 19 de octubre de 2015: actualización del paquete de compilación de Node.js v2.6.1-20151015-1326

Node.js v2.6.1 presenta una corrección de errores para el [manejador de gestión de la app StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) y una versión de NPM más coherente.

## 15 de octubre de 2015: actualización del paquete de compilación Node.js v2.6-20151006-1309

Este release del paquete de compilación de Node.js incluye la integración del [Gestor de procesos de StrongLoop](https://strong-pm.io) en la característica de App Management. Para obtener más información, consulte el artículo del blog [StrongLoop DevOps para aplicaciones de Node.js en Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 de junio de 2015: actualización del paquete de compilación Node.js v2.0-20150608-1503

En esta versión, hemos sincronizado nuestro paquete de compilación Node.js con el último [paquete de compilación Node.js de CF community](https://github.com/cloudfoundry/nodejs-buildpack), que incluye varias características nuevas de la comunidad.
Además, hemos reformado la característica de gestión de aplicaciones del paquete de compilación Node.js, que habilita funciones tales como el shell, node-inspector y Bluemix Live Sync, entre otras. Consulte [App Management](../../manageapps/app_mng.html) para obtener más detalles.

## 5 de mayo de 2015: actualización del paquete de compilación Node.js v1.17-20150429-1033

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Si la aplicación no especifica un tiempo de ejecución en su paquete package.json, la aplicación ahora se iniciará con v0.12.1, en lugar de v0.10.x. Si necesita utilizar la versión anterior, especifique v0.10.x en package.json como se muestra a continuación

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* La versión v0.12.1 presenta algunos problemas conocidos:
   * Al utilizar la función de Herramientas de depuración proporcionada por Bluemix Live Sync, la función "Suspender" se bloquea.
   * El módulo mqlight utilizado para el servicio MQ Light no recibe soporte en la versión v0.12.x

* Se han resuelto varias vulnerabilidades de seguridad:
  * Vulnerabilidades corregidas en OpenSSL que afectan a IBM SDK para Node.js. Hay disponibles más detalles en el [boletín de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnerabilidad corregida en el cifrado de secuencia RC4 que afecta a IBM SDK para Node.js. Hay disponibles más detalles en el [boletín de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 de abril de 2015: actualización del paquete de compilación Node.js v1.15-20150331-2231

* El paquete de compilación Node.js ahora incluye tres nuevas funciones para ayudar a desarrollar en Bluemix con la misma rapidez con la que desarrollaría en el escritorio, sin necesidad de volver a implementar.
  * Sincronización del escritorio: sincronice cualquier árbol de escritorio (Windows) en un espacio de trabajo de proyectos basado en la nube
  * Edición en directo: puede realizar cambios en una aplicación Node.js que se ejecute en Bluemix y probarlos directamente en el navegador.
  * Depuración: conéctese mediante shell a su entorno e inicie la depuración. Con el depurador de node Inspector puede, de manera dinámica, editar el código, insertar puntos de interrupción, recorrer el código, reiniciar el tiempo de ejecución, entre otras características.
  * Consulte [App Management](../../manageapps/app_mng.html#Utilities) para obtener más información.
* Hemos integrado los últimos cambios del [paquete de compilación Node.jgs de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Esto incluye varias correcciones y mejoras realizadas por la comunidad.
* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 de enero de 2015: actualización del paquete de compilación Node.js v1.9.1-20141208-1221

* El paquete de compilación Node.js ahora incluye soporte para la configuración dinámica de registros. Con esto, los desarrolladores pueden cambiar el nivel de registro de su aplicación al momento si la aplicación utiliza módulos log4js, bunyan o
ibmbluemix para el registro.
* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Incluye arreglos para el problema de POODLE.

## 23 de octubre de 2014: Actualizado el paquete de compilación Node.js v1.6-20141013-1736

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Esto significa que tendrá un soporte completo al tiempo de ejecución de IBM Node.js cuando especifique el tiempo de ejecución Node.js más estable para la aplicación, v0.10.32. Este último SDK incluye un arreglo de un problema con el módulo qs incorporado que provocaba un a denegación de servicio. También contiene una versión actualizada del módulo npm y otras mejoras en los módulos http y url. Para obtener detalles adicionales, consulte el [registro de cambios de v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* El paquete de compilación también contiene un arreglo de un error que provocaba la adición de un archivo index.html incorrecto en la aplicación del cliente durante el despliegue.

## 30 de septiembre de 2014: Actualizado el paquete de compilación Node.js v1.4-20140908-1746

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Esto significa que obtendrá un soporte completo al tiempo de ejecución de IBM Node.js al especificar el tiempo de ejecución Node.js más estable para la aplicación, v0.10.31. Con soporte completo para el tiempo de ejecución Node.js, los clientes pueden crear sobre él sabiendo que pueden confiar en el mismo soporte integral que siempre han obtenido de los productos de IBM.
* El paquete de compilación contiene una infraestructura de servicio mejorada. En concreto, funciona mejor al enlazar el servicio Monitoring and Analytics y proporciona información adicional de diagnóstico en caso de errores.

## 28 de agosto de 2014: Actualizado el paquete de compilación Node.js v1.3-20140821-1143

* El paquete de compilación Node.js más reciente se suministra ahora con IBM SDK for Node.js v1.1.0.6. Esto significa que tendrá un soporte completo al tiempo de ejecución de Node.js de IBM al especificar el tiempo de ejecución de Node.js más estable, v0.10.30, para la aplicación. Este tiempo de ejecución arregla la [Vulnerabilidad de daños en la memoria de V8](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* El paquete de compilación también incluye mejoras y correcciones de errores de la extensión de servicio Monitoring and Analytics, lo que le permite diagnosticar el rendimiento y condiciones de error a través del servicio.

## 29 de julio de 2014: Actualizado el paquete de compilación Node.js v1.1-20140717-1447

El paquete de compilación Node.js se suministra ahora con IBM SDK for Node.js v1.1.0.5. Esto significa que tendrá un soporte completo al tiempo de ejecución de Node.js de IBM al especificar el tiempo de ejecución de Node.js más estable para la aplicación, v0.10.29. Consulte más información sobre los SDK del Node.js de IBM [aquí](https://developer.ibm.com/node/sdk/).

# rellinks
## general
* [tiempo de ejecución de node.js](index.html)
