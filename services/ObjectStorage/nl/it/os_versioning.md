---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Utilizzo delle versioni dell'oggetto {: #work-with-object-versioning}

*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Con le versioni dell'oggetto puoi mantenere versioni separate dei tuoi oggetti senza ridenominare i tuoi file. Questo ti permette di visualizzare la cronologia di ogni oggetto e tenere traccia di quando sono state effettuate le modifiche.
{: shortdesc}


### Configurazione delle versioni dell'oggetto {: #setting-up-versioning}

Puoi configurare le versioni di ogni oggetto nel tuo contenitore utilizzando il parametro `X-Versions-Location`. Per farlo, crea un contenitore aggiuntivo per mantenere le vecchie versioni dei tuoi oggetti nel seguente modo.

Puoi configurare le versioni dell'oggetto tramite il client Swift o utilizzando i comandi cURL.
* Se stai utilizzando il client Swift, esegui il seguente comando:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* Se stai utilizzando cURL, puoi configuralo in questo modo:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**Nota**: gli oggetti nel tuo contenitore di backup saranno automaticamente denominati con il  seguente formato: `<Length><Object_name>/<Timestamp>`.
<table>
  <tr>
    <th> Attributo</th>
    <th> Descrizione</th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> La lunghezza del nome del tuo oggetto. Questo è un numero esadecimale a 3 caratteri senza zeri. </td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> Il nome del tuo oggetto. </td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> La data/ora in cui questa versione dell'oggetto è stata caricata originalmente. </td>
  </tr>
</table>

### Disabilitazione delle versioni dell'oggetto. {: #disabling-versioning}

Puoi disabilitare le versioni dell'oggetto tramite il client Swift o utilizzando i comandi cURL. 

* Per utilizzare il client Swift esegui il seguente comando:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Esegui il seguente comando cURL per disabilitare le versioni:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### Esercitazione sulle versioni dell'oggetto {: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

Puoi utilizzare la seguente esercitazione per ottenere una descrizione del ciclo di vita completo delle versioni dell'oggetto.

1. Crea un contenitore denominato `container_one`.

    ```
    swift post container_one
    ```
    {: pre}
    
3. Crea un secondo contenitore con il nome `container_two`.

    ```
    swift post container_two
    ```
    {: pre}
    
2. Configura le versioni.

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. Carica un oggetto nel tuo contenitore principale per la prima volta.

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. Carica una nuova versione dell'oggetto in container_one. Quando carichi una nuova versione del tuo file, la versione precedente viene automaticamente spostata nel contenitore di backup che hai specificato quando hai configurato le versioni.

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. Per visualizzare la nuova versione del tuo file nel contenitore, elenca gli oggetti in container_one.

    ```
    swift list container_one
    ```
    {: pre}
    
9. Elenca gli oggetti in container_two. La versione precedente del tuo file sarà archiviata in questo contenitore.

    ```
    swift list container_two
    ```
    {: pre}
    
10. Elimina l'oggetto in container_one. Quando elimini l'oggetto, la versione precedente nel tuo contenitore di backup sarà automaticamente spostata nel tuo contenitore principale.

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. Elenca entrambi i contenitori. Il tuo file originale in `container_one` e `container_two` sarà vuoto.

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
