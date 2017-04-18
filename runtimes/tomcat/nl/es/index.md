---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}

El tiempo de ejecución de Tomcat en {{site.data.keyword.Bluemix}} está basado en el java_buildpack.
{: shortdesc}

Para utilizar el tiempo de ejecución de Tomcat en {{site.data.keyword.Bluemix}}, debe especificar el java_buildpack con la opción -b. Por ejemplo:
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Para obtener más información sobre el tiempo de ejecución de Tomcat, consulte el
[java-buildpack readme](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Aplicación de inicio
{: #starter_application}

{{site.data.keyword.Bluemix}} proporciona una aplicación de inicio de Tomcat.  La aplicación de inicio de Tomcat es una app de Tomcat sencilla que proporciona una plantilla que puede utilizar. Puede experimentar con la app de inicio, y realizar y enviar los cambios por push al entorno de Bluemix. Consulte [Utilización de las aplicaciones de inicio](/docs/cfapps/starter_app_usage.html) para obtener ayuda con el uso de la aplicación de inicio.

## Versiones de tiempo de ejecución
{: #runtime_versions}

Puede cambiar la versión de Tomcat que utilizará la app con la variable de entorno JBP_CONFIG_TOMCAT.
Puede cambiar la versión de Java que utilizará la app con la variable de entorno JBP_CONFIG_OPEN_JDK_JRE.
Ambos se pueden especificar en el archivo de manifiesto de la aplicación.  Por ejemplo:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
La versión actual de java_buildpack es v3.6, que contiene la versión de Tomcat predeterminada 8.30.0 y la versión de Java predeterminada 1.8.0_71.
Para obtener más información, consulte [releases de java-buildpack](https://github.com/cloudfoundry/java-buildpack/releases).

## Redirección de HTTPS
{: #https_redirect}

El tiempo de Tomcat se puede configurar de modo que confíe en los proxies internos de Bluemix y permita la redirección del tráfico de HTTP a HTTPS (SSL).
Para ello, modifique el archivo server.xml estableciendo el elemento RemoteIpValve Valve con las opciones internalProxies y protocolHeader. 

El tiempo de ejecución de Tomcat [server.xml](https://github.com/cloudfoundry/java-buildpack/blob/master/resources/tomcat/conf/server.xml) que se incluye en el paquete de compilación solo establece la opción protocolHeader del elemento RemoteIpValve Valve de forma predeterminada. Para redirigir el tráfico de HTTP a HTTPS en Bluemix configure el elemento RemoteIpValve en el archivo server.xml personalizado del siguiente modo: 

```
 <Valve className='org.apache.catalina.valves.RemoteIpValve' protocolHeader='x-forwarded-proto' internalProxies='.*' />
```
{: codeblock}

Encontrará más opciones de configuración para RemoteIpValve en la [documentación de Tomcat](https://tomcat.apache.org/tomcat-8.0-doc/api/org/apache/catalina/valves/RemoteIpValve.html).

# rellinks
{: #rellinks}
## general
{: #general}
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
