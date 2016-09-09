---

copyright:
  years: 2016

---
{:new_window: target="_blank"}

# Creazione di progetti mobili dal dashboard Mobile
{: #mobile}
Ultimo aggiornamento: 21 luglio 2016
{: .last-updated} 

Con i servizi mobili {{site.data.keyword.Bluemix}} puoi incorporare i servizi cloud precostruiti, gestiti e scalabili nelle tue applicazioni mobili senza dipendere dall'intervento del settore IT. Puoi concentrarti sulla creazione delle applicazioni mobili anziché sulla complessità della gestione dell'infrastruttura
  di back-end.

Il dashboard Mobile fornisce un'esperienza integrata su {{site.data.keyword.Bluemix_notm}}. Puoi creare nuovi progetti mobili facilmente dall'interno del dashboard. Con la vista **Progetti**, puoi gestire tutti i tuoi progetti in un solo posto. La vista **Servizi** visualizza le tue istanze del servizio mobile esistenti.

Per visualizzare il dashboard Mobile, fai clic sulla categoria **Mobile** dalla tua home di {{site.data.keyword.Bluemix_notm}}.
Home <img src="images/mobile_dashboard.jpg" alt="{{site.data.keyword.Bluemix_notm}} ">

Per iniziare, fai clic su **Nuovo progetto** dalla vista **Progetti** del dashboard Mobile.

## Panoramica dei servizi mobili {{site.data.keyword.Bluemix_notm}}
{: #mobile_services_overview}

La seguente tabella contiene descrizioni dei servizi mobili {{site.data.keyword.Bluemix_notm}} disponibili. Puoi utilizzare i servizi individuali dal catalogo {{site.data.keyword.Bluemix_notm}} o puoi integrarli nel tuo progetto mobile.

<table summary="Questa tabella descrive i servizi mobili {{site.data.keyword.Bluemix_notm}} e fornisce link alla documentazione del servizio">
<caption>Tabella 1. Servizi mobili {{site.data.keyword.Bluemix_notm}}</caption>
<th>Servizio mobile {{site.data.keyword.Bluemix_notm}}</th>
<th>Descrizione</th>
<tr>
<td> <img src="images/mobile_analytics_icon.png" alt="{{site.data.keyword.mobileanalytics_short}}icona"><br/>{{site.data.keyword.mobileanalytics_short}} (sperimentale)</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobileanalytics_full}} per misurare lo stato, il comportamento e in contesto delle applicazioni mobili, degli utenti mobili e dei dispositivi mobili.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella documentazione <a href="../services/mobileanalytics/index.html" alt="{{site.data.keyword.mobileanalytics_short}} link documentazione">{{site.data.keyword.mobileanalytics_short}}</a>.
</td>
</tr>
<tr>
<td><img src="images/catalog_icons-05.png" alt="{{site.data.keyword.amashort}} icona servizio"><br/>{{site.data.keyword.amashort}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.amafull}} per aggiungere funzionalità di sicurezza alla tua applicazione mobile. Puoi configurare l'autenticazione client e l'identità dei fornitori in modo che gli utenti possano accedere all'applicazione con i propri account Google o Facebook.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella documentazione <a href="../services/mobileaccess/index.html" alt="{{site.data.keyword.amashort}} link documentazione">{{site.data.keyword.amashort}}</a>.</td>
</tr>
<tr>
<td><img src="images/MFPFoundation_icon.png" alt="{{site.data.keyword.mobilefoundation_short}} icona servizio"><br/> {{site.data.keyword.mobilefoundation_short}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobilefoundation_long}} per velocizzare la configurazione di un ambiente {{site.data.keyword.mfp_full}} da cui puoi sviluppare, testare e operare applicazioni mobili aziendali.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella documentazione <a href="../services/mobilefoundation/index.html" alt="{{site.data.keyword.mobilefoundation_short}} link documentazione">{{site.data.keyword.mobilefoundation_short}}</a>.</td>
</tr>
<tr>
<td><img src="images/mqa_icon.png" alt="{{site.data.keyword.mqa}} icona servizio"><br/>{{site.data.keyword.mqa}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mqafull}} per scoprire e configurare i servizi di qualità mobili per le tue applicazioni. Puoi visualizzare le metriche di qualità di alto livello per le applicazioni mobili per comprendere rapidamente i problemi relativi alle applicazioni su cui stai lavorando. Queste metriche includono informazioni su arresti anomali, bug, feedback e sensazioni degli utenti. Visualizzando queste informazioni per le applicazioni, puoi stabilire se analizzare ulteriormente gli specifici problemi.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella documentazione <a href="../services/MobileQualityAssurance/index.html" alt="{{site.data.keyword.mqa}} link documentazione">{{site.data.keyword.mqa}}</a>.</td>
</tr>
<tr>
<td><img src="images/catalog_icons-09.png" alt="icona servizio Push Notifications"><br/>{{site.data.keyword.mobilepushshort}}</td>
<td valign="top">Utilizza il servizio {{site.data.keyword.mobilepushfull}} per inviare e gestire notifiche di push mobili mirate a piattaforme iOS e Android. Questo servizio gestisce l'associazione dei tuoi utenti delle applicazioni ai loro dispositivi e alla loro piattaforma del dispositivo e gestisce l'invio delle notifiche di push ai dispositivi. Con questo servizio, puoi inviare broadcast, unicast (basati su ID utente e ID dispositivo) e tag (o argomenti) basati sulle notifiche di push ai tuoi utenti delle applicazioni mobili.<br/><br/>
Leggi maggiori informazioni sull'utilizzo di questo servizio nella documentazione <a href="../services/mobilepush/index.html" alt="{{site.data.keyword.mobilepushshort}} link documentazione">{{site.data.keyword.mobilepushshort}}</a>.</td>
</table>

## Integrazione dei servizi mobili
{: #services_integration}
Puoi integrare i tuoi servizi mobili {{site.data.keyword.Bluemix_notm}}, come {{site.data.keyword.mobilepushshort}} e {{site.data.keyword.cloudant}}, nel tuo progetto.

#### Integrazione di {{site.data.keyword.mobilepushshort}}
{: #push_integration}

Per integrare il tuo servizio {{site.data.keyword.mobilepushshort}} esistente, completa la seguente procedura:

1. Fai clic sulla tua istanza del servizio {{site.data.keyword.mobilepushshort}}.
2. Fai clic su **Opzioni mobili** e copia i valori **Rotta** e **AppGuid**.

   **Nota**: il tuo servizio {{site.data.keyword.mobilepushshort}} deve essere associato a un'applicazione per visualizzare **Opzioni mobili**.

3. Ritorna alla vista **Progetti** del dashboard Mobile.
4. Fai clic sul tuo progetto per modificarlo.
5. Fai clic su **Push** e abilita le notifiche.
6. Fornisci il valore **AppGuid** che hai precedentemente copiato nell'**ID applicazione**.
7. Fornisci il valore **Rotta** che hai precedentemente copiato nell'**URL della rotta dell'applicazione**.

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


# Link correlati
{: #rellinks}

<!-- links to internal services don't work
## {{site.data.keyword.Bluemix_notm}} Mobile services
{: #general}
* [Mobile Analytics (Experimental)](../services/mobileanalytics/index.html){: new_window}
* [Mobile Client Access](../services/mobileaccess/index.html){: new_window}
* [Mobile Foundation](../services/mobilefoundation/index.html){: new_window}
* [Mobile Quality Assurance)](../services/MobileQualityAssurance/index.html){: new_window}
* [Push Notifications](../services/mobilepush/index.html){: new_window}
-->

## Post di blog
{: #general}
* [Blog Post: Introducing the Bluemix Mobile dashboard](https://developer.ibm.com/bluemix/2016/07/08/new-bluemix-mobile-dashboard/){: new_window}
* [Blog Post: Bluemix Mobile, Part 1: Creating a Store Catalog application](https://developer.ibm.com/bluemix/2016/07/13/bluemix-mobile-creating-store-catalog-app-part1/){: new_window}
* [Blog Post: Bluemix Mobile, Part 2: Integrating custom Bluemix backend into the Store Catalog app](https://developer.ibm.com/bluemix/2016/07/14/bluemix-mobile-integrating-custom-backend-part2/){: new_window}
 
## Esercitazioni ed esempi
{: #samples}
* [Mobile Backend for Bluemix](https://github.com/ibm-bluemix-mobile-services/mobiledashboard-storecatalog-backend){: new_window}

