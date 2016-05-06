---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Liberty for Java
{: #liberty_runtime}

*Última actualización: 23 de marzo de 2016*

Las aplicaciones Liberty for Java de {{site.data.keyword.Bluemix}} se basan en el paquete de compilación liberty-for-java. El paquete de compilación liberty-for-java proporciona un entorno de ejecución completo para la ejecución de aplicaciones Java EE 7 y OSGi sobre el perfil de Liberty. Admite infraestructura extendidas, como Spring e incluye IBM JRE. WebSphere Liberty permite desarrollar rápidamente aplicaciones adaptadas a la nube.
{: shortdesc}

## Detección
{: #detection}
El paquete de compilación de Liberty se utiliza cuando se despliegan los siguientes tipos de aplicaciones:
* [Archivos WAR](optionsForPushing.html#stand_alone_apps)
* [Archivos EAR](optionsForPushing.html#stand_alone_apps)
* [Directorio del servidor de Liberty](optionsForPushing.html#server_directory)
* [Servidor empaquetado de Liberty](optionsForPushing.html#packaged_server)
* Principal de Java
* [Distzip](https://github.com/cloudfoundry/ibm-websphere-liberty-buildpack/blob/master/docs/container-distZip.md)

## Aplicación de inicio
{: #starter_application}
{{site.data.keyword.Bluemix}} proporciona varias aplicaciones de inicio de Liberty.  Las aplicaciones de inicio de Liberty son apps de Liberty sencillas que proporcionan una plantilla que puede utilizar. Puede experimentar con las apps de inicio, y realizar y enviar los cambios al entorno de Bluemix.  Consulte [Utilización de las aplicaciones de inicio](../../cfapps/starter_app_usage.html) para obtener ayuda con el uso de las aplicaciones de inicio.

# rellinks
## general
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
* [Gestión de apps de Liberty](../../manageapps/app_mng.html#Utilities)
* [Despliegue de apps con IBM Eclipse Tools for Bluemix](../../manageapps/eclipsetools/eclipsetools.html#eclipsetools)
* [Iniciación a IBM Monitoring and
Analytics for Bluemix Service](../../services/monana/index.html#monana_oview)
## muestras
* [Cloud Foundry Architecture Labs](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/)
