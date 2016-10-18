---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Últimas actualizaciones
{: #latest_updates}
Última actualización: 17 de agosto de 2016
{: .last-updated}

Lista con las últimas actualizaciones del servicio.

## 17 de agosto de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Se han actualizado los binarios de WebSphere Application Server for Bluemix de 8.5.5.9 a 8.5.5.10
* Se han corregido [varias vulnerabilidades de seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21988710){: new_window} que afectan a WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Vulnerabilidades de Apache Struts que afectan a WebSphere Application Server y a la Consola de administración de WebSphere Application Server Hypervisor Edition.
  * Una posible denegación de la vulnerabilidad del servicio con IBM WebSphere Application Server cuando se utilizan servicios SIP.
  * Varias vulnerabilidades que pueden afectar al IBM HTTP Server utilizado por WebSphere Application Server.
  * Una vulnerabilidad que muestra la redirección del tráfico HTTP con aplicaciones CGI que puede afectar a IBM HTTP Server (IHS). Esta vulnerabilidad se conoce como "HTTPOXY".
  * Una vulnerabilidad de divulgación de la información en IBM WebSphere Application Server.
  * Una posible vulnerabilidad de omisión de la restricción de seguridad en IBM WebSphere Application Server que solo se produce en entornos en los que la propiedad personalizada de contenedor web HttpSessionIdReuse está habilitada.


## 24 de junio de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Se ha añadido una función para que los clientes puedan elegir entre V8.5 y V9.0 al crear una nueva instancia de *Traditional ND* o *Traditional WebSphere*.
* Se han actualizado los archivos binarios de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de modo que las nuevas instancias de WebSphere Application Server Liberty (Core y ND Plans) tengan el fixpack 16.0.0.2 instalado. 16.0.0.2 es el siguiente fixpack después de 8.5.5.9. A partir de 16.0.0.2, todas las funciones opcionales de Liberty admitidas para estos planes se instalarán de forma predeterminada.
* Se han corregido [varias vulnerabilidades relacionadas con la seguridad](http://www-01.ibm.com/support/docview.wss?uid=swg21984977){: new_window} que afectan a WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}, incluidas las siguientes:
  * Una vulnerabilidad de XML External Entity Injection (XXE) en Apache Standard Taglibs que afecta a IBM WebSphere Application Server.
  * Posibilidad de un nivel de seguridad inferior al esperado al utilizar la función de descubrimiento de la API de perfil de WebSphere Application Server Liberty y documentos de Swagger.
  * Una posible vulnerabilidad de divulgación de la información en Admin Center para IBM WebSphere Application Server Liberty.
  * Una posible vulnerabilidad de división de respuestas HTTP en IBM WebSphere Application Server.
  * Vulnerabilidades OpenSSL divulgadas el 3 de mayo de 2016 por OpenSSL Project.

## 13 de junio de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Se ha añadido la capacidad para que los clientes creen, suministren, gestionen y supriman instancias de máquinas virtuales mediante la creación de una aplicación o un script que utiliza las API RESTful de WebSphere Application Server for Bluemix.
* Se ha añadido la función que permite a un cliente tener un número fijo de instancias DETENIDAS con no más de 10 direcciones IP o 64 GB de memoria. Los clientes ahora se han cargado para instancias acumuladas en el estado DETENIDO a una tasa reducida del 5%.

## 26 de abril de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Se han abordado [las vulnerabilidades de seguridad potenciales](http://www-01.ibm.com/support/docview.wss?uid=swg21982128){: new_window} en WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} si FIPS 140-2 está habilitado y varias vulnerabilidades en Samba - incluido Badlock.
* Se ha integrado el mantenimiento de servicio.

## 15 de abril de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}

* Se han actualizado los archivos binarios de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de la versión 8.5.5.8 a la 8.5.5.9
* Se ha solucionado una vulnerabilidad de [scripts entre sitios](http://www-01.ibm.com/support/docview.wss?uid=swg21981221){: new_window} en Liberty para Java para IBM {{site.data.keyword.Bluemix_notm}} que afecta a los consumidores que utilizan el cliente OIDC (OpenID Connect).
* Se ha integrado el mantenimiento de servicio.

## 19 de febrero de 2016: Se ha actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Se ha añadido una opción para los clientes con aplicaciones que utilizan mucha memoria con el objeto de dimensionar adecuadamente el entorno con máquinas virtuales de mayor tamaño. Los clientes pueden seleccionar el tamaño de recurso específico de un componente de WebSphere Application Server determinado o un único sistema hasta una máquina virtual con 32 GB de RAM.
* Se han actualizado los binarios de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de 8.5.5.7 a 8.5.5.8
* Se han solucionado varias vulnerabilidades en IBM SDK Java Technology Edition que afectan a WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} y a las que comúnmente se hace referencia como [SLOTH](http://www-01.ibm.com/support/docview.wss?uid=swg21977244){: new_window}.
* Se ha solucionado una vulnerabilidad de [scripts entre sitios](http://www-01.ibm.com/support/docview.wss?uid=swg21976337){: new_window} que afecta a los consumidores de la salida del proveedor OAuth.
* Se ha integrado el mantenimiento de servicio.

## 11 de diciembre de 2015: Actualizado WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
* Ha cambiado el nombre oficial del producto IBM Application Server on Cloud for {{site.data.keyword.Bluemix_notm}} a IBM WebSphere Application Server for
{{site.data.keyword.Bluemix_notm}}
* Se han añadido nuevas funciones al plan de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment. El plan consiste en un entorno de células de WebSphere Application Server Network Deployment con dos o más máquinas
virtuales. Estas nuevas funciones permiten a los usuarios configurar un entorno en clúster para obtener alta
disponibilidad, migración tras error y escalabilidad.
* Se han añadido nuevas funciones para el plan Liberty Core de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}. El plan incluye
la utilización de Liberty Collective, que es un dominio administrativo para un grupo de perfiles de Liberty
(servidores) y consta de dos o más máquinas virtuales
* Se han actualizado los archivos binarios de WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} de 8.5.5.6 a 8.5.5.7
* Se ha resuelto una vulnerabilidad de [Apache Commons Collections](https://www.us-cert.gov/ncas/current-activity/2015/11/13/Apache-Commons-Collections-Java-Library-Vulnerability){: new_window} para gestionar la deserialización de objetos Java.
* Se ha resuelto la vulnerabilidad que podía permitir un ataque de división de respuestas [HTTP](http://www-01.ibm.com/support/docview.wss?uid=swg21972254){: new_window}.
* Se ha integrado el mantenimiento de servicio.

## 15 de octubre de 2015: Se ha actualizado Application Server on Cloud
* Se han añadido los siguientes planes nuevos:
  * [WebSphere Application Server Traditional V9 Beta](https://www-01.ibm.com/marketing/iwm/iwmdocs/web/cc/earlyprograms/websphere.shtml){: new_window}
  * WebSphere Application Server ND
* Mantenimiento de servicio
