---

copyright:
  years: 2017
lastupdated: "2017-02-07"

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Oracle JRE verwenden
{: #using_oraacle_jre}

Sie können Ihre Liberty-Anwendung in Bluemix mit Oracle JRE ausführen.  Dazu müssen Sie:
* JRE an einer Position hosten, von der es vom Buildpack heruntergeladen werden kann,
* die Datei `index.yml` hosten, die die Position des Host-JRE bereitstellt, und
* Ihre Anwendung für die Verwendung von JRE konfigurieren.

## JRE und index.yml hosten
{: #hosting_jre}

Die Oracle JRE-Datei muss als Host einen Web-Server haben und das Liberty-Buildpack muss diese Datei von diesem Server herunterladen können. Sie können sie mithilfe einer beliebigen verfügbaren Serverfunktion in Bluemix selbst hosten oder Sie können sie an einer öffentlich verfügbaren Position hosten. Der Server muss mit der Datei `index.yml` konfiguriert werden, die Details zu der JRE-Datei angibt. Führen Sie die Schritte aus, die im Folgenden für das Hosten des der JRE-Datei und der Datei `index.yml` angegeben sind:
  1. Fordern Sie Oracle JRE an. Beachten Sie, dass die JRE-Version unter einem Unix-64-Bit-Betriebssystem und eine `tar.gz`-Datei sein muss.
  2. Hosten Sie die JRE-Datei an einer Position, von der das Liberty-Buildpack sie herunterladen kann. 
  3. Stellen Sie sicher, dass Sie an der Hostingposition die Datei `index.yml` bereitstellen. Die Datei `index.yml`  muss einen Eintrag enthalten, der aus der Versions-ID der Oracle JRE-Datei besteht, auf die ein Doppelpunkt und die vollständige URL der Position folgt, an der sich diese JRE-Datei befindet. Das Format der Datei `index.yml` ist wie folgt:
```
   ---
   jre_version: https://hostingLocation/jreName.tar.gz
```
{: codeblock}

    * Beispiel:
    ```
       ---
       1.8.0_91: https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz
    ```

## Die App konfigurieren
{: #configure_app}

Es müssen zwei Umgebungsvariablen für die Liberty-Anwendung festgelegt werden. *JBP_CONFIG_OPENJDK* muss festgelegt werden, um die Position der Datei `index.yml` anzugeben. Die *JVM*-Umgebungsvariable muss auf *openjdk* festgelegt werden, um das Buildpack für die Verwendung einer alternativen JRE zu konfigurieren.

Der Wert der Variable JBP_CONFIG_OPENJDK ist
```
   'repository_root: "https://locationToIndexYml"'
```
{: codeblock}

Um dies festzulegen, können Sie einen Befehl wie den folgenden ausgeben:
```
   $ cf se myApp JBP_CONFIG_OPENJDK 'repository_root: https://myHostingApp.ng.bluemix.net'
```
{: codeblock}

Beachten Sie, dass die URL *repository_root* die Datei `index.yml` nicht einbezieht, aber vor ihrer Position stoppt.

Um die JVM-Umgebungsvariable festzulegen, können Sie einen ähnlichen Befehl wie diesen ausgeben:
```
   $ cf se myApp JVM 'openjdk'
```
{: codeblock}

**Hinweis**: Sie müssen nach dem Festlegen der Umgebungsvariablen ein erneutes Staging für Ihre Anwendung durchführen.

## Bestätigung
{: #confirmation}

Um zu bestätigen, dass die erwartete JRE verwendet wird, überprüfen Sie das Stagingprotokoll und suchen nach einer Nachricht wie der folgenden: 
```
   -----> Downloading OpenJdk 1.8.0_91 from https://myHostingApp.ng.bluemix.net/jre-8u91-fcs-bin-b14-linux-x64-01_apr_2016.tar.gz (6.2s)
```
{: codeblock}

# Zugehörige Links
{: #rellinks notoc}
## Allgemein
{: #general notoc}
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
