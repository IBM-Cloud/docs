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


# Autenticazione della tua istanza {{site.data.keyword.objectstorageshort}} con Keystone

Per interagire con il servizio, devi autenticare la tua istanza {{site.data.keyword.objectstorageshort}} con Keystone per ottenere i tuoi URL e token di connessione.
{: shortdesc}


Il provisioning di una nuova istanza {{site.data.keyword.objectstorageshort}} crea un progetto Keystone isolato in IBM Public Cloud. La struttura delle credenziali Keystone contiene una serie completa di attributi in modo che puoi scegliere il metodo di richiesta di token OpenStack o l'SDK OpenStack che meglio si adatta alla tua applicazione. Quando esegui il bind di una nuova applicazione all'istanza, viene creato un nuovo utente Keystone con l'accesso al progetto. Quando effettui il deprovisioning dell'istanza, il progetto e l'utente vengono eliminati.

Per ulteriori informazioni sull'utilizzo di OpenStack Swift e Keystone, consulta il <a href="http://docs.openstack.org" target="_blank">sito della documentazione di OpenStack. <img src="../../icons/launch-glyph.svg" alt="icona link esterno"></a>



1. Effettua una richiesta POST a `https://identity.open.softlayer.com/v3/auth/tokens` come mostrato nel seguente comando cURL.
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

2. Seleziona un endpoint `object-store` dalla risposta del catalogo e prendine nota. Ne hai bisogno per creare il tuo URL completo. Il seguente esempio di risposta è stato snellito per visualizzare solo le informazioni rilevanti di {{site.data.keyword.objectstorageshort}}.

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
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "38b8c081b11a452bb951698c334a406d",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "internal"
  	          },
  	          {
  	            "id" : "4207049680fa4effbecd044c7448a8cb",
                "region" : "dallas",
                "region_id" : "dallas",
                "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
                "interface" : "public"
  	          },
  	          {
  	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
  	            "region" : "london",
  	            "region_id" : "london",
  	            "url" : "https://lon.objectstorage.open.softlayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "public"
  	          },
  	          {
  	            "id" : "a60cf32be624491d89170ef8264de5e8",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
  	            "interface" : "admin"
  	          },
  	          {
  	            "id" : "c769862200124a308d6748e418c971ba",
  	            "region" : "dallas",
  	            "region_id" : "dallas",
  	            "url" : "https://dal.objectstorage.service.open.networklayer.com/v1/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
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

  <table>
  <caption> Tabella 1. Risposta richiesta POST spiegata </caption>
    <tr>
      <th> Endpoint di risposta </th>
      <th> Spiegazione </th>
    </tr>
    <tr>
      <td> <code> X-Subject-Token </code> </td>
      <td> Il tuo token di autenticazione </td>
    </tr>
    <tr>
      <td> <code> id </code> </td>
      <td> Il tuo ID dell'istanza {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> region </code> </td>
      <td> La tua regione di archiviazione. Assicurati di selezionare la regione che corrisponde al campo elencato nelle tue credenziali. </td>
    </tr>
    <tr>
      <td> <code> url </code> </td>
      <td> Il tuo URL {{site.data.keyword.objectstorageshort}}. </td>
    </tr>
    <tr>
      <td> <code> interface </code> </td>
      <td> L'interfaccia interna non è accessibile da {{site.data.keyword.Bluemix_notm}}. Utilizza l'interfaccia pubblica (<code>publicURL</code>). </td>
    </tr>
  </table>
