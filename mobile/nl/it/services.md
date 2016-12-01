---

copyright:
  years: 2016
lastupdated: "2016-10-18"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock: .codeblock}

# Servizi
{: #services}

Dal dashboard {{site.data.keyword.Bluemix}} Mobile, vista **Servizi**, puoi visualizzare i tuoi servizi esistenti o crearne di nuovi. Il dashboard Mobile fornisce una singola ubicazione per visualizzare tutti i servizi Bluemix che stanno venendo gestiti dai progetti.  

Se elimini dei servizi dalla vista **Servizi**, scollegherai il servizio dal progetto a cui è associato. Crea una nuova istanza del servizio se desideri ricollegare il servizio al progetto.

## Panoramica dei servizi mobili {{site.data.keyword.Bluemix_notm}}
{: #mobile_services_overview}

La seguente tabella contiene descrizioni dei servizi mobili {{site.data.keyword.Bluemix_notm}}. Puoi utilizzare i servizi individuali dal catalogo {{site.data.keyword.Bluemix_notm}} o puoi integrarli nel tuo progetto mobile.

<table summary="Questa tabella descrive i servizi mobili {{site.data.keyword.Bluemix_notm}} e fornisce link alla documentazione del servizio">
<caption>Tabella 1. Servizi mobili {{site.data.keyword.Bluemix_notm}}</caption>
<th>Servizio mobile {{site.data.keyword.Bluemix_notm}}</th>
<th>Descrizione</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}icona"><br/>{{site.data.keyword.mobileanalytics_short}} (Beta)</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobileanalytics_full}} per acquisire informazioni su come le applicazioni mobili stanno venendo eseguite e utilizzate.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella <a href="/docs/services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} link documentazione">{{site.data.keyword.mobileanalytics_short}} documentazione</a>.
</td>
</tr>
<tr>
<td><img src="images/authentication_icon
.png" alt="{{site.data.keyword.amashort}} icona servizio"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.amafull}} per aggiungere funzionalità di sicurezza alla tua applicazione mobile. Puoi configurare l'autenticazione client e l'identità dei fornitori in modo che gli utenti possano accedere all'applicazione con i propri account Google o Facebook.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella <a href="/docs/services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} link documentazione">{{site.data.keyword.amashort}} documentazione</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} icona servizio"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobilefoundation_long}} per velocizzare la configurazione di un ambiente {{site.data.keyword.mfp_full}} da cui puoi sviluppare, testare e operare applicazioni mobili aziendali.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella <a href="/docs/services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} link documentazione">{{site.data.keyword.mobilefoundation_short}} documentazione</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} icona servizio"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mqafull}} per scoprire e configurare i servizi di qualità mobili per le tue applicazioni. Puoi visualizzare le metriche di qualità di alto livello per le applicazioni mobili per comprendere rapidamente i problemi relativi alle applicazioni su cui stai lavorando. Queste metriche includono informazioni su arresti anomali, bug, feedback e sensazioni degli utenti. Visualizzando queste informazioni per le applicazioni, puoi stabilire se analizzare ulteriormente gli specifici problemi.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella <a href="/docs/services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} link documentazione">{{site.data.keyword.mqa}} documentazione</a>.</td>
</tr>
<tr>
<td><img src="images/push_icon.png" alt="icona servizio Push Notifications"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobilepushfull}} per inviare e gestire notifiche di push mobili mirate a piattaforme iOS e Android. Questo servizio gestisce l'associazione dei tuoi utenti delle applicazioni ai loro dispositivi e alla loro piattaforma del dispositivo e gestisce l'invio delle notifiche di push ai dispositivi. Con questo servizio, puoi inviare broadcast, unicast (basati su ID utente e ID dispositivo) e tag (o argomenti) basati sulle notifiche di push ai tuoi utenti delle applicazioni mobili.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella <a href="/docs/services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} link documentazione">{{site.data.keyword.mobilepushshort}} documentazione</a>.</td>
</table>

## Integrazione dei servizi mobili
{: #services_integration}
Puoi integrare i tuoi servizi {{site.data.keyword.Bluemix_notm}} Mobile esistenti, come {{site.data.keyword.cloudant}}, nel tuo progetto.


#### Integrazione di {{site.data.keyword.cloudant}}
{: #cloudant_integration}

Per integrare il tuo servizio {{site.data.keyword.cloudant}} esistente, completa la seguente procedura:

1. Fai clic sulla tua istanza del servizio {{site.data.keyword.cloudant}}.
2. Fai clic su **AVVIA**.
3. Nella vista **Database**, fai clic sul tuo nome database.
4. Fai clic su **API** e copia il valore **Chiave API** nel tuo nome database.

   **Nota**: non copiare il contenuto passato nel tuo nome database.

5. Fai clic su **Autorizzazioni** > **Genera chiave API** e copia i valori **Chiave** e **Password**.
6. Ritorna alla vista **Progetti** del dashboard Mobile.
7. Fai clic sul tuo progetto per modificarlo.
8. Fai clic su **Dati** > **+ Origine dati** > **Cloudant** e fornisci il tuo nome dell'origine dati e fai clic su **Aggiungi**.
9. Fai clic su **Configurazione Cloudant**.
10. Fornisci il valore **Chiave API** che hai precedentemente copiato nell'**URL API**.
11. Fornisci il valore **Chiave** che hai precedentemente copiato nell'**Utente**.
12. Fornisci il valore **Password** che hai precedentemente copiato nella **Password**.
13. Fai clic su **Ok**.
