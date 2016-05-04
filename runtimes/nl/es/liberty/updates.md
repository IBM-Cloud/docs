---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Actualizaciones más recientes al paquete de compilación de Liberty
{: #latest_updates}

## Una lista de las últimas actualizaciones del paquete de compilación de Liberty.

*Última actualización: 23 de marzo de 2016*

### 25 de marzo de 2016: se ha actualizado el paquete de compilación de Liberty v2.7-20160321-1358
* El paquete de compilación contiene una versión actualizada de WebSphere Liberty basada en la versión [beta de marzo](https://developer.ibm.com/wasdev/blog/2016/03/18/new-websphere-liberty-features-march-2016/). La versión actualizada de Liberty hace que la función beta cloudant-1.0 esté disponible en Bluemix.
* El paquete de compilación también contiene versiones actualizadas de IBM JRE: 8 SR2 FP12 y 7.1 SR3 FP32. 
* El paquete de compilación proporciona una versión actualizada del agente para el [servicio de Auto-Scaling](../../services/Auto-Scaling/index.html). 
* Ahora el paquete de compilación se suministra con un nuevo recopilador de datos para el [servicio de Monitoring and Analytics](../../services/monana/index.html#monana_oview). El nuevo recopilador permite la configuración de umbrales de supervisión y contiene un número de correcciones de errores.
* El paquete de compilación proporciona un controlador DB2® JDBC actualizado versión 4.19.49. 
* El tiempo de ejecución de Node.js utilizado por los [programas de utilidad devconsole y shell de App Management](../../manageapps/app_mng.html#app_management) se ha actualizado a la versión 0.12.12 más reciente.

### 7 de marzo de 2016: se ha actualizado el paquete de compilación de Liberty v2.6-20160225-1649
* El paquete de compilación añade soporte para la supervisión de la aplicación Dynatrace. Consulte [Utilización de Dynatrace](dynatrace.html) para obtener más detalles.
* El paquete de compilación añade soporte para [DynamicPULSE](www.fujitsu.com/jp/group/fsweb/products/dynamic-pulse/).

### 10 de febrero de 2016: se ha actualizado el paquete de compilación de Liberty v2.5-20160209-1336
* El paquete de compilación contiene una versión actualizada de WebSphere Liberty basada en la versión [beta de febrero](https://developer.ibm.com/wasdev/blog/2016/02/12/beta-websphere-liberty-and-tools-february/). La versión actualizada del perfil de Liberty hace la función GA apiDiscovery-1.0 disponible en Bluemix.

### 4 de febrero de 2016: se ha actualizado el paquete de compilación de Liberty v2.4-20160127-1437
* El paquete de compilación contiene una versión actualizada de WebSphere Liberty basada en la versión beta de enero. Con esta actualización, la característica scim-1.0 de Liberty, anteriormente disponible como una característica de versión beta, pasa a estar disponible como una característica disponible en producción. La versión actualizada de Liberty también hace que la función beta de passwordUtilities-1.0 esté disponible en Bluemix.
* El paquete de compilación también contiene una versión actualizada de IBM JRE 7.1 SF3 FP20 e IBM JRE 8 SR2 FP10.
* El paquete de compilación se ha actualizado para descargar el [conector MariaDB/controlador J JDBC](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) 1.x más reciente al realizar la [configuración automática para el tipo de servicios MySQL](autoConfig.html).

### 16 de diciembre de 2015: actualización del paquete de compilación de Liberty v2.3-20151208-1311
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de diciembre](https://developer.ibm.com/wasdev/blog/2015/11/20/beta-was-liberty-beta-with-tools-december-2015/). La versión actualizada del perfil de Liberty hace que las funciones spnego-1.0 y GA wsSecuritySaml-1.1 y la función beta scim-1.0 esté disponible en Bluemix.
* El paquete de compilación también contiene una versión actualizada de IBM JRE 8 SR2.
* El paquete de compilación también se ha actualizado para descargar el [controlador 9.4.x PostgreSQL JDBC](https://jdbc.postgresql.org/) más reciente y 1.2.x [conector MariaDB/controlador J JDBC](https://mariadb.com/kb/en/mariadb/about-mariadb-connector-j/) al realizar la [configuración automática](autoConfig.html) para el tipo de servicios PostgreSQL o MySQL.

### 23 de noviembre de 2015: actualización del paquete de compilación de Liberty v2.2-20151119-1720
* El paquete de compilación contiene una versión actualizada del tiempo de ejecución del perfil de Liberty y WebSphere eXtreme Scale Client con arreglos de seguridad para la [vulnerabilidad de Apache Commons Collection](http://www-01.ibm.com/support/docview.wss?uid=swg21971426).
* El paquete de compilación también contiene una versión actualizada del [controlador Java MongoDB](https://docs.mongodb.org/ecosystem/drivers/java/), v2.13.3. El nuevo controlador es compatible con MongoDB versión 2.4, 2.6 y 3.0.
* El paquete de compilación también proporciona una versión actualizada del recopilador de datos para el [servicio Monitoring and Analytics](../../services/monana/index.html). El recopilador de datos actualizado ha mejorado las prestaciones de rastreo de método.

### 16 de octubre de 2015: actualización del paquete de compilación de Liberty v2.1-20151006-0912
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de octubre](https://developer.ibm.com/wasdev/blog/2015/09/25/beta-was-liberty-beta-with-tools-october-2015/). Con esta actualización, las características de Liberty bells-1.0, rtcomm-1.0, rtcommGateway-1.0, samlWeb-2.0, sipServlet-1.1, anteriormente disponibles como versiones beta, pasan a estar disponibles como características disponibles en producción.
* El paquete de compilación también contiene una versión actualizada de IBM JRE 8 SR1 FP11.
* El paquete de compilación también proporciona un número de mejoras y optimizaciones del rendimiento:
  * La característica de exploración del archivador de beans implícito de [CDI 1.2](optionsForPushing.html) está inhabilitada de forma predeterminada al desplegar archivos WAR o EAR.
  * Para reducir el tamaño de gotas, los [Programas de utilidad de gestión de apps](../../manageapps/app_mng.html) devconsole y shell, requieren una operación de volver a transferir en lugar de un reinicio.
  * La memoria caché de clases compartidas de IBM JRE está inhabilitada ya que no se estaba reutilizando en el entorno de Bluemix.

### 18 de septiembre de 2015: actualización del paquete de compilación de Liberty v2.0-20150914-1535
* El paquete de compilación introduce dos cambios importantes:
  * La configuración predeterminada para los archivos WAR y EAR permite las características de Java EE 7 Web Profile en lugar
de las características de Java EE 6 Web Profile.
  * La versión predeterminada de Java es la versión 8 en lugar de la versión 7.
* Consulte la [Upcoming Liberty for Java buildpack changes](https://developer.ibm.com/bluemix/2015/09/08/upcoming-liberty-for-java-buildpack-changes/) blog post para obtener más detalles sobre estos cambios y cómo afectan a la aplicación.
* El paquete de compilación también introduce la opción de configuración app_state para inhabilitar la característica appstate mediante la variable de entorno JBP_CONFIG_LIBERTY. La característica appstate
se integra con el proceso de comprobación de estado de Cloud Foundry para asegurarse de que la aplicación Liberty se inicialice
completamente para que la aplicación pueda recibir solicitudes HTTP. Para inhabilitar la característica appstate, puede establecer la variable de entorno JBP_CONFIG_LIBERTY en “app_state: false”.

### 4 de septiembre de 2015: actualización del paquete de compilación de Liberty v1.22-20150824-1104
* El paquete de compilación da soporte a las [Variables de entorno HTTP_PROXY y
HTTPS_PROXY](environmentVariables.html). Si se establece, el paquete de compilación utiliza el servidor proxy especificado por estas variables de entorno cuando descarga diversos componentes del paquete de compilación.

### 19 de agosto de 2015: actualización del paquete de compilación de Liberty v1.21-20150811-1342
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de agosto](https://developer.ibm.com/wasdev/blog/2015/07/30/beta-was-liberty-beta-with-tools-august-2015/). La versión actualizada de los perfiles de Liberty convierte en disponibles las siguientes [características beta](usingBetaFeatures.html) nuevas en Bluemix: bells-1.0, rtcommGateway-1.0, samlWebSso-2.0.

### 31 de julio de 2015: actualización del paquete de compilación de Liberty v1.20.1-20150729-1255
* El paquete de compilación contiene versiones actualizadas de IBM JRE: 7.1 SR1 FP10 y 8 SR1 FP10.
Los JRE actualizados
contienen [mejoras de seguridad más recientes](http://www-01.ibm.com/support/docview.wss?uid=swg21964161) y otras mejoras.
* El plugin de servicio que proporciona [soporte de configuración automática](autoConfig.html) para el servicio [Cloudant NoSQL Database](../../services/Cloudant/index.html#Cloudant) se ha actualizado para asegurarse de que se establezcan las conexiones al servicio en un canal seguro.

### 21 de julio de 2015: actualización del paquete de compilación de Liberty v1.20-20150713-1450
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [release 8.5.5.6](https://developer.ibm.com/wasdev/blog/2015/06/25/java-ee-7-has-landed-in-was-liberty/). Con
este release, todas las características de Java EE 7 Liberty anteriormente disponibles como versiones beta, pasan a
estar disponibles como características disponibles en producción. Debido a las restricciones de puerto y otras más en Bluemix,
algunas características como por ejemplo los EJB remotos no se admiten totalmente en esta plataforma.
* El paquete de compilación reconoce y ejecuta aplicaciones empaquetadas en el [distZip-style](https://docs.gradle.org/current/userguide/application_plugin.html).
* El paquete de compilación contiene un recopilador de datos actualizado para el servicio
[Monitoring and Analytics Service](../../services/monana/index.html) (Servicio de supervisión y análisis) y el cliente WebSphere eXtreme Scale que tiene soporte para la nueva versión
ejecutable de Liberty.

### 30 de junio de 2015: actualización del paquete de compilación de Liberty v1.19.1-20150622-1509
* Esta versión del paquete de compilación contiene un IBM JRE actualizado con un arreglo de seguridad para
la [Vulnerabilidad LogJam](http://www-01.ibm.com/support/docview.wss?uid=swg21961390).
* El agente [New Relic](newRelic.html) se ha actualizado a la versión 3.17. La versión nueva proporciona integración mejorada
con el tiempo de ejecución del perfil de Liberty.

### 14 de junio de 2015: actualización del paquete de compilación de Liberty v1.19-20150608-1717
* El paquete de compilación contiene una serie de mejoras de gestión de aplicaciones incluyendo soporte
para la consola de desarrollo y el acceso de shell basado en web. Para obtener detalles, consulte la [documentación de app management](../../manageapps/app_mng.html).
* El paquete de compilación también contiene un arreglo para un problema por el que la característica de Liberty para
[Monitoring and Analytics Service](../../services/monana/index.html) no se puede encontrar.

### 27 de mayo de 2015: actualización del paquete de compilación de Liberty v1.18-20150519-1642
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de mayo](https://developer.ibm.com/wasdev/blog/2015/05/08/beta-liberty-and-tools-may-2015/).

### 5 de mayo de 2015: actualización del paquete de compilación de Liberty v1.17-20150501-1729
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de abril](https://developer.ibm.com/wasdev/blog/2015/04/10/announcing-liberty-beta-with-tools-aprilmay-2015/). Con
esta actualización, las características jsp-2.3,
el-3.0 y jdbc-4.1 de Liberty anteriormente disponibles como versiones beta, pasan a
estar disponibles como características disponibles en producción. Además las características adicionales de Java EE 7 como jsf-2.2, javaMail-1.5, webProfile-7.0 y javaee-7.0 están ahora disponibles como [características beta](usingBetaFeatures.html).
* El paquete de compilación también proporciona soporte inicial para Java 8. IBM JRE 7.1 sigue siendo
el JRE predeterminado, pero IBM JRE 8 se puede habilitar para una aplicación estableciendo la variable de entorno
JBP_CONFIG_IBMJDK. También se admite la configuración de la versión OpenJDK. Para ver todos los detalles,
consulte [Personalización del JRE](customizingJRE.html).
* El paquete de compilación proporciona una nueva variable de entorno JBP_CONFIG_LIBERTY que se puede utilizar
para alterar temporalmente el conjunto predeterminado de características de Liberty habilitado para una aplicación
cuando se despliega el archivo WAR o EAR. Para obtener más información, consulte [Aplicaciones autónomas](optionsForPushing.html#stand_alone_apps).
* El plugin de servicio para [Monitoring and Analytics Service](../../services/monana/index.html) se ha actualizado para reducir el tamaño de los registros generados para el servicio.
* Con esta versión del paquete de compilación, la forma en que se distribuyen los archivos de aplicación
en el droplet ha cambiado. El cambio en la estructura de archivos ha eliminado la complejidad relacionada
con el mantenimiento de enlaces simbólicos y no debería afectar a las aplicaciones.

### 15 de abril de 2015: actualización del paquete de compilación de Liberty v1.16-20150407-1737
* Esta versión del paquete de compilación contiene un IBM JRE 7.1-2.11 actualizado con un
[arreglo de seguridad para la vulnerabilidad Bar Mitzvah](http://www-01.ibm.com/support/docview.wss?uid=swg21882777).
* Cuando se despliegan archivos WAR autónomos, si se proporciona, el paquete de compilación utilizará ahora
la raíz de contexto especificada en el archivo **ibm-web-ext.xml** incorporado como la raíz de
contexto de la aplicación. Con este cambio, las aplicaciones que antes se desplegaban bajo el contexto raíz
se podrá desplegar bajo un contexto distinto, en base al archivo **ibm-web-ext.xml**.

### 3 de abril de 2015: actualización del paquete de compilación de Liberty v1.15-20150402-1422
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de marzo](https://developer.ibm.com/wasdev/blog/2015/03/13/announcing-liberty-beta-tools-march-2015/). La versión actualizada de los perfiles de Liberty hace que la función beta jsf-2.2 esté disponible en Bluemix.
* El paquete de compilación también contiene una versión actualizada del recopilador de datos para el servicio
[Monitoring and Analytics service](../../services/monana/index.html).

### 20 de marzo de 2015: actualización del paquete de compilación de Liberty v1.14-20150319-1159
* Esta versión del paquete de compilación contiene un IBM JRE 7.1.2.11 actualizado con un arreglo de seguridad para la [vulnerabilidad de FREAK](http://www-01.ibm.com/support/docview.wss?uid=swg21699864).
* El servicio de [ base de datos SQL](services/SQLDB/index.html#SQLDB) ofrece planes de pago que proporcionan una opción para la conexión con el servidor de bases de datos sobre el
protocolo SSL. El soporte de auto-configuración del paquete de compilación para el servicio de base de datos SQL
se ha actualizado para configurar el tiempo de ejecución para conectar con la base de datos
sobre SSL si está disponible la información de conexión SSL.
* El paquete de compilación se ha actualizado para que informe de un error cuando se despliegue un archivo
WAR o EAR que contiene un archivo de configuración **server.xml ** en la raíz del
archivo de la aplicación.
* El paquete de compilación contiene un arreglo para el plugin del servicio de auto-configuración que en algunos
casos ha generado configuración de **server.xml** no válida.

### 10 de febrero de 2015: actualización del paquete de compilación de Liberty v1.13-20150209-1122
* El paquete de compilación contiene arreglos de seguridad para [componentes de Apache Http y vulnerabilidades de la característica de superposición de Java](https://www-304.ibm.com/connections/blogs/PSIRT/entry/ibm_security_bulletin_multiple_vulnerabilities_fixed_in_liberty_for_java_for_ibm_bluemix_cve_2012_6153_cve_2014_3577_cve_2015_0178?lang=en_us).
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de febrero](https://developer.ibm.com/wasdev/blog/2015/02/13/announcing-liberty-beta-tools-february-2015/). La versión actualizada del perfil de Liberty proporciona una versión actualizada de la característica websocket-1.1 de WebSocket GA. También hace que las características beta de Java EE
7 estén disponibles en Bluemix:
  * cdi-1.2, el-3.0, jsp-2.3, jca-1.7, jacc-1.5 y jaspic-1.1
* El paquete de compilación proporciona integración con la [herramienta ZeroTrunaround's JRebel](http://zeroturnaround.com/software/jrebel/). La integración facilita el uso de JRebel con aplicaciones Bluemix
y realiza actualizaciones de aplicación sin volver a desplegar o transferir la aplicación. Solo se admiten las aplicaciones web autónomas.

### 6 de febrero de 2015: actualización del paquete de compilación de Liberty v1.12-20150130-1016
* El paquete de compilación contiene una versión actualizada del perfil de Liberty basado en la versión [beta de enero](https://developer.ibm.com/wasdev/blog/2015/01/16/announcing-liberty-beta-tools-january-2015/).
* El paquete de compilación contiene una versión recortada del recopilador de datos para el [servicio Monitoring and Analytics](../../services/monana/index.html#gettingstartedtemplate).

### 23 de enero de 2015: actualización del paquete de compilación de Liberty v1.11-20150119-1511
* El paquete de compilación contiene una versión actualizada de IBM JRE
7.1 SR2 FP1.
* También contiene una versión actualizada de WebSphere eXterme
Scale Client v8.6.0.6 y el agente actualizado para el servicio Auto-Scaling.
* El soporte del servicio de [New Relic](newRelic.html) se ha mejorado para dar soporte a los servicios definidos por el usuario.
* El paquete de compilación se ha mejorado para informar de versiones detalladas del
perfil de Liberty e IBM JRE.

### 19 de diciembre de 2014: actualización del paquete de compilación de Liberty v1.10-20141218-0103
* El paquete de compilación proporciona una modalidad de desarrollo de aplicaciones. La modalidad de desarrollo es una modalidad especial que permite a los desarrolladores realizar muchas actividades para una instancia de aplicación que antes no era posible realizar. Con esta característica, esta versión de IBM Eclipse Tools for Bluemix da soporte a la depuración remota con actualizaciones incrementales de archivo sobre una aplicación Liberty que se ejecuta en Bluemix. Por eso resulta cómodo para el desarrollador que utiliza Eclipse para depurar una aplicación en la nube y aplicar los cambios a dicha aplicación de forma instantánea.
* El paquete de compilación también contiene una versión actualizada del perfil de Liberty basado en la versión [beta de diciembre](https://developer.ibm.com/wasdev/blog/2014/12/10/announcing-liberty-beta-december/).
* Además, las cuatro siguientes características de Liberty que antes estaban disponibles como características beta ahora están listas para producción:
  * concurrent-1.0
  * jsonp-1.0
  * servlet-3.1
  * websocket-1.0.
* El paquete de compilación proporciona integración con el servicio New Relic. Cuando una aplicación se ha enlazado al servicio New Relic, el paquete de compilación descarga y configura
automáticamente el tiempo de ejecución con el agente New Relic.
* El paquete de compilación tiene las siguientes limitaciones conocidas:
  * Cuando está en modalidad de desarrollo, el servicio SessionCache no se puede enlazar.
  * Cuando está en modalidad de desarrollo, no se puede crear un volcado de hebra.
  * Cuando se utiliza la característica servlet-3.1 o websocket-v1.0, no se puede enlazar el servicio Monitoring &
Analytics.

### 5 de diciembre de 2014: actualización del paquete de compilación de Liberty v1.9-20141202-0947
* El paquete de compilación proporciona un soporte mejorado de la opción JVM. Ahora las opciones de JVM se puede aplicar con una operación de reinicio. No es necesario volver a transferir la aplicación. Además, las opciones predeterminadas de JVM se han optimizado para error rápido y se han preconfigurado con una ubicación común que facilita la búsqueda de los volcados generados. Se proporcionan más detalles en el [artículo sobre Configuración personalizada de Java JVM for Liberty Runtime](https://developer.ibm.com/bluemix/2014/12/12/custom-configurations-java-jvm-liberty-runtime/).
* El paquete de compilación contiene un controlador DB2 JDBC actualizado versión 4.17.29.
* También contiene un arreglo para un problema que impedía la recopilación de información sobre uso de la agrupación de hebras de Liberty para el servicio Monitoring &
Analytics.

### 21 de noviembre de 2014: actualización del paquete de compilación de Liberty v1.8-20141118-1610
* El paquete de compilación contiene una versión actualizada de IBM JRE 7.1 SR2 que ofrece un arreglo para la [vulnerabilidad de POODLE](http://www-01.ibm.com/support/docview.wss?uid=swg21687173).
* También contiene una versión actualizada del perfil de Liberty basado en la versión [beta de noviembre](https://developer.ibm.com/wasdev/blog/2014/11/07/announcing-liberty-profile-beta-november/).

### 30 de octubre de 2014: actualización del paquete de compilación de Liberty v1.7-20141020-1759
* El paquete de compilación contiene una versión actualizada de IBM JRE 7.1 SR1 FP3.
* También proporciona un arreglo para un problema que impedía el despliegue de aplicaciones con una configuración de servidor que contuviera caracteres Unicode.

### 23 de octubre de 2014: actualización del paquete de compilación de Liberty
v1.6-20141013-1628
* Ahora el paquete de compilación se suministra con un nuevo recopilador de datos para [Monitoring and Analytics](../../services/monana/index.html). El nuevo recopilador de datos recopila información de diagnóstico muy detallada, que permite a los usuarios del plan de diagnósticos del servicio diagnosticar problemas con sus aplicaciones hasta la línea de código específica.
* El paquete de compilación contiene versiones actualizadas de los agentes de gestión y escalado automático que incluyen arreglos a problemas y pequeñas mejoras. También incluye una versión actualizada del [perfil de Liberty](https://developer.ibm.com/wasdev/) y del [controlador Java MongoDB](https://docs.mongodb.org/ecosystem/drivers/java/), v2.12.3.
* En la característica cloudAutowiring, se ha solucionado un error que generaba anomalías en la inyección de recursos en algunas aplicaciones.

### 3 de octubre de 2014: actualización del paquete de compilación de Liberty
v1.5-20140923-1143
* Con el paquete de compilación actualizado, ahora las aplicaciones pueden utilizar características beta de Liberty, incluidos WebSocket 1.0, Servlet 3.1 o JAX-RS 2.0. Para obtener más información, consulte [Utilización de las características beta](usingBetaFeatures.html).

### 30 de septiembre de 2014: actualización del paquete de compilación de Liberty
v1.4-20140908-1803
* Ahora el paquete de compilación ofrece soporte para los servicios de terceros ElephantSQL y ClearDB
MySQL Database. El soporte de configuración automática también funciona con los servicios experimentales
posgresql y mysql. Con un nuevo total de
13 servicios, el soporte de configuración automática del paquete de compilación de Liberty
agiliza y facilita el consumo de servicios Bluemix en aplicaciones Liberty.
* Durante la transferencia de la aplicación, el paquete de compilación muestra mensajes de registro mejorados sobre la configuración automática y otras acciones que emprende.
* El paquete de compilación contiene una versión actualizada del perfil de Liberty con arreglos y mejoras.
* También contiene una versión actualizada de IBM JRE versión 7.1 con mejoras en el rendimiento. Consulte también la página [Novedades](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.71.doc/diag/preface/changes_71/changes.html) para ver el conjunto de cambios detallado.

### 28 de agosto de 2014: actualización del paquete de compilación de Liberty
v1.3-20140818-1538
* El paquete de compilación contiene una versión actualizada del [perfil de Liberty](https://developer.ibm.com/wasdev/) con los últimos arreglos y mejoras.
* Esta versión del paquete de compilación arregla el soporte de la variable de entorno JAVA_OPTS para pasar opciones de JVM adicionales al tiempo de ejecución de la aplicación.
* También soluciona un problema que impedía el despliegue de aplicaciones Jar autónomas basadas en Spring.
* Ahora se puede generar y descargar rastreos snap JVM de IBM mediante la interfaz de usuario de Bluemix. Consulte el [tema sobre resolución de problemas](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/troubleshooting.html) de la documentación de JVM de IBM para obtener más información sobre los rastreos snap y otra información de diagnóstico que genera JVM.

### 29 de julio de 2014: actualización del paquete de compilación de Liberty
v1.1-20140725-1341
* Ya ha llegado la nueva versión de Bluemix Edition de Liberty.
  * Con esta versión de Liberty, hay arreglos además de nuevas características que le permiten consumir los servicios Bluemix de forma más eficiente.
  * Con la nueva característica CouchDB, ahora el servicio Cloudant® puede configurarla automáticamente para que un objeto de conector esté disponible de inmediato. Ya no es necesario analizar mediante
VCAP_SERVICES ni proporcionar los archivos jar del cliente de ektorp.
* La versión nueva de IBM SDK para Java ya ha llegado.
  * Cuando las aplicaciones se envíen de nuevo, utilizarán IBM SDK para Java Versión 7.1-1.0. Se acompaña
de una mejora sustancia en rendimiento. Su aplicación muestra mejor rendimiento y un menor uso de la memoria. Consulte más información sobre IBM Java SDK [aquí](http://www-01.ibm.com/support/docview.wss?uid=swg21671466).

  # rellinks
  ## general
  * [Tiempo de ejecución de Liberty](index.html)
  * [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
