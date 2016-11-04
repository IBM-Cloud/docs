---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Dateien schützen{: #understanding-authentication}
*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

## OpenStack Identity (Keystone) v3 {: #keystone-authentication}

Durch die Bereitstellung einer neuen {{site.data.keyword.objectstorageshort}}-Instanz wird in der IBM Public Cloud ein isoliertes Keystone-Projekt erstellt.
{: shortdesc}

Die Struktur der Berechtigungsnachweise enthält einen vollständigen Satz von Attributen, sodass Sie die Methode für die OpenStack-Tokenanforderung oder das OpenStack-SDK auswählen können, das sich am besten für Ihre App eignet. Wenn Sie eine neue App an die Instanz binden, wird ein neuer Keystone-Benutzer mit Zugriff auf das Projekt erstellt. Wenn Sie die Instanz löschen, werden auch Projekt und Benutzer gelöscht.

Weitere Informationen zur Verwendung von OpenStack Swift und Keystone sind auf der [OpenStack-Dokumentationssite](http://docs.openstack.org) verfügbar.

Die empfohlene v3-Tokenanforderung ist eine POST-Anforderung an https://identity.open.softlayer.com/v3/auth/tokens, wie im folgenden curl-Befehl gezeigt:

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

Verwenden Sie den Wert des Felds `X-Subject-Token` aus dem Antwortheader als `X-Auth-Token`, wenn Sie Anforderungen an den {{site.data.keyword.objectstorageshort}}-Service senden.

Eine Beispielantwort könnte wie folgt aussehen. Die Antwort wird so abgeschnitten, dass nur die für {{site.data.keyword.objectstorageshort}} releventen Informationen angezeigt werden.

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

Die {{site.data.keyword.objectstorageshort}}-URL befindet sich im Servicekatalog. Der Servicekatalog ist im Antworthauptteil der Tokenanforderung enthalten. Die Antwort ist ein vollständiger Katalog der OpenStack-Services, die verfügbar sind. Wählen Sie den Endpunkt im Servicekatalog mit dem Typ `object-store` und mit der Region aus, die dem Feld für die Region in den Berechtigungsnachweisen entspricht.

**Anmerkung:** Verwenden Sie die allgemein zugängliche Schnittstelle (`publicURL`). Auf die interne Schnittstelle (`internalURL`) kann von {{site.data.keyword.Bluemix_notm}} aus nicht zugegriffen werden.


## Informationen zu Berechtigungsnachweisen{: #understanding-credentials}

Serviceberechtigungsnachweise werden zur Bereitstellung der Authentifizierung und Sicherheit für den Service verwendet. Bei der Bereitstellung einer Instanz wird automatisch ein Satz von Berechtigungsnachweisen generiert. Der Swift-Client entnimmt die Authentifizierungsinformationen den Umgebungsvariablen in der folgenden Tabelle:

<table>
  <tr>
    <th> Umgebungsvariable</th>
    <th> Beschreibung</th>
  </tr>
  <tr>
    <td> `OS_USER_ID` </td>
    <td> Ihre {{site.data.keyword.objectstorageshort}}-Benutzer-ID.</td>
  </tr>
  <tr>
    <td> `OS_PASSWORD` </td>
    <td> Das Kennwort für Ihre {{site.data.keyword.objectstorageshort}}-Instanz.</td>
  </tr>
  <tr>
    <td> `OS_PROJECT_ID` </td>
    <td> Ihre Projekt-ID.</td>
  </tr>
  <tr>
    <td> `OS_REGION_NAME` </td>
    <td> Die Region, in der Ihre Objekte gespeichert sind. {{site.data.keyword.objectstorageshort}} steht in den Regionen Dallas und London zur Verfügung.</td>
  </tr>
  <tr>
    <td> `OS_AUTH_URL` </td>
    <td> Die Endpunkt-URL. Achten Sie darauf, am Ende der URL die Angabe `/v3` hinzuzufügen. </td>
  </tr>
</table>

*Tabelle 1: Variablen und Beschreibungen für die Authentifizierung*

####  Serviceberechtigungsnachweise in der Benutzerschnittstelle hinzufügen
1. Klicken Sie auf der Registerkarte **Serviceberechtigungsnachweise** in Ihrem Serviceinstanz-Dashboard auf **Neuer Berechtigungsnachweis** und benennen Sie diesen.
2. (*Optional*) Geben Sie in das Textfeld **Lineare Konfigurationsparameter hinzufügen** die Informationen zu dem Berechtigungsnachweis für die Rolle ein, die Sie erstellen wollen. Die Informationen müssen als JSON-Nutzdaten formatiert sein. Weitere Informationen zu {{site.data.keyword.objectstorageshort}}-Benutzerrollen finden Sie unter [Zugriffstypen](../os_security.html#access-types).
    - Zum Erstellen eines Benutzers mit Administratorberechtigungen: `{"role":"admin"}`
    - Zum Erstellen eines Benutzers ohne Administratorberechtigungen: `{"role":"member"}`
3. Klicken Sie auf **Hinzufügen**.


## Zugriffstypen {: #access-types}

Der Zugriff auf den Service wird durch Benutzerrollen und Zugriffssteuerungslisten für Container gesteuert. {{site.data.keyword.objectstorageshort}}-Benutzer können Benutzer mit Administratorberechtigungen oder Benutzer ohne Administratorberechtigungen sein. Zugriffssteuerungslisten werden durch Administratorbenutzer auf der Containerebene aktiviert und sind für die Serviceinstanz, das Speicherkonto oder auf Projektebene nicht verfügbar.

<table>
  <tr>
    <th> Benutzer mit Administratorberechtigungen (admin) </th>
    <th> Benutzer ohne Administratorberechtigungen (member) </th>
  </tr>
  <tr>
    <td> Zugriffssteuerung verwalten </td>
    <td> Standardmäßig kein Zugriff auf den Service oder seine Container </td>
  </tr>
  <tr>
    <td> Container erstellen und löschen </td>
    <td> Aktionen abhängig von den Lese-/Schreibzugriffssteuerungslisten der Container </td>
  </tr>
  <tr>
    <td> Containerinhalt lesen und schreiben </td>
    <td> Durch den Administrator festgelegte Aktionen </td>
  </tr>
</table>

*Tabelle 2: Definierte Benutzerrollen*

Sie können {{site.data.keyword.objectstorageshort}}-Benutzer über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle, die Cloud Foundry-API oder die Cloud Foundry CLI verwalten.




## Lesezugriff erteilen{: #read-access}

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit Administratorrolle kann einem anderen Benutzer Lesezugriff auf einen Container erteilen und verschiedene ACL-Kombinationen für Lesezugriff angeben.

<table>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Lesezugriffssteuerung (Read ACL) </th>
  </tr>
  <tr>
    <td> Lesen für alle Referrer unabhängig von der Kontozuordnung </td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für alle Referrer und Listen </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> `< Projekt-ID>:< Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für angegebenen Benutzer in jedem Projekt </td>
    <td> `<*>:< Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in angegebenem Projekt </td>
    <td> `< Projekt-ID>:<*>` </td>
  </tr>
  <tr>
    <td> Lesen und Auflisten für jeden Benutzer in jedem Projekt  </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabelle 3: Lesezugriffsberechtigungen nach Option*



1. Authentifizieren Sie Ihre Berechtigungsnachweise. Sie können entweder die Berechtigungsnachweise aus der Registerkarte 'Serviceberechtigungsnachweise' der Benutzerschnittstelle verwenden oder neue Berechtigungsnachweise generieren. Weitere Informationen zum Generieren neuer Berechtigungsnachweise finden Sie unter [Serviceberechtigungsnachweise generieren](insert link here). Sie erhalten Ihre {{site.data.keyword.objectstorageshort}}-URL und das Authentifizierungstoken als Ausgabe.
    Swift-Befehl:
    
    ```
    export OS_USER_ID=<Benutzer-ID>
  export OS_PASSWORD=<Kennwort>
  export OS_TENANT_ID=<Projekt-ID>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<Region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}
    
    cURL-Befehl:
    
    ```
    curl -i -H "X-Auth-User: <Benutzer-ID>" -H "X-Auth-Key: <Kennwort>" <Authentifizierungs-URL>
    ```
    {: pre}
    
2. Führen Sie folgenden Befehl aus, um Lesezugriff zu erteilen:
    Swift-Befehl:
    
    ```
    swift post <Containername> --read-acl "<Benutzer-ID>:<Projekt-ID>"
    ```
    {: pre}
    
    cURL-Befehl:
    
    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <Tenant-ID>:<Projekt-ID>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}
    **Hinweis**: Verwenden Sie zum Trennen der Zugriffssteuerungslisten ein Komma (,).


3. Überprüfen Sie den Wert für die Lesezugriffssteuerungsliste (Read ACL).
    Swift-Befehl:
    
    ```
    swift stat <Containername>
    ```
    {: pre}
    cURL-Befehl:
    
    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
    
    In der folgenden Beispielausgabe sehen Sie, dass Lesezugriff erteilt wurde:
    
    ```
    HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
    ```
    {: screen}



## Schreibzugriff erteilen{: #write-access}

Ein {{site.data.keyword.objectstorageshort}}-Benutzer mit Administratorrolle kann einem anderen Benutzer Schreibzugriff auf einen Container erteilen und verschiedene ACL-Kombinationen für Schreibzugriff angeben.

<table>
  <tr>
    <th> Berechtigung </th>
    <th> Optionen für Schreibzugriffssteuerung (Write ACL) </th>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in bestimmtem Projekt </td>
    <td> `<Projekt-ID>:<Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Schreiben für angegebenen Benutzer in jedem Projekt </td>
    <td> `*:<Benutzer-ID>` </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in angegebenem Projekt </td>
    <td> `<Projekt-ID>:<*>` </td>
  </tr>
  <tr>
    <td> Schreiben für jeden Benutzer in jedem Projekt </td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*Tabelle 4: Schreibzugriffsberechtigungen nach Option*




1. Authentifizieren Sie Ihre Berechtigungsnachweise mit den Informationen in den Serviceberechtigungsnachweisen, die Sie erstellt haben.  Sie erhalten Ihre {{site.data.keyword.objectstorageshort}}-URL und das Authentifizierungstoken als Ausgabe.
    Swift-Befehl:
    
    ```
    export OS_USER_ID="<user_id>"
    export OS_PASSWORD="<password>"
    export OS_TENANT_ID=<project_id>
    export OS_AUTH_URL=https://identity.open.softlayer.com/v3
    export OS_REGION_NAME=<region>
    export OS_IDENTITY_API_VERSION=3
    export OS_AUTH_VERSION=3

    swift auth
    ```
    {: codeblock}
    
    cURL-Befehl:
    
    ```
    curl -i -H "X-Auth-User:<Benutzer-ID>" -H "X-Auth-Key:<Kennwort>" https://identity.open.softlayer.com/v3
    ```
    {: pre}
    
2. Führen Sie folgenden Befehl aus, um Schreibzugriff zu erteilen:
    Swift-Befehl:
    
    ```
    swift post <Containername> --write-acl "<Benutzer-ID>:<Projekt-ID>"
    ```
    {: pre}
    
    cURL-Befehl:
    
    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <Benutzer-ID>: <Projekt-ID>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}
    
    **Hinweis**: Verwenden Sie zum Trennen der Zugriffssteuerungslisten ein Komma (,).

3. Überprüfen Sie den Wert für die Schreibzugriffssteuerungsliste (Write ACL).
    Swift-Befehl:
    
    ```
    swift stat <Containername>
    ```
    {: pre}
    
    cURL-Befehl:
    
    ```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
    ```
    {: pre}



## Zugriff entfernen {: #removing-access}

Gehen Sie wie folgt vor, um Lesezugriffssteuerungslisten von einem Container zu entfernen:
* Swift-Befehl:

    ```
    swift post <Containername> --read-acl “”
    ```
    {: pre}
    
*  cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Gehen Sie wie folgt vor, um Schreibzugriffssteuerungslisten von einem Container zu entfernen:

* Swift-Befehl:

    ```
    swift post <Containername> --write-acl “”
    ```
    {: pre}
    
*  cURL-Befehl:

    ```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
    {: pre}

Überprüfen Sie, ob eine Zugriffssteuerungsliste (ACL) entfernt wurde:

* Swift-Befehl:

    ```
    swift stat <Containername>
    ```
    {: pre}

  Die folgende Beispielausgabe zeigt sowohl die Lesezugriffssteuerung (Read ACL) als auch die Schreibzugriffssteuerung (Write ACL) leer an, d. h. der Zugriff wurde entfernt.
  
  ```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8
  ```
  {: screen}

* cURL-Befehl:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
  {: pre}
