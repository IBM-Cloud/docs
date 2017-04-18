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

# Plugin SDK Generator
{: #sdk-cli}

Il plug-in {{site.data.keyword.IBM}} SDK Generator può essere installato nella CLI [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/cli/reference/bluemix_cli/index.html).

In qualità di sviluppatore in {{site.data.keyword.Bluemix_notm}}, puoi utilizzare questo plug-in per generare gli SDK dalla tua definizione API REST conforme alla [Specifica Open API ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.openapis.org/). Quando apporti modifiche alla tua definizione API REST, puoi utilizzare il plug-in per rigenerare solo l'SDK anziché rigenerare l'intero progetto.

Puoi anche vedere se le tue applicazioni Cloud Foundry in un determinato spazio hanno definizioni API REST valide per la generazione dell'SDK. Infine, puoi utilizzare il plug-in {{site.data.keyword.IBM_notm}} SDK Generator per convalidare qualsiasi definizione API REST al fine di garantire che siano conformi ai requisiti del generatore SDK.

Questo plug-in {{site.data.keyword.IBM_notm}} SDK Generator ti consente di integrare facilmente i tuoi servizi di backend alla tua applicazione con un SDK generato. Quando viene apportata una modifica a un'API REST, puoi rigenerare l'SDK e sostituire quello vecchio per un aggiornamento SDK senza interruzioni. Puoi anche integrare la CLI in una pipeline DevOps e garantire che l'SDK sia sempre conforme alla specifica API ogni volta che l'applicazione viene creata.

La definizione API REST deve essere valida e deve essere ospitata su un endpoint server live o in un file locale sul tuo sistema. Se la definizione API REST è ospitata, l'URL relativo deve essere definito nella variabile di ambiente `OPENAPI_SPEC`.


## Requisiti
{: #prereqs}

Assicurati di soddisfare i seguenti requisiti.

* Disponi di un account [{{site.data.keyword.Bluemix_notm}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://bluemix.net)
* Hai una definizione API valida conforme alla specifica [Open API ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](https://www.openapis.org/)


## Installazione
{: #installation}

1. [Installa la CLI {{site.data.keyword.Bluemix}} ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](http://clis.ng.bluemix.net/ui/home.html).

2. [Installa il plug-in ![Icona link esterno](../icons/launch-glyph.svg "Icona link esterno")](/docs/cli/reference/bluemix_cli/index.html#install_plug-in).

	```
	bx plugin install sdk-gen -r Bluemix
	```
	{: codeblock}


## Comandi
{: #commands}

Utilizza i seguenti comandi per generare un SDK, per convalidare i file di definizione Open API o per elencare le applicazioni Cloud Foundry.


### Generazione di un SDK
{: #gen}

Use `bluemix sdk generate [arguments...][command options]`.


#### Argomenti
{: #gen-args}

* `APP_NAME` - il nome dell'applicazione Cloud Foundry nel tuo spazio corrente
* `OPENAPI_DOC_LOCATION` - un URL o percorso file relativo al JSON o Yaml della definizione API REST non elaborata
* `GENERATED_SDK_NAME` (facoltativo) - il nome dell'SDK generato


#### Opzioni
{: #gen-options}

* `PLATFORM` (obbligatorio)
   * `--android` - genera un SDK Android
   * `--ios` - genera un SDK iOS Swift
   * `--swift` - genera un SDK server Swift
* `--output "YOUR_RELATIVE_PATH"` (facoltativo) - inserisce l'SDK generato nella directory specificata da `YOUR_RELATIVE_PATH` (sovrascrive l'SDK esistente, se presente)
* `--unzip` (facoltativo) - estrae l'SDK generato (sovrascrive le risorse SDK esistenti, se presenti)


#### Utilizzo
{: #gen-usage}

Per generare un SDK da un'applicazione Cloud Foundry in esecuzione in {{site.data.keyword.Bluemix_notm}}, puoi utilizzare il nome dell'applicazione come parametro nella CLI. Il seguente comando utilizza il nome dell'applicazione come `SDK_Name`.

```
bluemix sdk generate [APP_NAME] [PLATFORM]
```
{: codeblock}

Per generare un SDK da un URL di un file di definizione Open API o un file JSON o Yaml locale, utilizza il seguente comando.

```
bluemix sdk generate [OPENAPI_DOC_LOCATION] [SDK_Name] [Platform]
```
{: codeblock}


### Convalida delle definizioni API Open
{: #validating}

Utilizza `bluemix sdk validate [argument]`.


#### Argomenti
{: #val-args}

* `APP_NAME` - il nome dell'applicazione Cloud Foundry nel tuo spazio corrente
* `OPENAPI_DOC_LOCATION` - un URL o percorso file relativo al JSON o Yaml della definizione API REST non elaborata


#### Utilizzo
{: #val-usage}

Per convalidare la specifica API di un'applicazione Cloud Foundry in esecuzione in {{site.data.keyword.Bluemix_notm}}, puoi utilizzare il nome dell'applicazione come parametro nella CLI.

```
bluemix sdk validate [APP_NAME]
```
{: codeblock}

Per convalidare un SDK dall'URL di un documento di specifiche API o un file JSON o Yaml locale, utilizza il seguente comando.

```
bluemix sdk validate [OPENAPI_DOC_LOCATION]
```
{: codeblock}



### Elenca applicazioni (Cloud Foundry)
{: #list-apps}

Utilizza `bluemix sdk list [argument][option]` per elencare le applicazioni e convalidare le specifiche API. Devi impostare la variabile di ambiente `OPENAPI_SPEC` sul percorso URL relativo che ospita la tua specifica.


#### Argomenti
{: #list-args}

* `SPACE_NAME` (facoltativo) - il nome dello spazio Cloud Foundry all'interno della tua organizzazione in cui ricercare le applicazioni. Se non viene fornito, la ricerca avviene nello spazio corrente.


#### Opzioni
{: #list-options}

* `--url` (facoltativo) - visualizza un URL completamente formato della definizione Open API per ogni applicazione nell'elenco


#### Utilizzo
{: #list-usage}

Per elencare le applicazioni nello spazio corrente, utilizza il seguente comando.

```
bluemix sdk list
```
{: codeblock}

Per elencare le applicazioni nello spazio corrente e visualizzare l'URL della specifica API, utilizza il seguente comando.

```
bluemix sdk list --url
```
{: codeblock}

Per elencare le applicazioni in uno specifico spazio, utilizza il seguente comando.

```
bluemix sdk list [SPACE_NAME]
```
{: codeblock}

Per elencare le applicazioni in uno specifico spazio e visualizzare l'URL della specifica API, utilizza il seguente comando.

```
bluemix sdk list [SPACE_NAME] --url
```
{: codeblock}
