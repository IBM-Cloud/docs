---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Configurazione delle versioni dell'oggetto {: #setting-up-versioning}

Le versioni dell'oggetto ti consentono di mantenere le vecchie versioni dei tuoi oggetti archiviandole automaticamente in un contenitore di backup. Questo ti permette di visualizzare la cronologia di ogni oggetto e tenere traccia di quando sono state effettuate le modifiche.
{: shortdesc}

Quando carichi una nuova versione del tuo file nel tuo contenitore principale, la versione precedente viene automaticamente spostata nel contenitore di backup. Se elimini il file dal tuo contenitore principale, la versione più recente viene automaticamente spostata dal tuo contenitore di backup nel contenitore principale per sostituire il file eliminato.

1. Crea un contenitore e forniscigli un nome. Sostituisci la variabile *container_name* con il nome che desideri fornire al tuo contenitore.

    ```
    swift post <container_name>
    ```
    {: pre}

2. Crea un secondo contenitore da utilizzare come archivio di backup e forniscigli un nome.

    ```
    swift post <backup_container_name>
    ```
    {: pre}

3. Configura le versioni.

    Comando Swift:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

    Comando cURL:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. Carica un oggetto nel tuo contenitore principale per la prima volta.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

5. Fai una modifica al tuo oggetto.

6. Carica la nuova versione dell'oggetto nel tuo contenitore principale.

    ```
    swift upload <container_name> <object>
    ```
    {: pre}

7.  Gli oggetti nel tuo contenitore di backup vengono automaticamente denominati con il seguente formato: `<Length><Object_name>/<Timestamp>`.
  <table>
    <tr>
      <th> Attributo </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i>Length</i> </td>
      <td> La lunghezza del nome del tuo oggetto. Questo è un numero esadecimale a 3 caratteri senza zeri. </td>
    </tr>
    <tr>
      <td> <i>Object_name</i> </td>
      <td> Il nome del tuo oggetto. </td>
    </tr>
    <tr>
      <td> <i>Timestamp</i> </td>
      <td> La data/ora in cui questa versione dell'oggetto è stata caricata originalmente. </td>
    </tr>
  </table>

  Tabella 1: Denominazione degli attributi descritti

6. Elenca gli oggetti nel tuo contenitore principale per visualizzare la nuova versione del tuo file.

    ```
    swift list --lh <container_name>
    ```
    {: pre}

7. Elenca gli oggetti nel tuo contenitore di backup. La versione precedente del tuo file viene archiviata in questo contenitore. Tieni presente che è stata aggiunta una data/ora al tuo file.

    ```
    swift list --lh <backup_container_name>
    ```
    {: pre}

8. Elimina l'oggetto dal tuo contenitore principale. Quando elimini l'oggetto, la versione più recente nel tuo contenitore di backup viene automaticamente rispostata nel tuo contenitore principale.

    ```
    swift delete <container_name> <object>
    ```
    {: pre}

9. Facoltativo: disabilita le versioni dell'oggetto.

    Comando Swift:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    Comando cURL:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
