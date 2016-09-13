---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Esempi di azione

I tipi di azione Invia email, IFTTT, Node-RED e webhooks aprono le porte a un intero universo di opzioni per l'esecuzione di attività, limitato solo dalla tua immaginazione e dai connettori utilizzati dagli altri strumenti, Citiamo, ad esempio, le azioni per pubblicare messaggi di stato del dispositivo su Slack, inviare messaggi di testo al personale di servizio, creare delle richieste di servizio per i dispositivi e molto altro ancora.
{: shortdesc}

Gli esempi di seguito rappresentano tutti un'azione che invia una segnalazione a un tecnico addetto alla manutenzione quando il punto dati della temperatura di un dispositivo supera i 100 gradi utilizzando la seguente condizione della regola:
`temp >= 100`

Puoi attivare uno o più dei seguenti tipi di azione quando si verifica la condizione della regola:  
 - [Invia email](#emailex "Invia email")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## Utilizza invio email {: #emailex}
In questo esempio, l'azione è configurata per utilizzare la funzione Invia email di Real-Time Insights per inviare una email al responsabile addetto all'assistenza principale e per inviare anche una email di backup al suo responsabile.

Per creare un'azione email:
1. In Real-Time Insights, vai a **Analisi > Azioni**.
2. Fai clic su **Aggiungi nuova azione**.
3. Seleziona il tipo **Invia email**.
4. Immetti il nome azione `Invia email di richiesta di servizio`.
5. Immetti la descrizione `Invia una email al tecnico addetto all'assistenza e al suo responsabile`.
6. Nel campo A, immetti `service.engineer@company.com`.
7. Nel campo CC, immetti: `service.manager@company.com`.
8. Nella riga dell'oggetto, immetti: `Assistenza richiesta.`
9. Seleziona per aggiungere come prefisso "{{site.data.keyword.iotrtinsights_short}} alert" per chiarire da dove proviene la email.
10. Per includere i dati dispositivo nell'email, deseleziona la casella di spunta **Non includere i dati dispositivo nel messaggio email**.
11. Fai clic su **OK** per salvare l'azione.  




## Utilizza un webhook per pubblicare su Slack {: #webhookex}

In questo esempio, l'azione è configurata per utilizzare un webhook per pubblicare un messaggio nel nostro canale Slack #service-requests.

Per creare l'azione di pubblicazione in Slack:
1. In Slack, configura l'integrazione Incoming Webhooks per il canale #service-requests. Annota l'URL dei webhook. Per ulteriori informazioni,
consulta la [documentazione di Slack](https://api.slack.com/incoming-webhooks).
2. In Real-Time Insights, vai a **Analisi > Azioni** e crea una nuova azione che ha i seguenti parametri:
 - Tipo - **Webhook**
 - Nome - `Pubblicazione di richiesta di servizio su Slack`
 - URL - `Il tuo URL dei webhook Slack`
 - Metodo - **POST**
 - Tipo di contenuto - application/json
 - Seleziona **Utilizza corpo del messaggio personalizzato**
 - Corpo
 ```{"text":"*Un dispositivo richiede la tua attenzione*\n Data/ora: {{timestamp}}\n Istanza {{site.data.keyword.iotrtinsights_short}}: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regola: {{ruleName}}\n Descrizione: {{ruleDescription}}\n Condizione: {{ruleCondition}}\n Messaggio dispositivo non elaborato: \n{{message}}"}```
 {: codeblock}  
 **Importante:** il webhook Slack deve contenere come minimo il campo "text". Per informazioni, vedi [Incoming Webhooks](https://api.slack.com/incoming-webhooks "Documentazione di Slack") nella documentazione di Slack.
11. Fai clic su **OK** per salvare l'azione.

## Utilizza Node-RED per inviare un messaggio di testo {: #noderedex}

In questo esempio, l'azione è configurata per utilizzare Node-RED con un nodo Twilio per inviare un messaggio di testo al tecnico addetto all'assistenza.

Per creare l'azione di invio del messaggio di testo:
1. In Twilio, individua o crea un nuovo servizio di messaggistica da utilizzare per inviare messaggi di testo dal tuo account Twilio. Per informazioni, consulta
la [documentazione di Twilio](https://www.twilio.com/help).
1. In Bluemix, configura il, e accedi al, tuo account Node-RED con l'URL Node-RED `http://mynodered.mybluemix.net/red/`. Per ulteriori
informazioni, vedi l'argomento [Creazione di applicazioni con starter Node-RED](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html) nella documentazione di Bluemix.
2. In Node-RED, crea un semplice flusso a due nodi come [RTI-alert]->[SMS].
In questo caso, il primo nodo è un nodo http e il secondo è un nodo twilio.
 1. Aggiungi il nodo di input "http" e configuralo con i seguenti attributi:
  <ul>
  <li>Metodo - POST</li>
  <li>URL - `avviso-RTI`</li>
  <li>Nome - Azione RTI</li>
  </ul>
  2. Aggiungi un nodo di output "http response" e connettilo ai nodi di input "http" mediante trascinamento tra la porta di output dell'uno e la porta di input dell'altro.
  3. Aggiungi un nodo di output "twilio" e configuralo con i seguenti attributi:
  <ul>
  <li>Servizio - **Servizio esterno**</li>
  <li>Twilio - Aggiungi nuova twilio-api</li>
  <li>SMS a - `Numero di telefono per il tecnico addetto all'assistenza`</li>
  <li>Nome - **SMS**</li>
  </ul>
  4. Collega i nodi
  Connetti i nodi http e twilio mediante trascinamento tra la porta di output dell'uno e la porta di input dell'altro.
  5. Fai clic sul pulsante **Distribuisci** per distribuire il flusso al server
3. In {{site.data.keyword.iotrtinsights_short}}, vai a **Analisi > Azioni** e crea un'azione che ha i seguenti parametri:
 - Tipo - **Node-RED**
 - Nome - `Invia testo utilizzando Node-RED e Twilio`
 - Descrizione - `Invia un avviso di messaggio di testo al tecnico addetto all'assistenza.`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```{"text":"*Un dispositivo richiede la tua attenzione*\n Data/ora: {{timestamp}}\n Istanza {{site.data.keyword.iotrtinsights_short}}: {{tenantId}}\n Dispositivo: {{deviceId}}\n Regola: {{ruleName}}\n Descrizione: {{ruleDescription}}\n Condizione: {{ruleCondition}}\n Messaggio dispositivo non elaborato: \n{{message}}"}```
 {: codeblock}
4. Fai clic su **OK** per salvare l'azione.

## Utilizza IFTTT per pubblicare una scheda Trello {: #iftttex}

In questo esempio, configuriamo l'azione per utilizzare IFTTT per pubblicare una scheda in un elenco di richieste di servizio su Trello.

Per creare un'azione di pubblicazione di una scheda su Trello:
1.	In IFTTT, stabilisci una connessione al canale Trello.
2.	In IFTTT, stabilisci una connessione al canale Maker. Annota la tua chiave IFTTT. Ti servirà per stabilire una connessione a IFTTT da Real-Time Insights.
5.	In IFTTT, crea una ricetta:
 1. Fai clic su **THIS**.
 2. Seleziona il canale **Maker**.  
 2. Fai clic su **Receive a web request**.
 3. Immetti il nome evento `post-Trello-card`.
 4. Fai clic su **THAT**.
 5. Seleziona il canale **Trello**.
 6. Seleziona la board Trello in cui creare la scheda.
 7. Immetti un nome elenco in cui aggiungere le schede.
 8. Modifica il titolo e la descrizione.
 9. Assegna i membri @service.engineer e @service.manager.
 8. Fai clic su **Create Action**.   
3. In {{site.data.keyword.iotrtinsights_short}}, vai a **Analisi > Azioni** e crea un'azione che ha i seguenti parametri:
<ul>
<li>Tipo - **IFTTT**</li>
<li>Nome - `Pubblica scheda di richiesta di servizio`</li>
<li>Descrizione - `Utilizza IFTTT per pubblicare una scheda nell'elenco delle richieste di servizio in Trello.`</li>
<li>Chiave - la tua chiave IFTTT</li>
<li>Evento - `post-Trello-card`</li>
<li>Facoltativamente, aggiungi dei valori per Value da 1 a 3. **Suggerimento:** puoi utilizzare la [sostituzione variabile](actions.html#variable_substitution) per includere dinamicamente i dati dispositivo.</li>
</ul>
4. Fai clic su **OK** per salvare l'azione.
