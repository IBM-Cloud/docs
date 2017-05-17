---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-02"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:tip: .tip}

# Abilitazione della messaggistica vocale ed SMS
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} supporta l'integrazione con Twilio per abilitare la messaggistica vocale ed SMS. Twilio è un'applicazione di terze parti, che puoi installare nel tuo dashboard {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

## Prerequisiti
Per abilitare la messaggistica vocale, devi disporre di un account Twilio autorizzato e un numero di telefono Twilio.  Se utilizzi un account gratuito Twilio, devi anche autorizzare un numero di telefono a ricevere chiamate o messaggi. Per ulteriori informazioni, consulta la [documentazione Twilio![External link icon](../../icons/launch-glyph.svg)](https://support.twilio.com/hc/en-us/articles/223136107-How-does-Twilio-s-Free-Trial-work-){:new_window}.

## Creazione e configurazione di un'istanza Twilio
1. Crea un'istanza Twilio  nella stessa organizzazione e nello stesso spazio {{site.data.keyword.Bluemix_notm}} in cui hai installato {{site.data.keyword.iotinsurance_short}}.
    1. Accedi a [{{site.data.keyword.Bluemix_notm}}](https://console.ng.bluemix.net).
    2. Seleziona la scheda **Catalogo**.
    3. Individua la sezione Mobile del catalogo dei servizi e fai clic su **Twilio**.

    **Suggerimento:** fai clic [qui ![icona link esterno](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/catalog/services/twilio/){: new_window} per accedere direttamente alla pagina Twilio.
    {: tip}

    4. Nella pagina Twilio, fornisci le tue credenziali ed esegui il bind dell'applicazione come segue:

      1. Immetti `Twilio-00` come nome del servizio.  **Importante:** devi utilizzare `Twilio-00` per connetterti correttamente a {{site.data.keyword.iotinsurance_short}}.

      2. Immetti le tue credenziali Twilio.

      3. Nel menu **Connetti a**, seleziona la tua applicazione iot4i-action-engine per eseguire il bind dell'istanza Twilio a {{site.data.keyword.iotinsurance_short}}.

      4. Fai clic su **Crea**.  

    L'applicazione Twilio viene installata nel tuo ambiente. Un messaggio ti richiede di ripreparare o riavviare la tua applicazione iot4i-action-engine per abilitare il bind. Puoi riavviare subito o in seguito dopo l'aggiunta della nuova variabile di ambiente nel passo successivo.

2. Crea una variabile di ambiente denominata TWILIO_FROM_NUMBER per il componente iot4i-action-egine.
    1. Dal dashboard Bluemix, apri l'applicazione iot4i-action-engine.
    2. Seleziona **Runtime**, quindi fai clic su **Variabili di ambiente**.
    3. Nella sezione **Definito dall'utente**, fai clic su **Aggiungi**.
    4. Nella colonna Nome, immetti `TWILIO_FROM_NUMBER` e poi, nella colonna Valore, immetti il tuo numero abilitato per gli SMS e chiamate Twilio.
    5. Fai clic su **Salva**.

3. Riavvia l'applicazione Iot4i-action-engine facendo clic sull'icona Riavvia che si trova accanto al pulsante Rotte.

## Aggiunta di azioni SMS e vocali a una shield

Per aggiungere le capacità SMS e vocali a una shield, devi aggiungere le seguenti azioni alla definizione della shield:
  - `send-sms`
  - `phone-call`

Per un esempio di shield che contiene un elenco di azioni, vedi [Create a sample shield example ![icona link esterno](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/blob/master/bl/shield.js){:new_window}. Nell'esempio, le azioni SMS e vocali possono essere aggiunte all'elenco di azioni che contiene le azioni `email` e `pushios`.

Per ulteriori informazioni sulla creazione delle shield, vedi [Using the shield toolkit](iotinsurance_shield_toolkit.html).
