---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Einführung in Cloudant
{: #getting-started-with-cloudant}
Letzte Aktualisierung: 12. August 2016
{: .last-updated}

{{site.data.keyword.cloudant}} ist eine Database as a Service (DBaaS) für Dokumente, in der Daten in JSON gespeichert werden.
Diese Datenbank integriert Skalierbarkeit,
Hochverfügbarkeit und
Dauerhaftigkeit.
Sie bietet eine umfassende Vielfalt an Indexierungsoptionen
wie 'map-reduce',
'Cloudant Query',
'full-text' und
'geospatial'.
Durch die Replikationsfunktionalität ist eine einfache
Datensynchronisation zwischen Datenbankclustern, Desktop-PCs
und mobilen Geräten möglich.
{:shortdesc}

Sie können die {{site.data.keyword.cloudant}}-Konsole von der Startseite des Service im Bluemix-Dashboard aus starten.

Führen Sie zur Nutzung des Service die folgenden Schritte aus:
<ol>
<li>Erstellen Sie entweder über das Bluemix-Dashboard oder
über die CloudFoundry-Befehlszeilenschnittstelle eine Serviceinstanz.
<p>Führen Sie die folgenden Schritte aus, um mithilfe des Dashboards
eine Instanz zu erstellen:
<ol>
<li>Melden Sie sich bei Bluemix an.</li>
<li>Klicken Sie im Dashboard in der Anzeige 'Data &amp; Analytics' auf
den Link '<code>Mit Daten arbeiten</code>'.</li>
<li>Klicken Sie auf die Schaltfläche '<code>Neuer Service</code>'.</li>
<li>Klicken Sie in der Liste der Services
auf die Schaltfläche {{site.data.keyword.cloudant}}.</li>
<li>Klicken Sie auf der Informationsseite von {{site.data.keyword.cloudant}}
auf die Schaltfläche '<code>{{site.data.keyword.cloudant}} auswählen</code>'.</li>
<li>Geben Sie auf der Katalogseite für {{site.data.keyword.cloudant}}
die Details für den Service an, die Sie benötigen.
Klicken Sie auf die Schaltfläche '<code>Erstellen</code>', wenn Sie bereit sind, fortzufahren.</li>
<li>Wenn die Cloudant-Instanz erstellt wurde,
sehen Sie das Dashboard für diese Instanz.
Klicken Sie auf den Link '<code>Serviceberechtigungsnachweise</code>', um alle Details anzuzeigen, die Sie für den Zugriff auf Ihre Instanz benötigen.</li>
</ol>
</p>
<p>Führen Sie die folgenden Schritte aus, um mithilfe der CloudFoundry-Befehlszeilenschnittstelle
eine Instanz zu erstellen:
<ol>
<li>Installieren Sie das CloudFoundry-Tool <code>cf</code> auf Ihrem System.
Anweisungen hierfür finden Sie im <a href="https://console.ng.bluemix.net/docs/cli/index.html">Bluemix-Leitfaden zu den CLI- und Dev-Tools</a>.</li>
<li>Erstellen Sie mithilfe des folgenden Befehls eine neue Serviceinstanz:<br/>
<pre><code>cf create-service</code></pre></li>
<li>Sie sehen eine Liste der verfügbaren Services.
Wählen Sie einen Service aus und
geben Sie für den Service einen eindeutigen Instanznamen und einen Plan ein.
Für die Instanz wird ein zufälliger Name vorgeschlagen, den
Sie aber beliebig ändern können.</li>
<li>Nach der Erstellung des Service
können Sie eine Liste aller von Ihnen erstellten Services abrufen:<br/>
<pre><code>cf services</code></pre></li>
<li>Vor der Verwendung eines Service in einer Anwendung müssen Sie
den Service an Ihre Anwendung binden.
Verwenden Sie hierfür den folgenden Befehl:<br/>
<pre><code>cf bind-service</code></pre>
Wählen Sie in der Ergebnisliste eine der
Anwendungen und einen der
Services aus.
Mit dem Befehl <code>cf</code> werden Sie über den Erfolg der Bindeaktion benachrichtigt.</li>
</ol>
</p>
</li>
<li><p>Nach der Erstellung einer Serviceinstanz sind JSON-Daten ähnlich wie im folgenden Beispiel zu sehen; sie können im Bluemix-Dashboard angezeigt werden:<br/>
<pre><code>{
  "cloudantNoSQLDB": {
    "name": "Cloudant-3s",
    "label": "cloudantNoSQLDB",
    "plan": "shared",
    "credentials": {
      "username": "someusername",
      "password": "secret",
      "host": "myhost-bluemix.cloudant.com",
      "port": 443,
      "url": "https://someusername:secret@myhost-bluemix.cloudant.com"
    }
  }
}</code></pre></p>
{: screen}
<p>Die Daten werden außerdem zur Umgebungsvariablen <code>VCAP_SERVICES</code> sämtlicher Bluemix-Anwendungen hinzugefügt, an die der Service gebunden ist.</p>
<p>Die Serviceberechtigungsnachweise werden in einem JSON-Objekt mit den folgenden Feldern gespeichert:
<ul>
<li><code>key</code>: Der Name des Service (cloudantNoSQLDB)</li>
<li><code>name</code>: Der vom Benutzer angegebene Name der Serviceinstanz</li>
<li><code>host</code>: Der Hostname des Servers</li>
<li><code>port</code>: Die Nummer des Ports, auf dem der Service ausgeführt wird, in der Regel 443</li>
<li><code>username</code>: Der Benutzername für die Authentifizierung</li>
<li><code>password</code>: Das Kennwort für die Authentifizierung</li>
<li><code>url</code>: Die URL der Serviceinstanz</li>
</ul></li>
<li><p>Lesen Sie in Ihren Bluemix-Anwendungen die Berechtigungsnachweise aus der Umgebungsvariablen <code>VCAP_SERVICES</code>.</p>
<p>In Anwendungen, die außerhalb von Bluemix oder in einer anderen geografischen Region in
Bluemix ausgeführt werden, können Sie die Berechtigungsnachweise
aus dem Bluemix-Dashboard abrufen uns sie zur Konfiguration Ihrer Anwendung hinzufügen.</p>
</li>
<li>Um auf die Datenbank zuzugreifen, müssen Sie als grundlegenden Schritt über HTTPS Anforderungen an den angegebenen Host und den angegebenen Port senden;
verwenden Sie für die Authentifizierung Benutzername und Kennwort.
Ihre Anforderungen können mithilfe einer Reihe von Anwendungssprachen und Plattformen gesendet werden,
darunter die folgenden:
<ul>
<li><a href="https://github.com/cloudant/sync-android">Android</a></li>
<li><a href="https://github.com/cloudant/CDTDatastore">Apple iOS</a></li>
<li><a href="https://github.com/cloudant/java-cloudant">Java</a></li>
<li><a href="https://github.com/cloudant/objective-cloudant">Objective C und Swift</a></li>
<li><a href="https://github.com/cloudant/python-cloudant">Python</a></li>
</ul>
sowie viele andere.
Weitere Informationen finden Sie auf der
<a href="https://cloudant.com/for-developers/">Cloudant-Homepage für Entwickler</a>
sowie in der Liste der <a href="http://docs.cloudant.com/libraries.html">Clientbibliotheken</a>.
</li>
<li>Sobald Ihre Anwendung bereit ist, können Sie sie
zur Verifizierung in der Bluemix-Umgebung bereitstellen.
Verwenden Sie den folgenden Befehl,
um eine Anwendung bereitzustellen:<br/>
<pre><code>cf push</code></pre></li>
<li>Verwenden Sie den folgenden Befehl,
um die Bindung einer Serviceinstanz an eine Anwendung aufzuheben:<br/>
<pre><code>cf unbind-service</code></pre></li>
<li>Verwenden Sie den folgenden Befehl,
um eine Serviceinstanz zu löschen:<br/>
<pre><code>cf delete-service</code></pre></li>
</ol>

Weitere Informationen zur Authentifizierung bei der Datenbank sowie zum Durchführen von Anforderungen finden Sie in der [API-Referenz](https://docs.cloudant.com/api.html).

# Zugehörige Links
{: #rellinks}

## Lernprogramme und Beispiele
{: #samples}

* [Cloudant-Clientbibliotheken](https://docs.cloudant.com/libraries.html)
* [Cloudant mit Liberty unter Bluemix verwenden](https://developer.ibm.com/bluemix/2014/07/08/cloudant_on_bluemix/)
* [Handbücher zu Cloudant](https://docs.cloudant.com/guides.html)

## API-Referenz
{: #api}

* [Cloudant-API-Referenz](https://docs.cloudant.com/api.html)

## Zugehörige Links
{: #general}

* [Cloudant-Website und -Dashboard](https://cloudant.com/)
* [Cloudant-Blog](https://cloudant.com/blog)
