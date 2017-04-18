---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-07"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Fornitori e dispositivi supportati
{: #supportedcloud}

{{site.data.keyword.iotinsurance_full}} supporta l'integrazione con più dispositivi e fornitori cloud.
{: shortdesc}

## Fornitore e dispositivi supportati
{: #supportedvendors}
La seguente tabella elenca i fornitori e i dispositivi supportati da {{site.data.keyword.iotinsurance_short}} e descrive il tipo di integrazione. Sono disponibili i seguenti tipi di integrazione:

  - **{{site.data.keyword.iot_short_notm}}** - il dispositivo o l'hub pubblica gli eventi del sensore direttamente in {{site.data.keyword.iot_short_notm}}. {{site.data.keyword.iotinsurance_short}} può elaborare gli eventi del sensore direttamente o dopo che il trasformatore {{site.data.keyword.iotinsurance_short}} li abbia lievemente modificati.

  - **Cloud a Cloud** - il dispositivo o l'hub pubblica gli eventi del sensore in cloud di terze parti. Il trasformatore {{site.data.keyword.iotinsurance_short}} legge tali eventi dal cloud di terze parti e li pubblica in {{site.data.keyword.iot_short_notm}}.

<table>
<thead>
<tr>
<th>Nome fornitore</th>
<th>Tipo integrazione</th>
<th>Dispositivi verificati</th>
<th>Informazioni sul fornitore </th>
</tr>
</thead>
<tbody>
<tr>
<td>Bosch E-Call</td>
<td>{{site.data.keyword.iot_short_notm}}.  
È stata scritta un'applicazione gateway per verificare l'integrazione.</td>
<td>Bosch Retrofit E-Call</td>
<td>[Sito web fornitore ![icona link esterno](../../icons/launch-glyph.svg)](http://www.bosch-connectivity.com/en/what_we_offer/products_and_solutions_1/retrofit_ecall/connected_devices_3){: new_window}</td>
</tr>
<tr>
<td>EnOcean</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Pulsante</li>
<li>Contatto</li>
<li>Temperatura</li>
</ul>
</td>
<td>[Sito web fornitore ![icona link esterno](../../icons/launch-glyph.svg)](https://www.enocean.com/en/</td>){: new_window}
</tr>
<tr>
<td>WiButler (iExergy)</td>
<td>{{site.data.keyword.iot_short_notm}}</td>
<td>
<ul>
<li>Rilevatore di fumo</li>
<li>Pulsante</li></td>
</ul>
<td>[Sito web fornitore ![icona link esterno](../../icons/launch-glyph.svg)](https://www.wibutler.com/en_GB){: new_window}</td>
</tr>
<tr>
<td>Wink</td>
<td>Cloud a Cloud</td>
<td>Fuoriuscita d'acqua</td>
<td>[Sito web fornitore ![icona link esterno](../../icons/launch-glyph.svg)](https://www.wink.com/){: new_window}</td>
</tr>
<tr>
<td>Yanzi</td>
<td>{{site.data.keyword.iot_short_notm}} e Cloud a Cloud</td>
<td>Nessun sensore è stato verificato.</td>
<td>[Sito web fornitore ![icona link esterno](../../icons/launch-glyph.svg)](https://ibm.ent.box.com/notes/126680846739){: new_window}</td>
</tr>
</tbody>
</table>

## Integrazione cloud fornitore e dispositivi
{: #integratingdevices}
Puoi integrare i tuoi dispositivi e cloud del fornitore con {{site.data.keyword.iotinsurance_short}}. Le seguenti sezioni forniscono le procedure di integrazione e i record utente di esempio per ogni fornitore.

Per ulteriori informazioni sull'integrazione dei sensori e dei dispositivi, consulta [Toolkit del dispositivo](iotinsurance_device_toolkit.html):


### EnOcean
#### Procedura di integrazione
  1. Crea un gateway nell'istanza {{site.data.keyword.iot_short_notm}} collegato a {{site.data.keyword.iotinsurance_short}}.
  2. Collega l'hub EnOcean al gateway {{site.data.keyword.iot_short_notm}}.
  3. Aggiungi l'identificativo del gateway al record utente in {{site.data.keyword.iotinsurance_short}}.

#### Record utente di esempio

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "digital-concepts-gateway1"
    ],
    ...
}
```

### WiButler (iExergy)

#### Procedura di integrazione
L'integrazione con i dati di WiButler è al momento supportata come una prova di utilizzo o un'anteprima tecnica soltanto e non è pensata per l'utilizzo di produzione. L'hardware WiButler richiede un aggiornamento firmware per eseguire il flusso dei dati a {{site.data.keyword.iot_short_notm}}.

#### Record utente di esempio

```
{
    "username": "user@example.com",
    "password": "",
    "accessLevel": "13",
    "fullname": "John Doe",
    "email": "user@example.com",
    "phonenumber": "+123456789",
    "address": {
      ...
    },
    "gatewayIds": [
      "Wibutler-Gateway-ID"
    ],
    ...
}
```

### Wink

#### Procedura di integrazione

**Opzione 1**
  1. Ottieni i [token di autorizzazione Wink ![icona link esterno](../../icons/launch-glyph.svg)](http://docs.winkapiv2.apiary.io/#){: new_window}.
  2. Aggiungi il token di autorizzazione all'utente corrispondente nel sistema {{site.data.keyword.iotinsurance_short}} utilizzando l'API {{site.data.keyword.iotinsurance_short}}.

**Opzione 2**  
Integra utilizzando l'applicazione mobile (obsoleto). Questo metodo funziona con la versione 1.0 di {{site.data.keyword.iotinsurance_short}}.

#### Record utente di esempio

```
{
  "username": "user@example.com",
  "password": "",
  ....
  "deviceID": "528DB5CA-7F3D-4478-A4EB-994E7F118B6B",
  "assets": [
    {
      "name": "default",
      "providers": [
        {
          "name": "wink",
          "tokens": {
            "data": {
              "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
              "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
              "token_type": "bearer",
              "token_endpoint": "https://api.wink.com/oauth2/token",
              "scopes": "full_access"
            },
            "errors": [],
            "pagination": {},
            "access_token": "fjyw9nN_YhU-fZU9kCqTQ6Ijsr_9XdvO",
            "refresh_token": "OOMyB8JGCHgjOHku8zp2Yrevoeci48Ou",
            "token_type": "bearer",
            "token_endpoint": "https://api.wink.com/oauth2/token",
            "scopes": "full_access"
          }
        }
      ]
    }
  ]
}

```

### Yanzi
#### Procedura di integrazione
**Opzione 1**  
  Aggiungi le credenziali del cloud Yanzi in yanzi-config.json nella directory del fornitore del repository del trasformatore.  L'oggetto "yanziCloud" è l'ubicazione corrente delle credenziali.  

**Opzione 2**  
  Yanzi utilizza un'integrazione cloud-a-cloud tra i cloud Yanzi e {{site.data.keyword.iot_short_notm}}. L'autorizzazione per questa integrazione avviene nel cloud Yanzi. Dopo il completamento dell'autorizzazione, il cloud Yanzi invia gli eventi a {{site.data.keyword.iot_short_notm}}. Devi inoltre aggiungere le credenziali dell'istanza {{site.data.keyword.iot_short_notm}} in yanzi-config.json nella directory del fornitore del repository del trasformatore utilizzando l'oggetto "iotfCredentials".

#### Record utente di esempio

```
{
  "yanziCloud": {
      "cirrusHost": "wss://",
      "username": "",
      "password": "",
      "locationId": "",
      "unitDid": ""
  },
  "iotfCredentials": {
      "org": "",
      "apiKey": "",
      "apiToken": "",
      "type": "shared",
      "mqtt_host": "gbdprt.messaging.internetofthings.ibmcloud.com",
      "domain": "internetofthings.ibmcloud.com"
  }
}
```

### Dati Weather Company
#### Procedura di integrazione
L'integrazione con i dati di Weather Company è al momento supportata come una prova di utilizzo o un'anteprima tecnica soltanto e non è pensata per l'utilizzo di produzione.

Fornisci un indirizzo per richiamare le condizioni meteo correnti (temperatura esterna) da Weather Company per un'ubicazione specifica.



#### Record utente di esempio

```
{ "username": "johndoe",
   "fullname": "John Doe",
    "firstname": "John",
    "lastname": "Doe",
    "password": "",
     "accessLevel": 13,
     "address": "Mies-van-der-Rohe-Straße 6, 80807 München, Germany",
     ...
}

```
