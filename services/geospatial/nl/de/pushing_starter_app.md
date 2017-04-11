---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#Starteranwendung mit Push-Operation an {{site.data.keyword.Bluemix_short}} übertragen
{: #pushing_starter_app}


 
Sie können die Starteranwendung bereitstellen und sich mit der Verwendung des Service {{site.data.keyword.geospatialshort_Geospatial}} rasch vertraut machen:
{:shortdesc}

1. Falls Sie das [CF-Befehlszeilentool](docs/starters/install_cli.html) noch nicht installiert haben,
führen Sie diesen Schritt nun aus.
2. [Rufen Sie den Code](https://hub.jazz.net/project/streamscloud/geo-starter/overview) der {{site.data.keyword.geospatialshort_Geospatial}}-Starter-App ab. 
3. Benennen Sie das Verzeichnis, in dem die Anwendungsdateien enthalten sind, so um, dass der Name mit dem Namen übereinstimmt, den Sie für die Anwendung in {{site.data.keyword.Bluemix_short}} definiert haben. Beispiel: Wenn Sie für die Anwendung den Namen 'myapp' festgelegt haben, benennen Sie das Verzeichnis in 'myapp' um.
4. Wechseln Sie in der Befehlszeile in das umbenannte Verzeichnis.
<pre><code>cd myapp</code></pre>
5. Stellen Sie eine Verbindung zu {{site.data.keyword.Bluemix_short}} her:
<pre><code>cf api https://api.DomainName</code></pre>
6. Melden Sie sich bei {{site.data.keyword.Bluemix_short}} an und legen Sie Ihre
Zielorganisation fest, wenn Sie dazu aufgefordert werden, und
stellen Sie Ihre Anwendung bereit.
<pre><code>
cf login
cf push myapp
</code></pre>

##Nächste Schritte

* Wechseln Sie zur Übersichtsseite für die Anwendung, die über das {{site.data.keyword.Bluemix_short}}-Dashboard verfügbar ist, um zu überprüfen, ob die Anwendung erfolgreich gestartet wurde.
* Starten Sie die Anwendung, damit sie im Browser angezeigt wird. Sie finden die URL (oder "Route") der Anwendung auf der Übersichtsseite der Anwendung. Auf der Webseite für die Beispielanwendung werden Informationen zum Status der REST-API-Aufrufe im Anwendungscode und die Ereignisse angezeigt, die von {{site.data.keyword.geospatialshort_Geospatial}} erkannt wurden.
