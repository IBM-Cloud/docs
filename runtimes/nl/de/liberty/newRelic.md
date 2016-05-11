---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# New Relic verwenden
{: #new_relic}

*Letzte Aktualisierung: 23. März 2016*

Bei New Relic handelt es sich um einen Service eines anderen Anbieters, der Überwachungsmetriken für Ihre Anwendung
bereitstellt. Weitere Informationen zu den vom New Relic-Service bereitgestellten Funktionen finden Sie in [New Relic](http://newrelic.com/java).

Gemäß dieser [Dokumentation zur manuellen Installation des Java-Agenten](https://docs.newrelic.com/docs/agents/java-agent/installation/java-agent-manual-installation) müssen Java-Anwendungen, die anhand des New Relic-Service überwacht werden sollen, normalerweise zu einem Paket zusammengefasst und mit einem New Relic-Agenten und einem Lizenzschlüssel für ein Konto konfiguriert werden. In der Bluemix-Umgebung können Sie eine New Relic-Lizenzvereinbarung und ein zugehöriges Konto anfordern, indem Sie eine Serviceinstanz in IBM Bluemix erstellen. Java-Anwendungen können dann an die New Relic-Serviceinstanz gebunden werden. Das Liberty-Buildpack kann die Anwendung, die zur Überwachung durch den New Relic-Service bereitsteht, dann automatisch konfigurieren.
Das Buildpack hat hierbei die folgenden Funktionen:

* Bereitstellen der Anwendung mit einem New Relic-Agenten.
* Abrufen des Anwendungsnamens und des Lizenzschlüssels aus den Umgebungsvariablen VCAP_APPLICATION und VCAP_SERVICES der Anwendung.
* Konfigurieren der Eigenschaften und der Konfigurationsvorlage, die für den New Relic-Agenten benötigt wird.

Im Folgenden ist die Beispielkonfiguration
dargestellt, die vom Liberty-Buildpack für die Anwendung generiert wird:

```
    -javaagent:/home/vcap/app/.new_relic_agent/new_relic_agent-3.12.0.jar
    -Dnewrelic.home=/home/vcap/app/.new_relic_agent
    -Dnewrelic.config.license_key=123456
    -Dnewrelic.config.app_name=myapp
    -Dnewrelic.config.log_file_path=../../../../../logs
```
{: #codeblock}

## New Relic-Service hinzufügen
{: #add_new_relic}

Führen Sie die folgenden Schritte aus, um eine bereits vorhandene Java-Anwendung mit New Relic in IBM Bluemix zu überwachen.
1. Erstellen Sie eine New Relic-Serviceinstanz in IBM Bluemix.
```
    $ cf create-service newrelic standard mynewrelic
```
{: #codeblock}

2. Implementieren Sie Ihre Anwendung mithilfe des New Relic-Service in IBM Bluemix.  Im Folgenden ist ein Beispiel für ein Anwendungsmanifest aufgeführt:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Greifen Sie direkt über das IBM Bluemix-Dashboard Ihrer Anwendung auf das New Relic-Dashboard zu.

### Vom Benutzer bereitgestellten New Relic-Service hinzufügen
{: #add_user_provided_new_relic}

Wenn Sie über ein vorhandenes New Relic-Konto und den zugehörigen Lizenzschlüssel verfügen, können Sie den vorhandenen New Relic-Service mit einem vom Benutzer bereitgestellten Service an Ihre Anwendung binden.

1. Erstellen Sie eine vom Benutzer bereitgestellte Serviceinstanz und verwenden Sie dazu den bereits vorhandenen Lizenzschlüssel.  Wenn Ihr vorhandener Lizenzschlüssel '1234567' lautet, können Sie die CF-CLI zum Erstellen eines vom Benutzer bereitgestellten Service (create-user-provided-service) verwenden und an der Eingabeaufforderung wie im Folgenden den Lizenzschlüssel '1234567' angeben:
```
    $ cf create-user-provided-service mynewrelic -p "licenseKey"
    licenseKey> 1234567
```
{: #codeblock}

2. Implementieren Sie Ihre Anwendung mit der vom Benutzer bereitgestellten New Relic-Serviceinstanz in IBM Bluemix.  Im Folgenden ist ein Beispiel für ein Anwendungsmanifest aufgeführt, das eine vom Benutzer bereitgestellte New Relic-Serviceinstanz verwendet:
```
        ---
        applications:
        - name: myapp
         memory: 1G
         instances: 1
         host: myapp
         domain: mybluemix.net
         path: myapp.war
         services:
          - mynewrelic
```
{: #codeblock}

3. Greifen Sie auf das New Relic-Dashboard zu, um die Anwendungsmetriken anzuzeigen.

Die automatische Konfiguration des New Relic-Service unterscheidet sich von der automatischen Konfiguration anderer Services, da es sich um einen containerverwalteten Service handelt, der über das Framework des Buildpacks bereitgestellt wird.  Da die Bereitstellung über das Framework erfolgt, unterscheidet sich die automatische Konfiguration für diesen Service von der Konfiguration anderer Services in drei Punkten:
* Der Ausschluss (Opt-out) kann nicht verwendet werden.
* Die Serviceintegration basiert auf dem New Relic-Agenten, bei dem es sich um einen Java-Agenten handelt. Aus diesem Grund erfolgt die Konfiguration in der Datei 'server.xml' mithilfe von Java-Optionen und nicht mit Cloudvariablen.
* Die Konfiguration basiert auf den Umgebungsvariablen VCAP_SERVICES und VCAP_APPLICATION.

# Zugehörige Links
## Allgemein
* [Liberty-Laufzeit](index.html)
* [Übersicht über das Liberty-Profil](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
