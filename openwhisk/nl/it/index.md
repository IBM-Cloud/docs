---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Introduzione a {{site.data.keyword.openwhisk_short}}
*Ultimo aggiornamento: 17 febbraio 2016*

{{site.data.keyword.openwhisk}} è un servizio di calcolo distribuito guidato dagli eventi. {{site.data.keyword.openwhisk_short}} esegue la logica dell'applicazione in risposta a eventi o chiamate dirette provenienti da applicazioni Web o mobile su HTTP. Gli eventi possono essere forniti da servizi Bluemix quali Cloudant e da fonti esterne. Gli sviluppatori possono concentrarsi sulla scrittura della logica dell'applicazione e sulla creazione di azioni eseguite su richiesta. Il tasso di esecuzione delle azioni corrisponde sempre al tasso degli eventi, con conseguenti utilizzo ottimale e resilienza e ridimensionamento intrinsechi. Paghi solo per ciò che usi e non devi gestire alcun server. Puoi anche ottenere il [codice sorgente](https://github.com/openwhisk/openwhisk) ed eseguire il sistema autonomamente.
{: shortdesc}

Per ulteriori dettagli sul funzionamento di {{site.data.keyword.openwhisk_short}}, vedi [Informazioni su {{site.data.keyword.openwhisk_short}}](./openwhisk_about.html).

## Configurazione di {{site.data.keyword.openwhisk_short}}
Puoi utilizzare l'interfaccia di riga comando (CLI) {{site.data.keyword.openwhisk_short}} per configurare il tuo spazio dei nomi e la tua chiave di autorizzazione. Passa a [Configura CLI](https://console.{DomainName}/openwhisk/cli){: new_window} e segui la procedura di installazione guidata. Nota che per utilizzare la CLI è necessario che Python 2.7 sia installato sul tuo sistema.

Una volta configurato {{site.data.keyword.openwhisk_short}} con la CLI, puoi iniziare a utilizzarlo dalla riga di comando o attraverso le API REST.

## Utilizzo della CLI {{site.data.keyword.openwhisk_short}}
Una volta configurato il tuo ambiente, puoi iniziare a utilizzare la CLI {{site.data.keyword.openwhisk_short}} per effettuare le seguenti operazioni:

* Eseguire i tuoi frammenti di codice, o le azioni, su {{site.data.keyword.openwhisk_short}}. Vedi [Creazione e richiamo di azioni](./openwhisk_actions.html).
* Utilizzare i trigger e le regole per consentire alle tue azioni di rispondere agli eventi. Vedi [Creazione di trigger e regole](./openwhisk_triggers_rules.html).
* Imparare in che modo i pacchetti riuniscono le azioni e configurano origini eventi esterne. Vedi [Utilizzo e creazione di pacchetti](./openwhisk_packages.html).
* Esplorare il catalogo dei pacchetti e ampliare le tue applicazioni con servizi esterni, quali un'[origine eventi Cloudant](./openwhisk_catalog.html#openwhisk_catalog_cloudant). Vedi [Utilizzo di servizi con attivazione {{site.data.keyword.openwhisk_short}}](./openwhisk_catalog.html).


## Utilizzo di {{site.data.keyword.openwhisk_short}} da un'applicazione iOS
Puoi utilizzare {{site.data.keyword.openwhisk_short}} dalla tua applicazione mobile iOS o Apple Watch, attraverso l'SDK iOS {{site.data.keyword.openwhisk_short}}. Per maggiori dettagli, fai riferimento alla documentazione di [iOS](./openwhisk_mobile_sdk.html).

## Utilizzo delle API REST con {{site.data.keyword.openwhisk_short}}
Una volta abilitato il tuo ambiente {{site.data.keyword.openwhisk_short}}, puoi utilizzare {{site.data.keyword.openwhisk_short}} con le tue applicazioni Web o mobile con chiamate API REST. Per ulteriori dettagli sull'utilizzo delle API per azioni, attivazioni, pacchetti, regole e trigger, vedi la [{{site.data.keyword.openwhisk_short}} API documentation](https://new-console.{DomainName}/apidocs/98).

## {{site.data.keyword.openwhisk_short}}Esempio Hello World
Per iniziare a utilizzare {{site.data.keyword.openwhisk_short}}, prova il seguente esempio di codice JavaScript.

```
/**
 * Hello world come azione OpenWhisk.
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

    ```
    {
        "payload": "Hello, World!"
    }
```
    {: screen}

    ```
    wsk action invoke hello --blocking --result --param name Fred
```
    {: pre}  

    Questo comando ha il seguente output:

    ```
    {
        "payload": "Hello, Fred!"
    }
```
    {: screen}

Puoi anche utilizzare le funzionalità guidate dagli eventi in {{site.data.keyword.openwhisk_short}} per richiamare questa azione in risposta agli eventi. Segui l'[esempio di servizio di allerta](./openwhisk_packages.html#openwhisk_packages_trigger) per configurare un'origine eventi che richiami l'azione `hello` ogni volta che viene generato un evento periodico.


## Dettagli del sistema

Puoi trovare ulteriori informazioni su {{site.data.keyword.openwhisk_short}} nei seguenti argomenti:

* [Nomi entità](./openwhisk_reference.html#openwhisk_entities)
* [Semantica delle azioni](./openwhisk_reference.html#openwhisk_semantics)
* [Limiti](./openwhisk_reference.html#openwhisk_syslimits)
* [API REST](https://new-console.{DomainName}/apidocs/98)

# rellinks
## api
* [Documentazione API REST](https://new-console.{DomainName}/apidocs/98){:new_window}

## generale
* [Scopri: {{site.data.keyword.openwhisk_short}}](http://www.ibm.com/cloud-computing/bluemix/openwhisk/){:new_window}
* [{{site.data.keyword.openwhisk_short}} su IBM developerWorks](https://developer.ibm.com/openwhisk/){:new_window}
