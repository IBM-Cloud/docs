---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-19"

---

# Creazione delle applicazioni mobili dal contenitore tipo starter {{site.data.keyword.mobilefirstbp}}
{: #try_mobile}

Puoi utilizzare ognuno dei servizi mobili {{site.data.keyword.Bluemix}} indipendentemente. Puoi anche utilizzarli insieme, con il contenitore tipo starter {{site.data.keyword.mobilefirstbp}}, per trarne il massimo vantaggio.

Per iniziare, utilizza {{site.data.keyword.mobilefirstbp}} Starter per creare la tua applicazione. Il contenitore tipo ti permette di completare le seguenti azioni:

* Crea un runtime Node.js con un'applicazione template. Puoi utilizzare questa applicazione per fornire funzioni lato server, come le API RESTful e i file statici. <!-- You can read more about operating this application in the Developing Mobile Backend section.-->
* Fornisce un'istanza di ciascuno dei servizi mobili {{site.data.keyword.Bluemix_notm}} ed esegue il bind del servizio all'applicazione Node.js.

<!--
<img src="images/mf_boiler_icon.png" alt="Bluemix mobile services" width="500"> {{site.data.keyword.mobilefirstbp}} Starter boilerplate
-->

Dopo che hai utilizzato il contenitore tipo {{site.data.keyword.mobilefirstbp}} Starter per creare la tua applicazione, puoi ottenere degli esempi Hello Bluemix per ciascuno dei servizi oppure iniziare a strumentare la tua applicazione esistente per utilizzare i servizi {{site.data.keyword.Bluemix_notm}}.


## Panoramica sui servizi
{: #services-overview}
Puoi utilizzare tutti i servizi mobili {{site.data.keyword.Bluemix_notm}} insieme utilizzando il contenitore tipo {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.mobilefirstbp}} Starter oppure puoi utilizzare dei singoli servizi dal catalogo {{site.data.keyword.Bluemix_notm}}. Il seguente diagramma illustra i componenti dei servizi mobili {{site.data.keyword.Bluemix_notm}}.

![Architettura dei servizi mobili {{site.data.keyword.Bluemix_notm}}](images/bms_architecture.jpg)

<table summary="Questa tabella descrive i servizi mobili {{site.data.keyword.Bluemix_notm}} ">
<caption>Tabella 1. {{site.data.keyword.Bluemix_notm}} e sistemi aziendali</caption>
<th>{{site.data.keyword.Bluemix_notm}}</th>
<th>Sistemi aziendali</th>
<tr>
<td> <img src="images/i_js_64.png" alt="Icona di runtime Node.js"><b>Node.js</b> <br/> Un runtime Node.js che ospita un'applicazione template viene fornito come parte del contenitore tipo {{site.data.keyword.mobilefirstbp}} Starter. Puoi utilizzare l'applicazione template per fornire funzioni lato server, come le API RESTful e i file statici. <br/>Ad esempio, puoi estendere l'applicazione Node.js per l'elaborazione logica personalizzata oppure per stabilire una connessione alle API REST nell'infrastruttura esistente della tua azienda. Ciascuna applicazione da te creata su {{site.data.keyword.Bluemix_notm}} ha un ID applicazione univoco. La tua applicazione mobile utilizza questo ID con l'SDK per accedere ai servizi associati a tale applicazione. L'ID applicazione viene utilizzato dalla piattaforma come contesto per le funzioni comuni, come misurazione e registrazione.
<!--You can read more about operating this application in the "Developing Mobile Backend" section.--></td>
<td valign="top"><b>Provider di informazioni</b> <br/>Puoi utilizzare un runtime Node.js ospitato su {{site.data.keyword.Bluemix_notm}} per stabilire una connessione a qualsiasi tipo di provider di informazioni:
<ul>
	<li>Backend aziendale</li>
	<li>Database </li>
	<li>Un altro servizio di terzi ospitato</li>
</ul>
</td>
</tr>
<tr>
<td><img src="images/authentication_icon.png" alt="{{site.data.keyword.amashort}} - icona di servizio"> <b>{{site.data.keyword.amashort}}</b><br/>Utilizza il servizio {{site.data.keyword.amafull}}  per proteggere le applicazioni Node.js e Liberty for Java ospitate su {{site.data.keyword.Bluemix_notm}}. Strumentando la tua applicazione mobile con SDK {{site.data.keyword.amashort}}, puoi richiedere agli utenti di eseguire il login per accedere ai servizi mobili {{site.data.keyword.Bluemix_notm}}. <!-- In addition to security capabilities, {{site.data.keyword.amashort}} also gathers analytics data, so that you can monitor your mobile application performance and collect client logs and usage statistics.--> </td>
<td valign="top"><b>Provider di identità utente</b> <br/>Puoi utilizzare i seguenti provider di identità: <ul><li>Facebook</li><li>Google</li><li> Personalizzata </li></ul></td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="{{site.data.keyword.mobilepushshort}} icona servizio "> <b>{{site.data.keyword.mobilepushshort}}</b><br/>Il servizio  {{site.data.keyword.mobilepushfull}} fornisce una piattaforma unificata per inviare e gestire le notifiche di push destinate alle piattaforme mobili (iOS e Android) e alle applicazioni del browser Web. Questo servizio gestisce l'associazione dei tuoi utenti delle applicazioni ai loro dispositivi, alla loro piattaforma del dispositivo e ai browser e gestisce l'invio delle notifiche di push ai sottoscrittori. Con questo servizio, puoi inviare broadcast, unicast (basati su ID utente e ID dispositivo) e tag (o argomenti) basati sulle notifiche di push ai tuoi clienti.</td>
<td valign="top"><b>Provider di servizi di push</b><ul><li>APNS (Apple Push Notifications Service)</li><li>FCM (Firebase Cloud Messaging)</li></ul></td>
</tr>
<tr>
<td><img src="images/cloudant64.png" alt="Icona del servizio Cloudant"><b>Cloudant NoSQLDB</b><br/> Cloudant è un DBaaS (database as a service) NoSQL. Viene creato da zero per ingrandirsi fino a un livello globale, essere eseguito non-stop e gestire un'ampia varietà di tipi di dati come JSON, full-text e geospaziali. </td>
<td>Cloudant.com</td>
</tr>
</table>
