---

copyright:
  years: 2016

---

{:new_window: target="_blank"}

{:shortdesc: .shortdesc}


# Creazione di applicazioni con lo starter {{site.data.keyword.iotelectronics}}
*Ultimo aggiornamento: 14 giugno 2016*
{: .last-updated}

{{site.data.keyword.iotelectronics_full}} è una soluzione integrata, end-to-end che abilita le tue applicazioni a comunicare con, controllare, analizzare e aggiornare le applicazioni collegate. Lo starter include un'applicazione starter che ti permette di creare e controllare le applicazioni simulate e un'applicazione mobile di esempio che ti permette di controllare queste applicazioni dal tuo dispositivo mobile.
{:shortdesc}

**Prerequisiti**:  
Assicurati di aver distribuito lo starter {{site.data.keyword.iotelectronics}} dalla sezione dei contenitori tipo del catalogo Bluemix. In questo modo i servizi e le applicazioni del componente sono distribuite automaticamente dallo starter, incluso {{site.data.keyword.amafull}}.

Per iniziare ad utilizzare {{site.data.keyword.iotelectronics}}, completa queste attività come descritto nelle seguenti sezioni:

1. Abilita le comunicazioni con l'applicazione mobile di esempio configurando {{site.data.keyword.amashort}}.
2. Crea le applicazioni simulate utilizzando l'applicazione web starter {{site.data.keyword.iotelectronics}}.
3. Installa e collega l'applicazione mobile di esempio.

## Configurazione di {{site.data.keyword.amashort}}
{: #configureMCA}
Per utilizzare l'applicazione mobile, devi configurare {{site.data.keyword.amashort}}, nel seguente modo:
1. Nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, apri [{{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html).
2. Nella sezione **Personalizza**, seleziona **Configura**.
3. Immetti le seguenti credenziali di autenticazione:
  - **Nome realm**: myRealm
  - **URL**: https://<*myIoT4eStarterApp*>.mybluemix.net  

    **Suggerimento:** assicurati di utilizzare il prefisso `https://` sicuro nell'URL. Puoi trovare l'URL della tua applicazione starter facendo clic su **Opzioni mobili**.)
4. Salva.

  Per istruzioni dettagliate, consulta [Configurazione di {{site.data.keyword.amashort}}](iotelectronics_config_mobile.html#iot4e_configureMCA).

##Creazione di applicazioni simulate
Per creare un'applicazione simulata, completa la seguente procedura:
1. Nel tuo dashboard {{site.data.keyword.Bluemix_notm}}, avvia la tua applicazione {{site.data.keyword.iotelectronics}}.
2. Attendi il messaggio di stato *La tua applicazione è in esecuzione* e quindi fai clic su **Visualizza applicazione** per visualizzare l'applicazione starter.  
3. Seleziona **Controlla in remoto le tue applicazioni collegate**.
4. Vai alla sezione etichettata **Successivo, scegli o aggiungi una nuova rondella simulata** e fai clic sul pulsante Aggiungi (+). Viene creata una nuova rondella.

## Installazione e collegamento dell'applicazione mobile di esempio
Per installare e collegare l'applicazione mobile di esempio, completa la seguente procedura:

*Nota*: devi disporre di un dispositivo iOS per utilizzare l'applicazione mobile di esempio.

1. Sul tuo telefono, apri l'App store e cerca `ibm iot`. Scegli **IBM IoT for Electronics** e installa.
2. Collega il tuo telefono alla tua organizzazione scansionando il codice QR di connessione trovato nella tua applicazione starter.
3. Collega la tua applicazione simulata scansionando il codice QR dell'applicazione trovato nella tua applicazione starter.

  Per istruzioni dettagliate, consulta [Collegamento dell'applicazione mobile al tuo ambiente {{site.data.keyword.iotelectronics}}](iotelectronics_config_mobile.html#iot4e_connecting_mobile).

##Operazioni successive
Scopri cosa puoi fare con {{site.data.keyword.iotelectronics}}.

- Esplora l'applicazione starter per vedere come un produttore aziendale può monitorare le applicazioni collegate a {{site.data.keyword.iot_short_notm}}.
- Esplora l'applicazione mobile di esempio per vedere come i proprietari dell'applicazione possono registrare e interagire con le loro applicazioni.
- Crea manualmente un errore nel dispositivo per attivare avvisi, notifiche e azioni per il produttore e il proprietario dell'applicazione.
- Associa i dati operativi ai dati utente per comprendere come i tuoi prodotti e dispositivi funzionano e chi li fa funzionare.


# Link correlati
{: #rellinks}
## Documentazione API
{: #api}
* [{{site.data.keyword.iotelectronics}} API](http://ibmiotforelectronics.mybluemix.net/public/iot4eregistrationapi.html)
* [{{site.data.keyword.iot_short}} API](https://developer.ibm.com/iotfoundation/recipes/api-documentation/)


## interessati
{: #general}

* [Documentazione {{site.data.keyword.iotelectronics}}](iotelectronics_overview.html)
* [Documentazione {{site.data.keyword.iot_full}}](https://new-console.ng.bluemix.net/docs/services/IoT/index.html)
*  [Documentazione {{site.data.keyword.amashort}}](https://new-console.ng.bluemix.net/docs/services/mobileaccess/overview.html)
* [Documentazione {{site.data.keyword.sdk4nodefull}}](https://new-console.ng.bluemix.net/docs/runtimes/nodejs/index.html#nodejs_runtime)

## Esempi
{: #samples}
* [Applicazione mobile di esempio](https://new-console.ng.bluemix.net/docs/starters/IotElectronics/iotelectronics_config_mobile.html)
