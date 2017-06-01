---

copyright:
  years: 2015, 2016
lastupdated: "2017-04-07"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Últimas actualizaciones
{: #latest_updates}

Lista con las últimas actualizaciones del servicio.

## 15 de marzo de 2017: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha integrado el mantenimiento de servicio.
* Se han actualizado los archivos binarios de WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} de modo el fixpack 8.5.5.11 ó 9.0.0.3 se instala con nuevas instancias de WebSphere Application Server tradicional. 
* Se han solucionado [varias vulnerabilidades de seguridad](https://www-01.ibm.com/support/docview.wss?uid=swg22000587){: new_window} en WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} que incluyen: 
  * Una vulnerabilidad no especificada relacionada con el componente Bibliotecas que no afecta a la confidencialidad ni a disponibilidad y tiene un alto impacto sobre la integridad. 
  * Una vulnerabilidad no especificada relacionada con el componente Bibliotecas que podía permitir que un atacante remoto obtuviera información confidencial, lo que tendría un alto impacto sobre la confidencialidad, utilizando vectores de ataque desconocidos. 
  * Una vulnerabilidad no especificada relacionada con el componente Bibliotecas que podía permitir que un atacante ocasionara una denegación de servicio, lo que tendría un alto impacto sobre la disponibilidad, utilizando vectores de ataque desconocidos. 
  * Una potencial vulnerabilidad en OpenSSL que permitía a un atacante remoto obtener información confidencial, ocasionada por un error en el cifrado DES/3DES, utilizado como parte del protocolo SSL/TLS. 
  * Una vulnerabilidad que permitía a los usuarios incorporar código JavaScript arbitrario en la IU web, modificando la funcionalidad inicial, lo que podría dar lugar a una divulgación de credenciales dentro de una sesión fiable. 
  * Una vulnerabilidad en cuanto a ataques de división de respuestas de HTTPD a HTTP, ocasionada por una validación incorrecta de la información de entrada especificada por el usuario. 
  * Una vulnerabilidad en Samba que podría permitir que un atacante autenticado remoto obtuviera privilegios elevados sobre el sistema, ocasionada por un error de gestión de la suma de comprobación de PAC. 
  * Una vulnerabilidad en Samba que podría permitir que un atacante autenticado remoto obtuviera privilegios elevados sobre el sistema, ocasionada por el reenvío de un TGT (Ticket Granting Ticket) a otro servicio cuando se utilizaba la autenticación Kerberos. 
  * Una vulnerabilidad en Samba relacionada con un desbordamiento del almacenamiento intermedio basado en almacenamiento dinámico, ocasionada por un defecto de acomodamiento de enteros en la función ndr_pull_dnsp_name(). 


## 10 de febrero de 2017: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha integrado el mantenimiento de servicio.
* Se han actualizado los archivos binarios de WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} de modo el fixpack 8.5.5.11 ó 9.0.0.2 se instala con nuevas instancias de WebSphere Application Server tradicional. 
* Se han actualizado los archivos binarios de WebSphere Application Server in {{site.data.keyword.Bluemix_notm}} de modo que el fixpack 16.0.0.4 se instala con nuevas instancias de WebSphere Application Server Liberty (Core y ND Plans). 
* Se han solucionado [varias vulnerabilidades de seguridad](https://www-01.ibm.com/support/docview.wss?uid=swg21997657){: new_window} en WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} que incluyen: 
  * Una vulnerabilidad de denegación de servicio ocasionada porque se permitía la ejecución de objetos serializados procedentes de fuentes no fiables derivada que ocasionaba un consumo de recursos. 
  * El uso de solicitudes SOAP mal formadas, que podría permitir que un atacante remoto obtuviera información confidencial. 


## 16 de diciembre de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha integrado el mantenimiento de servicio.
* Se han solucionado [varias vulnerabilidades de seguridad](https://www-01.ibm.com/support/docview.wss?uid=swg21995995){: new_window} en IBM SDK Java Technology Edition que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} que incluyen: 
  * Una vulnerabilidad no especificada en Oracle SE y Java SE Embedded relacionada con el componente Hotspot con un alto impacto sobre la confidencialidad, la integridad y la disponibilidad. 
  * Una vulnerabilidad no especificada en Oracle Java SE y Java SE Embedded relacionada con el componente Red que podía permitir que un atacante remoto obtuviera información confidencial, lo que tendría un alto impacto sobre la confidencialidad, utilizando vectores de ataque desconocidos. 
  *  Una vulnerabilidad en el script entre sitios en IBM WebSphere Application Server que permitía a los usuarios incorporar código JavaScript arbitrario en la IU web, modificando la funcionalidad inicial, lo que podría dar lugar a una divulgación de credenciales dentro de una sesión fiable. 


## 8 de noviembre de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha añadido a los clientes capacidad para solicitar una dirección [IP pública](networkEnvironment.html#networkEnvironment) para su WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} VM
* Se han corregido [varias vulnerabilidades de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21993842){: new_window} que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Una vulnerabilidad en IBM WebSphere Application Server que permitía a atacantes remotos ejecutar código Java arbitrario con un objeto serializado desde orígenes no fiables. 
  * Una vulnerabilidad de denegación de servicio causada por una lectura fuera de límite en la función TS_OBJ_print_bio. Un atacante remoto podía aprovechar esta vulnerabilidad utilizando un archivo con una indicación de fecha y hora especialmente adaptada para hacer que la aplicación se bloqueara. 
  * Una potencial vulnerabilidad en OpenSSL que permitía a un atacante remoto obtener información confidencial, ocasionada por un error en Triple-DES en la cifra de bloque de 64 bits que se utiliza como parte del protocolo SSL/TLS. Mediante la captura de grandes cantidades de tráfico cifrado entre el servidor SSL/TLS y el cliente, un atacante remoto capaz de realizar un ataque de tipo man-in-the-middle podía aprovechar esta vulnerabilidad para recuperar los datos de texto din cifrar y obtener información confidencial. Esta vulnerabilidad se conoce como ataque SWEET32 Birthday. 
  * OpenSSL es vulnerable a la denegación de servicio. Mediante la solicitud repetida de renegociación, un atacante remoto autenticado podría enviar una extensión de OCSP Status de gran tamaño para consumir todos los recursos de memoria disponibles. 
  * OpenSSL es vulnerable a una denegación de servicio debido a un desbordamiento de enteros de una función MDC2_Update. Mediante el uso de vectores de ataque desconocidos, un atacante remoto podía aprovechar esta vulnerabilidad para activar una grabación fuera de límites y hacer que la aplicación se bloqueara. 
  * Una potencial vulnerabilidad en OpenSSL que permitía a un atacante remoto obtener información confidencial, ocasionada por un error en la implementación de DSA que permite el seguimiento de una vía de acceso de código en tiempo no constante para ciertas operaciones. Un atacante podía aprovechar esta vulnerabilidad utilizando un ataque de sincronización de caché para recuperar la clave DSA privada. 
  * OpenSSL es vulnerable a una denegación de servicio debido a la falta de comprobaciones de la longitud de los mensajes cuando se analizan certificados. Un atacante remoto autenticado podía aprovechar esta vulnerabilidad para activar una lectura fuera de límites y ocasionar una denegación de servicio. 

## 19 de septiembre de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se han actualizado los archivos binarios de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} de modo que las nuevas instancias de WebSphere Application Server Liberty (Core y ND Plans) tengan el fixpack 16.0.0.3 instalado. 
* Se han corregido [varias vulnerabilidades de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21990236){: new_window} que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Una vulnerabilidad en IBM WebSphere Application Server Liberty que permitía a un atacante remoto realizar ataques de tipo phishing. 
  * Una vulnerabilidad en IBM WebSphere Application Server Liberty que permitía cruzar scripts en clientes de OpenID Connect. 
  * Una potencial vulnerabilidad en IBM WebSphere Application Server Liberty que permitía a un atacante remoto obtener información confidencial debido al manejo incorrecto de excepciones cuando no existe una página de error predeterminada. 
  * Una vulnerabilidad en Apache Tomcat frente a una denegación de servicio, ocasionada por un error en el componente Apache Commons File Upload. 
  * Una vulnerabilidad en IBM WebSphere Application Server e IBM WebSphere Application Server Liberty que permitía a un atacante remoto obtener información confidencial debido al manejo incorrecto de respuestas bajo determinadas circunstancias. 
  * Una vulnerabilidad no especificada relacionada con el componente Networking que no afecta a la confidencialidad ni a disponibilidad y tiene un bajo impacto sobre la integridad. 

## 17 de agosto de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se han actualizado los binarios de WebSphere Application Server en Bluemix de 8.5.5.9 a 8.5.5.10
* Se han corregido [varias vulnerabilidades de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Vulnerabilidades de Apache Struts que afectan a WebSphere Application Server y a la Consola de administración de WebSphere Application Server Hypervisor Edition.
  * Una posible denegación de la vulnerabilidad del servicio con IBM WebSphere Application Server cuando se utilizan servicios SIP.
  * Varias vulnerabilidades que pueden afectar al IBM HTTP Server utilizado por WebSphere Application Server.
  * Una vulnerabilidad que muestra la redirección del tráfico HTTP con aplicaciones CGI que puede afectar a IBM HTTP Server (IHS). Esta vulnerabilidad se conoce como "HTTPOXY".
  * Una vulnerabilidad de divulgación de la información en IBM WebSphere Application Server.
  * Una posible vulnerabilidad de omisión de la restricción de seguridad en IBM WebSphere Application Server que solo se produce en entornos en los que la propiedad personalizada de contenedor web HttpSessionIdReuse está habilitada.


## 24 de junio de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha añadido una función para que los clientes puedan elegir entre V8.5 y V9.0 al crear una nueva instancia de *Traditional ND* o *Traditional WebSphere*.
* Se han actualizado los archivos binarios de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} de modo que las nuevas instancias de WebSphere Application Server Liberty (Core y ND Plans) tengan el fixpack 16.0.0.2 instalado. 16.0.0.2 es el siguiente fixpack después de 8.5.5.9. A partir de 16.0.0.2, todas las funciones opcionales de Liberty admitidas para estos planes se instalarán de forma predeterminada.
* Se han corregido [varias vulnerabilidades relacionadas con la seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Una vulnerabilidad de XML External Entity Injection (XXE) en Apache Standard Taglibs que afecta a IBM WebSphere Application Server.
  * Posibilidad de un nivel de seguridad inferior al esperado al utilizar la función de descubrimiento de la API de perfil de WebSphere Application Server Liberty y documentos de Swagger.
  * Una posible vulnerabilidad de divulgación de la información en Admin Center para IBM WebSphere Application Server Liberty.
  * Una posible vulnerabilidad de división de respuestas HTTP en IBM WebSphere Application Server.
  * Vulnerabilidades OpenSSL divulgadas el 3 de mayo de 2016 por OpenSSL Project.

## 13 de junio de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se ha añadido la capacidad para que los clientes creen, suministren, gestionen y supriman instancias de máquinas virtuales mediante la creación de una aplicación o un script que utiliza las API RESTful de WebSphere Application Server en Bluemix.
* Se ha añadido la función que permite a un cliente tener un número fijo de instancias DETENIDAS con no más de 10 direcciones IP o 64 GB de memoria. Los clientes ahora se han cargado para instancias acumuladas en el estado DETENIDO a una tasa reducida del 5%.

## 26 de abril de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se han abordado [las vulnerabilidades de seguridad potenciales](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} en WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} si FIPS 140-2 está habilitado y varias vulnerabilidades en Samba - incluido Badlock.
* Se ha integrado el mantenimiento de servicio.

## 15 de abril de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}

* Se han actualizado los archivos binarios de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} de la versión 8.5.5.8 a la 8.5.5.9
* Se ha solucionado una vulnerabilidad de [scripts entre sitios](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} en Liberty para Java para IBM {{site.data.keyword.Bluemix_notm}} que afecta a los consumidores que utilizan el cliente OIDC (OpenID Connect).
* Se ha integrado el mantenimiento de servicio.

## 19 de febrero de 2016: Se ha actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}
* Se ha añadido una opción para los clientes con aplicaciones que utilizan mucha memoria con el objeto de dimensionar adecuadamente el entorno con máquinas virtuales de mayor tamaño. Los clientes pueden seleccionar el tamaño de recurso específico de un componente de WebSphere Application Server determinado o un único sistema hasta una máquina virtual con 32 GB de RAM.
* Se han actualizado los binarios de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} de 8.5.5.7 a 8.5.5.8
* Se han solucionado varias vulnerabilidades en IBM SDK Java Technology Edition que afectan a WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} y a las que comúnmente se hace referencia como [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Se ha solucionado una vulnerabilidad de [scripts entre sitios](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} que afecta a los consumidores de la salida del proveedor OAuth.
* Se ha integrado el mantenimiento de servicio.

## 11 de diciembre de 2015: Actualizado WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}
* Ha cambiado el nombre oficial del producto IBM Application Server on Cloud en {{site.data.keyword.Bluemix_notm}} a IBM WebSphere Application Server en
{{site.data.keyword.Bluemix_notm}}
* Se han añadido nuevas funciones al plan de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} Network Deployment. El plan consiste en un entorno de células de WebSphere Application Server Network Deployment con dos o más máquinas
virtuales. Estas nuevas funciones permiten a los usuarios configurar un entorno en clúster para obtener alta
disponibilidad, migración tras error y escalabilidad.
* Se han añadido nuevas funciones para el plan Liberty Core de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}}. El plan incluye
la utilización de Liberty Collective, que es un dominio administrativo para un grupo de perfiles de Liberty
(servidores) y consta de dos o más máquinas virtuales
* Se han actualizado los archivos binarios de WebSphere Application Server en {{site.data.keyword.Bluemix_notm}} de 8.5.5.6 a 8.5.5.7
* Se ha resuelto una vulnerabilidad de [Apache Commons Collections](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} para gestionar la deserialización de objetos Java.
* Se ha resuelto la vulnerabilidad que podía permitir un ataque de división de respuestas [HTTP](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Se ha integrado el mantenimiento de servicio.

## 15 de octubre de 2015: Se ha actualizado Application Server on Cloud
* Se han añadido los siguientes planes nuevos:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Mantenimiento de servicio
