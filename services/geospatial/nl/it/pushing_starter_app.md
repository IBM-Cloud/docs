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

#Distribuzione dell'applicazione starter a {{site.data.keyword.Bluemix_short}}
{: #pushing_starter_app}


 
Distribuisci l'applicazione starter e impara rapidamente come utilizzare il servizio {{site.data.keyword.geospatialshort_Geospatial}}:
{:shortdesc}

1. Se non l'hai già fatto, [installa lo strumento riga di comando cf](docs/starters/install_cli.html).
2. [Ottieni il codice](https://hub.jazz.net/project/streamscloud/geo-starter/overview) dell'applicazione starter {{site.data.keyword.geospatialshort_Geospatial}}. 
3. Rinomina la directory contenente i file dell'applicazione in modo che corrisponda al nome fornito alla tua applicazione in {{site.data.keyword.Bluemix_short}}. Ad esempio, se la tua applicazione si chiama myapp, rinomina la directory in myapp.
4. Sulla riga di comando, passa alla directory
            ridenominata.
<pre><code>cd myapp</code></pre>
5. Connettiti a {{site.data.keyword.Bluemix_short}}:
<pre><code>cf api https://api.DomainName</code></pre>
6. Accedi a {{site.data.keyword.Bluemix_short}} e, quando richiesto,
imposta la tua organizzazione di destinazione e distribuisci la tua applicazione.
<pre><code>
cf login
cf push myapp
</code></pre>

##Operazioni successive

* Passa alla pagina della panoramica della tua applicazione, accessibile dal dashboard {{site.data.keyword.Bluemix_short}}, per verificare che
            l'applicazione venga avviata correttamente.
* Avvia l'applicazione per visualizzarla nel browser. Puoi trovare l'URL (o "rotta") della
            tua applicazione nella pagina della panoramica dell'applicazione. La pagina Web per l'applicazione di esempio
            visualizza informazioni sullo stato delle chiamate dell'API REST nel codice applicativo e degli eventi
            che {{site.data.keyword.geospatialshort_Geospatial}}
            rileva.
