---

copyright:
  years: 2017
lastupdated: "2017-04-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
{:note:.deprecated}

# Risoluzione dei problemi
{: #ts}

Alcuni problemi noti con la {{site.data.keyword.dev_cli_notm}} sono documentati insieme alle rispettive soluzioni alternative.
{:shortdesc}

<!-- Add a headings and paragraphs about troubleshooting for your service, or a list of known issues and workarounds. -->

## Problemi noti
{: #knownissues}

Le seguenti sezioni descrivono problemi noti e risoluzioni possibili.


### Nome host già preso durante la creazione di un progetto con un modello non mobile
{: #hostname}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare un progetto dai modelli applicazione web, BFF, o microservizio:

```
Il nome host <myHostname> è preso.
```
{: codeblock}


#### Causa
{: #hostname-cause}
   
Questo errore è dovuto ad un token di accesso scaduto.


#### Soluzione
{: #hostname-resolution}

Riaccedi.

```
bx login
```
{: codeblock}


### Errori generali con la {{site.data.keyword.dev_cli_short}}
{: #general}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} con i comandi create, delete, list o code:

```
Errore nel <command> progetto.
```
{: codeblock}


#### Causa
{: #general-cause}
   
Questo errore è dovuto ad un token di accesso scaduto.


#### Soluzione
{: #general-resolution}

Riaccedi.

```
bx login
```
{: codeblock}


### Errore con il broker di servizi durante l'aggiunta della funzionalità {{site.data.keyword.objectstorageshort}}
{: #os}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare due progetti con la funzionalità {{site.data.keyword.objectstorageshort}}:

```
NON RIUSCITO
Errore broker di servizi: {"description"=>"Non puoi creare questa istanza Object Storage. Ogni organizzazione che utilizza il servizio Object Storage è limitata a un'istanza del piano gratuito."}
```
{: codeblock}


#### Causa
{: #os-cause}
   
Questo errore è dovuto al servizio {{site.data.keyword.objectstorageshort}} che fornisce solo una istanza del piano Gratuito {{site.data.keyword.objectstorageshort}}.


#### Soluzione
{: #os-resolution}

Per evitare questo errore ti viene richiesto di scegliere un piano diverso.


### Errore durante l'ottenimento del codice durante la creazione del progetto
{: #code}

Potresti visualizzare il seguente errore se utilizzi la {{site.data.keyword.dev_cli_short}} per creare un progetto:
	
```
NON RIUSCITO
Progetto creato, ma non è possibile ottenere il codice
https://console.ng.bluemix.net/developer/projects/b22165f3-cbc6-4f73-876f-e33cbec199d4/code
```
{: codeblock}
	

#### Causa
{: #code-cause}

Questo errore è dovuto a un timeout interno.
	

#### Soluzione
{: #code-resolution}

Puoi ottenere il codice in uno dei seguenti modi:

* Immetti il seguente comando utilizzando la CLI:

   ```
   bx dev code <your-project-name>
   ```
   {: codeblock}

   Sostituisci `<your-project-name>` con il nome progetto che hai specificato durante la creazione del progetto.

* Utilizza la {{site.data.keyword.dev_console}}.

	1. Seleziona il tuo progetto [ ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://console.{DomainName}/developer/projects) nella {{site.data.keyword.dev_console}} e fai clic su **Ottieni codice**.

	2. Fai clic su **Genera codice**.

	3. Dopo aver generato il codice, fai clic su **Scarica codice**.


### Errore durante l'esecuzione di `bx dev run` per i progetti Node.js
{: #node}

Potresti visualizzare il seguente errore se stai eseguendo `bx dev run` con la {{site.data.keyword.dev_cli_short}} per i progetti Node.js Web o BFF:

```
module.js:597
  return process.dlopen(module, path._makeLong(filename));
                 ^

Error: /app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/appmetrics.node: invalid ELF header
    at Error (native)
    at Object.Module._extensions..node (module.js:597:18)
    at Module.load (module.js:487:32)
    at tryModuleLoad (module.js:446:12)

    at Function.Module._load (module.js:438:3)
    at Module.require (module.js:497:17)
    at require (internal/module.js:20:19)
    at Object.<anonymous> (/app/node_modules/bluemix-autoscaling-agent/node_modules/appmetrics/index.js:25:13)
    at Module._compile (module.js:570:32)
    at Object.Module._extensions..js (module.js:579:10)
```
{: codeblock}


#### Causa
{: #node-cause}
   
Questo errore è causato dal modulo `appmetrics` installato su un'architettura diversa. I moduli npm nativi installati su un'architettura non funzionano su un'altra. Le immagini Docker incluse si basano sul kernel Linux.


#### Soluzione
{: #node-resolution}

Elimina la cartella `node_modules` ed esegui nuovamente `bx dev run`.


<!--
## Troubleshooting techniques
{: #tstechniques}
-->

<!-- Add a heading and content for how to get help and support. Use this template for beta and GA services:  -->


## Come ottenere aiuto e supporto
{: #gettinghelp}

Se hai dei problemi o delle domande relative a {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} o {{site.data.keyword.dev_cli_notm}}, puoi ottenere aiuto ricercando le informazioni o facendo delle domande in un forum. Puoi anche aprire un ticket di supporto.

Quando fai una domanda nei forum, contrassegnala con una tag in modo che possa essere vista dai team di sviluppo {{site.data.keyword.Bluemix_notm}}.

<!--Insert the appropriate Stack Overflow tag for your service for <service_keyword> in URL and text below:  -->

Se hai domande tecniche sullo sviluppo o la distribuzione di un'applicazione con {{site.data.keyword.dev_console}} o {{site.data.keyword.dev_cli_notm}}:

* Inserisci la tua domanda in [Stack Overflow ![Icona link esterno](../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/search?q=bluemix-dev-services+ibm-bluemix) e contrassegnala con le tag `bluemix-dev-services` e `ibm-bluemix`.
* Inserisci la tua domanda in [Slack
![Icona link esterno](../icons/launch-glyph.svg "External link icon")](http://ibm-cloud-tech.slack.com/) nel canale bluemix-dev-services. [Registrati a ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://ibm.biz/IBMCloudNativeSlack) oggi.


<!--Insert the appropriate dW Answers tag for your service for <service_keyword> in URL below:  -->
<!--
* For questions about the service and getting started instructions, use the [IBM developerWorks dW Answers ![External link icon](../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/answers/topics/bluemix-dev-services/?smartspace=bluemix) forum. Include the  "bluemix-dev-services" and "bluemix" tags.
* -->

Consulta [Come ottenere supporto
![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/support/index.html#getting-help) per ulteriori dettagli sull'utilizzo dei forum.

Per informazioni su come aprire un ticket di supporto {{site.data.keyword.IBM}} o sui livelli di supporto e sulla gravità dei ticket, consulta
[Come contattare il supporto ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/support/index.html#contacting-support).

<!--Add a heading and content for how to get help. (Support not available for experimental.) Use this template for experimental services:  -->

