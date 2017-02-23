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


# Eliminazione di oggetti

Dopo che non hai più bisogno di essi, puoi eliminare gli oggetti e i contenitori dalla tua istanza di archiviazione. Puoi eseguire l'eliminazione manualmente o puoi [pianificare una data/ora](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion) per la scadenza degli oggetti.
{: shortdesc}

**Nota**: se elimini il tuo contenitore, elimini tutti gli oggetti archiviati in tale contenitore.


## Eliminazione degli oggetti e dei contenitori tramite la IU {: #deleting-ui}

1. Nel tuo dashboard dell'istanza del servizio, seleziona il contenitore con il file di cui non hai più bisogno.
2. Seleziona **Elimina file** dal menu a discesa **Azioni**.
3. Se non hai più bisogno di utilizzare il tuo contenitore, seleziona **Elimina contenitore** dal menu a discesa **Azioni**.



## Eliminazione degli oggetti e dei contenitori tramite la CLI {: #deleting-cli}

1.  Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Facoltativo: Conferma di avere un backup dei tuoi oggetti prima di eliminare i tuoi file e contenitori.

3. Esegui il seguente comando per eliminare un file:
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

4. Per eliminare il tuo contenitore, esegui il seguente comando:
  ```
  swift delete <container_name>
  ```
  {: pre}



## Pianificazione dell'eliminazione dell'oggetto {: #schedule-object-deletion}


Puoi pianificare l'eliminazione dei tuoi oggetti utilizzando le intestazioni `X-Delete-At` o `X-Delete-After`.
{: shortdesc}

L'intestazione `X-Delete-At` è un numero intero che rappresenta il momento nel quale eliminare l'oggetto. L'intestazione `X-Delete_After` è un numero intero che rappresenta il numero di secondi dopo cui l'oggetto viene eliminato.

**Nota:** l'eliminazione effettiva di un oggetto potrebbe non verificarsi nell'esatto momento indicato. Tuttavia, l'oggetto scadrà nel momento specificato. In quel momento, l'oggetto non è più raggiungibile. L'eliminazione effettiva avrà luogo la volta successiva in cui viene eseguito il daemon swift-object-expirer configurato nel tuo cluster Swift.

#### Per utilizzare i comandi Swift:

* Per impostare che l'oggetto venga eliminato in una data/ora specifica, utilizza il seguente comando:

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    Esempio:
    Per impostare che l'oggetto venga eliminato il "2016/04/01 08:00:00", dovrai eseguire il seguente comando:

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* Per impostare che l'oggetto venga eliminato dopo un lasso di tempo specifico, utilizza il seguente comando:

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    Esempio:
    Per impostare che l'oggetto venga eliminato tra un'ora, dovrai eseguire il seguente comando:

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* Per rimuovere la data/ora di scadenza dal tuo oggetto, utilizza il seguente comando:

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### Per utilizzare i comandi cURL:

* Per impostare che l'oggetto venga eliminato il "2016/04/01 08:00:00", utilizza il seguente comando:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Per impostare che l'oggetto venga eliminato tra un'ora, utilizza il seguente comando:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Per controllare se l'oggetto ha un'intestazione, utilizza il seguente comando:

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Per rimuovere la data/ora di scadenza, utilizza il seguente comando:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
