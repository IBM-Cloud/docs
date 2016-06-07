---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilizzo e creazione di pacchetti {{site.data.keyword.openwhisk_short}}
{: #openwhisk_packages}
*Ultimo aggiornamento: 28 marzo 2016*

In {{site.data.keyword.openwhisk}}, puoi utilizzare i pacchetti per raggruppare una serie di azioni correlate e condividerle con altri.

Un pacchetto può includere *azioni* e *feed*.
- Un'azione è una parte di codice eseguita su {{site.data.keyword.openwhisk_short}}. Ad esempio, il pacchetto Cloudant include azioni per la lettura e scrittura di record in un database Cloudant.
- Il feed serve a configurare un'origine eventi esterna per l'attivazione di eventi trigger. Ad esempio,il pacchetto Alarm include un feed che può attivare un trigger alla frequenza indicata.

Ogni entità {{site.data.keyword.openwhisk_short}}, inclusi i pacchetti, appartiene a uno *spazio dei nomi* e il nome completo di un'entità è `/nomeSpazioNomi[/nomePacchetto]/nomeEntità`. Per ulteriori informazioni, vedi le [linee guida di denominazione](./openwhisk_reference.html#openwhisk_entities).

Le seguenti sezioni descrivono come navigare tra i pacchetti e utilizzare i trigger e i feed al loro interno. Inoltre, per coloro che sono interessati a portare i propri pacchetti nel catalogo, leggere le sezioni sulla creazione e la condivisione dei pacchetti.

## Esplorazione dei pacchetti
{: #openwhisk_packagedisplay}

In {{site.data.keyword.openwhisk_short}} sono registrati vari pacchetti. Puoi ottenere un elenco dei pacchetti di uno spazio dei nomi, elencare le entità di un pacchetto e ottenere una descrizione delle singole entità di un pacchetto.

1. Ottieni un elenco dei pacchetti dello spazio dei nomi `/whisk.system`.

```
  wsk package list /whisk.system
```
  {: pre}
```
  packages
  /whisk.system/alarms                                              shared
  /whisk.system/cloudant                                            shared
  /whisk.system/github                                              shared
  /whisk.system/samples                                             shared
  /whisk.system/slack                                               shared
  /whisk.system/util                                                shared
  /whisk.system/watson                                              shared
  /whisk.system/weather                                             shared
```
  {: screen}

2. Ottieni un elenco delle entità del pacchetto `/whisk.system/cloudant`.

```
  wsk package get --summary /whisk.system/cloudant
```
  {: pre}
```
  package /whisk.system/cloudant: Cloudant database service
     (params: {{site.data.keyword.Bluemix_notm}}ServiceName host username password dbname includeDoc overwrite)
   action /whisk.system/cloudant/read: Read document from database
   action /whisk.system/cloudant/write: Write document to database
   feed   /whisk.system/cloudant/changes: Database change feed
```
  {: screen}

  Questo output mostra che il pacchetto Cloudant fornisce due azioni, `read` e `write`, e un solo feed trigger denominato `changes`. Il feed `changes` causa l'attivazione dei trigger all'aggiunta di documenti al database Cloudant specificato.

  Il pacchetto Cloudant definisce, inoltre, i parametri `username`, `password`, `host` e `port`. Affinché le azioni e i feed siano significativi, è necessario specificare questi parametri. Ad esempio, i parametri permettono alle azioni di operare su un account Cloudant specifico.

3. Ottieni una descrizione dell'azione `/whisk.system/cloudant/read`.

```
  wsk action get --summary /whisk.system/cloudant/read
```
  {: pre}
```
  action /whisk.system/cloudant/read: Read document from database
     (params: dbname includeDoc id)
```
  {: screen}

  Questo output mostra che l'azione Cloudant `read` richiede tre parametri, compreso il database e l'ID documento da richiamare.


## Chiamata di azioni in un pacchetto
{: #openwhisk_package_invoke}

Puoi chiamare le azioni di un pacchetto con la stessa modalità seguita per le altre azioni. La seguente procedura mostra come chiamare l'azione `greeting` nel pacchetto `/whisk.system/samples` con parametri differenti.

1. Ottieni una descrizione dell'azione `/whisk.system/samples/greeting`.

```
  wsk action get --summary /whisk.system/samples/greeting
```
  {: pre}
```
  action /whisk.system/samples/greeting: Print a friendly greeting
     (params: name place)
```
  {: screen}

  Nota che l'azione `greeting` utilizza due parametri: `name` e `place`.

2. Chiama l'azione senza alcun parametro.

```
  wsk action invoke --blocking --result /whisk.system/samples/greeting
```
  {: pre}
```
  {
      "payload": "Hello, stranger from somewhere!"
  }
```
  {: screen}

  L'output è un messaggio generico perché non è stato specificato alcun parametro.

3. Chiama l'azione con parametri.

```
  wsk action invoke --blocking --result /whisk.system/samples/greeting --param name Mork --param place Ork
```
  {: pre}
```
  {
      "payload": "Hello, Mork from Ork!"
  }
```
  {: screen}

  Nota che l'output utilizza i parametri `name` e `place` che sono stati trasmessi all'azione.


## Creazione e utilizzo dei bind dei pacchetti
{: #openwhisk_package_bind}

Sebbene tu possa utilizzare direttamente le entità di un pacchetto, potresti trovarti ogni volta a trasmettere gli stessi parametri all'azione. Puoi evitare questo problema eseguendo il bind di un pacchetto e specificando parametri predefiniti. Questi parametri vengono ereditati dalle azioni del pacchetto.

Ad esempio, nel pacchetto `/whisk.system/cloudant` puoi impostare valori `username`, `password` e `dbname` predefiniti in un bind del pacchetto, che verranno trasmessi automaticamente a qualsiasi azione del pacchetto.

Nel semplice esempio di seguito riportato, puoi eseguire il bind del pacchetto `/whisk.system/samples`.

1. Esegui il bind del pacchetto `/whisk.system/samples` e imposta un valore predefinito per il parametro `place`.

```
  wsk package bind /whisk.system/samples valhallaSamples --param place Valhalla
  ```
  {: pre}
```
  ok: created binding valhallaSamples
```
  {: screen}

2. Ottieni una descrizione del bind del pacchetto.

```
  wsk package get --summary valhallaSamples
```
  {: pre}
```
  package /myNamespace/valhallaSamples
   action /myNamespace/valhallaSamples/greeting: Print a friendly greeting
   action /myNamespace/valhallaSamples/wordCount: Count words in a string
   action /myNamespace/valhallaSamples/helloWorld: Print to the console
   action /myNamespace/valhallaSamples/echo: Returns the input arguments, unchanged
```
  {: screen}

  Nota che tutte le azioni del pacchetto `/whisk.system/samples` sono disponibili nel bind del pacchetto `valhallaSamples`.

3. Chiama un'azione nel bind del pacchetto.

```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin
```
  {: pre}
```
  {
      "payload": "Hello, Odin from Valhalla!"
  }
```
  {: screen}

  Osserva dal risultato che l'azione eredita il parametro `place` che hai impostato
 quando hai creato il bind del pacchetto `valhallaSamples`.

4. Chiama un'azione e sovrascrivi il valore predefinito del parametro.

```
  wsk action invoke --blocking --result valhallaSamples/greeting --param name Odin --param place Asgard
```
  {: pre}
```
  {
      "payload": "Hello, Odin from Asgard!"
  }
```
  {: screen}

  Nota che il valore del parametro `place` specificato con la chiamata dell'azione sovrascrive il valore predefinito impostato nel bind del pacchetto `valhallaSamples`.


## Creazione e utilizzo dei feed di trigger
{: #openwhisk_package_trigger}

I feed possono essere opportunamente utilizzati per configurare un'origine eventi esterna per l'attivazione di questi eventi in un trigger {{site.data.keyword.openwhisk_short}}. Questo esempio mostra come utilizzare un feed del pacchetto Alarms per attivare un trigger e utilizzare una regola per chiamare un'azione ogni secondo.

1. Ottieni una descrizione del feed del pacchetto `/whisk.system/alarms`.

```
  wsk package get --summary /whisk.system/alarms
```
  {: pre}
```
  package /whisk.system/alarms
   feed   /whisk.system/alarms/alarm
```
  {: screen}

```
  wsk action get --summary /whisk.system/alarms/alarm
```
  {: pre}
```
  action /whisk.system/alarms/alarm: Fire trigger when alarm occurs
     (params: cron trigger_payload)
```
  {: screen}

  Il feed `/whisk.system/alarms/alarm` utilizza due parametri:
  - `cron`: una specifica crontab che indica quando attivare il trigger.
  - `trigger_payload`: il valore del parametro payload da impostare in ogni evento di trigger.

2. Crea un trigger che si attiva ogni 8 secondi.

```
  wsk trigger create everyEightSeconds --feed /whisk.system/alarms/alarm -p cron '*/8 * * * * *' -p trigger_payload '{"name":"Mork", "place":"Ork"}'
```
  {: pre}
```
  ok: created trigger feed everyEightSeconds
```
  {: screen}

3. Crea un file 'hello.js' con il seguente codice azione.

```
  function main(params) {
      return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
```
  {: codeblock}

4. Accertati che l'azione esista.

```
  wsk action update hello hello.js
```
  {: pre}

5. Crea una regola che chiama l'azione `hello` ogni volta che viene attivato il trigger `everyEightSeconds`.

```
  wsk rule create --enable myRule everyEightSeconds hello
```
  {: pre}
```
  ok: created rule myRule
  ok: rule myRule is activating
```
  {: screen}

6. Controlla che l'azione venga richiamata tramite il polling dei log di attivazione.

```
  wsk activation poll
```
  {: pre}

  Ogni otto secondi verranno effettuate attivazioni per il trigger, la regola e l'azione. L'azione riceve i parametri `{"name":"Mork", "place":"Ork"}` su ogni chiamata.


## Creazione di un pacchetto
{: #openwhisk_packages_create}

Un pacchetto serve a organizzare un insieme di feed e azioni correlati.
Inoltre, consente la condivisione dei parametri tra tutte le entità del pacchetto.

Per creare un pacchetto personalizzato che contenga un'azione semplice, prova il seguente esempio:

1. Crea un pacchetto denominato "custom".

```
  wsk package create custom
```
  {: pre}
```
  ok: created package custom
```
  {: screen}

2. Ottieni un riepilogo del pacchetto.

```
  wsk package get --summary custom
```
  {: pre}
```
  package /myNamespace/custom
```
  {: screen}

  Nota che il pacchetto è vuoto.

3. Crea un file denominato `identity.js` che contenga il seguente codice azione. Questa azione restituisce tutti i parametri di input.

```
  function main(args) { return args; }
```
  {: codeblock}

4. Crea un'azione `identity` nel package `custom`.

```
  wsk action create custom/identity identity.js
```
  {: pre}
```
  ok: created action custom/identity
```
  {: screen}

  Per creare un'azione in un pacchetto devi prefissare il nome dell'azione con un nome pacchetto. La nidificazione dei pacchetti non è consentita. Un pacchetto può contenere solo azioni e non può contenere un altro pacchetto.

5. Ottieni nuovamente un riepilogo del pacchetto.

```
  wsk package get --summary custom
```
  {: pre}
```
  package /myNamespace/custom
   action /myNamespace/custom/identity
```
  {: screen}

  Ora l'azione `custom/identity` viene mostrata nel tuo spazio dei nomi.

6. Chiama l'azione del pacchetto.

```
  wsk action invoke --blocking --result custom/identity
```
  {: pre}
```
  {}
```
  {: screen}


Puoi impostare parametri predefiniti per tutte le entità di un pacchetto. Per far ciò, imposta i parametri a livello di pacchetto ereditati da tutte le azioni del pacchetto. Per vedere come funziona, prova il seguente esempio:

1. Aggiorna il pacchetto `custom` con due parametri: `city` e `country`.

```
  wsk package update custom --param city Austin --param country USA
```
  {: pre}
```
  ok: updated package custom
```
  {: screen}

2. Visualizza i parametri del pacchetto e dell'azione e osserva in che modo l'azione `identity` del pacchetto eredita parametri dal pacchetto.

```
  wsk package get custom parameters
```
  {: pre}
```
  ok: got package custom, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
```
  {: screen}

```
  wsk action get custom/identity parameters
```
  {: pre}
```
  ok: got action custom/identity, projecting parameters
  [
      {
          "key": "city",
          "value": "Austin"
      },
      {
          "key": "country",
          "value": "USA"
      }
  ]
```
  {: screen}

3. Chiama l'azione identity senza alcun parametro, al fine di verificare che l'azione erediti effettivamente i parametri.

```
  wsk action invoke --blocking --result custom/identity
```
  {: pre}
```
  {
      "city": "Austin",
      "country": "USA"
  }
```
  {: screen}

4. Chiama l'azione identity con alcuni parametri. I parametri della chiamata vengono uniti ai parametri del pacchetto e li sostituiscono.

```
  wsk action invoke --blocking --result custom/identity --param city Dallas --param state Texas
```
  {: pre}
```
  {
      "city": "Dallas",
      "country": "USA",
      "state": "Texas"
  }
```
  {: screen}


## Condivisione di un pacchetto
{: #openwhisk_packages_share}

Una volta eseguiti i test e il debug delle azioni e dei feed compresi in un pacchetto, quest'ultimo può essere condiviso con tutti gli utenti {{site.data.keyword.openwhisk_short}}. La condivisione del pacchetto consente agli utenti di eseguire il bind del pacchetto, chiamare azioni del pacchetto e creare azioni sequenza e regole {{site.data.keyword.openwhisk_short}}.

1. Condividi i pacchetti con tutti gli utenti:

```
  wsk package update custom --shared
```
  {: pre}
```
  ok: updated package custom
```
  {: screen}

2. Visualizza la proprietà `publish` del pacchetto per verificare che ora sia true.

```
  wsk package get custom publish
```
  {: pre}
```
  ok: got package custom, projecting publish
  true
```
  {: screen}


Altri utenti possono ora utilizzare il tuo pacchetto `custom`, includendo il bind del pacchetto o richiamando direttamente un'azione in esso contenuta. Gli altri utenti devono conoscere i nomi completi del pacchetto per poterne eseguire il bind o per chiamare azioni in esso contenute. Le azioni e i feed di un pacchetto condiviso sono *pubblici*. Se il pacchetto è privato, lo sono anche tutti i suoi contenuti.

1. Ottieni una descrizione del pacchetto per visualizzare i nomi completi del pacchetto e dell'azione.

```
  wsk package get --summary custom
```
  {: pre}
```
  package /myNamespace/custom
   action /myNamespace/custom/identity
```
  {: screen}

  Nell'esempio precedente, hai utilizzato lo spazio dei nomi `myNamespace`, che appare nel nome completo.

