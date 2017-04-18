---

copyright:
  years: 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Calcolo
{: #compute}

Quando crei un'applicazione di canale digitale nativa del cloud per web e mobile, la procedura consigliata consiste nell'avere un BFF (Backend for Frontend) che sia dedicato al tuo canale digitale o che offra lo stesso supporto di integrazione di dati e logica sia per le applicazioni client Web che mobili. Per ulteriori informazioni su questa architettura, vedi [Microservices for web and mobile ![Icona link esterno](../icons/launch-glyph.svg)](https://www.ibm.com/devops/method/content/architecture/omnichannelArchitecture).

Il seguente diagramma mostra una panoramica dell'architettura.

![Architettura BFF](images/bff-arch.png)

Figura 1: architettura BFF

Il concetto di un BFF è quello di astrarre la logica di business e la logica di integrazione comune dai tuoi microservizi o dai servizi cloud {{site.data.keyword.Bluemix}} di alto valore. 

Con questa architettura, puoi distribuire e rilasciare aggiornamenti alla tua applicazione mobile o Web e distribuire nuove versioni del BFF utilizzando pipeline di fornitura continua con il servizio DevOps.

Se hai un BFF per iOS e un altro BFF per Android, i team di progettazione che forniscono la funzione per queste applicazioni non sono vincolati a rilasciare le funzioni con una pianificazione di rilascio API centralizzata. Questo è un obiettivo comune per le architetture di microservizi e canali digitali, ossia permettere ai team di rilasciare spesso le funzioni senza essere condizionati dalla pianificazione di rilascio di altri team.

<!--
## Backend for Frontends (BFF)
{: #bff}

Backend for Frontend patterns, commonly known as BFFs, really help you to focus on exposing business data and services in a form that matches the user interaction requirements. To optimize a user journey to your cloud solution, it may require a different user journey for the mobile application and a richer, more detailed journey for the Web application. With the introduction of voice-controlled devices like the [{{site.data.keyword.conversationfull}} ![External link icon](../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/watson/developercloud/conversation.html) service, the interaction with a user could be controlled by voice. This digital channel will require a very different BFF for managing these voice intent-based interactions.

With {{site.data.keyword.Bluemix_notm}}, you can build a BFF by using polyglot programming approach to define the BFF. IBM recommends using Node, Swift, or Java and running them in a cloud native pattern with either Cloud Foundry, Container services, or serverless.

The BFF will manage the integration with services for data persistence, caching, and integration with high-value services like {{site.data.keyword.ibmwatson}}, {{site.data.keyword.iot_short_notm}}, {{site.data.keyword.weather_short}}, and data analytics like {{site.data.keyword.sparks}}.

The BFF will expose an API most commonly using a REST pattern, but you can design your BFF to work from a messaging architecture using {{site.data.keyword.messagehub}}.
-->


## Integrazione di un client mobile con un Backend for Frontend
{: #integration}

Per consentire una facile integrazione tra un client mobile e un BFF, {{site.data.keyword.Bluemix_notm}} supporta la generazione dell'SDK client mobile per iOS e Android rispettivamente nei linguaggi Swift e Java. Per abilitare questa funzione, devi esporre la tua integrazione BFF utilizzando un documento di specifiche Open API (Swagger). Questo documento può essere in formato JSON o YAML.

Il generatore dell'SDK client utilizza il file di definizione Open API per definire un SDK per sviluppatori ottimizzato per il client che sia facile da utilizzare nella tua applicazione mobile nativa. Questo permetterà di accelerare l'integrazione del BFF nella tua applicazione mobile.


## Definizione di una API
{: #definition}

Il BFF deve esporre un file di definizione API che sia conforme alla specifica Open API in esecuzione su un endpoint server live. Per consentire a {{site.data.keyword.Bluemix_notm}} Developer Experience e {{site.data.keyword.Bluemix_notm}} SDK CLI (Command Line Interface) di rilevare questo endpoint, devi aggiungere una variabile di ambiente denominata `OPENAPI_SPEC` alla tua applicazione Cloud Foundry. Questa variabile di ambiente deve fare riferimento alla specifica utilizzando un percorso relativo.

Per aggiungere la variabile di ambiente `OPENAPI_SPEC` in {{site.data.keyword.Bluemix_notm}}, completa questa procedura:

1. Accedi a [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../icons/launch-glyph.svg)](http://bluemix.net).
2. Seleziona un'applicazione Cloud Foundry.
3. Seleziona **Runtime**.
4. Seleziona **Variabili di ambiente**.
5. Fai clic su **Aggiungi** nella sezione **Definito dall'utente**.
6. Specifica `OPENAPI_SPEC` per **NAME** e un percorso URL relativo del tuo file di definizione Open API.
7. Fai clic su **Salva**.

<!--
To add the `OPENAPI_SPEC` environment variable locally and push your changes to {{site.data.keyword.Bluemix_notm}} with the [Cloud Foundry CLI ![External link icon](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli#getting-started), follow these steps:

1. Open Terminal and navigate to your project directory.
2. Add the following code to the `manifest.yml` file.

   ```
   env:
       "OPENAPI_SPEC": "<relative URL path to your Open API definition file>"
   ```
   {: codeblock}
3. Save your changes to the `manifest.yml` file.
4. Run `cf push` to deploy the changes to {{site.data.keyword.Bluemix_notm}}.
-->

Ad
esempio:

```
OPENAPI_SPEC='/explorer/swagger.json'
```
{: codeblock}

{{site.data.keyword.apiconnect_long}} e le applicazioni Loopback funzionano particolarmente bene con questo approccio. Puoi utilizzare Loopback e {{site.data.keyword.apiconnect_short}} per definire un modello persistente ed esporre l'operazione CRUD (Create, Read, Update e Delete) utilizzando il file di definizione Open API.

Puoi definire anche operazioni logiche di business.


### Elementi supportati della specifica Open API
{: #supported-elements notoc}

L'unica parte della specifica Open API che non è completamente supportata è la struttura dei file. La specifica consente di suddividere le parti della definizione in file diversi e di farvi riferimento utilizzando il campo json `$ref`. L'intera definizione deve essere contenuta all'interno di un unico file.


## Esempio di Backend for Frontend che utilizza Bluegen
{: #bff-bluegen}

{{site.data.keyword.Bluemix_notm}} ha creato un BFF di riferimento utilizzando {{site.data.keyword.apiconnect_short}} e Strongloop, che associa un modello di prodotto a un {{site.data.keyword.cloudant}} e un'API di immagine per fare riferimento alle immagini in {{site.data.keyword.objectstorageshort}}.

Puoi utilizzare questo modello BFF per iniziare rapidamente con il provisioning di un BFF completamente funzionante in {{site.data.keyword.Bluemix_notm}} e utilizzarlo per capire come sia facile integrare un BFF in un progetto mobile e generare SDK nativi per iOS e Android in Swift e Java.

Segui le istruzioni riportate in [README ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://github.com/ibm-bluemix-mobile-services/backend-for-frontend-node) per creare un progetto e installarlo.


## Utilizzo di Backend for Frontend con un progetto Developer Experience
{: #bff-devex}

{{site.data.keyword.Bluemix_notm}} Mobile Developer Experience è progettato per semplificare la definizione di un progetto mobile con una serie di servizi cloud associati. Puoi aggiungere facilmente i servizi [{{site.data.keyword.mobilepushshort}} ![Icona link esterno](../icons/launch-glyph.svg)](/docs/services/mobilepush/index.html), [Analytics ![Icona link esterno](../icons/launch-glyph.svg)](/docs/services/mobileanalytics/index.html), Data o Storage.

{{site.data.keyword.Bluemix_notm}} {{site.data.keyword.dev_console}} ha introdotto la possibilità di integrare un BFF in un progetto mobile nella pagina **Calcolo**. Puoi aggiungere istanze del servizio Calcolo esistenti al tuo progetto mobile. Una volta aggiunte, puoi generare un SDK nativo per il linguaggio che hai scelto o puoi generare il progetto completo e l'SDK verrà integrato nel pacchetto di origine del progetto nella pagina **Codice**. Ciò è particolarmente utile per l'integrazione con BFF già ben definiti.

Dopo aver scaricato il progetto, puoi aprirlo con Xcode o Android Studio e compilarlo con l'SDK client.


## Utilizzo della CLI
{: #cli}

Mentre sviluppi il tuo BFF, la specifica API potrebbe cambiare. Per supportare queste modifiche, hai le due seguenti opzioni:

* Rigenera l'intero progetto in un nuovo ramo GitHub e unisci le modifiche nel tuo ramo di sviluppo.
* Rigenera direttamente l'SDK utilizzando lo strumento della riga comandi (CLI) e aggiorna solo la parte SDK del progetto mobile.

Per utilizzare la CLI, devi [installarla](sdk_cli.html#installation).

Utilizza il seguente comando per elencare le azioni che puoi effettuare.

```
bluemix sdk
```
{: codeblock}

Utilizza il seguente comando per elencare le istanze Cloud Foundry in esecuzione nel tuo spazio {{site.data.keyword.Bluemix_notm}} corrente.

```
bluemix sdk list
```
{: codeblock}

Vengono elencate tutte le applicazioni e l'API viene convalidata se la variabile di ambiente `OPENAPI_SPEC` è impostata. Nella colonna `VALID`, visualizzerai un segno di spunta verde o una `X` rossa. Il segno di spunta nella colonna `VALID` per l'applicazione significa che è presente una definizione Open API valida. Una `X` nella colonna `VALID` per l'applicazione può significare due cose:

* una variabile di ambiente `OPENAPI_SPEC` non è definita per la tua applicazione OPPURE
* la definizione API non è valida in relazione alla specifica Open API

Utilizza il seguente comando per visualizzare l'URL completamente formato per l'API. Vengono elencate la rotta e l'URI completamente formati della specifica API. Puoi visualizzare la specifica non elaborata in un browser, utilizzarla direttamente nella CLI o verificare che la variabile di ambiente del BFF `OPENAPI_SPEC` sia impostata correttamente.

```
bluemix sdk list --url
```
{: codeblock}

Utilizza il seguente comando per convalidare il file di definizione Open API di `<AppName>` per determinare se può essere utilizzato per generare un SDK. Il comando trova `<AppName>` nel tuo spazio corrente e utilizza il percorso relativo nella variabile di ambiente `OPENAPI_SPEC` per individuare la specifica per la convalida.

```
bluemix sdk validate <AppName>
```
{: codeblock}

Utilizza il seguente comando per generare un SDK per la `<Platform>` nativa da te scelta e per inserire un file compresso nella tua directory di lavoro corrente.

```
bluemix sdk generate <AppName> <SDKName> --<Platform>
```
{: codeblock}

L'utilizzo dell'opzione `--unzip` estrae automaticamente l'SDK nella tua directory di lavoro corrente. Puoi anche specificare la posizione in cui estrarre l'SDK utilizzando l'opzione `--output`. Puoi gestire il tuo codice sorgente con GitHub e creare un nuovo ramo specifico per l'aggiornamento dell'SDK. Mediante questo approccio sarà più semplice visualizzare le modifiche e unire l'SDK aggiornato al tuo ramo di sviluppo.


## Utilizzo di API e modelli generati dell'SDK
{: #models-apis}

Ora che il tuo BFF è stato integrato alla tua applicazione mobile mediante un SDK generato, puoi iniziare a utilizzarlo.

L'SDK viene fornito con la documentazione completa nella directory `docs` e nella directory `source`. Puoi aprire il file `README.html` per visualizzare la documentazione nel web o aprire il file `README.md` per visualizzarla in formato Markdown. La documentazione in formato Markdown è utile per la pubblicazione dell'SDK in Cocoapods o Maven Central.

All'interno della documentazione, puoi visualizzare un elenco delle API generate. Fai clic sull'API per visualizzare un frammento di codice che puoi incollare direttamente nella tua applicazione mobile.
