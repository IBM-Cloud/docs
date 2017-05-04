---

copyright:
  years: 2016, 2017
lastupdated: "2016-07-20"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Mit Proxys arbeiten
{: #working_with_proxy}



In einigen Umgebungen wie [Bluemix Dedicated](/docs/dedicated/index.html#dedicated) und
[Bluemix Local](/docs/local/index.html#local) kann ein Proxy konfiguriert werden, was sich auf das Verhalten der Anwendung beim Staging und während der Laufzeit auswirkt.

Mit den folgenden Umgebungsvariablen können Sie Ihre Anwendung für den Proxy konfigurieren:
  * [http_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [https_proxy](https://docs.cloudfoundry.org/buildpacks/proxy-usage.html)
  * [no_proxy](http://www.gnu.org/software/wget/manual/html_node/Proxies.html)

Diese Umgebungsvariablen werden mit *cf se* oder über die Datei *manifest.yml* definiert.  Wenn Sie beim Staging für Ihre Anwendung Ressourcen aus dem Internet herunterladen müssen und eine Proxy-Umgebungsvariable definiert ist, werden diese Ressourcen je nachdem, wie die Proxy-Umgebungsvariablen definiert sind, über den konfigurierten Proxy heruntergeladen.

Beispiel: Sie verfügen über eine Node.js-Anwendung und in Ihrer Umgebung ist *http_proxy* auf *yourProxyURL* gesetzt.  Sie möchten nicht, dass 'npm' Knotenmodule aus dem Internet herunterlädt. Zu diesem Zweck könnten Sie *no_proxy* auf *npmjs.org* setzen.

**Hinweis:** Es kann vorkommen, dass Ihre Anwendung den Proxy während der Laufzeit nutzt.  Dieses Verhalten ist anwendungsspezifisch und wird nicht vom Buildpack oder diesen drei Umgebungsvariablen beeinflusst.

## Java-Anwendungen
{: #java_apps}

Für [Liberty for Java](/docs/runtimes/liberty/index.html) und die [java_buildpack](/docs/runtimes/tomcat/index.html)-Anwendungen können die Proxy-Einstellungen über die Umgebungsvariable **JAVA_OPTS** an die Laufzeit übergeben werden.  Geben Sie beispielsweise den folgenden Befehl ein:
```
   $ cf se myApp JAVA_OPTS "-Dhttp.proxyHost=yourProxyURL -Dhttp.proxyPort=yourProxyPort"
```
{: codeblock}

Führen Sie ein erneutes Staging für die Anwendung durch.  Die angegebenen Proxy-Einstellungen werden daraufhin zur Laufzeit von der Anwendung verwendet. Weitere Informationen zu den Java-Proxy-Optionen finden Sie in [Java Networking and Proxies](https://docs.oracle.com/javase/8/docs/technotes/guides/net/proxies.html).

# rellinks
{: #rellinks notoc}
## general
{: #general}
* [Liberty for Java](/docs/runtimes/liberty/index.html)
* [SDK for Nodejs](/docs/runtimes/nodejs/index.html)
