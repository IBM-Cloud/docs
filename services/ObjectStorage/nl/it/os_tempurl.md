---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Creazione di un URL temporaneo {: #create-temporary-url}

*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Un URL temporaneo è un URL lungo e difficile da indovinare che può essere utilizzato per uno specifico periodo per scaricare oggetti senza che sia richiesta ulteriore autenticazione.
{: shortdesc}


1. Identifica le tue informazioni di autenticazione stampando le tue informazioni sull'account con il seguente comando:

    ```
    swift stat
    ```
    {: pre}
    
    **Nota**: individua il campo Account e annota la stringa completa dietro *Account*: compreso `AUTH_`.
2. Imposta una chiave segreta. Questa chiave può essere qualsiasi cosa tu selezioni ma è buona prassi selezionare una stringa lunga, casuale e difficile da indovinare. Per impostare la chiave, esegui il seguente comando: 

    ```
    swift post -m "Temp-URL-Key:<chiave>"
    ```
    {: pre}
    
3. Verifica che `Temp-URL-Key` sia stato impostato correttamente eseguendo il seguente comando.

    ```
    swift stat
    ```
    {: pre}
    
4. Crea un URL temporaneo eseguendo il seguente comando:

    ```
    swift tempurl GET <secondi> <percorso> <chiave>
    ```
    {: pre}
    
    La seguente tabella illustra gli argomenti posizionali che utilizza il comando `tempurl` Swift.
    <table>
      <tr>
        <th> Argomento</th>
        <th> Descrizione</th>
      </tr>
      <tr>
        <td> [metodo] </td>
        <td> GET per consentire lo scaricamento. PUT per consentire il caricamento. </td>
      </tr>
      <tr>
        <td> [secondi]</td>
        <td> Tempo in secondi per cui l'URL temporaneo sarà disponibile. </td>
      </tr>
      <tr>
        <td> [percorso] </td>
        <td> Il percorso completo dell'oggetto espresso come `/v1/<auth_account>/<container_name>/<object_name>`. Per ulteriori informazioni, vedi la documentazione URL [{{site.data.keyword.objectstorageshort}}](/os_api.html#access-points). </td>
      </tr>
      <tr>
        <td> [chiave] </td>
        <td> La chiave segreta da te impostata al passo 2. </td>
      </tr>
    </table>
    *Tabella 2: argomenti posizionali tempurl*
5. (*Facoltativo*): aggiunge l'URL restituito al tuo nome cluster per ottenere un URL completo. Puoi quindi utilizzare l'URL completo per scaricare gli oggetti con qualsiasi client HTTP compatibile come cURL, wget o Firefox. 
