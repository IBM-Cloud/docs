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


# Generazione delle credenziali del servizio {: #credentials}

Le credenziali del servizio sono utilizzate per fornire l'autenticazione e la protezione del servizio. Puoi generare nuove credenziali utilizzando la CLI o la IU {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}


## Per aggiungere le credenziali alla IU:

1. Nella scheda **Credenziali del servizio** nel dashboard della tua istanza del servizio, fai clic su **Nuova credenziale** e forniscile un nome.
2. Facoltativo: Nel campo di testo **Aggiungi i parametri di configurazione incorporati** immetti le informazioni sulla credenziale per il ruolo con il [tipo di accesso](/docs/services/ObjectStorage/os_access_types.html) che desideri fornire. Le informazioni devono essere formattate come payload JSON.
    - Per creare un utente amministrativo: `{"role":"admin"}`
    - Per creare un utente non amministrativo: `{"role":"member"}`
3. Fai clic su **Aggiungi**.


## Per aggiungere le credenziali utilizzando i comandi Cloud Foundry nella CLI:

1. Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi come utente con un ruolo da sviluppatore. Devi essere posizionato nello spazio dell'istanza del servizio che desideri gestire.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Generare le credenziali del servizio. Fornisci un nome alla tua credenziale sostituendo la variabile
`service-key-name`. Facoltativamente, puoi anche assegnare un [ruolo utente](/docs/services/ObjectStorage/os_access_types.html).

  ```
  cf create-service-key "<service_instance_name>" <service-key-name> -c '{"role":"<user_role>"}'
  ```
  {: pre}

  Esempio:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

3. Convalida delle credenziali per la chiave che hai creato.

  ```
  cf service-keys <service_instance_name>
  ```
  {: pre}

  Chiave di esempio per un'istanza denominata Object-Storage-Acl-Test per un utente con un ruolo di membro:

  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  {: screen}



#### Per aggiungere le credenziali utilizzando i comandi cURL nella CLI:

1. Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi come utente con un ruolo da sviluppatore. Devi essere posizionato nello spazio dell'istanza del servizio che desideri gestire.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Esegui il seguente comando per generare le credenziali del servizio.

  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name: <service_instance_name>", "role: <user_role>"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: <content_type" -H "Cookie: <cookie>"
  ```
  {: pre}

  <table>
  <caption> Tabella 1. Variabili della credenziale del servizio spiegate </caption>
    <tr>
      <th> Variabile  </th>
      <th> Spiegazione </th>
    </tr>
    <tr>
      <td> ```https://api.ng.bluemix.net/v2/service_keys``` </td>
      <td> L'endpoint della chiave del servizio.  </td>
    </tr>
    <tr>
      <td><i> service_instance_guid </i></td>
      <td> Può essere trovata nel tuo URL.  </td>
    </tr>
    <tr>
      <td><i> name </i></td>
      <td> Il nome della tua istanza del servizio. </td>
    </tr>
    <tr>
      <td><i> role </i></td>
      <td> Specifica il <a href= /docs/services/ObjectStorage/os_constructing.html>ruolo dell'utente</a>, amministratore o membro. </td>
    </tr>
    <tr>
      <td><i> bearer_token </i></td>
      <td> Il token che hai ricevuto durante l'autenticazione della tua istanza con Keystone. </td>
    </tr>
  </table>

3. Convalida le tue credenziali eseguendo il seguente comando.

  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: screen}
