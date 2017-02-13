---

copyright:
  years: 2016, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}

# Esercitazione - Starter codice linguaggio Watson
{: #tutorial_watson_language}

Il starter codice {{site.data.keyword.Bluemix}} Mobile per il linguaggio Watson illustra i servizi Text To Speech e Language Translation da Watson e ti fornisce punti di integrazione per ognuno dei servizi {{site.data.keyword.Bluemix_notm}} Mobile.


## Requisiti
{: #tutorial_requirements}

* Un account [Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net "Icona link esterno")
* Le istanze del servizio [Language Translator ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/language-translator/ "Icona link esterno") e [Text to Speech ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/services/text-to-speech/ "Icona link esterno") ottenute dal [Catalogo Bluemix ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/catalog/ "Icona link esterno")


## Introduzione
{: #tutorial_gs}

Per essere velocemente operativo con lo starter codice linguaggio Watson, segui la seguente procedura:

1. rea un progetto dashboard Mobile in {{site.data.keyword.Bluemix_notm}}.

   1. Dalla pagina **Introduzione** nel dashboard Mobile, fai clic su **Crea progetto**.

      In alternativa puoi fare clic su **Crea progetto** dalla pagina **Progetti**.

   2. Fai clic su **Starter codice**.

   3. Seleziona **Linguaggio Watson** e fai clic su **Crea progetto**.

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

6. Estrai l'archivio e visualizza il file `README.md` in un visualizzatore Markdown per completare la configurazione.


## Operazioni successive
{: #tutorial_next}

[Provatela! ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://console.{DomainName}/mobile/create-project?starter=512568a1-72db-35c7-b9c4-4f3e3bc89375 "Icona link esterno"){: new_window}



### Esercitazioni starter IU
{: #tutorials_UI}

* [Esercitazione - Catalogo negozio](tutorial_store_catalog.html)


### Esercitazioni starter codice
{: #tutorials_Code}

* [Esercitazione - Di base](tutorial.html)
* [Esercitazione - Cloudant Sync](tutorial_cloudant_synd.html)
* [Esercitazione - {{site.data.keyword.openwhisk_short}}](tutorial_openwhisk.html)
* [Esercitazione - {{site.data.keyword.visualrecognitionshort}}](tutorial_visual_recognition.html)
* [Esercitazione - Weather ](tutorial_weather.html)

