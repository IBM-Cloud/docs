---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Últimas actualizaciones para el paquete de compilación de SDK for Nodejs
{: #latest_updates}

Una lista de las últimas actualizaciones del paquete de compilación sdk-for-nodejs.

## 10 de marzo de 2017: Actualización del paquete de compilación Node.js v3.11
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK para Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.3, 4.8.0, 6.9.5 y 6.10.0. Ahora la versión predeterminada es 4.8.0.

Además de los nuevos tiempos de ejecución, este release contiene un arreglo para un error encontrado al habilitar el manejador de gestión de apps de shell cuando se utiliza la interfaz de usuario de devconsole. Este paquete de compilación también ha modificado el funcionamiento de la configuración automática para el servicio Monitoring and Analytics. Las aplicaciones que utilizan el plan gratuito ya no dispondrán de la capacidad de registro, se ha sustituido por logmet.

## 20 de enero de 2017: Actualización del paquete de compilación Node.js v3.10
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK for Node.js: 0.10.47, 0.10.48, 0.12.17, 0.12.18, 4.7.0, 4.7.2, 6.9.2 y 6.9.4. Ahora el valor predeterminado es 4.7.2.

Contiene un arreglo para un error por el que no siempre se llamaba a "npm start" para iniciar aplicaciones.

## 17 de noviembre de 2016: se ha actualizado el paquete de compilación Node.js v3.9
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK para Node.js: 0.10.47, 0.10.48, 0.12.16, 0.12.17, 4.6.1, 4.6.2, 6.7.0 y 6.9.1. Ahora el valor predeterminado es 4.6.2.

Observe que Node.js v6 se ha promocionado al estado LTS el 18 de octubre de 2016 y pronto se convertirá en el tiempo de ejecución predeterminado del paquete de compilación. Node.js v0.10 concluyó su ciclo de vida el 31 de octubre de 2016 y pronto se dejará de incluir en el paquete de compilación. Consulte [Soporte a largo plazo de versiones de Node.js y el paquete de compilación de SDK para Node.js](https://www.ibm.com/blogs/bluemix/2016/11/node-version-support-and-sdk-buildpack/) para obtener más información.

Los errores que afectan a los manejadores de gestión de apps de rastreo y de inspector, cuando se utilizan con Node.js v6, se han solucionado en este release. Consulte el apartado [Gestión de apps de Liberty y Node.js](/docs/manageapps/app_mng.html#inspector) para obtener más información sobre cómo está cambiando el manejador de inspector ahora que Node.js v6 incorpora la función del inspector.

## 7 de octubre de 2016: Se ha actualizado el paquete de compilación de Node.js v3.8-20161006-1211
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK para Node.js: 0.10.46, 0.10.47, 0.12.15, 0.12.16, 4.5.0, 4.6.0, 6.6.0 y 6.7.0. El valor predeterminado es ahora 4.6.0.

Además de los nuevos tiempos de ejecución, este release contiene arreglos de errores del paquete de compilación. Uno de ellos es un arreglo para el problema conocido cuando se utiliza Node.js 6.x en modalidad de desarrollo que se ha mencionado en las actualizaciones del release v3.7-20160826-1101. También está sincronizado con el [paquete de compilación de Cloud Foundry Node.js v1.5.20](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.20).

## 26 de agosto de 2016: se ha actualizado el paquete de compilación de Node.js v3.7-20160826-1101
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK para Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.7, 4.5.0, 6.2.2 y 6.4.0. El valor predeterminado es ahora 4.5.0.

Este release incluye arreglos de errores, incluidos los del [paquete de compilación Node.js de Cloud Foundry 1.5.18](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.18).

El release elimina soporte para el manejador de gestión de app strongpm tal como se ha publicado en [Paquete de compilación Bluemix Node.js v3.3 – modalidad FIPS y más](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/).

Tenga en cuenta que es un problema conocido cuando se utiliza Node.js 6.x y la [modalidad de desarrollo](/docs/manageapps/app_mng.html#devmode). Como una solución provisional será necesario volver a transferir la aplicación después de habilitar la modalidad de desarrollo antes de poder empezar a utilizarla.

## 22 de julio de 2016: Se ha actualizado el paquete de compilación de Node.js v3.6-20160715-0749
Este release del paquete de compilación da soporte a las versiones de tiempo de ejecución de IBM SDK for Node.js: 0.10.45, 0.10.46, 0.12.14, 0.12.15, 4.4.6, 4.4.7, 6.2.1 y 6.2.2. El valor predeterminado es ahora 4.4.7.

Este release incluye un proxy actualizado de App Management que da soporte a los inicios de sesión federados.

Se incluyen arreglos para las siguientes vulnerabilidades de seguridad:
* [CVE-2016-1669](http://www-01.ibm.com/support/docview.wss?uid=swg21986383)

## 22 de junio de 2016: Se ha actualizado el paquete de compilación de Node.js v3.5-20160609-1608

Este release del paquete de compilación añade el tiempo de ejecución de IBM SDK for Node.js versiones 4.4.5 y 6.2.0. El valor predeterminado es 4.4.5.

El release elimina soporte para versiones de tiempo de ejecución anteriores tal como se ha publicado en [Paquete de compilación Bluemix Node.js v3.3 – modalidad FIPS y más](https://developer.ibm.com/bluemix/2016/05/05/node-buildpack-update-fips-mode/). El paquete de compilación ahora da soporte a 0.10.44, 0.10.45, 0.12.13, 0.12.14, 4.4.4, 4.4.5, 6.1.0 y 6.2.0.

Este release incluye correcciones de errores del [paquete de compilación Node.js de Cloud Foundry 1.5.14](https://github.com/cloudfoundry/nodejs-buildpack/tree/v1.5.14).

## 20 de mayo de 2016: se ha actualizado el paquete de compilación de Node.js v3.4-20160518-1653

Este release del paquete de compilación añade IBM SDK para Node.js versiones 0.10.45, 0.12.14, 4.4.4, 6.0.0 y 6.1.0. El valor predeterminado es ahora 4.4.4.

Se incluyen arreglos para las siguientes vulnerabilidades de seguridad:
* [CVE-2015-8855](http://www-01.ibm.com/support/docview.wss?uid=swg21982852)
* [CVE-2016-2108 CVE-2016-2107 CVE-2016-2105 CVE-2016-2106 CVE-2016-2109 CVE-2016-2176 ![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://www.openssl.org/news/secadv/20160503.txt)

Observe que hay un problema conocido con npm v3 y el programa de utilidad del inspector de App Management. npm 3.8.6 es el valor predeterminado con los tiempos de ejecución de 6.0.0 y 6.1.0. Si desea utilizar los tiempos de ejecución 6.x y el programa de utilidad del inspector, debe especificar una versión 2.x npm en package.json como un método alternativo temporal.

## 29 de abril de 2016: se ha actualizado el paquete de compilación Node.js v3.3-20160428-1409

Este release del paquete de compilación añade el tiempo de ejecución de IBM SDK for Node.js versiones 0.10.44, 0.12.13, 4.4.0, 4.4.1, 4.4.2 y 4.4.3. El valor predeterminado es ahora 4.4.3.
Para 4.3.1 y versiones posteriores, ahora es posible utilizar una versión habilitada para FIPS del tiempo de ejecución estableciendo la variable de entorno `FIPS_MODE=true` para su app.

El paquete de compilación actualizado y las nuevas versiones de tiempo de ejecución también contienen arreglos para vulnerabilidades de seguridad:
* [CVE-2016-2515](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-2537](http://www-01.ibm.com/support/docview.wss?uid=swg21977578)
* [CVE-2016-3956](http://www-01.ibm.com/support/docview.wss?uid=swg21980827)

El paquete de compilación actualizado también contiene arreglos para varios errores:
* Ahora las compilaciones de IBM SDK for Node.js se utilizarán siempre si hay una disponible que coincida con el rango solicitado. Anteriormente, este caso solo era true para versiones de tiempo de ejecución 4.x.
* Ahora, el programa de utilidad del inspector de App Management funcionará con versiones de tiempo de ejecución 4.x.
* Se ha arreglado en una regresión en el programa de utilidad strongpm App Management.

## 18 de marzo de 2016: se ha actualizado el paquete de compilación Node.js v3.2-20160315-1257

Este release del paquete de compilación mueve el tiempo de ejecución de IBM SDK for Node.js predeterminado desde la versión 4.3.0 a 4.3.2. También incluye IBM SDK for Node.js versiones 0.10.43, 0.12.12 y 4.3.1. Utilice estas versiones recientes de Node.js para recoger arreglos para varias vulnerabilidades de seguridad.

## 4 de marzo de 2016: se ha actualizado el paquete de compilación Node.js v3.1-20160222-1123

Este release del paquete de compilación mueve el tiempo de ejecución de IBM SDK for Node.js predeterminado de la versión 4.2.4 a 4.3.0. También incluye IBM SDK for Node.js versiones 0.10.42, 0.12.10 y 4.2.6. Utilice estas versiones recientes de Node.js para recoger arreglos para varias vulnerabilidades de seguridad.

## 4 de febrero de 2016: se ha actualizado el paquete de compilación Node.js v3.0-20160125-1224

Este release está totalmente sincronizado con el paquete de compilación de [Cloud Foundry community Node.js](https://github.com/cloudfoundry/nodejs-buildpack). Además de los cambios de comunidad, se han realizado modificaciones en determinados valores predeterminados, junto con optimizaciones para reducir el momento de la transferencia y actualizaciones a la característica de App Management.

* Actualizaciones del paquete de compilación:

  * Node.js v4.2.4 (IBM SDK for Node.js Versión 4) es ahora el tiempo de ejecución predeterminado en Bluemix, que sustituye a v0.12.9. Este cambio puede provocar que su aplicación se comporte de forma distinta si no se especifica una versión concreta para la aplicación. Para obtener más información sobre cómo especificar una versión de Node.js para su aplicación Bluemix, consulte la documentación de [tiempo de ejecución de Node.js](index.html).

  * NODE_ENV ahora está establecido en *producción* de forma predeterminada. Este cambio hará que algunas dependencias de nodos se comporten de forma distinta. Por ejemplo, la infraestructura de Express ya no devolverá stacktraces en el navegador web para puntos finales defectuosos, pero en lugar de ello, mostrará *Error de servidor interno*. Cuando NPM_CONFIG_PRODUCTION se establece en *true*, NPM establecerá NODE_ENV en *producción* para scripts de subshell solo en la fase de instalación de npm. Esta función permitirá a los usuarios establecer NODE_ENV en otro valor como por ejemplo *desarrollo* para el tiempo de ejecución de la aplicación. Por razones de claridad, los scripts de npm verán el mensaje **NODE_ENV=production**.

  * Se incluye un arreglo de errores en el servicio Monitoring and Analytics.

* Actualizaciones de memoria caché:

  * Si se inhabilita la memoria caché (NODE_MODULES_CACHE=false), el paquete de compilación no intentará almacenar en la memoria caché ningún módulo/componente. Anteriormente, este valor hizo que la memoria caché no emergiera, pero aún puede almacenar en memoria caché los módulos instalados para despliegues futuros. Ahora no se hará emerger la memoria caché ni se intentará almacenar ninguna memoria caché.

  * Bower_components se almacenan en la memoria caché de forma predeterminada además de node_modules.

* Otras actualizaciones:

  * Se han añadido avisos útiles para dependencias que faltan, como por ejemplo gulp, bower y angular.

  * El script de detección se actualiza con la información de la versión del paquete de compilación.

  * La recomendación de agrupación en clúster (WEB_CONCURRENCY) introducida inicialmente por la comunidad se eliminará, ya que la determinación de la memoria no era precisa en Bluemix.


## 16 de diciembre de 2015: se ha actualizado el paquete de compilación Node.js v2.8-20151209-1403 y v3.0beta-20151211-2041

Este release del paquete de compilación de Node.js incluye dos versiones, v2.8 y v3.0beta. Ambas versiones incluyen los siguientes cambios:

Una corrección de errores para el servicio Monitoring and Analytics. La inclusión de un tiempo de ejecución almacenado en memoria caché para IBM SDK for Node.js v4.2.3.0, v4.2.2.0, v1.2.0.8 y v1.2.0.7, que se basan en las versiones de comunidad Node.js v4.2.3, v4.2.2, v0.12.9 y v0.12.8.
Además, en v3.0beta el tiempo de ejecución predeterminado de Node.js se cambia por v4.2.3.

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

Este cambio en el tiempo de ejecución predeterminado no afectará a su aplicación si ha configurado una versión específica de Node.js en el archivo package.json de la aplicación.

**Nota:** siempre puede especificar la versión de Node.js para ejecutar la aplicación utilizando la entrada engines.node en el package.json, como se explica en [Versiones disponibles](index.html#available_versions).

## 23 de noviembre de 2015: se ha actualizado el paquete de compilación de Node.js v2.7-20151118-1003

Con 2.7, se incluye la versión 4.2.1.0 de IBM SDK for Node.js (basado en v4.2.1 LTS). Todavía no es la versión predeterminada, pero se puede especificar para ser utilizada. **Nota:** Esta versión sustituye la compilación de código abierto que estaba disponible anteriormente. También hemos realizado algunas pequeñas correcciones de errores a nuestra infraestructura de extensión de servicio.

## 19 de octubre de 2015: se ha actualizado el paquete de compilación de Node.js v2.6.1-20151015-1326

Node.js v2.6.1 presenta una corrección de errores para el [manejador de gestión de la app StrongPM](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/) y una versión de NPM más coherente.

## 15 de octubre de 2015: se ha actualizado el paquete de compilación Node.js v2.6-20151006-1309

Este release del paquete de compilación de Node.js incluye la integración del [Gestor de procesos de StrongLoop![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](https://strong-pm.io) en la característica de App Management. Para obtener más información, consulte el artículo del blog [StrongLoop DevOps para aplicaciones de Node.js en Bluemix](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/).

## 15 de junio de 2015: se ha actualizado el paquete de compilación Node.js v2.0-20150608-1503

En esta versión, hemos sincronizado nuestro paquete de compilación Node.js con el último [paquete de compilación Node.js de CF community](https://github.com/cloudfoundry/nodejs-buildpack), que incluye varias características nuevas de la comunidad.
Además, hemos reformado la característica de gestión de aplicaciones del paquete de compilación Node.js, que habilita funciones tales como el shell, node-inspector y Bluemix Live Sync, entre otras. Consulte [App Management](/docs/manageapps/app_mng.html) para obtener más detalles.

## 5 de mayo de 2015: se ha actualizado el paquete de compilación Node.js v1.17-20150429-1033

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/).
* Si la aplicación no especifica un tiempo de ejecución en su paquete package.json, la aplicación ahora se iniciará con v0.12.1, en lugar de v0.10.x. Si necesita utilizar la versión anterior, especifique v0.10.x en package.json como se muestra a continuación

```
        "engines": {
            "node": "0.10.x"
        }
```
{: codeblock}

* Problemas conocidos con v0.12.1:
   * La función “Suspender” se bloquea cuando se utiliza la función de Herramientas de depuración que proporciona Bluemix Live Sync.
   * El módulo mqlight que se utiliza para el servicio MQ Light no recibe soporte en la versión v0.12.x

* Se han resuelto varias vulnerabilidades de seguridad:
  * Vulnerabilidades corregidas en OpenSSL que afectan a IBM SDK para Node.js. Hay disponibles más detalles en el [boletín de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21701494).
  * Vulnerabilidad corregida en el cifrado de secuencia RC4 que afecta a IBM SDK para Node.js. Hay disponibles más detalles en el [boletín de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21882778).

##  2 de abril de 2015: se ha actualizado el paquete de compilación Node.js v1.15-20150331-2231

* El paquete de compilación Node.js ahora incluye tres nuevas funciones para ayudar a desarrollar en Bluemix con la misma rapidez con la que desarrollaría en el escritorio, sin necesidad de volver a implementar.
  * Sincronización del escritorio: sincronice cualquier árbol de escritorio (Windows) en un espacio de trabajo de proyectos basado en la nube
  * Edición en directo: le permite realizar cambios en una aplicación Node.js que se ejecute en Bluemix y probarlos directamente en el navegador.
  * Depuración: conéctese mediante shell a su entorno e inicie la depuración. Puede editar dinámicamente código, insertar puntos de interrupción, examinar el código, reiniciar el tiempo de ejecución y más utilizando el depurador del inspector de nodos
  * Consulte [App Management](/docs/manageapps/app_mng.html#Utilities) para obtener más información.
* Hemos integrado los últimos cambios del [paquete de compilación Node.jgs de Cloud Foundry](https://github.com/cloudfoundry/nodejs-buildpack). Este cambio incluye varias correcciones y mejoras realizadas por la comunidad.
* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/).

## 5 de enero de 2015: se ha actualizado el paquete de compilación Node.js v1.9.1-20141208-1221

* El paquete de compilación Node.js ahora incluye soporte para la configuración dinámica de registros. Con este soporte, los desarrolladores pueden cambiar dinámicamente el nivel de registro de su aplicación si dicha aplicación utiliza módulos log4js, bunyan o ibmbluemix para el registro.
* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/). Esta actualización incluye arreglos para el problema de POODLE.

## 23 de octubre de 2014: Se ha actualizado el paquete de compilación de Node.js v1.6-20141013-1736

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/). Esta actualización significa que obtiene un soporte completo al tiempo de ejecución de IBM Node.js
cuando especifique el tiempo de ejecución Node.js más estable para la aplicación, v0.10.32. Este último SDK incluye un arreglo de un problema con el módulo qs incorporado que provocaba un a denegación de servicio. También contiene una versión actualizada del módulo npm y otras mejoras en los módulos http y url. Para obtener más detalles, consulte el [registro de cambios de v0.10.32](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog).
* El paquete de compilación también contiene un arreglo de un error que provocaba la adición de un archivo index.html incorrecto en la aplicación del cliente durante el despliegue.

## 30 de septiembre de 2014: se ha actualizado el paquete de compilación Node.js v1.4-20140908-1746

* El paquete de compilación Node.js se suministra ahora con [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/). Esta actualización significa que obtiene un soporte completo al tiempo de ejecución de IBM Node.js
cuando especifique el tiempo de ejecución Node.js más estable para la aplicación, v0.10.31. Con un tiempo de ejecución de Node.js con soporte completo, los clientes reciben una experiencia de soporte coherente.
* El paquete de compilación contiene una infraestructura de servicio mejorada. En concreto, funciona mejor al enlazar el servicio Monitoring and Analytics y proporciona más información de diagnóstico en caso de que el servicio falle.

## 28 de agosto de 2014: se ha actualizado el paquete de compilación Node.js v1.3-20140821-1143

* El paquete de compilación Node.js más reciente se suministra ahora con IBM SDK for Node.js v1.1.0.6. Esta actualización significa que tendrá un soporte completo al tiempo de ejecución de Node.js de IBM al especificar el tiempo de ejecución de Node.js más estable, v0.10.30, para la aplicación. Este tiempo de ejecución arregla la [Vulnerabilidad de daños en la memoria de V8![Icono de enlace externo](../../icons/launch-glyph.svg "Icono de enlace externo")](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow).
* El paquete de compilación también incluye mejoras y correcciones de errores de la extensión de servicio Monitoring and Analytics, lo que le permite diagnosticar el rendimiento y condiciones de error a través del servicio.

## 29 de julio de 2014: se ha actualizado el paquete de compilación Node.js v1.1-20140717-1447

El paquete de compilación Node.js se suministra ahora con IBM SDK for Node.js v1.1.0.5. Esta actualización significa que tendrá un soporte completo al tiempo de ejecución de Node.js de IBM al especificar el tiempo de ejecución de Node.js más estable para la aplicación, v0.10.29. Consulte más información sobre los [SDK IBM Node.js](https://developer.ibm.com/node/sdk/).

# rellinks
{: #rellinks notoc}
## general
{: #general notoc}
* [tiempo de ejecución de node.js](index.html)
