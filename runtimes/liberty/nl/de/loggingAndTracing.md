---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Protokollierung und Tracing
{: #logging_tracing}

## Protokolldateien
{: #log_files}

Die Liberty-Standardprotokolle wie beispielsweise 'messages.log' oder das Verzeichnis 'ffdc' stehen in IBM Bluemix in den Protokollverzeichnissen der einzelnen Anwendungsinstanzen zur Verfügung. Auf diese Protokolle kann über die Konsole von IBM Bluemix oder mithilfe der Befehle 'cf logs' und 'cf files' zugegriffen werden.
Führen Sie beispielsweise zum Anzeigen der Datei 'messages.log' folgenden Befehl aus:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

Die Protokollebene und weitere Traceoptionen können in der Liberty-Konfigurationsdatei definiert werden. Weitere Informationen hierzu finden Sie unter [Liberty-Profil: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Das Tracing kann mithilfe der Konsole von IBM Bluemix auch in einer aktive Anwendungsinstanz angepasst werden.

## Trace- und Speicherauszugsfunktionen verwenden
{: #using_trace_and_dump}

In der Benutzerschnittstelle von IBM Bluemix gibt es Trace- und Speicherauszugsfunktionen.
* Mit der Option 'Trace' kann die Tracespezifikation der Liberty-Protokollierung für aktive Anwendungsinstanzen angezeigt und aktualisiert werden.
* Mit der Option 'Speicherauszug' können Thread- und Heapspeicherauszüge für aktive Anwendungsinstanzen erstellt werden.

Wählen Sie hierzu eine Liberty-Anwendung in der Benutzerschnittstelle aus. In der Kategorie 'Laufzeit' in der Navigation können die Instanzdetails geöffnet werden. Wählen Sie eine oder mehrere Instanzen aus. Im Menü 'Aktionen' können Sie TRACE oder SPEICHERAUSZUG auswählen.

## Speicherauszugsdateien herunterladen
{: #download_dumps}

<strong>Voraussetzung:</strong>
* [Installieren Sie CF CLI](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html).
* [Installieren Sie Diego-Enabler-Plug-in](https://github.com/cloudfoundry-incubator/Diego-Enabler), wenn Ihre Anwendung in Diego ausgeführt wird.

<strong>Wenn Ihre Anwendung in DEA ausgeführt wird, führen Sie folgende Schritte aus: </strong>
  
1. Rufen Sie app_guid ab.
```
$ cf app <app_name> --guid
```

2. Laden Sie die Speicherauszugsdatei herunter.
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>Wenn Ihre Anwendung Diego ausgeführt wird, führen Sie folgende Schritte aus: </strong>
  
1. Rufen Sie app_guid ab.
```
$ cf app <app_name> --guid
```

2. Rufen Sie app_ssh_endpoint (Host und Port) und app_ssh_host_key_fingerprint ab.
```
$ cf curl /v2/info
```

3. Rufen Sie ssh-code für den Befehl scp ab.
```
$ cf ssh-code
```

4. Verwenden Sie den Befehl scp, um die ferne Speicherauszugsdatei lokal zu speichern. Verwenden Sie den ssh-code, wenn Sie aufgefordert werden, ein Kennwort einzugeben. 
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

Weitere Details finden Sie unter dem Thema über den Zugriff auf Apps mit SSH ([Accessing Apps with SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html)). 


# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

