---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Trabajar con un proxy
{: #working_with_proxy}



En algunos entornos como [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), es posible configurar un proxy que afecte al comportamiento de la aplicación durante la etapa de transferencia y de tiempo de ejecución.

Puede configurar la aplicación para que funcione con el proxy utilizando las variables de entorno siguiente:
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

Puede establecer estas variables de entorno utilizando *cf se* o a través del archivo
*manifest.yml*.  Si la aplicación necesita que los recursos se descarguen de Internet durante la transferencia y se establece una variable de entorno de proxy, en función de cómo se configuren las variables de entorno de proxy, los recursos se descargarán a través del proxy configurado.

Por ejemplo, supongamos que tiene una aplicación nodejs y que la ejecución se realiza en un entorno con *http_proxy* establecido en
*yourProxyURL*.  Supongamos también que desea permitir que npm pueda descargar módulos de nodo desde Internet. Para conseguirlo, podría establecer *no_proxy* en *npmjs.org*.

**Nota**: puede que sea el caso de que la aplicación se beneficie del proxy durante el tiempo de ejecución.  Esto es totalmente dependiente de la aplicación y no influye ni el paquete de compilación ni ninguna de estas tres variables de entorno.

## Aplicaciones Java
{: #java_apps}

Para [Liberty for Java](/docs/runtimes/liberty/index.html) y las aplicaciones [java_buildpack](/docs/runtimes/tomcat/index.html), los valores de proxy pueden pasarse al entorno de ejecución a través de la variable de entorno **JAVA_OPTS**.  Por ejemplo, puede emitir el mandato:
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

y volver a transferir la aplicación.  La aplicación utilizará los valores de proxy especificados en tiempo de ejecución. Consulte [Redes y proxies Java](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html) para obtener más información sobre las opciones de proxy de Java.

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
