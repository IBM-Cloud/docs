---

 

copyright:

  years: 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Creazione di trigger e regole
{: #openwhisk_triggers}
*Ultimo aggiornamento: 22 febbraio 2016*

I trigger e le regole {{site.data.keyword.openwhisk}} forniscono alla piattaforma funzionalità guidate dagli eventi. Gli eventi provenienti da origini eventi interne ed esterne vengono incanalati attraverso un trigger e le regole consentono alle tue azioni di reagire a tali eventi.
{: shortdesc}

## Trigger

I trigger sono un canale indicato per una classe di eventi. Di seguito vengono riportati esempi di trigger:
- Un trigger di eventi di aggiornamento dell'ubicazione.
- Un trigger di caricamenti di documenti su un sito Web.
- Un trigger di e-mail in entrata.

I trigger possono essere *attivati* attraverso un dizionario di coppie chiave/valore. Tale dizionario viene talvolta denominato *evento*. Così come con le azioni, ogni attivazione di un trigger comporta un ID di attivazione.

I trigger possono essere attivati esplicitamente da un utente o attivati per conto di un utente da un'origine eventi esterna.
Un *feed* rappresenta un modo utile per configurare un'origine eventi esterna
per l'attivazione di eventi trigger utilizzabili da {{site.data.keyword.openwhisk_short}}. Sono esempi di feed:
- Un feed di modifica dati Cloudant che attiva un evento trigger ad ogni aggiunta o modifica di documenti in un database.
- Un feed Git che attiva un evento trigger per ogni commit con un repository Git.

## Regole

Una regola associa un trigger a un'azione, per cui ogni attivazione del trigger comporta la chiamata dell'azione corrispondente in cui l'evento trigger viene utilizzato come input.

Con l'insieme appropriato di regole, è possibile che un singolo evento trigger
richiami più azioni o che un'azione venga richiamata in risposta a eventi
appartenenti a più trigger.

Ad esempio, considera un sistema con le seguenti azioni:
- Azione `classifyImage` che rileva gli oggetti contenuti in un'immagine e li classifica.
- Azione `thumbnailImage` che crea una versione in miniatura di un'immagine.

Supponi, inoltre, che due origini eventi stiano attivando i seguenti trigger:
- Il trigger `newTweet`, che viene attivato alla pubblicazione di un nuovo tweet.
- Il trigger `imageUpload`, che viene attivato al caricamento di un'immagine in un sito Web.

Puoi impostare le regole in modo che un unico evento trigger richiami più azioni e far sì che più trigger richiamino la stessa azione:
- Regola `newTweet -> classifyImage`.
- Regola `imageUpload -> classifyImage`.
- Regola `imageUpload -> thumbnailImage`.

Queste tre regole stabiliscono il seguente funzionamento: vengono classificate le immagini di entrambi i tweet e le immagini caricate, vengono classificate le immagini caricate e viene generata una versione in miniatura. 

## Creazione e attivazione di trigger
{: #openwhisk_triggers}

I trigger possono essere attivati al verificarsi di determinati eventi o manualmente.

Ad esempio, crea un trigger per l'invio di aggiornamenti sull'ubicazione dell'utente e attivalo manualmente.

1. Immetti il seguente comando per creare il trigger:
 
```
  wsk trigger create locationUpdate
```
  {: pre}
 
```
  ok: created trigger locationUpdate
```
  {: screen}

2. Verifica di aver creato il trigger, elencando l'insieme dei trigger.

```
  wsk trigger list
```
  {: pre}
 
```
  triggers
  /someNamespace/locationUpdate                            private
```
  {: screen}

  Finora hai creato un determinato "canale" per cui possono essere attivati gli eventi.

3. Successivamente, attiverai un evento trigger specificandone il nome e i parametri:

```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
```
  {: pre}

```
  ok: triggered locationUpdate with id fa495d1223a2408b999c3e0ca73b2677
```
  {: screen}

   Qualsiasi evento attivato per il trigger statusUpdate non ha attualmente alcun effetto. Per essere utile, il trigger necessita di una regola che lo associ a un'azione.


## Utilizzo delle regole per l'associazione di trigger e azioni
{: #openwhisk_rules}

Le regole vengono utilizzate per associare un trigger a un'azione. Ogni volta che un evento trigger viene attivato, l'azione viene richiamata con i parametri dell'evento.

Ad esempio, crea una regola che richiama l'azione "hello" ogni volta che viene pubblicato un aggiornamento sull'ubicazione. 

1. Crea un file "hello.js" con il codice azione che useremo:
  ```
  function main(params) {
     return {payload:  'Hello, ' + params.name + ' from ' + params.place};
  }
  ```
  {: codeblock}

2. Accertati che il trigger e l'azione esistano.
  ```
  wsk trigger update locationUpdate
  ```
  {: pre}
  
```
  wsk action update hello hello.js
```
  {: pre}

3. Crea e abilita la regola. I tre parametri sono il nome della regola, il trigger e l'azione.
  ```
  wsk rule create --enable myRule locationUpdate hello
  ```
  {: pre}

4. Attiva il trigger locationUpdate. Ogni volta attivi un evento, l'azione "hello" viene richiamata con i parametri dell'evento.
  ```
  wsk trigger fire locationUpdate --param name "Donald" --param place "Washington, D.C."
  ```
  {: pre}
  
```
  ok: triggered locationUpdate with id d5583d8e2d754b518a9fe6914e6ffb1e
```
  {: screen}

5. Verifica che l'azione sia stata richiamata, controllando l'attivazione più recente.
  ```
  wsk activation list --limit 1 hello
  ```
  {: pre}
  
```
  activations
  9c98a083b924426d8b26b5f41c5ebc0d             hello
```
  {: screen}
  
```
  wsk activation result 9c98a083b924426d8b26b5f41c5ebc0d
```
  {: pre}
```
  {
     "payload": "Hello, Donald from Washington, D.C."
  }
```
  {: screen}

  Puoi vedere che l'azione "hello" ha ricevuto il payload dell'evento e ha restituito la stringa prevista.

  Puoi creare più regole che associano lo stesso trigger ad azioni differenti.
