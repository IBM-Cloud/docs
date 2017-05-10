---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}}CLI
{: #containerregcli}

La CLI {{site.data.keyword.registrylong}} è un plugin che ti permette di gestire le tue risorse del registro, come gli spazi dei nomi e le immagini, nell'organizzazione.
{: shortdesc}

**Prerequisiti**
* Prima di eseguire i comandi del registro, accedi a {{site.data.keyword.Bluemix_short}}
 con il comando `bx login` per generare un token di accesso {{site.data.keyword.Bluemix_short}}
 e autenticare la tua sessione.

<table summary="Gestione del tuo registro dei contenitori">
<caption>Tabella 1. Comandi per la gestione di {{site.data.keyword.registryshort}} su {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Comandi per la gestione del registro</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
Restituisce i dettagli sull'endpoint dell'API del registro per cui vengono eseguiti i comandi.

```
bx cr api
```
{: codeblock}


## bx cr info
Visualizza il nome e l'organizzazione del registro a cui hai eseguito l'accesso.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Visualizza i dettagli su un'immagine specifica.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parametri**
<dl>
<dt>--format FORMAT</dt>
<dd>(Facoltativo) Formatta gli elementi di output utilizzando un modello Go.</dd>
<dt>IMMAGINE</dt>
<dd>Il percorso di registro {{site.data.keyword.Bluemix_short}} completo dell'immagine che desideri analizzare, in formato spaziodeinomi/immagine:tag. Se nel percorso dell'immagine non è specificata alcuna tag, viene analizzata l'immagine contrassegnata con `latest`. Puoi analizzare più immagini elencando ogni percorso del registro {{site.data.keyword.Bluemix_short}} privato nel comando con uno spazio tra ogni percorso.</dd>
</dl>


## bx cr image-list
Visualizza tutte le immagini nella tua organizzazione {{site.data.keyword.Bluemix_short}}.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parametri**
<dl>
<dt>--no-trunc</dt>
<dd>(Facoltativo) Non tronca l'output.</dd>
<dt>-q, --quiet</dt>
<dd>(Facoltativo) Visualizza un identificativo univoco per l'immagine nel formato: 'repository:tag'.</dd>
<dt>--include-ibm</dt>
<dd>(Facoltativo) Include le immagini pubbliche fornite da IBM nell'output. Senza questa opzione, vengono elencate solo le immagini private.</dd>
<dt>--format FORMAT</dt>
<dd>(Facoltativo) Formatta gli elementi di output utilizzando un modello Go.</dd>
</dl>


## bx cr image-rm
Elimina un'immagine specificata dal tuo registro.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parametri**
<dl>
<dt>IMAGE</dt>
<dd>Il percorso di registro {{site.data.keyword.Bluemix_short}} completo dell'immagine che desideri rimuovere , in formato spaziodeinomi/immagine:tag. Se nel percorso dell'immagine non è specificata alcuna tag, per impostazione predefinita verrà eliminata l'immagine con tag `latest`. Puoi rimuovere più immagini elencando ogni percorso del registro {{site.data.keyword.Bluemix_short}} privato nel comando con uno spazio tra ogni percorso.</dd>
</dl>


## bx cr login
Se è installato Docker, questo comando esegue il comando `docker login` per il registro. Il comando `docker login` è obbligatorio per abilitare l'esecuzione dei comandi `docker push` o `docker pull` per il registro. Questo comando non è obbligatorio per eseguire altri comandi `bx cr`. Se Docker non è installato, questo comando restituisce un messaggio di errore.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Aggiunge uno spazio dei nomi alla tua organizzazione Bluemix. 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parametri**
<dl>
<dt>NAMESPACE</dt>
<dd>Lo spazio dei nomi che desideri aggiungere. Lo spazio dei nomi deve essere univoco tra tutte le organizzazioni {{site.data.keyword.Bluemix_short}}.</dd>
</dl>


## bx cr namespace-list
Visualizza tutti gli spazi dei nomi della tua organizzazione {{site.data.keyword.Bluemix_short}}.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Rimuove uno spazio dei nomi dalla tua organizzazione {{site.data.keyword.Bluemix_short}}. Le immagini in questo spazio dei nomi vengono eliminate quando viene rimosso.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parametri**
<dl>
<dt>NAMESPACE</dt>
<dd>Lo spazio dei nomi che desideri rimuovere.</dd>
</dl>
