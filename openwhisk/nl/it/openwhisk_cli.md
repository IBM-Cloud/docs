---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}} offre una potente interfaccia riga di comando che consente la gestione completa di tutti gli aspetti del sistema.

## Configurazione della CLI {{site.data.keyword.openwhisk_short}} 

Puoi utilizzare l'interfaccia di riga comando (CLI) {{site.data.keyword.openwhisk_short}} per configurare il tuo spazio dei nomi e la tua chiave di autorizzazione.
Passa a [Configura CLI](https://new-console.{DomainName}/openwhisk/cli){: new_window} e segui le istruzioni per installarla.

Per utilizzare la CLI, è necessario configurare due proprietà obbligatorie:

1. **Host API** (nome o indirizzo IP) per la distribuzione {{site.data.keyword.openwhisk_short}} che vuoi utilizzare.
2. **Chiave di autorizzazione** (nome utente e password) che ti concede l'accesso all'API {{site.data.keyword.openwhisk_short}}.

Immetti il seguente comando per impostare l'host API:

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

Se conosci la tua chiave di autorizzazione, puoi configurare la CLI per utilizzarla. 

Immetti il seguente comando per impostare la chiave di autorizzazione:

```
wsk property set --auth <authorization_key>
```
{: pre}

**Suggerimento:** per impostazione predefinita, la CLI OpenWhisk memorizza le proprietà impostate in `~/.wskprops`. È possibile modificare la posizione di questo file impostando la variabile di ambiente `WSK_CONFIG_FILE`. 

Per verificare la configurazione della tua CLI, prova a [creare ed eseguire un'azione](./index.html#openwhisk_start_hello_world).

## Utilizzo della CLI {{site.data.keyword.openwhisk_short}}

Una volta configurato il tuo ambiente, puoi iniziare a utilizzare la CLI {{site.data.keyword.openwhisk_short}} per effettuare le seguenti operazioni:

* Eseguire i tuoi frammenti di codice, o le azioni, su {{site.data.keyword.openwhisk_short}}. Vedi [Creazione e richiamo di azioni](./openwhisk_actions.html).
* Utilizzare i trigger e le regole per consentire alle tue azioni di rispondere agli eventi. Vedi [Creazione di trigger e regole](./openwhisk_triggers_rules.html).
* Imparare in che modo i pacchetti riuniscono le azioni e configurano origini eventi esterne. Vedi [Utilizzo e creazione di pacchetti](./openwhisk_packages.html).
* Esplorare il catalogo dei pacchetti e ampliare le tue applicazioni con servizi esterni, quali un'[origine eventi Cloudant](./openwhisk_cloudant.html). Vedi [Utilizzo di servizi con attivazione OpenWhisk](./openwhisk_catalog.html).

## Configura la CLI per utilizzare un proxy HTTPS

La CLI può essere configurata per utilizzare un proxy HTTPS. Per configurare un proxy HTTPS, è necessario creare una variabile di ambiente denominata
`HTTPS_PROXY`. La variabile deve essere impostata sull'indirizzo del proxy HTTPS e sulla sua porta utilizzando il seguente formato:
`{PROXY IP}:{PROXY PORT}`.
