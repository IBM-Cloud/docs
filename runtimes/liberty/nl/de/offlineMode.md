---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Offlinemodus für Liberty
{: #offline_mode}

Wenn eine Liberty-Anwendung an {{site.data.keyword.Bluemix}} mit einer Push-Operation übertragen wird, kann das Liberty-Buildpack auf externe Sites in Bluemix zugreifen, um von der Anwendung benötigte Artefakte anzufordern.  Das Liberty-Buildpack kann auf folgende externe Sites zugreifen.  In den Umgebungen [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local) müssen diese Sites *in Whitelist aufgeführt* sein.

* https://download.run.pivotal.io und https://java-buildpack.cloudfoundry.org werden verwendet, um auf Komponenten zuzugreifen für:
  * [AppDynamics-Agent ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.appdynamics.com/)
  * [MariaDB JDBC-Treiber ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://mariadb.com/)
  * [New Relic-Agent](newRelic.html)
  * [OpenJDK](customizingJRE.html#OpenJDK)
  * [PostgreSQL JDBC-Treiber ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://www.postgresql.org)
* https://dl.zeroturnaround.com/jrebel/ wird verwendet, um auf Komponenten für [JRebel ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://zeroturnaround.com/software/jrebel/) zuzugreifen.
* https://download.ruxit.com/agent/paas/cloudfoundry/java wird verwendet, um auf Komponenten für den [Dynatrace Ruxit-Agenten](dynatrace.html) zuzugreifen.
* http://downloads.dynatracesaas.com/cloudfoundry/buildpack/java/ wird verwendet, um auf den [Dynatrace-Agenten](dynatrace.html) zuzugreifen.

## Mit einem Proxy arbeiten
{: #working_with_proxy}

In einigen Umgebungen, wie beispielsweise [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und [Bluemix Local](/docs/local/index.html#local), kann ein Proxy konfiguriert werden. Weitere Informationen finden Sie unter [Mit einem Proxy arbeiten](/docs/manageapps/workingWithProxy.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
