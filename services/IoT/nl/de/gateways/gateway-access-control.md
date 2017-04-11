---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}

# Gateway Access Control (Beta)

**Wichtig**: Diese Funktion ist momentan als begrenzte Betaversion verfügbar.

Gateway-Geräte sind berechtigt, im Namen anderer Geräte zu handeln. Gateway-Ressourcengruppen definieren, im Namen welcher Geräte innerhalb einer Organisation jedes Gateway handeln kann. Gateways kann die Rolle *Standardgateway* zugeordnet werden. Standardgateways können nur im Namen der Geräte aus der zugehörigen Ressourcengruppe Nachrichten publizieren oder subskribieren.
{: #shortdesc}


Informationen zum Publizieren von Ereignissen von Gateway-Geräten mithilfe von APIs finden Sie in [HTTP-Messaging-APIs für Gateway-Geräte](../gateways/gw_intro_api.html).

## Rolle einem Gateway zuordnen
{: #gw_roles}

Einem Gateway muss eine Rolle zugeordnet werden, damit das Gateway über eine Ressourcengruppe verfügen kann. Gateways ohne Ressourcengruppe können im Namen aller Geräte in der Organisation handeln. Beim Zuordnen der Rolle *Standardgateway* wird automatisch eine neue Ressourcengruppe für das Gateway erstellt. Ein Gateway, dem eine Ressourcengruppe zugeordnet ist, kann nur im Namen der Geräte in dieser Ressourcengruppe und im eigenen Namen handeln, selbst wenn die Rolle des Gateways geändert wird.

Verwenden Sie die folgende API, um einem Gateway eine Rolle zuzuordnen:

```
PUT /authorization/devices/{deviceId}/roles
```

Details zu dem Anforderungsschema finden Sie in der Dokumentation für die [{{site.data.keyword.iot_full}}-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}.

## Geräte in einer Ressourcengruppe hinzufügen und entfernen
{: #devices_groups}

Damit ein Gateway mit der Rolle *Standardgateway* im Namen eines Geräts handeln kann, muss das betreffende Gerät Mitglied der Ressourcengruppe sein, die dem Gateway zugeordnet ist. Verwenden Sie die folgende API, um mehrere Geräte gleichzeitig einer Ressourcengruppe hinzuzufügen:

```
 PUT /bulk/devices/{groupId}/add
```

Die Gruppe, der Geräte hinzugefügt werden sollen, muss im Pfad der Anforderung angegeben werden, und die Geräte, die hinzugefügt werden sollen, müssen im Hauptteil der Anforderung angegeben werden. Weitere Informationen zu dem Anforderungsschema und den Antworten finden Sie in der Dokumentation für die [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}.

Verwenden Sie die folgende API, um mehrere Geräte aus einer Ressourcengruppe zu entfernen:

```
PUT /bulk/devices/{groupId}/remove
```

Die im Hauptteil der Anforderung angegebenen Geräte werden aus der Gruppe entfernt, die im Pfad der Anforderung angegeben ist. Weitere Informationen zu dem Anforderungsschema und der Antwort finden Sie in der Dokumentation für die [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}.

## Ressourcengruppe suchen
{: #finding_groups}

Ressourcengruppen können Suchtags zugeordnet werden. Suchtags können verwendet werden, um mithilfe der folgenden API die Details zu einer Ressourcengruppe abzurufen:

```
GET /groups
```

Diese API gibt die Ressourcengruppen zurück, die dem verwendeten Suchtag zugeordnet sind. Wenn kein Suchtag angegeben ist, werden alle Ressourcengruppen zurückgegeben.<!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Die ID einer Ressourcengruppe kann mithilfe der folgenden API gefunden werden:

```
GET /authorization/devices/{deviceId}
```

Diese API gibt die eindeutige Kennung der Ressourcengruppe(n) zurück, der bzw. denen dieses Gerät als Mitglied zugeordnet ist. Weitere Informationen zu dieser API finden Sie in der Dokumentation für die [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window}.


## Ressourcengruppe abfragen
{: #querying_groups}

Beim Abfragen von Ressourcengruppen können verschiedene Parameter verwendet werden, um die vollständigen Eigenschaften aller Geräte in der Gruppe, die eindeutigen Kennungen aller Geräte in der Gruppe oder die Eigenschaften der Ressourcengruppe zurückzugeben.

Verwenden Sie die folgende API, um die vollständigen Eigenschaften für alle Geräte in der angegebenen Ressourcengruppe zurückzugeben:

```
GET /bulk/devices/{groupId}
```

Diese API gibt die vollständige Liste der Eigenschaften für alle Mitglieder der angegebenen Ressourcengruppe zurück. Weitere Informationen zum Anforderungsschema, zu den Antworten und zum Durchblättern der Ergebnisse finden Sie in der Dokumentation für die [{{site.data.keyword.iot_short_notm}}-API ![Symbol für externen Link](../../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}.

Verwenden Sie die folgende API, um nur die eindeutigen Kennungen der Mitglieder der Ressourcengruppe zurückzugeben:

```
GET /bulk/devices/{groupId}/ids
```

Diese API gibt die eindeutigen Kennungen aller Geräte zurück, die Mitglieder der Ressourcengruppe sind. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Verwenden Sie die folgende API, um die Eigenschaften der Ressourcengruppe zurückzugeben:

```
GET /groups/{groupId}
```

Diese API gibt die Eigenschaften der Ressourcengruppe (Name, Beschreibung, Suchtags und eindeutige Kennung) zurück, die im Pfad angegeben ist, jedoch keine Liste der Mitglieder der Ressourcengruppe. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Ressourcengruppe erstellen und löschen
{: #crt_del_groups}

Ressourcengruppen können unabhängig von den verbindenden Gateways erstellt und gelöscht werden. Verwenden Sie die folgende API, um eine Ressourcengruppe zu erstellen:

```
POST /groups
```

Diese API erstellt eine Ressourcengruppe und gibt die Gruppendetails zurück. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Verwenden Sie die folgende API, um eine Ressourcengruppe zu löschen:

```
DELETE /groups/{groupId}
```

Diese API löscht die angegebene Ressourcengruppe. Geräte, die Mitglieder der Gruppe waren, werden aus der Gruppe gelöscht, aber die Geräte an sich bleiben unverändert erhalten. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Gruppeneigenschaften aktualisieren
{: #update_groups}

  - /groups/{groupId}
    - PUT: Aktualisiert die Eigenschaften der angegebenen Gruppe.

## Geräteeigenschaften abrufen und aktualisieren
{: #fdevice_group_props}

Mit der API können Geräteeigenschaften auf verschiedene Arten abgerufen werden. Dabei gibt jede API andere Informationen zurück. Verwenden Sie die folgende API, um die Geräteeigenschaften für alle Geräte abzurufen, die mit Ihrer {{site.data.keyword.iot_short_notm}}-Organisation verbunden sind:

```
GET /authorization/devices:

```

Diese API gibt die Eigenschaften aller mit der Organisation verbundenen Geräte zurück, einschließlich der zugehörigen Eigenschaften für die Zugriffssteuerung wie Rolle, Status und Ablaufdatum.<!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Verwenden Sie die folgende API, um Geräteeigenschaften ohne die zugehörigen Informationen für die Zugriffssteuerung abzurufen:

```
GET /authorization/devices/{deviceId}
```

Diese API gibt alle Geräteeigenschaften für das angegebene Geräte ohne die Zugriffssteuerungsinformationen zurück. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Verwenden Sie die folgende API, um die Zugriffssteuerungsinformationen für ein bestimmtes Gerät abzurufen:

```
GET /authorization/devices/{deviceId}/roles:
```

Diese API gibt die zugehörigen Informationen für die Zugriffssteuerung des angegebenen Geräts ohne die übrigen Geräteeigenschaften zurück. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Die Geräteeigenschaften können mit zwei Methoden aktualisiert werden, entweder durch Aktualisieren ohne Ändern der Zugriffssteuerungseigenschaften oder durch direktes Aktualisieren der Zugriffsteuerungseigenschaften.

Verwenden Sie die folgende API, um Geräteeigenschaften ohne Änderung der Zugriffssteuerungseigenschaften zu aktualisieren:

```
PUT /authorization/devices/{deviceId}
```

Diese API aktualisiert nur Geräteeigenschaften, die nicht der Zugriffssteuerung zugeordnet sind. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Verwenden Sie die folgende API, um nur die Zugriffssteuerungseigenschaften für das angegebene Gerät zu aktualisieren:

```
PUT /authorization/devices/{deviceId}/withroles:
```

Diese API aktualisiert nur die Zugriffssteuerungseigenschaften für das angegebene Gerät. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
