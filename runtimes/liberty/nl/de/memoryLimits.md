---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Speicherbegrenzungen und das Liberty-Buildpack
{: #memory_limits}

Bei der Implementierung einer Anwendung mit dem Liberty-Buildpack muss eine
Speicherbegrenzung angegeben werden.

## Probleme vermeiden

Ein Hello World-Servlet, das mit dem Liberty-Buildpack
und einer Speicherbegrenzung von 256 MB implementiert wird, kann möglicherweise nicht ordnungsgemäß
implementiert und ausgeführt werden. Bei einer Implementierung wird der Grenzwert von 256 MB nahezu
erreicht. Auch für einfache Anwendungen sollte eine Speicherbegrenzung von mindestens 512 MB
festgelegt werden.

## Speicherbegrenzungen und das Liberty-Buildpack
{: #memory_limits_and_liberty}


Bei der Implementierung einer
Anwendung mit dem Liberty-Buildpack werden Sie zur Eingabe einer Speicherbegrenzung
aufgefordert.

Um den richtigen Wert für die Speicherbegrenzung zu bestimmen, müssen Sie sich
darüber im Klaren sein, dass Sie nicht die Größe des Java-Anwendungsheapspeichers angeben. Sie definieren
die Speichermenge, die vom gesamten Prozess verwendet werden kann. Dieser Wert schließt den von den
folgenden Komponenten verwendeten Speicher ein:

* Speicher, der vom Warden-Container verwendet wird.
* Speicher, der für die Zuordnung von Kernelerweiterungen und Systembibliotheken zum Prozess verwendet wird.
* Speicher, der für die ausführbaren JVM-Dateien, den JVM-Arbeitsheapspeicher, den JIT-Bereich und komprimierte
Referenzen verwendet wird.
* Speicher, der für Klassen (Anwendungsserver und Anwendung), Thread-Stacks und direkte E/A-Puffer verwendet wird.
* Speicher, der vom Heapspeicher der Java-Anwendung verwendet wird.

Weitere Informationen zur JVM-Speicherbelastung finden Sie im developerWorks-Artikel [Thanks for the memory](http://www.ibm.com/developerworks/library/j-nativememory-linux/).

Wenn
Sie eine Anwendung implementieren, wird die Speicherbelegung des gesamten Prozesses
überwacht. Wenn die Speicherbelegung die bei der Implementierung der Anwendung angegebene Speicherbegrenzung
überschreitet, stoppt der Kernel den Prozess. Diese Maßnahme erfolgt ohne Warnung und kann sich auf die
folgende Weise auswirken:

* Wenn die Speicherbegrenzung während der Anwendungsimplementierung überschritten wird, empfangen Sie
eine Nachricht mit dem Hinweis, dass ein Fehler aufgetreten ist. Es könnte zu einem Flapping
der Anwendung kommen. Oder Sie stellen fest, dass die Anwendung mehrere erfolglose Startversuche
unternommen hat. Sie könnten auch eine Nachricht empfangen, dass die Anwendungsimplementierung
fehlgeschlagen ist.
* Wenn die Speicherbegrenzung überschritten wird, während die Anwendung aktiv ist, wird der Prozess
gestoppt. Cloud Foundry versucht einen Neustart der Anwendung. Der Neustart der Anwendung kann erfolgen, die Anwendung ist aber für eine gewisse Zeit nicht verfügbar.

## Heapspeicher angeben
{: #specifying_heap_memory}

Sie können auf unterschiedliche Weise den Maximalwert für den Heapspeicher anpassen, der Ihrer Anwendung zugeordnet wird. 

*  Umgebungsvariable JVM_ARGS und das Argument -Xmx verwenden. Um beispielsweise die maximale Größe des Heapspeichers auf 512M zu setzen, geben Sie den folgenden Befehl ein und
führen anschließend ein erneutes Staging Ihrer App durch. 

```
    $ cf set-env myapp JVM_ARGS -Xmx512m
```
{: codeblock}

* Wenn Ihre Anwendung ein [Serververzeichnis](optionsForPushing.html#server_directory) oder ein [paketierter Server](optionsForPushing.html#packaged_server) ist, geben Sie das Argument -Xmx in der Datei 'jvm.options' an. 

* Sie können den Faktor für die Größe des Heapspeichers mithilfe der Umgebungsvariablen JBP_CONFIG_IBMJDK angeben. Der Gleitkommawert heap_size_ratio gibt an, wie viel des verfügbaren Speichers dem Heapspeicher zugeordnet wird. Um beispielsweise die Hälfte des verfügbaren Speichers dem Heapspeicher zuzuordnen, geben Sie den folgenden Befehl aus und führen anschließend ein erneutes Staging Ihrer App durch. 

```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "heap_size_ratio: 0.50"
```
{: codeblock}
