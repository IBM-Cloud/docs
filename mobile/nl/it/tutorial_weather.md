---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Esercitazione - Starter codice Weather
{: #tutorial_weather}

Lo starter codice {{site.data.keyword.Bluemix}} Mobile per Weather illustra un progetto ponte per iniziare ad utilizzare Weather, utilizzando Swift e che include i punti di integrazione Push e Analytics.


## Requisiti
{: #tutorial_requirements}

* Un account [Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net "Icona link esterno")
* Un'istanza del servizio [Weather Company Data ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/weather-company-data/ "Icona link esterno") ottenuta dal [Catalogo Bluemix![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/ "Icona link esterno")


## Introduzione
{: #tutorial_gs}

Per essere velocemente operativo con lo starter codice Weather, segui la seguente procedura:

1. rea un progetto dashboard Mobile in {{site.data.keyword.Bluemix_notm}}.

   1. Dalla pagina **Introduzione** nel dashboard Mobile, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Nuovo progetto** dalla pagina **Progetti**.

   2. Fai clic su **Starter codice**.

   3. Seleziona **Weather** e fai clic su **Crea progetto**.

   4. Immetti il nome del tuo progetto e fai clic su **Crea**.

2. Facoltativo: aggiungi la funzionalità {{site.data.keyword.mobilepushshort}}.

   1. Fai clic su **Aggiungi** per **{{site.data.keyword.mobilepushshort}}** nella pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **{{site.data.keyword.mobilepushshort}}**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.

   3. Per iOS, [configura il servizio Apple Push Notification![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_ios.html "Icona link esterno"){: new_window}.

   4. Per Android, [configura Google Cloud Messaging ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobilepush/t_push_provider_android.html "Icona link esterno"){: new_window}.
   
3. Facoltativo: aggiungi la funzionalità Analytics.

   1. Fai clic su **Aggiungi** per **Analytics** dalla pagina **Panoramica progetto**.

      In alternativa puoi fare clic su **Crea** dalla pagina **Analytics**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Disattiva la **Modalità demo** per visualizzare i tuoi dati di analisi dopo l'esecuzione della tua applicazione.

   4. Vedi [Introduzione a {{site.data.keyword.mobileanalytics_short}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileanalytics/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione di Analytics.

4. Facoltativo: aggiungi la funzionalità Authentication.

   1. Fai clic su **Aggiungi** per **Authentication** nella pagina **Panoramica progetto**.

      In alternativa puoi selezionare **Crea** nella pagina **Authentication Notifications**.

   2. Immetti il nome del tuo servizio e fai clic su **Crea**.
   
   3. Attiva **Authentication**.
   
   4. Seleziona il tuo provider di identità ed immetti le informazioni richieste per configurarlo. Puoi abilitare solo un provider di identità.

   5. Vedi [Introduzione a Mobile Client Access ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/services/mobileaccess/index.html "Icona link esterno"){: new_window} per ulteriori informazioni sulla configurazione dell'autenticazione .

5. Scarica il tuo progetto.

   1. Fai clic su **Codice** e seleziona il tuo linguaggio preferito.

   2. Fai clic su **Scarica codice**.

5. Estrai l'archivio e segui le istruzioni nel file `README.md`.


## Operazioni successive
{: #tutorial_next}

[Provatela! ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://console.{DomainName}/mobile/create-project?starter=fad1d49e-f7b6-3aff-9b53-14673fca4399 "Icona link esterno"){: new_window}


### Esercitazioni starter IU
{: #tutorials_UI}

* [Esercitazione - Catalogo negozio](tutorial_store_catalog.html)


### Esercitazioni starter codice
{: #tutorials_Code}

* [Esercitazione - Di base](tutorial.html)
* [Esercitazione - Cloudant Sync](tutorial_cloudant_synd.html)
* [Esercitazione - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Esercitazione - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Esercitazione - Linguaggio Watson](tutorial_watson_language.html)
