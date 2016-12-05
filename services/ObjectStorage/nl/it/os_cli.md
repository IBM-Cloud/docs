---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Accesso a {{site.data.keyword.objectstorageshort}} utilizzando la CLI Swift {: #using-swift-cli}


Il servizio {{site.data.keyword.objectstorageshort}} è basato su OpenStack Swift ed è possibile accedervi utilizzando qualsiasi applicazione client compatibile. Questa sezione descrive come utilizzare il client Python Swift, che è la CLI (command-line interface) per l'API {{site.data.keyword.objectstorageshort}} e le sue estensioni, per gestire contenitori e file.
{: shortdesc}




## Installazione del client Swift {: #install-swift-client}

Se non lo hai già fatto, installa il seguente [software prerequisito](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}.
* Python 2.7 o successive
* Package setuptools
* Package pip


Per installare il client Python Swift, esegui il seguente comando:
```
pip install python-swiftclient
```
{: pre}

Per installare il client Python Keystone, esegui il seguente comando:
```
pip install python-keystoneclient
```
{: pre}




## Impostazione del client {: #setup-swift-client}

Per configurare il client Swift, devi `esportare` le tue informazioni di autenticazione. Puoi generare le credenziali [tramite la IU](../ObjectStorage/os_security.html#understanding-credentials) o [tramite la CLI](../ObjectStorage/os_cli.html#generating-cli).

Per esportare le informazioni di autenticazione, immetti le tue credenzial ed esegui il seguente comando:
```
export OS_USER_ID=
export OS_PASSWORD=
export OS_PROJECT_ID=
export OS_AUTH_URL=
export OS_REGION_NAME=
export OS_IDENTITY_API_VERSION=
export OS_AUTH_VERSION=

swift auth
```
{: codeblock}


Esempio:
```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
  export OS_PASSWORD=*******
  export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=dallas
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

swift auth
```
{: screen}




## Generazione delle credenziali del servizio {{site.data.keyword.objectstorageshort}} {: #generating-cli}

Per generare le credenziali del servizio utilizzando la CLI Swift, puoi utilizzare la seguente procedura.

1. Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi come utente con un ruolo da sviluppatore. Devi essere posizionato nello spazio dell'istanza del servizio che desideri gestire.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Generare le credenziali del servizio. `service-key-name` è il nome che hai fornito alla credenziale. Puoi utilizzare il comando Cloud Foundry o il comando cURL.
  Comando Cloud Foundry:
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```
  {: pre}

  Esempio di comando Cloud Foundry:
  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'
  ```
  {: screen}

  Comando cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```
  {: pre}

3. Convalida delle credenziali per la chiave del servizio che hai creato.
  Comando Cloud Foundry:
  ```
  cf service-keys <service_instance>
  ```
  {: pre}

  Esempio di chiave del servizio membro per un'istanza denominata Object-Storage-Acl-Test:

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

  Comando cURL:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```
  {: pre}




## Archiviazione degli oggetti nei contenitori tramite la CLI {: #storing-cli}

1. Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Crea un nuovo contenitore {{site.data.keyword.objectstorageshort}} eseguendo il seguente comando. La variabile *container_name* viene impostata, da te, in questo momento.
  ```
  swift post <container_name>
  ```
  {: pre}

**Nota**: se ricevi un messaggio di errore, conferma di aver installato [il software prerequisito](../ObjectStorage/os_cli.html##install-swift-client).

3. (Facoltativo:) Per verificare che il contenitore sia stato creato, esegui il seguente comando per elencare i tuoi contenitori.
  ```
  swift list
  ```
  {: pre}

4. Per prevenire la distruzione di dati a causa di sovrascritture non intenzionali, [configura le versioni dell'oggetto](../ObjectStorage/os_versioning.html#work-with-object-versioning). Se non desideri le versioni dell'oggetto, elenca i tuoi file esistenti in un archivio e se necessario, ridenomina la directory o i file prima del caricamento.

4. Carica un file nel tuo contenitore eseguendo il seguente comando.
  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

**Nota**: per caricare file più grandi di 5GB [sono necessari ulteriori passi](../ObjectStorage/os_large_files.html#large-files).


5. (Facoltativo:) Per verificare che il caricamento ha avuto esito positivo, visualizza il contenuto del tuo contenitore eseguendo il seguente comando:
  ```
  swift list <container_name>
  ```
  {: pre}




## Scaricamento degli oggetti con la CLI Swift {: #downloading-cli}


1.  Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. Per prevenire la distruzione di dati a causa di sovrascritture non intenzionali, [configura le versioni dell'oggetto](../ObjectStorage/os_versioning.html#work-with-object-versioning). Se non desideri le versioni dell'oggetto, elenca i tuoi file esistenti in un archivio e se necessario, ridenomina la directory o i file prima dello scaricamento. 

3. Scarica un file eseguendo il seguente comando:

```
swift download <container_name> <file_name>
```
{: pre}




## Eliminazione degli oggetti e dei contenitori tramite la CLI {: #deleting-cli}

**Attenzione**: se elimini il tuo contenitore, eliminerai tutti gli oggetti archiviati all'interno del contenitore.

1.  Se non hai eseguito l'accesso a {{site.data.keyword.Bluemix_notm}}, accedi all'organizzazione o allo spazio che contiene la tua istanza di {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. (Facoltativo:) Conferma di avere un backup dei tuoi oggetti prima di eliminare i tuoi file e contenitori.

3. Esegui il seguente comando per eliminare un file:
  ```
  swift delete <container_name> <file_name>
  ```
  {: pre}

3. Per eliminare il tuo contenitore, esegui il seguente comando:
  ```
  swift delete <container_name>
  ```
  {: pre}

**Nota**: puoi pianificare un [intervallo di tempo specifico per l'eliminazione del tuo oggetto](../ObjectStorage/os_deletion.html#schedule-object-deletion).




## Utilizzo delle directory {: #directory-cli}

#### Aggiunta di una directory a un contenitore con la CLI Swift

Swift non ha una vera struttura di directory ma utilizza la denominazione per rappresentare un layout di directory. Se specifichi un nome della directory, sarà allegato a tutti i nomi file come parte del relativo percorso.

1. Localmente, crea una directory e salva il tuo file in essa.
2. Esegui il seguente comando per caricare una directory nel tuo contenitore: 
  ```
  swift upload <container_name> <directory_name>
  ```
  {: pre}

#### Download di una directory
Per scaricare una struttura di directory, utilizza il parametro `-prefix` per indicare la directory o la struttura di directory che vuoi scaricare.

1. Esegui il seguente comando per scaricare una directory:
  ```
  swift download <container_name> --prefix <directory>
  ```
  {: pre}
