---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Definizione delle politiche
{: #criteria}

Con {{site.data.keyword.DRA_short}}, la definizione delle politiche per la tua applicazione è facile. A tal fine, attenersi ai seguenti passaggi:
{:shortdesc}

1. Nel menu laterale, fai clic su **Policy**.

2. Fai clic su **Create Policy (+)** e immetti quindi un nome e una descrizione per la nuova politica.

3. Fai clic su **Next**.

4. Aggiungi almeno una regola alla politica:
  1. Fai clic su **Create Rule (+)**.
  2. Seleziona il tipo di regola.
  3. Immetti i dettagli e le condizioni per la regola.
  4. Fai clic su **Save**.

5. Quando ha terminato di aggiungere le regole alla politica, fai clic su **Complete**.

Le regole vengono create nell'organizzazione {{site.data.keyword.Bluemix_notm}} a cui è stato aggiunto {{site.data.keyword.DRA_short}}. Tutte le applicazioni nella stessa organizzazione possono utilizzare la politica.

{{site.data.keyword.DRA_short}} supporta questi tipi di metriche e formati:

* Test di verifica funzionale (Mocha, JUnit)
* Verifiche di unità (Mocha, JUnit, Karma/Mocha)
* Copertura del codice (Istanbul come formato di riepilogo JSON, Blanket.js)

{{site.data.keyword.DRA_short}} supporta inoltre i test Selenium e Jasmine. Questi test devono essere inclusi negli strumenti supportati ufficiali, come JUnit, xUnit e Mocha. Per ulteriori informazioni sull'utilizzo contemporaneo di {{site.data.keyword.deliverypipeline}}, {{site.data.keyword.DRA_short}} e Selenium, consulta [Running Selenium tests from the command line on a delivery pipeline](https://developer.ibm.com/devops-services/2016/07/21/running-selenium-tests-command-line-delivery-pipeline/).

Per gli elementi con scenari di test, puoi specificare gli scenari di test critici, che sono test che devono essere superati indipendentemente dalla percentuale accettabile. Il nome degli scenari di test critici devono corrispondere all'attributo `full title` dello scenario di test:    
* Per i test Karma/Mocha, le stringhe della descrizione `describe()` e `it()` sono collegate tra loro con gli spazi
* Per i test JUnit, il nome del pacchetto e della funzione sono collegati tra loro con gli spazi    

Puoi utilizzare Sauce Labs con {{site.data.keyword.DRA_short}} aggiungendo l'integrazione Sauce Labs alla tua pipeline. Quindi, incorpora le variabili di ambiente `SAUCE_USERNAME` e `SAUCE_ACCESS_KEY` nei test Selenium come credenziali.

Puoi visualizzare i titoli completi di tutti i test nei log dopo un'esecuzione.  

Note:
* {{site.data.keyword.DRA_short}} non supporta i test critici che contengono un trattino nel titolo completo.    
* Se modifichi il tuo nome dell'organizzazione, devi ricreare le politiche che sono state associate con il nome precedente. Perderai l'accesso ai report di decisione generati prima della modifica del nome.

## Creazione delle regole del test di verifica funzionale
{: #criteria_fvt}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico.

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


## Creazione delle regole per la verifica di unità
{: #criteria_ut}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di scenari di test che deve essere superata per essere considerata con esito positivo.

3. Definisci ogni scenario di test che è critico.

4. Per monitorare le regressioni dello scenario di test, seleziona la casella di spunta **Monitor for test case regression**.

5. Fai clic su **Save**.


## Creazione delle regole di copertura del codice
{: #criteria_codecoverage}

1. Immetti un descrizione e seleziona un formato.

2. Specifica la percentuale di copertura del codice necessaria per essere considerato con esito positivo.

3. Per monitorare le regressioni di copertura del codice, seleziona la casella di spunta **Monitor for test case regression**.

4. Fai clic su **Save**.
