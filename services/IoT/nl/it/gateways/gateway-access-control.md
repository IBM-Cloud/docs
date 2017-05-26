---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-20"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Controllo dell'accesso al gateway
{: #gateway-access-control}

I dispositivi gateway sono autorizzati ad agire per conto di altri dispositivi. I gruppi di risorse gateway definiscono in una organizzazione quali gateway possono interagire al posto di quali dispositivi. Ai gateway può essere assegnato il ruolo *Gateway standard*. I gateway standard possono soltanto pubblicare o sottoscrivere i messaggi al posto dei dispositivi nel loro gruppo di risorse.
{: #shortdesc}


Per informazioni sulla pubblicazione degli eventi dai dispositivi gateway utilizzando le API, consulta [API di messaggistica HTTP per i dispositivi gateway](../gateways/gw_intro_api.html).

## Assegnazione di un ruolo a un gateway
{: #gw_roles}

L'assegnazione di un ruolo a un gateway è obbligatoria per permettere al gateway di avere di un gruppo di risorse. I gateway senza un gruppo di risorse possono agire al posto di tutti i dispositivi nell'organizzazione. L'assegnazione automatica del ruolo *Gateway standard* crea un nuovo gruppo di risorse per il gateway. Quando un gateway viene assegnato a un gruppo di risorse, può agire solo al posto dei dispositivi in tale gruppo di risorse e per se stesso, anche se il suo ruolo viene modificato.

Per assegnare un ruolo a un gateway, utilizza la seguente API:

```
PUT /authorization/devices/{deviceId}/roles
```

Per i dettagli sullo schema della richiesta, consulta la [documentazione API {{site.data.keyword.iot_full}} Limited Gateway ![icona link esterno](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_authorization_devices_deviceId_roles){: new_window}.

## Aggiunta dei dispositivi e loro rimozione da un gruppo di risorse.
{: #devices_groups}

Prima che un gateway con il ruolo *Gateway standard* possa agire al posto di un dispositivo, esso deve essere un membro del gruppo di risorse assegnato al gateway. Per aggiungere molti dispositivi a un gruppo di risorse contemporaneamente, utilizza la seguente API:

```
 PUT /bulk/devices/{groupId}/add
```

Il gruppo a cui aggiungere i dispositivi deve essere specificato nel percorso della richiesta e i dispositivi da aggiungere devono essere specificati nel corpo della richiesta. Per ulteriori informazioni sullo schema della richiesta e sulle risposte, consulta la [documentazione API {{site.data.keyword.iot_short_notm}} Limited Gateway ![icona link esterno](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_add){: new_window}.

Per rimuovere più dispositivi da un gruppo di risorse, utilizza la seguente API:

```
PUT /bulk/devices/{groupId}/remove
```

I dispositivi specificati nel corpo della richiesta saranno rimossi dal gruppo specificato nel percorso della richiesta. Per ulteriori informazioni sullo schema della richiesta e sulla risposta, consulta la [documentazione API {{site.data.keyword.iot_short_notm}} Limited Gateway ![icona link esterno](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/put_bulk_devices_groupId_remove){: new_window}.

## Ricerca di un gruppo di risorse
{: #finding_groups}

I gruppi di risorse possono avere associate tag di ricerca. La ricerca delle tag può essere utilizzata per richiamare i dettagli di un gruppo di risorse utilizzando la seguente API:

```
GET /groups
```

Questa API restituisce i gruppi di risorse associati alla tag di ricerca utilizzata. Se non viene specificata alcuna tag di ricerca, vengono restituiti tutti i gruppi di risorse. <!-- For more information about the request schema, response, and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

È possibile trovare un ID del gruppo di risorse utilizzando la seguente API:

```
GET /authorization/devices/{deviceId}
```

Questa API restituisce l'identificativo univoco dei gruppi di risorse di cui questo dispositivo è membro. Ulteriori informazioni su questa API possono essere trovate nella [documentazione API {{site.data.keyword.iot_short_notm}} Limited Gateway ![icona link esterno](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_authorization_devices_deviceId){: new_window}.


## Query di un gruppo di risorse
{: #querying_groups}

È possibile eseguire la query dei gruppi di risorse in vari parametri per restituire le proprietà complete di tutti i dispositivi nel gruppo, gli identificativi univoci di tutti i dispositivi nel gruppo o le proprietà del gruppo di risorse.

Per restituire le proprietà complete di tutti i dispositivi nel gruppo di risorse specificato, utilizza la seguente API:

```
GET /bulk/devices/{groupId}
```

Questa API restituisce l'elenco delle proprietà complete di tutti i membri del gruppo di risorse specificato. Per ulteriori informazioni sullo schema della richiesta, sulle risposte e su come sfogliare i risultati, consulta la [documentazione API {{site.data.keyword.iot_short_notm}} Limited Gateway ![icona link esterno](../../../icons/launch-glyph.svg "External link icon")](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002-beta/security-gateway-beta.html#!/Limited_Gateway/get_bulk_devices_groupId){: new_window}.

Per restituire solo gli identificativi univoci dei membri del gruppo di risorse, utilizza la la seguente API:

```
GET /bulk/devices/{groupId}/ids
```

Questa API restituisce gli identificativi univoci di tutti i dispositivi che sono membri del gruppo di risorse. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per restituire le proprietà del gruppo di risorse, utilizza la seguente API:

```
GET /groups/{groupId}
```

Questa API restituisce le proprietà del gruppo di risorse (nome, descrizione, tag di ricerca e identificativo univoco) specificate nel percorso, ma non restituisce l'elenco dei membri del gruppo di risorse. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Creazione ed eliminazione di un gruppo di risorse.
{: #crt_del_groups}

I gruppi di risorse possono essere creati ed eliminati indipendentemente dalla connessione ai gateway. Per creare un gruppo di risorse, utilizza la seguente API:

```
POST /groups
```

Questa API crea un gruppo di risorse e restituisce i dettagli del gruppo. <!-- For details on the request schema and the responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per eliminare un gruppo di risorse, utilizza la seguente API:

```
DELETE /groups/{groupId}
```

Questa API elimina il gruppo di risorse specificato. I dispositivi che sono membri del gruppo vengono eliminati dal gruppo, ma i dispositivi stessi non sono altrimenti interessati. <!-- For more information, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

## Aggiornamento delle proprietà del gruppo
{: #update_groups}

  - /groups/{groupId}
    - PUT: aggiorna le proprietà del gruppo specificato.

## Richiamo e aggiornamento delle proprietà del dispositivo.
{: #fdevice_group_props}

Esistono diversi modi per richiamare le proprietà del dispositivo utilizzando l'API, ogni API restituisce informazioni diverse. Per richiamare le proprietà del dispositivo di tutti i dispositivi collegati alla tua organizzazione {{site.data.keyword.iot_short_notm}}, utilizza la seguente API:

```
GET /authorization/devices

```

Questa API restituisce le proprietà di tutti i dispositivi collegati all'organizzazione, incluse le loro proprietà rilevanti per il controllo dell'accesso (ruolo, stato, data di scadenza). <!-- For more information on responses and how to page through results, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per richiamare le proprietà del dispositivo senza richiamare le informazioni rilevanti per il controllo dell'accesso, utilizza la seguente API:

```
GET /authorization/devices/{deviceId}
```

Questa API restituisce tutte le proprietà del dispositivo specificato, senza restituire le informazioni sul controllo dell'accesso .<!-- For more information, see the [{{site.data.keyword.iot_short_notm}} device model documentation](LINK TO DEVICE MODEL) and [API documentation](LINK TO CORRECT API). -->

Per richiamare le informazioni sul controllo dell'accesso di un dispositivo specifico, utilizza la seguente API:

```
GET /authorization/devices/{deviceId}/roles
```

Questa API richiama le informazioni rilevanti per il controllo dell'accesso per il dispositivo specificato senza restituire altre proprietà del dispositivo. <!-- For more information on the request schema and responses, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Le proprietà del dispositivo possono essere aggiornate in due modi. Le proprietà possono essere aggiornate senza modificare le proprietà del controllo dell'accesso o le proprietà del controllo dell'accesso possono essere modificate direttamente.

Per aggiornare le proprietà del dispositivo senza influenzare le proprietà del controllo dell'accesso, utilizza la seguente API:

```
PUT /authorization/devices/{deviceId}
```

Questa API aggiornerà solo le proprietà del dispositivo non associate al controllo dell'accesso. <!-- For more information on request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->

Per aggiornare solo le proprietà del controllo dell'accesso di un dispositivo specifico, utilizza la seguente API:

```
PUT /authorization/devices/{deviceId}/withroles
```

Questa API aggiornerà solo le proprietà del controllo dell'accesso del dispositivo specificato. <!-- For more information on the request schema, see the [{{site.data.keyword.iot_short_notm}} API documentation](LINK TO CORRECT API). -->
