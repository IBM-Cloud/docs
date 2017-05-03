---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# JRE anpassen
{: #customizing_jre}

Anwendungen werden in einer vom Liberty-Buildpack bereitgestellten und konfigurierten
JRE (Java Runtime Environment) ausgeführt. Ferner bietet das Liberty-Buildpack die Möglichkeit, die JRE-Version bzw. den JRE-Typ zu konfigurieren, die
JVM-Optionen anzupassen oder die JRE-Funktionen zu überschreiben.

## IBM JRE

Standardmäßig werden Anwendungen für die Ausführung mit einer einfachen IBM JRE-Version
konfiguriert. Diese einfache JRE wurde verschlankt, um die Kernfunktionalität
mit einem deutlich geringeren Platten- und Speicherbedarf bereitzustellen. Weitere Informationen zum Inhalt der einfachen JRE finden Sie im Abschnitt zum Thema [Small Footprint JRE](http://www.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/user/small_jre.html).

Standardmäßig wird IBM JRE Version 8 verwendet. Mit der Umgebungsvariablen JBP_CONFIG_IBMJDK können Sie eine alternative Version der IBM JRE angeben. Legen Sie beispielsweise die folgende Umgebungsvariable fest, um die neueste Version von
IBM JRE 7.1 zu verwenden:
```
    $ cf set-env myapp JBP_CONFIG_IBMJDK "version: 1.7.+"
```
{: codeblock}

Die Versionseigenschaft kann auf einen Versionsbereich festgelegt werden. Es werden zwei Versionsbereiche unterstützt: 1.7.+ und 1.8.+. Die besten Ergebnisse erzielen Sie, wenn Sie Java 8 verwenden.

## OpenJDK
{: #openjdk}

Optional können Anwendungen für die Ausführung mit OpenJDK als JRE konfiguriert werden. Um die Ausführung einer Anwendung mit OpenJDK zu ermöglichen, geben Sie 'openjdk' für die JVM-Umgebungsvariable an. Führen Sie zum
Beispiel mithilfe des Befehlszeilentools 'cf' den folgenden Befehl aus:
```
    $ cf set-env myapp JVM 'openjdk'
```
{: codeblock}

Standardmäßig wird OpenJDK Version 8 verwendet, sofern aktiviert. Mit der Umgebungsvariablen JBP_CONFIG_OPENJDK können Sie eine alternative Version von OpenJDK angeben. Legen Sie beispielsweise die folgende Umgebungsvariable fest, um die neueste Version von
OpenJDK 7 zu verwenden:
```
    $ cf set-env myapp JBP_CONFIG_OPENJDK "version: 1.7.+"
```
{: codeblock}

Die Versionseigenschaft kann auf einen Versionsbereich wie '1.7.+ ' oder auf eine bestimmte in der
[Liste der
verfügbaren OpenJDK-Versionen](https://download.run.pivotal.io/openjdk/lucid/x86_64/index.yml) aufgeführte Version festgelegt werden. Die besten Ergebnisse erzielen Sie, wenn Sie Java 8 verwenden.

## Oracle JRE
{: #oracle_jre}

Informationen zur Verwendung von Oracle JRE finden Sie unter [Oracle JRE verwenden](oracle_jre.html).

## JRE-Optionen konfigurieren
{: #configuring_jre}

### JVM-Standardkonfiguration
{: #jvm_default_config}

Das Liberty-Buildpack
konfiguriert die JVM-Standardoptionen unter Berücksichtigung der folgenden Punkte:

* Speicherbegrenzung einer Anwendung.  Die angewendeten JVM-Heapspeichereinstellungen werden basierend auf
den folgenden Faktoren berechnet:
  * Speicherbegrenzung einer Anwendung, wie in [Speicherbegrenzungen und das Liberty-Buildpack](memoryLimits.html#memory_limits) erläutert.
  * JRE-Typ, da die auf den Heapspeicher bezogenen Optionen für die JVM in Abhängigkeit von den
unterstützten JRE-Optionen variieren.

* [In Bluemix unterstützte Liberty-Features](libertyFeatures.html#libertyfeatures).
  * Globale Datenbanktransaktionen mit zweiphasigem Commit werden in Bluemix nicht unterstützt und deshalb durch die Einstellung '-Dcom.ibm.tx.jta.disable2PC=true' inaktiviert.

* Bluemix-Umgebung.

    Die Konfiguration der JVM-Optionen sorgt für Optimierung in einer Bluemix-Umgebung und unterstützt die Diagnose von speicherbezogenen Fehlerbedingungen.
  * Schnelle Fehlerdiagnose und -behebung für eine Anwendung wird durch Inaktivierung der
JVM-Speicherauszugsoptionen und Beenden der Prozesse bei erschöpfter Speicherkapazität der Anwendung konfiguriert.
  * Virtualisierungsoptimierung (nur IBM JRE).
  * Weiterleitung von Informationen zu den verfügbaren Speicherressourcen der Anwendung im Fehlerfall an Loggregator.
  * Wenn eine Anwendung für die Aktivierung von JVM-Hauptspeicherauszügen konfiguriert ist, wird das Beenden von Java-Prozessen inaktiviert und die JVM-Hauptspeicherauszüge werden an das gemeinsame Anwendungsverzeichnis 'dumps' weitergeleitet. Diese Speicherauszüge können dann über das Bluemix-Dashboard oder die CF-CLI angezeigt werden.

Es folgt eine Beispielkonfiguration einer Standard-JVM, die vom Buildpack für eine Anwendung generiert wurde, die mit einer Speicherbegrenzung von 512M bereitgestellt wurde:

```
    -Xtune:virtualized
    -Xmx384M
    -Xdump:none
    -Xdump:heap:defaults:file=../../../../../dumps/heapdump.%Y%m%d.%H%M%S.%pid.%seq.phd
    -Xdump:java:defaults:file=../../../../../dumps/javacore.%Y%m%d.%H%M%S.%pid.%seq.txt
    -Xdump:snap:defaults:file=../../../../../dumps/Snap.%Y%m%d.%H%M%S.%pid.%seq.trc
    -Xdump:tool:events=systhrow,filter=java/lang/OutOfMemoryError,request=serial+exclusive,exec=../../../../.buildpack-diagnostics/killjava.sh
    -Dcom.ibm.tx.jta.disable2PC=true
```
{: codeblock}

### JVM-Konfiguration anpassen
{: #customizing_jvm}

Anwendungen
können die JVM-Optionen mit den Spezifikationen anpassen, die von der für die Anwendung konfigurierten JRE
definiert wurden. Entnehmen Sie die Richtlinien zum Angeben von Optionen und deren Syntax direkt
aus der JRE-Dokumentation, da die Optionen je nach JRE variieren.

<table>
<tr>
<th align="left">JRE</th>
<th align="left">Format von Befehlszeilenoptionen</th>
<th align="left">Referenz</th>
</tr>

<tr>
<td>IBM JRE</td>
<td>Enthält Laufzeitoptionen (Präfix '-X') und Java-Systemeigenschaften (Präfix '-D'). Die Angabe von '-XX' bei gelegentlicher Nutzung wird nicht empfohlen (Änderungen an diesen Optionen vorbehalten).
</td>
<td>[Befehlszeilenoptionen für Version 8](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_8.0.0/com.ibm.java.lnx.80.doc/diag/appendixes/cmdline/cmdline.html), [Befehlszeilenoptionen für Version 7](http://www-01.ibm.com/support/knowledgecenter/SSYKE2_7.0.0/com.ibm.java.lnx.70.doc/diag/appendixes/cmdline/cmdline.html)
</td>
</tr>

<tr>
<td> OpenJDK </td>
<td>Basiert auf der HotSpot-Laufzeit; Schreibweise: -X für Nicht-Standardoptionen, -XX für Entwickleroptionen
und boolesche Flags zum Aktivieren oder Inaktivieren von Optionen. </td>
<td>[HotSpot Runtime Overview ![Symbol 'Externer Link'](../../icons/launch-glyph.svg "Symbol 'Externer Link'")](http://openjdk.java.net/groups/hotspot//docs/RuntimeOverview.html) </td>
</tr>
</table>

Eine Anwendung, die angepasste JVM-Optionen erfordert, kann die Option als Wert für die Umgebungsvariable IBM_JAVA_OPTIONS, JAVA_OPTS oder JVM_ARGS in Bluemix definieren. Informationen zum Definieren von Umgebungsvariablen für eine Anwendung finden Sie in 'Umgebungsvariablen'. Anstatt eine Umgebungsvariable zu definieren, kann ein paketierter Server oder ein Serververzeichnis auch die Datei 'jvm.options' mit den Befehlszeilenoptionen enthalten.

Wenn die JVM-Optionen auf die JRE angewendet werden, erfolgt zuerst die Anwendung der
Standardoptionen des Liberty-Buildpacks gefolgt von den angepassten Optionen. Die angepassten Optionen
werden in einer bestimmten Reihenfolge angehängt (siehe Tabelle). Die Reihenfolge der angewendeten Java-Optionen gibt an, welche Optionen Vorrang haben. Optionen, die
zuletzt angewendet werden, haben Vorrang vor Optionen, die zuvor angewendet wurden.

Hinweis: Einige Optionen werden nur wirksam, wenn die Option durch einen Agenten ausgelöst wird.

<table>
<tr>
<th align="left">Reihenfolge</th>
<th align="left">Einstellung der JVM-Optionen der Anwendung</th>
<th align="left">Beschreibung</th>
<th align="left">Unterstützter Anwendungstyp</th>
<th align="left">Maßnahmen zur Aktualisierung der JVM-Option einer implementierten Anwendung</th>
<th align="left">Anwendbar auf OpenJDK-JRE</th>
</tr>

<tr>
<td>1</td>
<td>IBM_JAVA_OPTIONS</td>
<td>Von der IBM JRE unterstützte Umgebungsvariable</td>
<td>Alle</td>
<td>Anwendung erneut starten oder erneutes Staging für Anwendung</td>
<td>Nein</td>
</tr>

<tr>
<td>2</td>
<td>JAVA_OPTS</td>
<td>Umgebungsvariable über das Framework für Java-Optionen des Liberty-Buildpacks</td>
<td>Alle</td>
<td>Erneutes Staging für App</td>
<td>Ja</td>
</tr>

<tr>
<td>3</td>
<td>jvm.options</td>
<td>Eine JVM-Konfigurationsdatei, die vom paketierten Server oder Serververzeichnis der Liberty-Laufzeit unterstützt wird.</td>
<td>Serverpaket</td>
<td>Erneutes Staging für App</td>
<td>Ja</td>
</tr>

<tr>
<td>4</td>
<td>JVM_ARGS</td>
<td>Eine Umgebungsvariable, die von der Liberty-Laufzeit unterstützt wird.</td>
<td>Alle</td>
<td>App erneut starten oder erneutes Staging für App</td>
<td>Ja</td>
</tr>
</table>

### Angewendete JVM-Optionen einer aktiven Anwendung bestimmen
{: #determining_applied_jvm_options}

Mit Ausnahme von anwendungsdefinierten Optionen, die mit der Umgebungsvariable JVM_ARGS angegeben sind, bleiben die Ergebnisoptionen in der Laufzeitumgebung entweder als Befehlszeilenoption (eigenständige Java-Anwendungen) oder in der Datei `jvm.options` (keine eigenständige Java-Anwendungen) erhalten. Die angewendeten JVM-Optionen für die Anwendung können entweder über die Konsole von IBM Bluemix oder die CF-CLI angezeigt werden.

Die JVM-Optionen für eigenständige Java-Anwendungen werden als Befehlszeilenoptionen gespeichert. Sie können über die Datei `staging_info.yml` angezeigt werden. 

Um die Datei `staging_info.yml` in einer Anwendung anzusehen, die im DEA-Modus ausgeführt wird, geben Sie folgenden Befehl ein: 

```
    $ cf files myapp staging_info.yml
```
{: codeblock}

Um die Datei `staging_info.yml` in einer Anwendung anzusehen, die in einer Diego-Zelle ausgeführt wird, geben Sie den folgenden Befehl ein: 

```
    $ cf ssh myapp -c "cat staging_info.yml"
```
{: codeblock}

Die JVM-Optionen für WAR-, EAR- und Serververzeichnisbereitstellungen sowie Bereitstellungen für paketierte Server sind in der Datei `jvm.options` gespeichert. Die Datei `jvm.options` befindet sich im Verzeichnis `app/wlp/usr/servers/<serverName>/`. In den meisten Fällen wird für ```<serverName>``` die Einstellung `defaultServer` festgelegt. Es sei denn, ein paketierter Server wurde mit einem anderen Servernamen implementiert. Beispiel:

Um die Datei `jvm.options` in einer Anwendung anzusehen, die im DEA-Modus ausgeführt wird, geben Sie folgenden Befehl ein: 

```
    $ cf files myapp app/wlp/usr/servers/defaultServer/jvm.options
```
{: codeblock}

Um die Datei `jvm.options` in einer Anwendung anzusehen, die in einer Diego-Zelle ausgeführt wird, geben Sie den folgenden Befehl ein: 

```
    $ cf ssh myapp -c "cat app/wlp/usr/servers/defaultServer/jvm.options"
```
{: codeblock}


#### Beispielsyntax
{: #example_usage}

Anwendung mit angepassten JVM-Optionen bereitstellen, um ausführliche IBM JVM-Garbage-Collection-Protokollierung zu aktivieren: 
* Die in der Datei `manifest.yml` einer Anwendung enthaltenen JVM-Optionen: 

```
    env:
      JAVA_OPTS: "-verbose:gc -Xverbosegclog:./verbosegc.log,10,1000"
```
{: codeblock}

* Um die ausführliche JVM-Garbage-Collection-Protokolldatei in einer Anwendung anzusehen, die im DEA-Modus ausgeführt wird, geben Sie folgenden Befehl ein: 

```
    $ cf files myapp app/wlp/usr/servers/defaultServer/verbosegc.log.001
```
{: codeblock}

* Um die ausführliche JVM-Garbage-Collection-Protokolldatei in einer Anwendung anzusehen, die in einer Diego-Zelle ausgeführt wird, geben Sie folgenden Befehl ein: 

```
    $ cf ssh myapp -c "cat app/wlp/usr/servers/defaultServer/verbosegc.log.001"
```
{: codeblock}

* Wenn Sie die IBM JRE-Option einer bereitgestellten Anwendung aktualisieren möchten, um 'heap', 'snap' und 'javacore' für eine OutOfMemory-Bedingung auszulösen, definieren Sie die Umgebungsvariable der Anwendung mit der JVM-Option und führen Sie einen Neustart der Anwendung durch:

```
    $ cf set-env myapp JVM_ARGS '-Xdump:heap+java+snap:events=systhrow,filter=java/lang/OutOfMemoryError'
    $ cf restart myapp
```
{: codeblock}

 Details zum Anzeigen und Herunterladen der generierten Speicherauszugsdateien finden Sie in der Dokumentation über [Protokollierung und Tracing](loggingAndTracing.html#download_dumps). 

### JRE überschreiben
{: #overlaying_jre}

In manchen Fällen müssen Dateien mit der JRE gepackt werden,
um deren Funktionen bereitzustellen. Der Anwendungsentwickler kann JRE-Dateien für die Anpassung
angeben.

Die zu überschreibenden Dateien können mit der WAR-, EAR- oder JAR-Anwendungsdatei in
einem Ressourcenordner im Stammverzeichnis des Archivs gepackt werden. Für einen Server (komprimierte Datei oder Serververzeichnis) können die Dateien in einem Ressourcenordner im Serververzeichnis mit der Datei 'server.xml' gepackt werden.

* WAR-Datei
  * WEB-INF
  * resources
    * other files
    * .java-overlay


* EAR-Datei
  * META-INF
  * resources
    * other files
    * .java-overlay


* JAR-Datei
  * META-INF
  * resources
    * other files
    * .java-overlay


* server_name DIR
  * apps
  * dropins
  * server.xml
  * resources
    * other files
    * .java-overlay

Das Verzeichnis '.java-overlay' enthält in derselben Dateihierarchie wie die zu überschreibende JRE bestimmte Dateien, die mit '.java/jre' beginnen.

Wenn Sie beispielsweise die 256-Bit-AES-Verschlüsselung verwenden möchten, müssen die folgenden Java-Richtliniendateien überschrieben werden:

```
    .java\jre\lib\security\US_export_policy.jar
    .java\jre\lib\security\local_policy.jar
```
{: codeblock}

Laden Sie die entsprechenden uneingeschränkten Richtliniendateien
herunter und fügen Sie sie Ihrer Anwendung wie folgt hinzu:

```
    resources\.java-overlay\.java\jre\lib\security\US_export_policy.jar
    resources\.java-overlay\.java\jre\lib\security\local_policy.jar
```
{: codeblock}

Bei Durchführung einer Push-Operation für Ihre Anwendung überschreiben diese JAR-Dateien die JAR-Standardrichtliniendateien in der Java-Laufzeit. Dieser Prozess aktiviert die 256-Bit-AES-Verschlüsselung.

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
