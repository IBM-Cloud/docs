---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Annotazioni sugli asset OpenWhisk

Le azioni, i trigger, le regole e i pacchetti OpenWhisk (denominati collettivamente come asset) possono essere decorati con `annotazioni`. Le annotazioni vengono collegate agli asset proprio come i parametri, con una `key` che definisce un nome e un `value` che definisce un valore. È opportuno impostarle dalla CLI (command line interface) tramite `--annotation` o l'abbreviazione `-a`.
{: shortdesc}

Motivazione: le annotazioni sono state aggiunte ad OpenWhisk per consentire la sperimentazione senza apportare modifiche allo schema di asset sottostante. Fino alla stesura di questo documento, non abbiamo deliberatamente definito quali `annotazioni` sono consentite. Tuttavia, poiché abbiamo iniziato a utilizzare maggiormente le annotazioni per impartire modifiche semantiche, è importante che finalmente vengano documentate.

Fino ad oggi, l'utilizzo più diffuso delle annotazioni è quello di documentare le azioni e i pacchetti. In molti dei pacchetti nel catalogo OpenWhisk potrai vedere delle annotazioni, come ad esempio una descrizione della funzionalità offerta dalle loro azioni, quali parametri sono richiesti in fase di bind del pacchetto e quali sono i parametri per il tempo di richiamata, se un parametro è un "segreto" (ad esempio, password) o meno. Le abbiamo inventate in base alle esigenze, ad esempio per consentire l'integrazione della IU.

Di seguito è riportata una serie di annotazioni di esempio per un'azione `echo` che restituisce i suoi argomenti di input non modificati (ad esempio, `function main(args) { return args }`). Questa azione può essere utile ad esempio per la registrazione dei parametri di input come parte di una sequenza o regola.

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

Le annotazioni utilizzate per descrivere i pacchetti sono:

- `description`: una descrizione concisa del pacchetto
- `parameters`: un array che descrive i parametri nell'ambito del pacchetto (descritti più avanti)

Allo stesso modo, per le azioni: 

- `description`: una descrizione concisa dell'azione
- `parameters`: un array che descrive le azioni richieste per eseguire l'azione
- `sampleInput`: un esempio che mostra lo schema di input con i valori tipici
- `sampleOutput`: un esempio che mostra lo schema di output, solitamente per `sampleInput`

Le annotazioni utilizzate per descrivere i parametri sono:

- `name`: il nome del parametro
- `description`: una descrizione concisa del parametro
- `doclink`: un link a un'ulteriore documentazione per il parametro (utile, ad esempio, per i token OAuth) 
- `required`: true per i parametri obbligatori e false per quelli facoltativi
- `bindTime`: true se è necessario specificare il parametro quando si esegue il bind del pacchetto
- `type`: il tipo di parametro, può essere `password` o `array` (ma può essere utilizzato in modo più ampio)

Le annotazioni *non* vengono controllate. Quindi, mentre è possibile utilizzare le annotazioni per dedurre ad esempio se una composizione di due azioni in una sequenza è legale, il sistema non lo fa ancora.

## Annotazioni specifiche delle azioni web
{: #openwhisk_annotations_webactions}

Di recente abbiamo esteso l'API principale con nuove funzioni. Per poter inserire i pacchetti e le azioni in queste funzioni, abbiamo introdotto le seguenti nuove annotazioni semanticamente significative. Per avere effetto, queste annotazioni devono essere impostate esplicitamente su `true`. Se si modifica il valore da `true` a `false`, l'asset collegato verrà escluso dalla nuova API. Le annotazioni non hanno significato al di fuori del sistema. Esse sono:

- `final`: si applica solo a un'azione. Rende immutabili tutti i parametri di azione già definiti. Un parametro di un'azione con l'annotazione non può essere sovrascritto dai parametri per il tempo di richiamata una volta che il parametro ha un valore definito tramite il suo pacchetto di inclusione o la definizione dell'azione.
- `web-export`: si applica solo a un'azione. Se presente, rende accessibile la sua azione corrispondente alle chiamate REST *senza* eseguire l'autenticazione. Queste sono chiamate [*azioni web*](openwhisk_webactions.html) in quanto consentono di utilizzare le azioni OpenWhisk, ad esempio, da un browser. È importante notare che al *proprietario* delle azioni web verranno addebitati i costi delle loro esecuzioni nel sistema (vale a dire, il *proprietario* dell'azione possiede anche il record delle attivazioni).
- `require-whisk-auth`: si applica a un'azione. Se un'azione contiene l'annotazione `web-export` e questa annotazione è `true`, la rotta è accessibile solo a un soggetto autenticato. È importante notare che al *proprietario* delle azioni web verranno addebitati i costi delle loro esecuzioni nel sistema (vale a dire, il *proprietario* dell'azione possiede anche il record delle attivazioni).
- `raw-http`: si applica solo a un'azione in presenza di un'annotazione `web-export`. Se presente, i parametri di query e corpo della richiesta HTTP vengono passati all'azione come proprietà riservate.

