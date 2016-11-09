---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Gestione di {{site.data.keyword.objectstorageshort}} tra le regioni {: #multi-regions}
*Ultimo aggiornamento: 19 ottobre 2016*
{: .last-updated}

Il servizio {{site.data.keyword.objectstorageshort}} supporta le regioni di archiviazione di Dallas e Londra. Queste regioni di archiviazione sono indipendenti dalla regione {{site.data.keyword.Bluemix_notm}}, come Stati Uniti Sud e Regno Unito, in cui viene creata l'istanza
del servizio {{site.data.keyword.objectstorageshort}}. Se crei un'istanza nella regione {{site.data.keyword.Bluemix_notm}} Stati Uniti Sud, puoi leggere e scrivere dati nella regione di archiviazione di Dallas o in quella di Londra.
{: shortdesc}

Per la regione {{site.data.keyword.Bluemix_notm}} Stati Uniti Sud, la regione di archiviazione di Dallas è quella predefinita. Per la regione {{site.data.keyword.Bluemix_notm}} del Regno Unito, la regione di archiviazione di Londra è quella predefinita.  L'interfaccia utente {{site.data.keyword.objectstorageshort}} viene sempre avviata alla regione di archiviazione predefinita della regione {{site.data.keyword.Bluemix_notm}}. Per spostarti da una regione all'altra, fai clic sull'elenco a discesa delle regioni di {{site.data.keyword.objectstorageshort}} e scegline un'altra.

**Nota:** il servizio {{site.data.keyword.objectstorageshort}} NON supporta la replica tra regioni di archiviazione.

### Accesso a più regioni

Per utilizzare il servizio {{site.data.keyword.objectstorageshort}}, devi [eseguire l'autenticazione presso OpenStack Keystone](../ObjectStorage/os_security.html#keystone-authentication){: new_window}. Dopo che hai eseguito correttamente l'autenticazione, un `X-Subject-Token` e gli endpoint {{site.data.keyword.objectstorageshort}} saranno disponibili nella risposta. Ogni regione di archiviazione ha un diverso [punto di accesso](../ObjectStorage/os_api.html#access-points).


Ad esempio, per creare un contenitore denominato `my_container` nella regione di archiviazione di Dallas, specifica un punto di accesso Dallas nel comando curl nel seguente modo: 

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Riceverai il seguente output:

  ```
  HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

Per creare un contenitore denominato `my_container` nella regione di archiviazione di Londra, specifica un punto di accesso Londra nel comando curl nel seguente modo:

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Riceverai il seguente output:

  ```
  HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Nota:** `X-Subject-Token` acquisito da Keystone, etichettato come `X-Trans-ID` nell'esempio, funziona tra più regioni.
