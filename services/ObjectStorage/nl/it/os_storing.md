---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Archiviazione di oggetti

Puoi caricare gli oggetti per l'archiviazione utilizzando la IU o la CLI. Il caricamento degli oggetti è limitato a una dimensione massima di 5 GB per singolo caricamento. Tuttavia, puoi caricare oggetti grandi segmentandoli in oggetti più piccoli.
{: shortdesc}


## Archiviazione degli oggetti nei contenitori tramite la IU {: #storing-ui}

**Nota**: quando carichi un file con lo stesso nome, {{site.data.keyword.objectstorageshort}} sostituisce il file archiviato con il nuovo file. Se scarichi un file ed effettui delle modifiche, assicurati di fornire al file un altro nome o [imposta le versioni dell'oggetto](/docs/services/ObjectStorage/os_versioning.html) prima del tuo caricamento per mantenere entrambe le versioni del file.


1. Dal tuo dashboard dell'istanza del servizio, aggiungi un contenitore dal menu a discesa **Azioni**.
2. Denomina il tuo contenitore e fai clic su **CREA**.
3. Dal menu a discesa **Azioni**, seleziona **Aggiungi file**. Viene visualizzata una finestra di dialogo.
4. Seleziona il file o i file che desideri caricare e fai clic su **Apri**.



## Archiviazione degli oggetti nei contenitori tramite la CLI {: #storing-cli}

1. Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Crea un contenitore {{site.data.keyword.objectstorageshort}} eseguendo il seguente comando. La variabile*container_name* viene impostata, da te, in questo momento.

  ```
  swift post <container_name>
  ```
  {: pre}

  **Nota**: se ricevi un messaggio di errore, conferma di aver installato [il software prerequisito](/docs/services/ObjectStorage/os_configuring.html#install-swift-client).

3. Facoltativo: Per verificare che il contenitore sia stato creato, esegui il seguente comando per elencare i tuoi contenitori.

  ```
  swift list
  ```
  {: pre}

4. Per prevenire la distruzione di dati a causa di sovrascritture non intenzionali, [configura le versioni dell'oggetto](/docs/services/ObjectStorage/os_versioning.html). Se non desideri le versioni dell'oggetto, elenca i tuoi file esistenti in un archivio e se necessario, ridenomina la directory o i file prima del caricamento.

5. Carica un file nel tuo contenitore eseguendo il seguente comando.

  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

  **Nota**: per caricare file più grandi di 5 GB [sono necessari ulteriori passi](/docs/services/ObjectStorage/os_large_files.html).

6. Facoltativo: Per verificare che il caricamento ha avuto esito positivo, visualizza il contenuto del tuo contenitore eseguendo il seguente comando.

  ```
  swift list <container_name>
  ```
  {: pre}
