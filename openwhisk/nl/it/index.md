---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Introduzione a {{site.data.keyword.openwhisk_short}}


{{site.data.keyword.openwhisk}} è un servizio di calcolo distribuito guidato dagli eventi, indicato anche come Serverless computing o FaaS (Function as a Service); {{site.data.keyword.openwhisk_short}} esegue la logica dell'applicazione in risposta a eventi o chiamate dirette provenienti da applicazioni Web o mobili su HTTP. Gli eventi possono essere forniti da servizi Bluemix come Cloudant e da fonti esterne. Gli sviluppatori possono concentrarsi sulla scrittura della logica dell'applicazione e sulla creazione di azioni eseguite su richiesta.
I vantaggi di questo nuovo paradigma sono molteplici: non dovrai più eseguire esplicitamente il provisioning dei server e occuparti del ridimensionamento automatico e non dovrai più preoccuparti dell'elevata disponibilità, degli aggiornamenti, della manutenzione e del pagamento per le ore del tempo del processore quando il tuo server è in esecuzione ma non completa le richieste.
Il tuo codice viene eseguito ogni volta che si verifica una chiamata HTTP, una modifica dello stato del database o un altro tipo di evento che attiva l'esecuzione del codice.
Ti viene addebitata una fattura in base a ogni millisecondo del tempo di esecuzione (arrotondato a 100 ms) e non all'ora di utilizzo della VM, indipendentemente dal fatto che la VM fosse operativa o meno.
{: shortdesc}

Questo modello di programmazione è una soluzione perfetta per i microservizi, le applicazioni mobili, IoT e tante altre applicazioni – ti consente di ottenere il ridimensionamento automatico e il bilanciamento del carico predefiniti senza dover configurare manualmente cluster, servizi di bilanciamento del carico, plug-in http ecc. Se ti capita di eseguire applicazioni su {{site.data.keyword.openwhisk}}, hai anche il vantaggio di non doverti preoccupare dell'amministrazione, il che significa che l'hardware, la rete e il software sono tutti gestiti da IBM. Tutto quello che devi fare è fornire il codice che vuoi eseguire e darlo a {{site.data.keyword.openwhisk}}. Il resto è “magia”. Un'accurata introduzione al modello di programmazione serverless è disponibile sul [blog di Martin Fowler](https://martinfowler.com/articles/serverless.html).

Puoi anche ottenere il [codice sorgente Apache OpenWhisk](https://github.com/openwhisk/openwhisk) ed eseguire il sistema autonomamente.

Per ulteriori dettagli sul funzionamento di {{site.data.keyword.openwhisk_short}}, vedi [Informazioni su {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

Per sviluppare le tue applicazioni {{site.data.keyword.openwhisk_short}} puoi utilizzare il browser o la CLI.
Entrambi hanno funzionalità simili per sviluppare le applicazioni, tuttavia la CLI fornisce maggiore controllo sulle attività di distribuzione e operative.

## Sviluppa nel tuo browser
{: #openwhisk_start_editor}

Prova {{site.data.keyword.openwhisk_short}} nel tuo [Browser](https://console.{DomainName}/openwhisk/editor){: new_window} per creare azioni, automatizzare le azioni mediante i trigger e scoprire i pacchetti pubblici. 
Visita la pagina [Ulteriori informazioni](https://console.{DomainName}/openwhisk/learn){: new_window} per un rapido tour dell'interfaccia utente OpenWhisk.

## Sviluppa con la CLI
{: #openwhisk_start_configure_cli}

Puoi utilizzare l'interfaccia di riga comando (CLI) {{site.data.keyword.openwhisk_short}} per configurare il tuo spazio dei nomi e la tua chiave di autorizzazione.
Passa a [Configura CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} e segui le istruzioni per installarla.

## Panoramica
{: #openwhisk_start_overview}
- [Come funziona OpenWhisk](./openwhisk_about.html)
- [Casi d'uso comuni per le applicazioni Serverless](./openwhisk_use_cases.html)
- [Configurazione e utilizzo della CLI OpenWhisk](./openwhisk_cli.html)
- [Utilizzo di OpenWhisk da un'applicazione iOS](./openwhisk_mobile_sdk.html)

## Modello di programmazione 
{: #openwhisk_start_programming}
- [Dettagli del sistema](./openwhisk_reference.html)
- [Catalogo dei servizi forniti da OpenWhisk](./openwhisk_catalog.html)
- [Azioni](./openwhisk_actions.html)
- [Trigger e regole](./openwhisk_triggers_rules.html)
- [Feed](./openwhisk_feeds.html)
- [Pacchetti](./openwhisk_packages.html)
- [Annotazioni](./openwhisk_annotations.html)
- [Azioni web](./openwhisk_webactions.html)
- [Gateway API](./openwhisk_apigateway.html)
- [Nomi entità](./openwhisk_reference.html#openwhisk_entities)
- [Semantica delle azioni](./openwhisk_reference.html#openwhisk_semantics)
- [Limiti](./openwhisk_reference.html#openwhisk_syslimits)

## {{site.data.keyword.openwhisk_short}}Esempio Hello World
{: #openwhisk_start_hello_world}
Per iniziare a utilizzare {{site.data.keyword.openwhisk_short}}, prova il seguente esempio di codice JavaScript.

```javascript
/**
 * Hello world as an OpenWhisk action.
 */
function main(params) {
    var name = params.name || 'World';
    return {payload:  'Hello, ' + name + '!'};
}
```
{: codeblock}

Per utilizzare questo esempio, completa la seguente procedura:

1. Salva il codice in un file. Ad esempio, *hello.js*.

2. Dalla riga di comando CLI {{site.data.keyword.openwhisk_short}}, crea l'azione inserendo il seguente comando:

    ```
    wsk action create hello hello.js
    ```
    {: pre}

3. Quindi, richiama l'azione immettendo i seguenti comandi.

    ```
    wsk action invoke hello --blocking --result
    ```
    {: pre}  

    Questo comando ha il seguente output:

    ```json
    {
        "payload": "Hello, World!"
    }
    ```
    
    ```
    wsk action invoke hello --blocking --result --param name Fred
    ```
    {: pre}  

    Questo comando ha il seguente output:

    ```json
    {
        "payload": "Hello, Fred!"
    }
    ```

Puoi anche utilizzare le funzionalità guidate dagli eventi in {{site.data.keyword.openwhisk_short}} per richiamare questa azione in risposta agli eventi. Segui l'[esempio di servizio di allerta](./openwhisk_packages.html#openwhisk_packages_trigger) per configurare un'origine eventi che richiami l'azione `hello` ogni volta che viene generato un evento periodico.


## Guida di riferimento API
{: #openwhisk_start_api notoc}
* [Documentazione API REST](./openwhisk_reference.html#openwhisk_ref_restapi)
* [API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## Link correlati
{: #general notoc}
* [Scopri: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} su IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
* [Sito web dei progetti Apache {{site.data.keyword.openwhisk_short}}](http://openwhisk.org){:new_window}
