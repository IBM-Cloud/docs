---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# Tomcat
{: #tomcat_runtime}
*Letzte Aktualisierung: 19. März 2016*

Die Laufzeit von Tomcat in {{site.data.keyword.Bluemix}} basiert auf dem Buildpack 'java_buildpack'.
{: shortdesc}

Zum Verwenden der Tomcat-Laufzeit in {{site.data.keyword.Bluemix}} müssen Sie das Buildpack 'java_buildpack' zusammen mit der Option '-b' angeben. Beispiel:
<pre>
    cf push &lt;myApp&gt; -p &lt;pathToMyApp&gt; -b java_buildpack
</pre>

Weitere Informationen zur Tomcat-Laufzeit finden Sie in der [Readme-Datei zu 'java-buildpack'](https://github.com/cloudfoundry/java-buildpack/blob/master/README.md).

## Starteranwendung
{: #starter_application}

{{site.data.keyword.Bluemix}} stellt eine Tomcat-Starteranwendung bereit.  Die Tomcat-Starteranwendung ist eine einfache Tomcat-App, die Sie als Schablone verwenden können. Sie können mit der Starter-App experimentieren, Änderungen an der Bluemix-Umgebung vornehmen und diese mit einer Push-Operation übertragen. Hilfe zur Verwendung der Starteranwendung finden Sie in [Starteranwendungen verwenden](../../cfapps/starter_app_usage.html).

## Laufzeitversionen
{: #runtime_versions}

Sie können die Version von Tomcat, die von Ihrer App verwendet werden soll, mit der Umgebungsvariablen JBP_CONFIG_TOMCAT ändern.
Sie können die Version von Java, die von Ihrer App verwendet werden soll, mit der Umgebungsvariablen JBP_CONFIG_OPEN_JDK_JRE ändern.
Beide können in der Manifestdatei der Anwendung angegeben werden.  Beispiel:
```
    env:
        JBP_CONFIG_TOMCAT: '{tomcat: { version: 8.0.+ }}'
        JBP_CONFIG_OPEN_JDK_JRE: '{jre: { version: 1.7.0_+ }}'
```
{: codeblock}
Die aktuelle Tomcat-Standardversion ist 8.0.30.  Die aktuelle Java-Standardversion ist 1.8.0_65.
Weitere Informationen finden Sie in [java-buildpack releases](https://github.com/cloudfoundry/java-buildpack/releases).

# Zugehörige Links
## Allgemein
* [java-buildpack](https://github.com/cloudfoundry/java-buildpack)
