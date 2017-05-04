---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Protokollierung und Tracing
{: #logging_tracing}

## Protokolldateien
{: #log_files}

Die Liberty-Standardprotokolle wie `messages.log` oder das Verzeichnis `ffdc` stehen unter IBM Bluemix im Verzeichnis `logs` jeder Anwendungsinstanz zur Verfügung. Auf diese Protkolle kann über die Konsole von IBM Bluemix zugegriffen werden. Beispiel:

* Um auf die aktuellen Protokolle für eine App zuzugreifen, führen Sie den folgenden Befehl aus: 

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* Um die Datei `messages.log` einer App anzuzeigen, die auf einem DEA-Knoten ausgeführt wird, führen Sie den folgenden Befehl aus:

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Um die Datei `messages.log` einer App anzuzeigen, die in einer Diego-Zelle ausgeführt wird, führen Sie den folgenden Befehl aus:

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

Die Protokollebene und weitere Traceoptionen können in der Liberty-Konfigurationsdatei definiert werden. Weitere Informationen hierzu finden Sie unter [Liberty-Profil: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). Das Tracing kann mithilfe der Konsole von IBM Bluemix auch in einer aktive Anwendungsinstanz angepasst werden.

## Trace- und Speicherauszugsfunktionen verwenden
{: #using_trace_and_dump}

Die Liberty-Tracekonfiguration kann für die Ausführung einer Anwendung direkt über die Konsole von IBM Bluemix angepasst werden. Die Konsole bietet ferner die Funktion zur Abfrage und zum Herunterladen von Thread- und Heapspeicherauszügen. Um die Tracekonfiguration anzupassen oder um einen Speicherauszug anzufordern, wählen Sie eine Liberty-Anwendung in der Konsole von Bluemix aus und dann das Menü `Laufzeit` in der Navigation. Wählen Sie in der Ansicht `Laufzeit `eine Instanz aus und drücken Sie die Taste für *TRACE* oder *SPEICHERAUSZUG*. Wenn Sie die Tracestufe anpassen, finden Sie Informationen zu Syntaxdetails der Tracespezifikation unter [Liberty-Profil: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html). 

### Diego: Speicherauszüge über SSH auslösen

Eine Anwendung, die in einer Diego-Zelle ausgeführt wird, kann ebenfalls über die CF CLI unter Verwendung der SSH-Funktion einen Thread und einen Heapspeicherauszug auslösen. Beispiel:

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

Details zum Herunterladen der generierten Speicherauszugsdateien finden Sie in der Dokumentation unten. 

## Speicherauszugsdateien herunterladen
{: #download_dumps}

Verschiedene Speicherauszugsdateien werden standardmäßig im Verzeichnis `dumps` des Anwendungscontainers gespeichert.

### DEA-Anwendung

Bei einer Anwendung, die auf einem DEA-Knoten ausgeführt wird, verwenden Sie die Funktion "cf files", um die Speicherauszugsdateien anzuzeigen und herunterzuladen.

* Um die generierten Speicherauszüge anzuzeigen, führen Sie den folgenden Befehl aus:

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* Um eine Speicherauszugsdatei herunterzuladen, führen Sie die folgenden Befehle aus:

    1. Anwendungs-GUID abrufen

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. Speicherauszugsdatei herunterladen

      ```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```
      {: codeblock}

### Diego-Anwendung

Bei einer Anwendung, die in einer Diego-Zelle ausgeführt wird, verwenden Sie die Funktion "cf ssh", um die Speicherauszugsdatei anzuzeigen und herunterzuladen.

* Um die generierten Speicherauszüge anzuzeigen, führen Sie den folgenden Befehl aus:

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* Um eine Speicherauszugsdatei herunterzuladen, führen Sie folgenden Befehl aus:

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

Es ist auch möglich, `scp` und andere ähnliche Tools zu verwenden, um die Speicherauszugsdateien anzuzeigen und herunterzuladen. Weitere Informationen finden Sie unter [Accessing Apps with SSH ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html).

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
