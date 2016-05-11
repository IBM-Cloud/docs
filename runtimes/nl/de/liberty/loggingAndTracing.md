---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Protokollierung und Tracing
{: #logging_tracing}

*Letzte Aktualisierung: 23. März 2016*

## Protokolldateien
{: #log_files}

Die Liberty-Standardprotokolle wie beispielsweise 'messages.log' oder das Verzeichnis 'ffdc' stehen in IBM Bluemix in den Protokollverzeichnissen der einzelnen Anwendungsinstanzen zur Verfügung. Auf diese Protokolle kann über die Konsole von IBM Bluemix oder mithilfe der Befehle 'cf logs' und 'cf files' zugegriffen werden.
Führen Sie beispielsweise zum Anzeigen der Datei 'messages.log' folgenden Befehl aus:
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

Die Protokollebene und weitere Traceoptionen können in der Libertry-Konfigurationsdatei definiert werden. Weitere Informationen hierzu finden Sie unter [Liberty-Profil: Protokollierung und Trace](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0). Das Tracing kann mithilfe der Konsole von IBM Bluemix auch in einer aktive Anwendungsinstanz angepasst werden.

## Trace- und Speicherauszugsfunktionen verwenden
{: #using_trace_and_dump}

In der Benutzerschnittstelle von IBM Bluemix gibt es Trace- und Speicherauszugsfunktionen.
* Mit der Option 'Trace' kann die Tracespezifikation der Liberty-Protokollierung für aktive Anwendungsinstanzen angezeigt und aktualisiert werden.
* Mit der Option 'Speicherauszug' können Thread- und Heapspeicherauszüge für aktive Anwendungsinstanzen erstellt und bearbeitet werden.

Wählen Sie hierzu eine Liberty-Anwendung in der Benutzerschnittstelle aus. Unter 'Laufzeit' in der Navigation auf der linken Seite können die Instanzdetails geöffnet werden. Wählen Sie eine oder mehrere Instanzen aus. Im Menü 'Aktionen' können Sie TRACE oder SPEICHERAUSZUG auswählen.

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
