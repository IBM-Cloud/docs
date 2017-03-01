---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Entwicklungstools und Entwicklungsumgebung
{: #c_beta_tooling}


Die folgenden Überlegungen beziehen sich auf die Tools und die Umgebung, die Sie
zur Entwicklung Ihrer {{site.data.keyword.streaminganalyticsshort}}-Anwendungen verwenden.
{:shortdesc}


* {{site.data.keyword.streaminganalyticsshort}} enthält keine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung oder Streams Studio in der Cloud. Entwickeln Sie Ihre Anwendungen in einer lokal installierten {{site.data.keyword.streamsshort}}-Umgebung und übergeben Sie sie als Anwendungsbundles. Wenn Sie nicht über die Entwicklungsumgebung verfügen, können Sie die {{site.data.keyword.streamsshort}} Quick Start Edition gebührenfrei von der [{{site.data.keyword.streamsshort}}-Produktseite](https://www.ibm.com/analytics/us/en/technology/stream-computing/#products) herunterladen.
* Kompilieren Sie das Anwendungsbundle in einer Red Hat Enterprise Linux 6.5-Umgebung oder einer funktional entsprechenden CentOS-Version, um die Kompatibilität sicherzustellen.
* Legen Sie in Ihrer {{site.data.keyword.streamsshort}}-Entwicklungsumgebung die Umgebungsvariable `JAVA_HOME` auf $STREAMS_INSTALL/java fest.
