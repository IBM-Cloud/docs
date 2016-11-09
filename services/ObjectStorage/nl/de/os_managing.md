---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.objectstorageshort}} regionenübergreifend verwalten{: #multi-regions}
*Letzte Aktualisierung: 19. Oktober 2016*
{: .last-updated}

Der {{site.data.keyword.objectstorageshort}}-Service unterstützt die Speicherregionen Dallas und London. Diese Speicherregionen sind unabhängig von der {{site.data.keyword.Bluemix_notm}}-Region, wie zum Beispiel 'US-South' und 'United Kingdom', in der die {{site.data.keyword.objectstorageshort}}-Serviceinstanz erstellt wurde. Wenn Sie eine Instanz in der {{site.data.keyword.Bluemix_notm}}-Region 'USA-Süden' erstellen, haben Sie Lese- und Schreibzugriff auf Daten in der Speicherregion Dallas oder in der Speicherregion London.
{: shortdesc}

Für die {{site.data.keyword.Bluemix_notm}}-Region 'US-South' ist Dallas die Standardspeicherregion. Für die {{site.data.keyword.Bluemix_notm}}-Region 'United Kingdom' ist London die Standardspeicherregion.  Die {{site.data.keyword.objectstorageshort}}-Benutzerschnittstelle startet immer mit der Standardspeicherregion der {{site.data.keyword.Bluemix_notm}}-Region. Wenn Sie die Region wechseln wollen, klicken Sie auf die Dropdown-Liste für die {{site.data.keyword.objectstorageshort}}-Regionen und wählen eine andere Region aus.

**Anmerkung:** Der {{site.data.keyword.objectstorageshort}}-Service unterstützt keine speicherregionsübergreifende Replikation.

### Zugriff auf mehrere Regionen

Für die Verwendung des {{site.data.keyword.objectstorageshort}}-Service müssen Sie sich [bei OpenStack Keystone authentifizieren](../ObjectStorage/os_security.html#keystone-authentication){: new_window}. Nach der erfolgreichen Authentifizierung werden ein `X-Subject-Token` und die {{site.data.keyword.objectstorageshort}}-Endpunkte in der Antwort zur Verfügung gestellt. Jede Speicherregion verfügt über einen anderen [Zugriffspunkt](../ObjectStorage/os_api.html#access-points).


Beispiel: Wenn Sie einen Container mit dem Namen `my_container` in der Speicherregion Dallas erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von Dallas im curl-Befehl an:

  ```
  curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Sie erhalten folgende Ausgabe:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

Wenn Sie einen Container mit dem Namen `my_container` in der Speicherregion London erstellen wollen, geben Sie wie folgt einen Zugriffspunkt von London im curl-Befehl an:

  ```
  curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAABAABWlw4mwttbb_6G3LnTiGusyoOSEFMG7oTnDYWN1vBZB6XAxUEhe4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5L7lEZyyKQlsgmQWcrch9VOO_OiSKKToORZR7luI-2TrR_JIVZm-8AAS7hLhl9"
  ```
  {: pre}
Sie erhalten folgende Ausgabe:

  ```
  HTTP/1.1 201 Created
  Content-Length: 0
  Content-Type: text/html; charset=UTF-8
  X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
  Date: Thu, 14 Jan 2016 03:16:13 GMT
  ```
  {: screen}

**Hinweis:** Das von Keystone angeforderte `X-Subject-Token` mit der Kennzeichnung `X-Trans-ID` im Beispiel funktioniert in unterschiedlichen Speicherregionen.
