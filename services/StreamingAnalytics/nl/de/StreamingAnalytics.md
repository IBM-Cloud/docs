---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Produktinformationen
{: #about}

Sie können eine Echtzeitanalyse bewegter Daten im Rahmen Ihrer {{site.data.keyword.Bluemix_short}}-Anwendungen unter Verwendung von {{site.data.keyword.streaminganalyticsfull}} ausführen.
{:shortdesc}

Sie kennen {{site.data.keyword.streaminganalyticsshort}} noch nicht? Hier finden Sie eine [kurze Einführung in den Service](https://developer.ibm.com/streamsdev/docs/streaming-analytics-now-available-bluemix-2/){:new_window}.

Der {{site.data.keyword.streaminganalyticsshort}}-Service bietet die folgenden Funktionen, mit denen Sie Ihre Daten in der Cloud bereitstellen, analysieren und überwachen können:

**Interaktive und programmgesteuerte Verwendung des Service:**

Sie können den Service interaktiv über die [{{site.data.keyword.streaminganalyticsshort}}-Konsole](/docs/services/StreamingAnalytics/c_streams_console.html) oder programmgesteuert über die [{{site.data.keyword.streaminganalyticsshort}}-REST-API](https://console.ng.bluemix.net/apidocs/220){:new_window} verwenden.

**Bereitstellung und Überwachung von SPL-, Java-, Scala- und Python-Anwendungen:**

Sie können {{site.data.keyword.streamsshort}}-Anwendungen in SPL, Java, Scala und Python schreiben. Mithilfe der {{site.data.keyword.streaminganalyticsshort}}-Konsole können Sie [diese Anwendungen bereitstellen und überwachen.](/docs/services/StreamingAnalytics/t_deploytocloud.html)

Wenn Sie Ihre Anwendungen in SPL schreiben möchten, sollten Sie wissen, dass {{site.data.keyword.streamsfull}} Processing Language (SPL) eine Programmiersprache ist, die zum Erstellen von Streamverarbeitungsanwendungen verwendet wird. Wenn Sie Ihre eigenen SPL-Anwendungen noch weitergehend einsetzen wollen, können Sie eine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung einrichten und Sie müssen Ihre SPL-Apps für die Cloud vorbereiten.

Um Python-Anwendungen ohne eine {{site.data.keyword.streamsshort}}-Entwicklungsumgebung zu erstellen und bereitzustellen, verwenden Sie unsere Notebooks in IBM Data Science Experience (DSX) oder die {{site.data.keyword.streamsshort}}-Python-API. Weitere Informationen finden Sie im Abschnitt [Entwicklung von Python-Anwendungen für {{site.data.keyword.streaminganalyticsshort}}](/docs/services/StreamingAnalytics/t_develop_apps_python.html).

**Kompatibilität mit {{site.data.keyword.streamsshort}}-Operatoren:**

Alle {{site.data.keyword.streamsshort}}-Operatoren im SPL-Standardtoolkit ([{{site.data.keyword.streamsshort}} Processing Language) müssen mit {{site.data.keyword.streaminganalyticsshort}} kompatibel sein](/docs/services/StreamingAnalytics/c_beta_adapters.html).

## {{site.data.keyword.streaminganalyticsfull}} - Zuständigkeiten
{: #responsibilities notoc}

### Zuständigkeiten des Kunden
{: #clientresponsibilities notoc}

Der Kunde ist für Folgendes zuständig:

* Für das Überwachen, Konfigurieren und Verwalten der in seiner Instanz aktiven {{site.data.keyword.streamsshort}}-Jobs nach der Erstkonfiguration von {{site.data.keyword.streamsshort}} durch IBM. Der Kunde ist im Hinblick auf das Starten und Stoppen der Instanz und der unter den Instanzen ausgeführten Jobs flexibel.
* Für das erforderliche oder für den eigenen Bedarf notwendige Entwickeln von Programmen und Anwendungen für den Service zur Analyse von Daten sowie zur Erkenntnisgewinnung im Hinblick auf diese Analyse. Der Kunde ist zudem für Qualität und Leistung dieser so entwickelten Programme oder Anwendungen verantwortlich. Programme können in SPL, Java oder anderen Sprachen entwickelt werden, und zwar mithilfe des {{site.data.keyword.streamsshort}} Topology-Features. Sie müssen entweder mit {{site.data.keyword.streamsshort}} Developer Edition oder mit {{site.data.keyword.streamsshort}} Quick Start Edition kompiliert werden, und zwar unter Verwendung des Betriebssystems, das auch für {{site.data.keyword.streaminganalyticsshort}} verwendet wird.
* Für das regelmäßige Prüfen des folgenden Links für den Abruf von Informationen zu einer geplanten, unterbrechungsfreien Ausfallzeit oder einer Ausfallzeit mit Unterbrechung: [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window}.  
* Für das Sichern aller Daten, Metadaten, Konfigurationsdateien und Umgebungsparameter gemäß der Geschäftsanforderungen zur Garantie der Kontinuität.
* Für das Wiederherstellen von Daten, Metadaten, Konfigurationsdateien und Umgebungsparametern aus einem Backup zur Garantie der Kontinuität, falls es zu einem Ausfall eines beliebigen Typs kommt, einschließlich eines Ausfalls des Rechenzentrums oder eines Podausfalls, eines Server-, Festplatten- oder Softwareausfalls.

### Zuständigkeiten von IBM
{: #ibmresponsibilities notoc}

Im Rahmen von {{site.data.keyword.streaminganalyticsfull}} ist IBM für Folgendes zuständig:

* Für das Bereitstellen und Verwalten von Servern, Speicher und Netzinfrastruktur für die Kundeninstanz.
* Für das Bereitstellen einer Erstkonfiguration von {{site.data.keyword.streamsshort}} auf Basis der Anzahl der ausgewählten Knoten.
* Für das Bereitstellen und Verwalten einer Infrastruktur für Internet-Facing und einer internen Firewall zum Schutz und als Isolation.
* Für das Überwachen und Verwalten der folgenden Komponenten in {{site.data.keyword.streaminganalyticsfull}}:
	* Netzkomponenten
	* Server und deren lokaler Speicher
	* Infrastrukturbetriebssysteme
	* {{site.data.keyword.streamsshort}}-Management-Services
	* {{site.data.keyword.streamsshort}}-Instanzen
* Für das Bereitstellen von Wartungspatches einschließlich der entsprechenden Sicherheitspatches für die Infrastrukturbetriebssysteme und für {{site.data.keyword.streamsshort}}.
* Für das Durchführen einer regelmäßigen Wartung, für die es zu keiner Systemausfallzeit (unterbrechungsfreie Wartung) kommen sollte, sowie einer Wartung, für die es zu einer Systemausfallzeit samt Systemneustart (Wartung mit Unterbrechung) kommen kann; diese werden zu geplanten Zeiten durchgeführt, die unter [https://developer.ibm.com/bluemix/support/#status](https://developer.ibm.com/bluemix/support/#status){:new_window} veröffentlicht werden.
* Alle Änderungen an den geplanten Wartungszeiten werden durch entsprechende Benachrichtigungen bekanntgemacht.
