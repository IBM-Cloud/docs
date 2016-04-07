---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Gestione di risorse {: #manage-assets}

Una delle capacità di {{site.data.keyword.iotrtinsights_full}} è quella di associare i tuoi dispositivi alle tue risorse gestite e di creare delle regole che si applicano a tutti i dispositivi associati a una risorsa.
{: shortdesc}

Ad esempio, una singola risorsa che sei interessato a monitorare può includere diversi dispositivi e un gran numero di sensori.

>**Suggerimento:** puoi ripetere la procedura di associazione quando le tue risorse vengono aggiornate o modificate. Il parametro `action`  nei file di contesto e di associazione ti consente di aggiungere e rimuovere risorse e dispositivi.

Per associare i tuoi dispositivi alle tue risorse:
1. Crea un elenco di risorse e salva come un file CSV.
Questo file include i dati risorsa dal tuo software di gestione risorse.
Formato file di esempio:
```
ASSETNUM,ASSETTYPE,AS_DESCRIPTION,AS_DESCRIPTION_LD,INSTALLDATE,AS_ITEMNUM,AS_ITEMSETID,AS_LOCATION,PRIORITY,PURCHASEPRICE,REPLACECOST,SERIALNUM,AS_SITEID,AS_STATUS,ACTION
5001,FACILITIES,New Asset 1,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123451,MYSITE,OPERATING,+
5002,FACILITIES2,New Asset 2,,2015-03-16,1001,ITEMSET,CONFRMA1,1,1000,1200,123452,MYSITE,OPERATING,+
```
{: codeblock}

  Dove:  
  - ASSETNUM - **Obbligatorio:** il numero di ID risorsa nel tuo sistema.(12)
  - ASSETTYPE - il tipo di risorsa. (15)
  - AS_DESCRIPTION - una breve descrizione della risorsa. (100)
  - AS_DESCRIPTION_LD - una descrizione completa della risorsa. (32,000)
  - INSTALLDATE - (la data in formato aaaa-MM-gg) la data in cui la risorsa è stata installata.
  - AS_ITEMNUM - un numero elemento correlato per la risorsa. (30)
  - AS_ITEMSETID - il numero di serie di elementi per la risorsa. (8)
  - AS_LOCATION - l'ubicazione della risorsa. (12)
  - PRIORITY - (numero intero) la priorità della risorsa. (12)
  - PURCHASEPRICE - (decimale) il prezzo di acquisto della risorsa. (10.2)
  - REPLACECOST - (decimale) il costo per sostituire la risorsa. (10.2)
  - SERIALNUM - il numero di serie della risorsa. (64)
  - AS_SITEID - l'ID del sito in cui è installata la risorsa. (8)
  - AS_STATUS - lo stato della risorsa. (20)
  - ACTION - un simbolo `+` significa che la risorsa viene aggiunta e un simbolo `-` significa che la risorsa viene rimossa.  
  >**Suggerimento:** il numero tra parentesi indica la lunghezza massima della stringa. Se non diversamente indicato, il formato del parametro consiste di caratteri alfanumerici, maiuscoli e minuscoli.
5. Crea un file di associazione di risorse e dispositivi e salvalo come un file CSV.
Questo file viene utilizzato per associare le risorse importate nell'elenco risorse ai tuoi dispositivi {{site.data.keyword.iot_short}}.
  Formato file di esempio:
  ```
  sourceType,sourceId,targetType,targetId,action
  d:orgid:iot-device-type,device001,asset,5001,+
  d:orgid:iot-device-type,device002,asset,5002,+
  d:orgid:iot-device-type,device003,asset,5002,+
  ```
  {: screen}   

  Dove:
    - sourceType - consiste nei seguenti dati {{site.data.keyword.iot_short}} per il tuo dispositivo:
      - orgid - il tuo ID organizzazione {{site.data.keyword.iot_short}}
      - iot-device-type - il tuo tipo di dispositivo {{site.data.keyword.iot_short}}  
    - sourceID - il tuo ID dispositivo {{site.data.keyword.iot_short}}  
    - targetType - utilizza la parola `asset` per creare un'associazione di risorse.
    - targetID - la voce ASSETNUM per la risorsa dal file di contesto da te creato
    - action - un simbolo `+` significa che la risorsa viene associata e un simbolo `-` significa che la risorsa viene rimossa dall'associazione.
2. Accedi alla console {{site.data.keyword.iotrtinsights_short}} come un utente amministratore.
2. Vai a **Dispositivi > Gestisci gruppi di dispositivi** e fai clic su **Importa risorsa**.  
3. Individua e seleziona il file di risorse da te creato.
4. Fai clic su ![icona Crea.](images/create.png "Icona Crea") per creare l'elenco di risorse.
3. Individua e seleziona il file di associazione di risorse e dispositivi da te creato.
4. Fai clic su ![icona Crea.](images/create.png "Icona Crea") per creare l'elenco di risorse.
5. Vai a **Dispositivi > Gestisci gruppi di dispositivi** e fai clic su una delle tue risorse per visualizzare un elenco dei dispositivi che hai associato alla risorsa.
