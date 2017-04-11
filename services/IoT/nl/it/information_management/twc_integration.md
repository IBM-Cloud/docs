---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Utilizza i dati di The Weather Company con i tuoi dispositivi
{: #weathercompany}

L'estensione Weather Company ti permette di combinare i dati meteo con i tuoi dispositivi {{site.data.keyword.iot_short_notm}} esistenti.
{:shortdesc}

I dati da Weather Company sono visualizzati nella vista dei dettagli del dispositivo se è stata effettuata una richiesta di ubicazione aggiornata utilizzando l'API o se il dispositivo ha già impostato la sua ubicazione utilizzando un messaggio di gestione del dispositivo.

**Importante:** solo i dispositivi gestiti possono impostare le proprie ubicazioni. Tutti i dispositivi non gestiti devono avere le loro ubicazioni impostate manualmente utilizzando l'API. Per ulteriori informazioni sull'impostazione di un'ubicazione del dispositivo, consulta [Richieste di aggiornamento dell'ubicazione](../../devices/device_mgmt/index.html#update-location).

### API REST per Weather Company
Per accedere all'API REST per Weather Company, consulta la sezione
Device Location Weather nella [Documentazione {{site.data.keyword.iot_short_notm}} HTTP REST API ![icona link esterno](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/v0002.html#!/Device_Location_Weather){: new_window}.

### Visualizzazione dei dati meteo 

Per visualizzare i dati meteo richiamati per un'ubicazione del dispositivo: 
1. Fai clic sul dispositivo nel pannello **Devices**.
2. Nella vista del dispositivo dettagliata scorri fino alla sezione **Extensions**.  
Sono elencati i seguenti dati meteo:
 - Meteo corrente.
 - Temperatura corrente.
 - Temperatura massima e minima previste.
 - Umidità relativa.
 - Pressione.
 - Visibilità.
 - Velocità del vento.
 - Direzione del vento.
 - Latitudine.
 - Longitudine.

<!-- Weather data from The Weather Company extension can be retrieved by using the API. For information on the Weather Company API, see [The Weather Company API documentation ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/swagger/ext-twc.html){: new_window}. -->
