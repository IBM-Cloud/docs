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

# Utilizzo dell'API REST Swift per accedere a {{site.data.keyword.objectstorageshort}} {: #using-swift-restapi}


Puoi utilizzare l'API REST Swift con un'interfaccia client di riga di comando, come cURL, oppure richiamare l'API dalla tua applicazione.
{: shortdesc}



## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

Il provisioning di una nuova istanza {{site.data.keyword.objectstorageshort}} crea un progetto Keystone isolato in IBM Public Cloud.

La struttura delle credenziali contiene una serie completa di attributi per consentirti di scegliere il metodo di richiesta di token OpenStack o l'SDK OpenStack che meglio si adatta alla tua applicazione. Quando esegui il bind di una nuova applicazione all'istanza, viene creato un nuovo utente Keystone con l'accesso al progetto. Quando effettui il deprovisioning dell'istanza, il progetto e l'utente vengono eliminati.

Per ulteriori informazioni sull'utilizzo di OpenStack Swift e Keystone, consulta il [sito della documentazione di OpenStack](http://docs.openstack.org).

La richiesta di token v3 consigliata è una richiesta POST a https://identity.open.softlayer.com/v3/auth/tokens come mostrato nel seguente comando curl:
```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "XXXXXXXXXX"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
{: codeblock}

Utilizza il valore del campo `X-Subject-Token` dall'intestazione della risposta come campo `X-Auth-Token` quando effettui richieste al servizio {{site.data.keyword.objectstorageshort}}.

Ecco una risposta di esempio. La risposta è snellita per visualizzare solo le informazioni rilevanti di {{site.data.keyword.objectstorageshort}}.
```
	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints": [
			{
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```
{: screen}

L'URL {{site.data.keyword.objectstorageshort}} si trova nel catalogo servizi. Il catalogo servizi è contenuto nel corpo della risposta della richiesta di token. La risposta è un catalogo completo dei servizi OpenStack disponibili. Seleziona l'endpoint dal catalogo dei servizi immettendo `object-store` e la regione che corrisponde al campo regione nelle credenziali.

**Nota:** utilizza l'interfaccia pubblica (`publicURL`). L'interfaccia interna (`internalURL`) non è accessibile da {{site.data.keyword.Bluemix_notm}}.






## Messa a punto del tuo URL {{site.data.keyword.objectstorageshort}} {: #access-points}

Per interagire con l'API {{site.data.keyword.objectstorageshort}}, crea l'URL {{site.data.keyword.objectstorageshort}} nel seguente modo:
  ```
  https://<punto di accesso>/<versione API>/AUTH_<ID progetto>/<spazio dei nomi contenitore>/<object namespace>
  ```
  {: pre}

<table>
  <tr>
    <th> Parti URL  </th>
    <th> Definizione </th>
  </tr>
  <tr>
    <td> Versione API  </td>
    <td> Versione 1: v1 </td>
  </tr>
  <tr>
    <td> Informazioni sull'account  </td>
    <td> Questi sono il tuo ProjectID e prefisso combinati. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Spazio dei nomi del contenitore  </td>
    <td> Il nome del tuo contenitore. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Spazio dei dell'oggetto  </td>
    <td> Il nome del tuo file o oggetto. Può essere trovato nella IU. </td>
  </tr>
  <tr>
    <td> Punto di accesso</td>
    <td> Londra: https://lon.objectstorage.open.softlayer.com/
    <br> Dallas: https://dal.objectstorage.open.softlayer.com/ </br> </td>
  </tr>
</table>

Tabella 1. Parti URL {{site.data.keyword.objectstorageshort}} spiegate 

Ad esempio:

Parti URL ![{{site.data.keyword.objectstorageshort}} visualizzate in un'immagine di esempio](images/Swift_URL.png)





## API {{site.data.keyword.objectstorageshort}} {: #openstack-reference}

Consulta il [Riferimento completo all'API OpenStack Swift](http://developer.openstack.org/api-ref-objectstorage-v1.html) per un elenco completo degli esempi e delle opzioni API REST {{site.data.keyword.objectstorageshort}}.
