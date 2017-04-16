---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Modo fuera de línea para Liberty
{: #offline_mode}

Cuando se envía por push una aplicación Liberty a {{site.data.keyword.Bluemix}}, el paquete de compilación de Liberty puede acceder a sitios externos a Bluemix
para adquirir artefactos que necesita la aplicación.  A continuación se muestran los sitios externos a los que puede acceder el paquete de compilación de Liberty.  En los entornos [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), es posible que estos sitios necesiten incluirse en una *lista blanca*.

* https://download.run.pivotal.io y https://java-buildpack.cloudfoundry.org se utilizan para acceder a componentes para:
  * [Agente de AppDynamics](https://www.appdynamics.com/)
  * [Controlador JDBC de MariaDB](https://mariadb.com/)
  * [Agente New Relic](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [Controlador JDBC de PostgreSQL](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ se utiliza para acceder a componentes para [JRebel](https://zeroturnaround.com/software/jrebel/).
* https://download.ruxit.com/agent/paas/cloudfoundry/java se utiliza para acceder a componentes para el [Agente de Dynatrace Ruxit](dynatrace.html).
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ se utiliza para acceder al [Agente de Dynatrace](dynatrace.html).

## Cómo trabajar con un proxy
{: #working_with_proxy}

En algunos entornos como por ejemplo [Bluemix dedicado](/docs/dedicated/index.html#dedicated) y
[Bluemix local](/docs/local/index.html#local), se puede configurar un proxy. Consulte [Cómo trabajar con un proxy](/docs/manageapps/workingWithProxy.html) para obtener más detalles.

# rellinks
{: #rellinks}
## general
{: #general}
* [Tiempo de ejecución de Liberty](index.html)
* [Visión general del perfil de Liberty](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
