---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Fehlerbehebung
{: #ts}

Manche bekannte Probleme mit dem {{site.data.keyword.dev_cli_notm}} sind zusammen mit den entsprechenden Problemumgehungen dokumentiert.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Bekannte Probleme
{: #knownissues}

In den folgenden Abschnitten werden bekannte Probleme und mögliche Lösungen beschrieben. 


### Fehler im Hostnamen beim Erstellen eines Projekts mit nicht mobilem Muster
{: #hostname}

Es wird der folgende Fehler angezeigt, wenn Sie mit dem {{site.data.keyword.dev_cli_short}} unter Verwendung von Web-App-, BFF- oder Microservice-Mustern ein Projekt erstellen: 

```
The hostname <myHostname> is taken.
```
{: codeblock}


#### Ursache
{: #hostname-cause}
   
Dieser Fehler tritt aufgrund einer abgelaufenen Anmeldung auf. 


#### Lösung
{: #hostname-resolution}

Erneute Anmeldung. 

```
bx login
```
{: codeblock}


### Allgemeine Fehler mit dem {{site.data.keyword.dev_cli_short}}
{: #general}

Es wird eventuell der folgende Fehler angezeigt, wenn Sie mit dem {{site.data.keyword.dev_cli_short}} Befehle erstellen, löschen, auflisten oder codieren: 

```
Failed to <command> project.
```
{: codeblock}


#### Ursache
{: #hostname-cause}
   
Dieser Fehler tritt aufgrund einer abgelaufenen Anmeldung auf. 


#### Lösung
{: #hostname-resolution}

Erneute Anmeldung. 

```
bx login
```
{: codeblock}


### Service-Broker-Fehler während Hinzufügen einer {{site.data.keyword.objectstorageshort}}-Funktion
{: #os}

Es wird eventuell der folgende Fehler angezeigt, wenn Sie das {{site.data.keyword.dev_cli_short}} zum Erstellen von zwei Projekten mit der {{site.data.keyword.objectstorageshort}}-Funktion verwenden. 

```
FAILED
Service broker error: {"description"=>"You can not create this Object Storage instance. Each organization using the Object Storage service is limited to one instance of the Free plan."}
```
{: codeblock}


#### Ursache
{: #os-cause}
   
Dieser Fehler tritt auf, weil der Service {{site.data.keyword.objectstorageshort}} nur eine Instanz des kostenlosen {{site.data.keyword.objectstorageshort}}-Plans zulässt. 


#### Lösung
{: #os-resolution}

Sie werden aufgefordert, einen anderen Plan zum Vermeiden dieses Fehlers auszuwählen. 


### Fehler beim Abrufen des Code während der Projekterstellung
{: #code}

Es wird eventuell der folgende Fehler angezeigt, wenn Sie das {{site.data.keyword.dev_cli_short}} zum Erstellen eines Projekts verwenden: 
	
```
FAILED
Project created, but could not get code
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Ursache
{: #code-cause}

Dieser Fehler tritt aufgrund einer internen Zeitlimitüberschreitung auf. 
	

#### Lösung
{: #code-resolution}

Sie können den Code auf eine der folgenden Arten abrufen: 

* Führen Sie den folgenden Befehl in der Befehlszeilenschnittstelle aus: 

	```
	bx dev code <your-project-name>
	```
	{: codeblock}
	
	`<your-project-name>` muss durch den Projektnamen ersetzt werden, den Sie während der Projekterstellung verwendet haben. 

* Verwenden Sie die {{site.data.keyword.dev_console}}.

	1. Verwenden Sie Ihr [Projekt ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://console.{DomainName}/developer/projects) in der {{site.data.keyword.dev_console}} und klicken Sie auf **Code abrufen**. 

	2. Klicken Sie auf **Code generieren**. 

	3. Klicken Sie nach der Generierung des Codes auf **Code herunterladen**. 


### Fehler beim Ausführen von `bx dev run` für Node.js-Projekte
{: #node}

Es wird eventuell der folgende Fehler angezeigt, wenn Sie `bx dev run` mit dem {{site.data.keyword.dev_cli_short}} für Node.js-Web- oder BFF-Projekte ausführen: 

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Ursache
{: #node-cause}
   
Dieser Fehler tritt auf, weil das Modul `appmetrics` in einer anderen Architektur installiert ist. Native NPM-Module, die in einer Architektur installiert sind, funktionieren nicht in einer anderen. Die im Lieferumfang enthaltenen Docker-Images basieren auf einem Linux-Kernel. 


#### Lösung
{: #node-resolution}

Löschen Sie den Ordner `node_modules` und führen Sie den Befehl `bx dev run` erneut aus. 


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Hilfe und Unterstützung abrufen
{: #gettinghelp}

Falls Sie Probleme oder Fragen haben, wenn Sie die {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} oder das {{site.data.keyword.dev_cli_notm}} verwenden, können Sie Hilfe abrufen, indem Sie in einem Forum nach Informationen suchen oder Fragen stellen. Sie können auch ein Support-Ticket öffnen. 

Wenn Sie in einem Forum eine Frage stellen, versehen Sie diese Frage mit einem Tag, damit Sie von den {{site.data.keyword.Bluemix_notm}}-Entwicklerteam angezeigt werden kann. 

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

Wenn Sie technische Fragen zum Entwickeln oder Bereitstellen einer App mit der {{site.data.keyword.dev_console}} oder dem {{site.data.keyword.dev_cli_notm}} haben: 

* Senden Sie Ihre Frage an [Stacküberlauf ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) und markieren Sie Ihre Frage mit `bluemix-dev-services` und `ibm-bluemix`. 
* Senden Sie Ihre Frage an [Slack ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm-cloud-tech.slack.com/) im `bluemix-dev-services`-Kanal. [Melden Sie sich heute an ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](http://ibm.biz/IBMCloudNativeSlack) an. 


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

Weitere Information zur Nutzung der Foren finden Sie unter [Hilfe abrufen ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/support/index.html#getting-help). 

Informationen zum Öffnen eines {{site.data.keyword.IBM}} Support-Tickets oder zu den Support-Leveln und der Dringlichkeit von Tickets finden Sie unter [Unterstützung anfordern ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](/docs/support/index.html#contacting-support). 

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

