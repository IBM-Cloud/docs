---

 

copyright:

  years: 2015, 2016

 

---
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Cloud Foundry-Befehle (cf-Befehle)

*Letzte Aktualisierung: 29. Januar 2016*

Sie können Cloud Foundry-Befehle ('cf'-Befehle) zur Verwaltung Ihrer Apps verwenden.
{:shortdesc}

Nachfolgend sind die 'cf'-Befehle aufgeführt, die am häufigsten für das Verwalten von Apps verwendet werden. Um alle 'cf'-Befehle und ihre zugehörigen Hilfeinformationen aufzulisten, verwenden Sie `cf help`. Mit dem Befehl `cf command_name -h` können Sie detaillierte Hilfeinformationen zu einem bestimmten Befehl anzeigen.

*Hinweis:* Wenn sich in Ihrem Netz zwischen dem Host, auf dem die cf-Befehle ausgeführt werden, und dem Cloud Foundry-API-Endpunkt ein HTTP-Proxy-Server befindet, müssen Sie den Hostnamen oder die IP-Adresse des Proxy-Servers durch Festlegen der Umgebungsvariablen `HTTP_PROXY` angeben. Details hierzu finden Sie
in [Using the cf CLI with an HTTP Proxy Server](http://docs.cloudfoundry.org/devguide/installcf/http-proxy.html).

## cf api

Zeigt oder gibt die URL des API-Endpunkts von {{site.data.keyword.Bluemix_notm}} an.
```
cf api BluemixServerURL
```
<dl>
<dt>BluemixServerURL</dt>
<dd>Die URL des Bluemix-API-Endpunkts, die Sie für das Herstellen einer Verbindung zu {{site.data.keyword.Bluemix_notm}} angeben müssen. In der Regel handelt es sich bei dieser URL um: URLhttps://api.{DomainName}. 
Wenn Sie die URL des API-Endpunkts anzeigen möchten, den Sie zurzeit verwenden, müssen Sie diesen Parameter für den Befehl 'cf api' nicht angeben. </dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Inaktiviert den Prozess der SSL-Validierung. Die Verwendung dieses Parameters kann zu Sicherheitsproblemen führen.</dd>
<dt>*--unset*</dt>
<dd>Entfernt Verbindungsinformationen für alle API-Endpunkte.</dd>
</dl>

## cf apps

Listet alle Anwendungen auf, die Sie im aktuellen Bereich bereitgestellt haben. Der Status der einzelnen Anwendungen wird auch angezeigt.

Nehmen Sie an, dass Sie über eine einzige Instanz für eine App verfügen und in der Instanzenspalte der Antwort auf den Befehl 'cf apps' 1/1 angezeigt wird, falls die App aktiv ist und 0/1, wenn die App inaktiv ist. Wenn der Status der App-Instanz ?/1 (unbekannt) ist, können Sie die App-URL in Ihren Browser kopieren und prüfen, ob die App antwortet, oder Sie können das Protokoll zurate ziehen; verwenden Sie hierfür den Befehl `cf logs appname`, um zu sehen, ob die App Inhalt für das Protokoll generiert.

## cf bind-service

Bindet eine vorhandene Serviceinstanz an Ihre Anwendung.
```
cf bind-service appname service_instance
```

Wenn Sie beispielsweise über eine Serviceinstanz namens `my_dataworks` in der aktuellen Organisation und im aktuellen Bereich verfügen, können Sie `cf bind-service my_app my_dataworks` zum Binden dieser Serviceinstanz an die Anwendung verwenden.

<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
<dt>service_instance</dt>
<dd>Der Name der vorhandenen Serviceinstanz.</dd>
</dl>

## cf create-service

Erstellt eine Serviceinstanz.
```
cf create-service service_name service_plan service_instance
```
Sie können beispielsweise `cf create-service DataWorks free my_dataworks` zum Erstellen einer Instanz des {{site.data.keyword.dataworks_short}}-Service mit einem kostenlosen Plan verwenden.

<dl>
<dt>service_name</dt>
<dd>Der Name des Service.</dd>
<dt>service_plan</dt>
<dd>Der Name des Serviceplans.</dd>
<dt>service_instance</dt>
<dd>Der Name, den Sie für die neue von Ihnen erstellte Serviceinstanz verwenden möchten.</dd>
</dl>

## cf create-space

Erstellt einen Bereich.
```
cf create-space space_name
```
<dl>
<dt>space_name</dt>
<dd>Der Name des Bereichs.</dd>
<dt>*-o*</dt>
<dd>Der Name der Organisation, in der Sie einen Bereich erstellen möchten.</dd>
<dt>*-q*</dt>
<dd>Das Kontingent, das dem neue erstellten Bereich zugeordnet werden soll. Wenn keine Angabe festgelegt wird, wird automatisch ein Standardkontingent zugeordnet.</dd>
</dl>

## cf delete

Löscht eine vorhandene Anwendung.
```
cf delete appname
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.<dd>
<dt>*-f*</dt>
<dd>Erzwingt die Löschung der Anwendung ohne Bestätigung. Dieser Parameter ist optional.</dd>
<dt>*-r*</dt>
<dd>Löscht alle Domänennamen, die der Anwendung zugeordnet sind. Dieser Parameter ist optional.</dd>
</dl>

## cf delete-space

Löscht einen Bereich.
```
cf delete-space space_name
```
<dl>
<dt>space_name</dt>
<dd>Der Name des Bereichs.</dd>
<dt>*-f*</dt>
<dd>Erzwingt die Löschung des Bereichs ohne Bestätigung. Dieser Parameter ist optional.</dd>
*Hinweis:* Das Löschen eines Bereichs ist eine Operation, die nicht rückgängig gemacht werden kann.
</dl>

## cf events

Zeigt Laufzeitereignisse an, die sich auf eine Anwendung beziehen.
```
cf events appname
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
</dl>

## cf help

Zeigt Hilfeinformationen für alle 'cf'-Befehle an bzw. für einen bestimmten 'cf'-Befehl, falls der Parameter Befehlsname verwendet wird.
```
cf help command_name
```
<dl>
<dt>command_name</dt>
<dd>Der Name eines Befehls. Wenn Sie spezifische Hilfeinformationen für einen Befehl wünschen, können Sie diesen Parameter verwenden.</dd>
<dd>Wenn Sie diesen Parameter nicht angeben, werden Hilfeinformationen zu allen 'cf'-Befehlen angezeigt.</dd>
</dl>


## cf login

Hiermit melden Sie sich bei {{site.data.keyword.Bluemix_notm}} an.
```
cf login
```
Für das Absetzen des Befehls 'cf login' können Sie mindestens einen der folgenden Parameter verwenden:
<dl>
<dt>*-a* https://api.{DomainName}</dt>
<dd>Die URL des API-Endpunkts von {{site.data.keyword.Bluemix_notm}}. Dieser Parameter ist optional.</dd>
<dt>*-u* user_name</dt>
<dd>Ihr Benutzername. Dieser Parameter ist optional.</dd>
<dt>*-p* password</dt>
<dd>Ihr Kennwort.</dd>
<dd>*Wichtig* Wenn Sie Ihr Kennwort mithilfe des Parameters *-p* in der Befehlszeilenschnittstelle angeben, wird es möglicherweise
im Befehlszeilenprotokoll aufgezeichnet. Sie sollten aus Sicherheitsgründen das Kennwort nicht
mithilfe des Parameters -p angeben. Geben Sie stattdessen das Kennwort ein, wenn Sie in der Befehlszeilenschnittstelle
dazu aufgefordert werden.</dd>
<dt>*-o* organization_name</dt>
<dd>Der Name der Organisation, bei der Sie sich anmelden möchten.</dd>
<dt>*-s* space_name</dt>
<dd>Der Name des Bereichs, bei dem Sie sich anmelden möchten.</dd>
<dt>*--skip-ssl-validation*</dt>
<dd>Inaktiviert den Prozess der SSL-Validierung. Die Verwendung dieses Parameters kann zu Sicherheitsproblemen führen.</dd>
</dl>

*Hinweis:* Wenn Sie im Parameter *-p* dieses Befehls Ihr Kennwort angeben, wird Ihr Kennwort möglicherweise in der Protokolldatei des Shellbefehls aufgezeichnet und kann für andere Benutzer des lokalen Betriebssystem sichtbar sein.


## cf logs

Zeigt die Protokolldatenströme STDOUT und STDERR einer Anwendung an.
```
cf logs appname
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
<dt>*--recent*</dt>
<dd>Ruft letzte Protokolle ab.</dd>
</dl>

## cf marketplace

Listet alle Services auf, die im Marktplatz verfügbar sind. Die von diesem Befehl aufgeführten Services werden auch im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt.
```
cf marketplace
```

## cf push

Stellt in Bluemix eine neue Anwendung bereit oder aktualisiert eine in Bluemix vorhandene Anwendung.
```
cf push appname 
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
<dt>*-b* buildpack_name</dt>
<dd>Der Name des Buildpacks. Der Name des Buildpacks (buildpack_name) kann der Name eines benutzerdefinierten Buildpacks oder eine Git-URL sein. Zum Beispiel `mein-buildpack` oder `https://github.com/heroku/heroku-buildpack-play.git`.</dd>
<dt>*-c* start_command</dt>
<dd>Der Startbefehl Ihrer Anwendung. Geben Sie für die Verwendung des standardmäßigen Startbefehls für diese Option den Wert null an. Beispiel:</dd>
<dd>```
cf push appname -c null
```</dd>
<dd>Mithilfe dieser Option können Sie auch Scriptdateien ausführen. Beispiel:
```
cf push appname -c “bash ./<run.sh>"
```</dd>
<dt>*-f* manifest_path</dt>
<dd>Der Pfad zur Manifestdatei. Die Standardmanifestdatei lautet 'manifest.yml'. Sie befindet sich im Stammverzeichnis der Anwendung.</dd>
<dt>*-i* instance_number</dt>
<dd>Die Anzahl der Instanzen.</dd>
<dt>*-k* disk_limit</dt>
<dd>Die Plattenbegrenzung für die Anwendung, zum Beispiel *256M*, *1024M* oder *1G*.</dd>
<dt>*-m* memory_limit</dt>
<dd>Die Speicherbegrenzung für die Anwendung, zum Beispiel *256M*, *1024M* oder *1G*.</dd>
<dt>*-n* host_name</dt>
<dd>Der Hostname für die Anwendung, zum Beispiel *meine-Unterdomäne*.</dd>
<dt>*-p* app_path</dt>
<dd>Der Pfad zum Anwendungsverzeichnis oder zur Archivdatei des Anwendungsverzeichnisses.</dd>
<dt>*-t* timeout</dt>
<dd>Die maximale Zeit für den Start der Anwendung in Sekunden. Möglicherweise wird dieser Wert durch andere serverseitige Zeitlimits überschrieben.</dd>
<dt>*-s* stackname</dt>
<dd>Der Stack zum Ausführen der Anwendungen. Ein Stack ist ein vorgefertigtes Dateisystem einschließlich Betriebssystem. Mit `cf stacks` können Sie die in {{site.data.keyword.Bluemix_notm}} verfügbaren Stacks anzeigen.</dd>
<dt>*--no-hostname*</dt>
<dd>Ordnet die Bluemix-Systemdomäne dieser Anwendung zu.</dd>
<dt>*--no-manifest*</dt>
<dd>Führt dazu, dass die Standardmanifestdatei ignoriert wird.</dd>
<dt>*--no-route*</dt>
<dd>Führt dazu, dass dieser Anwendung keine Route zugeordnet wird.</dd>
<dt>*--no-start*</dt>
<dd>Verhindert, dass die Anwendung nach der Bereitstellung gestartet wird.</dd>
<dt>*--random-route*</dt>
<dd>Erstellt eine zufällige Route für die Anwendung.</dd>
</dl>

## cf scale

Zeigt die Anzahl der Instanzen, die Platten- und die Speicherbegrenzung für eine Anwendung an bzw. ändert die entsprechenden Werte.
```
cf scale appname -i instance_number -k disk_limit -m memory_limit
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
<dt>*-i* instance_number</dt>
<dd>Die Anzahl der Instanzen.</dd>
<dt>*-k* disk_limit</dt>
<dd>Die Plattenbegrenzung für die Anwendung, zum Beispiel *256M*, *1024M* oder *1G*.</dd>
<dt>*-m* memory_limit</dt>
<dd>Die Speicherbegrenzung für die Anwendung, zum Beispiel *256M*, *1024M* oder *1G*.</dd>
<dt>*-f*</dt>
<dd>Erzwingt den Neustart der Anwendung ohne Eingabeaufforderung.</dd>
</dl>

## cf services

Listet alle Services auf, die im aktuellen Bereich verfügbar sind.
```
cf services
```

## cf set-env

Legt eine Umgebungsvariable für eine Anwendung fest.
```
cf set-env appname var_name var_value
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
<dt>var_name</dt>
<dd>Der Name der Umgebungsvariable.</dd>
<dt>var_value</dt>
<dd>Der Wert der Umgebungsvariable.</dd>
</dl>

## cf stacks

Mit diesem Befehl werden alle Stacks aufgeführt. Ein Stack ist ein vordefiniertes Dateisystem einschließlich eines Betriebssystems, das Apps ausführen kann.
```
cf stacks
```

## cf stop

Stoppt eine Anwendung.
```
cf stop appname
```
<dl>
<dt>appname</dt>
<dd>Der Name der Anwendung.</dd>
</dl>

## cf -v

Zeigt die Version der Befehlszeilenschnittstelle 'cf' an.
```
cf -v
```

# Zugehörige Links
{: #rellinks}
## Allgemein 
{: #general}
* [Referenzkarte - 'cf'-Befehle](ftp://public.dhe.ibm.com/cloud/bluemix/cli_reference_card.pdf)
