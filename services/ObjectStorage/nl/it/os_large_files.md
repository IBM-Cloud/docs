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


# Archiviazione di oggetti grandi {: #large-files}

I caricamenti sono limitati a una dimensione massima di 5 GB per singolo caricamento. Tuttavia, puoi suddividere gli oggetti grandi in parti più piccole e utilizzare il file manifest per concatenare i segmenti. Quando un oggetto è stato concatenato, non esiste una dimensione massima.
{: shortdesc}

Gli oggetti grandi possono essere dinamici o statici. Con gli SLO (Static Large Objects), i segmenti non devono essere nello stesso contenitore; ogni segmento può essere archiviato in un qualsiasi contenitore e può avere un nome qualsiasi. Con gli DLO (Dynamic Large Objects), il client Swift, crea il contenitore e i segmenti numerati vengono caricati in parallelo nel contenitore.


## DLO (Dynamic large objects): {: #dynamic}

Puoi caricare gli DLO (Dynamic large objects) in due modi:
  * Lasciare al client Swift gestire tutto automaticamente
  * Utilizzare l'API Swift per farlo personalmente

#### Utilizzo del client Swift per gestire gli DLO (dynamic large objects)

Il client Swift utilizza il parametro `-segment-size` per dividere il tuo oggetto in parti più piccole. Il client crea un nuovo contenitore con il nome del contenitore in cui desideri caricare i file e aggiunge un suffisso con il numero di segmento (`<container_name>_segments`). I segmenti vengono caricati in parallelo. Dopo che sono stati caricati tutti i segmenti, vengono scaricati come un oggetto concatenato in un file manifest con il nome del file originale.

1. Dopo aver eseguito l'accesso a {{site.data.keyword.Bluemix_notm}} ed essere pronto per il caricamento, esegui il seguente comando per frazionare il tuo file.
    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### Utilizzo dell'API Swift per gestire DLO (Dynamic Large Objects)

Puoi personalmente frazionare gli oggetti in modo che siano di 5 GB o meno e quindi caricarli tramite l'API Swift

**Nota**: durante il caricamento, tutti i segmenti devono essere caricati prima del file manifest. Se l'oggetto viene scaricato prima che siano stati caricati tutti i segmenti, l'oggetto scaricato si concatena in modo incongruente.

Puoi caricare file grandi completando la seguente procedura.

1. Ordina i segmenti per nome nell'ordine in cui dovrebbero essere concatenati per formare l'oggetto originale.
2. Carica i tuoi segmenti in un contenitore separato dal contenitore che ospita il file manifest. Limita in modo che i caricamenti si avviino dopo che il decimo segmento viene caricato e incrementa il tempo di caricamento sensibilmente.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}

3. Carica un file manifest vuoto con l'intestazione `X-Object-Manifest` impostata sul valore `<container>/prefix>` corrispondente.

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}

    **Nota**: il file manifest deve essere vuoto. Se non lo è, il contenuto del file viene considerato come uno dei segmenti e si riscontra un malfunzionamento nell'ordinamento della concatenazione indicata dai nomi ordinati.
4. Scarica l'oggetto. Come risultato, riceverai l'oggetto completo. Puoi aggiungere o rimuovere segmenti senza dover aggiornare il file manifest. I segmenti con il prefisso corretto rimangono parte dell'oggetto. L'eliminazione del manifest non elimina i segmenti.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## SLO (Static Large Objects) {: #static}

SLO (Static large objects) utilizza i segmenti e un file manifest, ma hai più controllo. Con SLO, i segmenti non devono essere nello stesso contenitore; ogni segmento può essere archiviato in un qualsiasi contenitore e può avere un nome qualsiasi. Tuttavia, i segmenti devono essere di almeno 1 MB. Non ti viene richiesto di impostare un'intestazione per il file manifest, anche se l'intestazione “X-Static-Large-Object” viene aggiunta automaticamente e impostata su true dopo che viene caricato un manifest correttamente.
{: shortdesc}

Il file manifest è un documento JSON che fornisce i dettagli sui segmenti e deve essere caricato dopo che sono stati caricati tutti i segmenti. I dati forniti per ogni documento nel manifest vengono confrontati con i metadati dei segmenti attuali. Se qualcosa non corrisponde, il manifest non viene caricato.

<table>
<caption> Tabella.1 gli attributi JSON nel file manifest </caption>
  <tr>
    <th> Attributo </th>
    <th> Descrizione </th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> L'ubicazione e il nome del segmento. Specificati come container_name/object_name. </td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> Fornita dalla richiesta PUT quando l'oggetto viene caricato. Puoi anche trovarla eseguendo un HEAD all'oggetto. </td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> La dimensione dell'oggetto in byte. </td>
  </tr>
</table>



#### Per caricare file grandi

1. Esegui il seguente comando per caricare i segmenti. Limita in modo che i caricamenti si avviino dopo che il decimo segmento viene caricato e incrementa il tempo di caricamento sensibilmente.  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}

2. Crea il manifest:

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}

3. Carica il file manifest aggiungendo la query `multipart-manifest=put` al nome del manifest.

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. Scarica l'oggetto.

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### Utilizzo degli SLO (Static Large Objects)

Puoi gestire i tuoi file utilizzando i seguenti comandi.

**Nota**: per aggiungere o rimuovere i segmenti all'oggetto, carica un nuovo file manifest con un nuovo elenco di segmenti. Il nome del manifest può rimanere lo stesso.

* Per scaricare il contenuto del file manifest, devi aggiungere la query `multipart-manifest=get` al tuo comando. Il contenuto che ricevi non è identico al contenuto che hai caricato.

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}

* Per eliminare il manifest esegui il seguente comando:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

* Per eliminare il manifest e tutti i segmenti, aggiungi la query `multipart-manifest=delete` dopo il nome del manifest:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}
