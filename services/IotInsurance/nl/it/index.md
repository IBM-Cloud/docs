---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Introduzione a {{site.data.keyword.iotinsurance_short}} (Beta)
{: #iotins_gettingstarted}
Ultimo aggiornamento: 16 settembre 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} è un servizio {{site.data.keyword.Bluemix_notm}} che puoi utilizzare per raccogliere, gestire e analizzare i dati dai possessori della polizza collegati. {{site.data.keyword.iotinsurance_short}} ti fornisce la capacità di fornire valutazioni del rischio, protezione in tempo reale e riduzione dei costi della polizza personalizzati.
{:shortdesc}

Per essere operativo con questo servizio, devi distribuire i servizi e le applicazioni richiesti, quindi configurare i servizi.

**Prerequisiti:** prima di iniziare, assicurati che siano implementati i seguenti prerequisiti:
- Deve esistere un'istanza del [ servizio {{site.data.keyword.iotinsurance_short}}](https://console.ng.bluemix.net/catalog/services/iot-for-insurance/) nel tuo spazio {{site.data.keyword.Bluemix_notm}}.
- Devono essere disponibili almeno 2 GB di memoria nella tua organizzazione {{site.data.keyword.Bluemix_notm}} per abilitare la funzione di distribuzione.

## Distribuzione delle applicazioni e dei servizi richiesti
{: #deploying_services}

1. Per distribuire tutti i servizi e le applicazioni richiesti, nella [ console {{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net/#all-items), fai clic sul tile del servizio {{site.data.keyword.iotinsurance_short}} e quindi su **Distribuisci**.

  {{site.data.keyword.iotinsurance_short}} distribuisce tutti i servizi e le applicazioni Node.js necessarie. Esegue automaticamente il bind delle applicazioni ai servizi.

  Ogni istanza del servizio utilizza il piano del servizio predefinito. Puoi eseguire l'upgrade di ogni piano del servizio in un secondo momento andando nella console del servizio. Puoi anche utilizzare un'istanza esistente di un servizio eliminando la nuova istanza e eseguendo il bind manualmente dell'istanza esistente al servizio {{site.data.keyword.iotinsurance_short}}. Per ulteriori informazioni sulle applicazioni, consulta [Informazioni su {{site.data.keyword.iotinsurance_short}}](iotinsurance_overview.html).

2. Verifica che tutti i servizi e le applicazioni siano stati creati e che funzionino correttamente. Nella tua console {{site.data.keyword.Bluemix_notm}}, controlla che tutte le applicazioni abbiano lo stato di `In esecuzione`.

3. Verifica che il dashboard {{site.data.keyword.iotinsurance_short}} sia funzionale e che tu possa accedere alle API.
  1. Fai clic sul tile del servizio {{site.data.keyword.iotinsurance_short}} e seleziona quindi la scheda **Credenziali del servizio**.
  2. Fai clic su **Visualizza credenziali** e prendi nota dell'ID utente e della password. Utilizzerai queste credenziali nei seguenti passi.
  3. Apri il dashboard {{site.data.keyword.iotinsurance_short}} selezionando la scheda **Gestione** e facendo clic su **Apri**.
  4. Torna alla scheda **Gestisci**. Visualizza le API facendo clic su **API**.

## Configurazione dei servizi
{: #iot4i_configservices}
Esegui le seguenti attività per configurare i servizi:

### Configurazione di {{site.data.keyword.amashort}}
{: #config_ama}
1. Nella tua console {{site.data.keyword.Bluemix_notm}}, copia l'URL dell'applicazione API {{site.data.keyword.iotinsurance_short}}. Fai clic con il tasto destro del mouse sul tile dell'applicazione API e seleziona **Copia posizione link**.

2. Apri il servizio {{site.data.keyword.amashort}}. Il servizio è disponibile nella sezione Servizi della tua console {{site.data.keyword.Bluemix_notm}}.

3. Nella sezione **Personalizza**, fai clic su **Configura** e immetti quindi le seguenti credenziali di autenticazione:

  - **Nome realm**: `IoT4I`

  - **URL provider di identità personalizzato**: incolla l'URL dell'applicazione API che hai copiato nel primo passo.

  - **I tuoi URI di reindirizzamento dell'applicazione web**: lascia questo campo vuoto.

### Configurazione di {{site.data.keyword.mobilepushshort}}
{: #config_push}
Per abilitare le notifiche push per un'applicazione mobile esistente, devi configurare il servizio {{site.data.keyword.mobilepushshort}} e aggiungere un file Public Key Cryptography Standards (PKCS) 12. Per informazioni sull'applicazione mobile, consulta [Installazione e collegamento dell'applicazione mobile di esempio](iotinsurance_mobile_app.html). Per informazioni su {{site.data.keyword.mobilepushshort}}, consulta [Getting started with Push Notifications](https://console.stage1.ng.bluemix.net/docs/services/mobilepush/index.html).

  1. Apri il servizio {{site.data.keyword.mobilepushshort}}.
  2. Fai clic su **Setup Push**.
  3. Nella sezione Apple Push Notifications Certificate, carica il file PKCS 12 per la tua applicazione mobile e immetti la password.

Operazioni successive
{: #whats_next}
Impara cosa puoi fare con {{site.data.keyword.iotinsurance_short}}.

- Creare [un'associazione scudo e un utente](iotinsurance_create_users.html).
- Installare e collegare l'[applicazione mobile di esempio](iotinsurance_mobile_app.html).
- Migliorare le prestazioni con i [servizi avanzati](iotinsurance_advancedservices.html).
- Visualizzare le [API](https://iot4i-docs-api.mybluemix.net/dist/).

# Link correlati
{: #rellinks}

## Esercitazioni ed esempi
{: #samples}
* [Sample mobile app code on Github](https://github.com/ibm-watson-iot/ioti-mobile){:new_window}

## Riferimento API
{: #api}
* [Esempi di API {{site.data.keyword.iotinsurance_short}}](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs){:new_window}

## Link correlati
{: #general}
* [Documentazione {{site.data.keyword.iot_full}}](https://console.ng.bluemix.net/docs/services/IoT/index.html)
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
