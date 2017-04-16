---

copyright:
  years: 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Offlinemodus für Liberty
{: #offline_mode}

Wenn eine Liberty-Anwendung an {{site.data.keyword.Bluemix}} mit einer Push-Operation übertragen wird, kann das Liberty-Buildpack auf externe Sites in Bluemix zugreifen, um von der Anwendung benötigte Artefakte anzufordern.  Das Liberty-Buildpack kann auf folgende externe Sites zugreifen.  In den Umgebungen [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local) müssen diese Sites *in Whitelist aufgeführt* sein.

* https://download.run.pivotal.io und https://java-buildpack.cloudfoundry.org werden verwendet, um auf Komponenten zuzugreifen für:
  * [AppDynamics-Agent](https://www.appdynamics.com/)
  * [MariaDB JDBC-Treiber](https://mariadb.com/)
  * [New Relic-Agent](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC-Treiber](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ wird verwendet, um auf Komponenten für [JRebel](https://zeroturnaround.com/software/jrebel/) zuzugreifen.
* https://download.ruxit.com/agent/paas/cloudfoundry/java um auf Komponenten für den [Dynatrace Ruxit-Agenten](dynatrace.html) zuzugreifen.
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ wird verwendet, um auf den [Dynatrace-Agenten](dynatrace.html) zuzugreifen.

## Mit einem Proxy arbeiten
{: #working_with_proxy}

In einigen Umgebungen, wie beispielsweise [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local), kann ein Proxy konfiguriert werden. Weitere Informationen finden Sie unter [Mit einem Proxy arbeiten](/docs/manageapps/workingWithProxy.html).

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
