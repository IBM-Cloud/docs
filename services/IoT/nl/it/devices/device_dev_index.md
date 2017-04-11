---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Sviluppo dei dispositivi su {{site.data.keyword.iot_short_notm}}
{: #device_dev_index}

Un dispositivo è qualsiasi cosa che dispone di una connessione a internet e dispone di dati da inviare o ricevere dal cloud. Puoi utilizzare i dispositivi per inviare informazioni sull'evento come le letture del sensore al cloud e per accettare i comandi dalle applicazioni nel cloud.

I dispositivi pubblicano i dati in {{site.data.keyword.iot_short_notm}}utilizzando gli eventi. Il dispositivo controlla il contenuto dell'evento e assegna un nome ad ogni evento che viene inviato. Quando un evento viene ricevuto da {{site.data.keyword.iot_short_notm}} da un dispositivo, le credenziali della connessione sulla quale è stato ricevuto l'evento vengono utilizzate per determinare da quale dispositivo è stato inviato l'evento. Questa architettura impedisce a un dispositivo di impersonarne un altro.

Per ulteriori informazioni sui concetti chiave, inclusi i dispositivi, consulta [Informazioni su Watson IoT Platform](https://console.ng.bluemix.net/docs/services/IoT/iotplatform_overview.html#watsoniotplatform_importantconcepts).


# Collegamento del tuo dispositivo a {{site.data.keyword.iot_short_notm}}
{: #device_connect}
Puoi collegare il tuo dispositivo a {{site.data.keyword.iot_short_notm}} utilizzando i protocolli HTTP o MQTT. Utilizza HTTP se desideri configurare uno scenario richiesta-risposta, come quando qualcuno effettua un acquisto e riceve un riconoscimento. Utilizza MQTT se desideri configurare uno scenario dell'evento, come quando qualcuno suona a un campanello e provoca l'attivazione di un avviso in un dispositivo mobile.

Un dispositivo deve essere registrato con un'organizzazione prima che possa essere collegato a {{site.data.keyword.iot_full}}. Per il collegamento sicuro a {{site.data.keyword.iot_short_notm}}, devi registrare un account Bluemix e creare la tua propria organizzazione {{site.data.keyword.iot_short_notm}}. Puoi quindi registrare il tuo dispositivo utilizzando questo ID dell'organizzazione. I dispositivi registrati si identificano per {{site.data.keyword.iot_short_notm}} con un identificativo del dispositivo univoco, ad esempio un indirizzo MAC e un token di autenticazione che viene accettato solo per quel dispositivo. Una volta eseguita la connessione sicura, utilizza Bluemix per creare le tue proprie applicazioni. Prova ad utilizzare Node-RED per collegare le tue applicazioni tra loro.

Se desideri collegarti a un dispositivo senza averlo registrato, ad esempio per eseguire una prova di utilizzo, puoi farlo utilizzando l'ID organizzazione speciale `QuickStart`. `QuickStart` è un'istanza sandbox pubblica di {{site.data.keyword.iot_short_notm}} eseguita nel cloud. Se non hai bisogno di collegarti in modo sicuro, puoi utilizzare `QuickStart` per verificare la connettività del tuo dispositivo e provare ad utilizzare {{site.data.keyword.iot_short_notm}}. Quando hai terminato la prova, ricollega il tuo dispositivo in modo sicuro alla tua propria istanza dell'ID dell'organizzazione specifica utilizzando TLS e il tuo token di autenticazione.

Per ulteriori informazioni sulla connessione del tuo dispositivo a {{site.data.keyword.iot_short_notm}} utilizzando il protocollo HTTP, consulta [API REST HTTP per i dispositivi](https://console.ng.bluemix.net/docs/services/IoT/devices/api.html).
Per ulteriori informazioni sulla connessione del tuo dispositivo a {{site.data.keyword.iot_short_notm}} utilizzando il protocollo MQTT, consulta [Connettività MQTT per i dispositivi](https://console.ng.bluemix.net/docs/services/IoT/devices/mqtt.html).

# Introduzione allo sviluppo dei dispositivi
{: #get_started}
Se disponi di un dispositivo che è già abilitato per {{site.data.keyword.iot_short_notm}}, puoi semplicemente iniziare ad utilizzarlo.

Se il tuo dispositivo non è ancora abilitato, controlla le ricette disponibili in [developerWorks](https://developer.ibm.com/recipes/). Sfoglia le ricette esistenti per controllare se è presente una ricetta per il tuo dispositivo e utilizzala come supporto per iniziare a sviluppare. Puoi anche pubblicare le tue proprie ricette se lo desideri.

Se non puoi trovare una ricetta per il tuo dispositivo in particolare, IBM fornisce alcune guide di programmazione e API che puoi utilizzare come introduzione. Queste guide contengono librerie client, esempi e informazioni che possono aiutarti nella creazione e sviluppo del codice per l'integrazione e il collegamento dei tuoi dispositivi e applicazioni a {{site.data.keyword.iot_short_notm}}. Le seguenti guide di programmazione sono al momento disponibili:

- Java
- Node.js
- Embedded C
- ARM mBed C++
- Python
- C#
- Node-RED

Per ulteriori informazioni e link alle guide di programmazione disponibili, consulta [Librerie client per lo sviluppo {{site.data.keyword.iot_short_notm}}](../iot_platform_client_lib.html).

Se non riesci a trovare una guida di programmazione {{site.data.keyword.iot_short_notm}} idonea, puoi scrivere il tuo proprio programma e utilizzare il protocollo MQTT o HTTP per collegare il tuo dispositivo a {{site.data.keyword.iot_short_notm}}.

MQTT è un open standard gestito dagli standard OASIS (organization and international recognized by ISO). Per ulteriori informazioni, consulta [OASIS Message Queuing Telemetry Transport ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.oasis-open.org/committees/tc_home.php?wg_abbrev=mqtt){: new_window}.

È disponibile un'ampia varietà di librerie client MQTT per molti sistemi differenti, inclusi i seguenti ambienti:
- http://www.eclipse.org/paho/
- https://github.com/mqtt/mqtt.github.io/wiki/software?id=software

Per ulteriori informazioni su MQTT, consulta [Messaggistica MQTT](https://console.ng.bluemix.net/docs/services/IoT/reference/mqtt/index.html?pos=3).
