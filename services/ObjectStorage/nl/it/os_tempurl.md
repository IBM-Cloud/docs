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


# Creazione di un URL temporaneo {: #create-temporary-url}

Un URL temporaneo è un URL lungo e difficile da indovinare che può essere utilizzato per uno specifico periodo di tempo per scaricare oggetti senza che sia richiesta ulteriore autenticazione o per fornire l'accesso completo all'account di archiviazione.
{: shortdesc}


1. Identifica le tue informazioni di autenticazione stampando le tue informazioni sull'account con il seguente comando:

  ```
  swift stat
  ```
  {: pre}
  **Nota**: prendi nota della stringa completa dietro *Account*, incluso `AUTH_`.

2. Imposta una chiave segreta. Scegli una stringa lunga, casuale e difficile da indovinare. Per impostare la chiave, esegui il seguente comando:

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
  <caption> Tabella 1. Argomenti posizionali URL temporanei </caption>
    <tr>
      <th> Argomento </th>
      <th> Descrizione </th>
    </tr>
    <tr>
      <td> <i> method </i> </td>
      <td> GET per consentire lo scaricamento. PUT per consentire il caricamento. </td>
    </tr>
    <tr>
      <td> <i> seconds </i> </td>
      <td> Il tempo in secondi in cui l'URL temporaneo è disponibile. </td>
    </tr>
    <tr>
      <td> <i> path </i> </td>
      <td> Il percorso completo dell'oggetto espresso come <code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i></code>. </td>
    </tr>
    <tr>
      <td> <i> key </i> </td>
      <td> La chiave segreta da te impostata al passo 2. </td>
    </tr>
  </table>

5. Facoltativo: Aggiunge l'URL restituito al tuo nome cluster per ottenere un URL completo. Puoi quindi utilizzare l'URL completo per scaricare gli oggetti con qualsiasi client HTTP compatibile come cURL, wget o Firefox.
