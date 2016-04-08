---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Tipi di azione {: #actions}

Oltre a visualizzare gli avvisi nel relativo dashboard, {{site.data.keyword.iotrtinsights_short}} supporta diversi tipi di azioni attivate dalle regole, come l'invio di email e di webhook.
{: shortdesc}

## Creazione di azioni {: #shared}
Puoi [creare delle azioni direttamente dall'editor di regole](rules.html "Creare regole") oppure creare le azioni nel pannello Azioni e selezionare quindi le azioni quando crei le tue regole.

Per creare un'azione dal pannello Azioni:
1. Nella console {{site.data.keyword.iotrtinsights_short}}, vai a **Analisi > Azioni**.
2. Fai clic su **Aggiungi nuova azione**, seleziona un tipo di azione, dai un nome all'azione e fornisci una descrizione.
3. Fornisci i parametri obbligatori per il tipo di azione che stai creando.
Tipi di azione:  
 - [Invia email](#email "Invia email")
 - [Webhook](#webhook "Webhook")
 - [Node-RED](#nodered "Node-RED")
 - [IFTTT](#ifttt "IFTTT")
4. Fai clic su **OK** per creare la nuova azione.

L'azione è ora disponibile nell'[editor di regole](rules.html#rules "Editor di regole").



## Invia email {: #email}
Utilizza l'azione Invia email per inviare una email a uno o più destinatari quando viene attivata una regola.

Esempio: [Invia email](action_examples.html#emailex).

I seguenti parametri vengono utilizzati per configurare l'azione Invia email:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, che viene utilizzato nel dashboard Avvisi.
Descrizione | Una breve descrizione dell'azione.
A | Uno o più indirizzi email, separati da virgole.
Cc | Uno o più indirizzi email, separati da virgole.
Oggetto | La riga dell'oggetto dell'email. Facoltativamente, puoi avviare automaticamente l'oggetto con "IoT Real-Time Insight alert".

Il corpo dell'email viene creato automaticamente dal messaggio del dispositivo al momento in cui è stata attivata la regola.  
**Importante:** se i dati del dispositivo contengono delle informazioni sensibili, puoi scegliere di non includere i dati del dispositivo nel messaggio email e di mostrare i dati sensibili solo nel pannello degli avvisi.


## Webhook {: #webhook}
Utilizzare l'azione webhook per effettuare una richiesta HTTP a un servizio web abilitato ai webhook quando viene attivato un avviso. Ad esempio, un webhook può essere utilizzato per aprire una richiesta di servizio per una risorsa se un sensore nel dispositivo segnala una lettura anomala.

Esempio: [Utilizza un webhook per pubblicare su Slack](action_examples.html#webhookex).

Per configurare un'azione webhook vengono utilizzati i seguenti parametri:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, che viene utilizzato nel dashboard Avvisi.
Descrizione | Una breve descrizione dell'azione.
URL | L'URL del server abilitato ai webhook di destinazione. **Suggerimento:** puoi utilizzare la [sostituzione di variabili](#variable_substitution) per includere dinamicamente dei dati aggiuntivi nell'URL.
Metodo | Il tipo di chiamata webhook da eseguire. Seleziona uno dei seguenti tipi: GET, HEAD, OPTIONS, PATCH, PUT, POST o DELETE.
Nome utente | Includi se richiesto dal servizio web.
Password | Includi se richiesto dal servizio web. **Importante:** la password viene inviata in testo in chiaro.
Intestazione | Le intestazioni sono costituite da coppie chiave - valore. **Suggerimento:** puoi usare la [sostituzione di variabili](#variable_substitution) per includere dinamicamente dei dati aggiuntivi nell'intestazione.
Tipo di contenuto | Il tipo di contenuto del corpo: JSON, XML, con codifica URL in formato WWW o testo semplice. Disponibile per i metodi OPTIONS, PATCH, PUT, POST e DELETE.
Corpo | Il corpo della chiamata webhook. Disponibile per i metodi OPTIONS, PATCH, PUT, POST e DELETE. Per impostazione predefinita, il campo del corpo è precompilato con tutte le variabili elencate nella [sostituzione di variabili](#variable_substitution). Seleziona **Utilizza corpo del messaggio personalizzato** per modificare il contenuto del
campo del corpo. **Importante:** il server webhook potrebbe richiedere che vengano inclusi nel corpo alcuni specifici campi. Ad esempio, un webhook Slack deve contenere il campo "text".   



## Node-RED {: #nodered}
Utilizza l'azione Node-RED per stabilire una connessione a un'applicazione Node-RED quando viene attivata una regola. Per ulteriori informazioni sull'utilizzo di Node-RED, vedi [Creazione di applicazioni con l'applicazione starter Internet delle cose](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html#iot500).

Esempio: [Utilizza Node-RED per inviare un messaggio di testo](action_examples.html#noderedex).

I seguenti parametri vengono utilizzati per configurare un'azione Node-RED:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, che viene utilizzato nel dashboard Avvisi.
Descrizione | Una breve descrizione dell'azione.
URL | L'URL del nodo di input HTTP Node-RED di destinazione.
Nome utente | Includi se richiesto dal servizio Node-RED.
Password | Includi se richiesto dal servizio Node-RED. **Importante:** la password viene inviata in testo in chiaro.
Corpo | Per impostazione predefinita, il campo del corpo è precompilato con tutte le variabili elencate nella [sostituzione di variabili](#variable_substitution). Seleziona **Utilizza corpo del messaggio personalizzato** per modificare il contenuto del campo del corpo.

## IFTTT {: #ifttt}
Utilizza l'azione IFTTT per attivare un ricetta IFTTT quando viene attivata una regola. Per ulteriori informazioni sull'attivazione di azioni Real-Time Insights come ricette IFTTT, vedi [Maker Channel](https://ifttt.com/maker) sul sito di IFTTT.

Esempio: [Utilizza IFTTT per pubblicare una scheda Trello](action_examples.html#iftttex).

I seguenti parametri vengono utilizzati per configurare un'azione IFTTT:

Parametro | Descrizione
---|---
Nome | Il nome dell'azione, che viene utilizzato nel dashboard Avvisi.
Descrizione | Una breve descrizione dell'azione.
Chiave | La chiave Maker Channel da utilizzare per attivare l'evento.
Evento | Il nome evento da te configurato come un trigger per l'evento Maker. Puoi creare più ricette con diversi trigger, ciascuno con un nome evento differente.
Valore 1-3 | Puoi passare qualsiasi contenuto in questi parametri, che vengono passati all'azione nella tua ricetta IFTTT. **Suggerimento:** puoi utilizzare
la [sostituzione di variabili](#variable_substitution) per includere dinamicamente dei dati aggiuntivi con l'intestazione.

## Sostituzione di variabili {: #variable_substitution}
Includi le seguenti sostituzioni di variabili per includere dinamicamente dei dati dispositivo. La variabile deve essere racchiusa tra doppie parentesi graffe.

Variabile | Descrizione
---|---
**URL, Intestazione e Corpo** |
`{{timestamp}}` | La data/ora dal messaggio
`{{tenantId}}` | L'ID del servizio Real-Time Insights
`{{deviceId}}` | L'ID del dispositivo
`{{ruleName}}` | Il nome della regola che include l'azione
**Solo corpo** |
`{{ruleDescription}}`| La descrizione della regola che include l'azione
`{{ruleCondition}}` | La condizione della regola che ha attivato l'azione
`{{message}}` | Il messaggio del dispositivo non elaborato che includeva il valore di punto dati che ha attivato la regola
