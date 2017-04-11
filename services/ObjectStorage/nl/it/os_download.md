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

# Scaricamento di oggetti

Puoi scaricare i tuoi oggetti archiviati per il controllo o la modifica tramite la IU o la CLI.
{: shortdesc}


## Scaricamento degli oggetti dalla IU {: #downloading-ui}

1. Per prevenire la distruzione di dati a causa di sovrascritture non intenzionali, [configura le versioni dell'oggetto](/docs/services/ObjectStorage/os_versioning.html). Se non desideri le versioni dell'oggetto, ridenomina la directory o i file prima dello scaricamento, se necessario.
2. Nel tuo dashboard dell'istanza del servizio, seleziona il contenitore con il file che desideri scaricare.
3. Seleziona il file.
4. Nel menu a discesa **Azioni**, seleziona **Scarica file**.


## Scaricamento degli oggetti con la CLI Swift {: #downloading-cli}

1.  Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.

    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}

2. Per prevenire la distruzione di dati a causa di sovrascritture non intenzionali, [configura le versioni dell'oggetto](/docs/services/ObjectStorage/os_versioning.html). Se non desideri le versioni dell'oggetto, elenca i tuoi file esistenti in un archivio e se necessario, ridenomina la directory o i file prima dello scaricamento.

3. Scarica un file eseguendo il seguente comando:

    ```
    swift download <container_name> <file_name>
    ```
    {: pre}
