---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2016-11-18"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Messaggistica MQTT
{: #ref-mqtt}

MQTT è il protocollo primario che i dispositivi e le applicazioni utilizzano per comunicare con {{site.data.keyword.iot_full}}. MQTT è un protocollo di trasporto di messaggistica di sottoscrizione e pubblicazione progettato per lo scambio efficiente dei dati in tempo reale tra il sensore e i dispositivi mobili.
{:shortdesc}

MQTT viene seguito su TCP/IP e mentre è possibile eseguire la codifica direttamente in TCP/IP, puoi anche scegliere di utilizzare una libreria che gestisce i dettagli del protocollo MQTT al tuo posto. Sono disponibili un'ampia gamma di librerie client MQTT. IBM contribuisce allo sviluppo e al supporto di librerie di client diversi, inclusi quelli che sono disponibili nei seguenti siti:

- [MQTT community wiki](https://github.com/mqtt/mqtt.github.io/wiki)
- [Eclipse Paho project](http://eclipse.org/paho/)

## Supporto versione
{: #version-support}
Per informazioni sulle versioni di MQTT supportate da  {{site.data.keyword.iot_short_notm}}, consulta
[Requisiti e standard](../standards_and_requirements.html#mqtt).

## Client applicazione, dispositivo e gateway
{: #device-app-clients}

In {{site.data.keyword.iot_short_notm}}, le classi di oggetti primarie sono i dispositivi e le applicazioni. Un gateway è una classe secondaria del dispositivo.

Il tuo client MQTT identifica se stesso per il servizio {{site.data.keyword.iot_short_notm}} come una classe di oggetti. La classe di oggetti determina le funzionalità del client quando è collegato. La classe di oggetti determina inoltre il meccanismo per l'autenticazione client.

Le applicazioni e i dispositivi funzionano con spazi argomento MQTT differenti.  I dispositivi operano all'interno di uno spazio argomenti in ambito dispositivo, mentre le applicazioni hanno accesso completo allo spazio argomenti per un'intera organizzazione. Per ulteriori informazioni, consulta i seguenti argomenti:

- [Messaggistica MQTT per i dispositivi](../../devices/mqtt.html)
- [Messaggistica MQTT per le applicazioni](../../applications/mqtt.html)
- [Messaggistica MQTT per i gateway](../../gateways/mqtt.html)

### Messaggi conservati
{{site.data.keyword.iot_short_notm}} fornisce supporto limitato per la funzione dei messaggi conservati della messaggistica MQTT. Se l'indicatore dei messaggi conservati è impostato su true in un messaggio MQTT inviato da un dispositivo, un gateway o un'applicaizone a {{site.data.keyword.iot_short_notm}}, il messaggio viene gestito come un messaggio non conservato. Le organizzazioni {{site.data.keyword.iot_short_notm}} non sono autorizzate a pubblicare i messaggi conservati. Il servizio {{site.data.keyword.iot_short_notm}} sovrascrive l'indicatore del messaggio conservato quando viene impostato su true ed elabora il messaggio come se l'indicatore fosse impostato su false.

## Livelli di QOS (quality of service)
{: #qos-levels}

Il protocollo MQTT fornisce tre qualità del servizio per la consegna dei messaggi tra i client e i server: "Al massimo una volta", "Almeno una volta" e "Esattamente una volta".
Mentre puoi inviare eventi e comandi utilizzando un qualsiasi livello di servizio, devi attentamente considerare quale è il livello di servizio corretto ai tuoi bisogni. QOS (quality of service) di livello '2' non sempre è un'opzione migliore del livello '0'.

### Al massimo una volta (QoS0)

Il livello QOS (quality of service) "Al massimo una volta" (QoS0) è il modo più veloce per trasferire i dati e alcune volte è chiamato "Attiva e dimentica". Il messaggio viene consegnato al massimo una volta o potrebbe non essere consegnato affatto. La consegna nella rete non viene riconosciuta e il messaggio non viene memorizzato. Potrebbe essere perso in caso di disconnessione del client o errore del server.

Il protocollo MQTT non richiede server per inoltrare le pubblicazioni al QOS (quality of service) di livello '0' a un client. Se il client è disconnesso nel momento in cui il server riceve la pubblicazione, la pubblicazione potrebbe essere eliminata, a seconda dell'implementazione del server.

**Suggerimento:** quando invii dati in tempo reale in un intervallo, utilizza il QOS (quality of service) di livello 0. Se viene perso un solo messaggio, non è molto importante perché un altro messaggio che contiene dati più recenti sarà inviato entro breve. In questo scenario, il costo extra dell'utilizzo di un QOS (quality of service) superiore non da alcun vantaggio tangibile.

### Almeno una volta (QoS1)

Con il QOS (quality of service) di livello 1 (QoS1), il messaggio viene sempre consegnato almeno una volta. Se si verifica un errore prima della ricezione di una conferma da parte del mittente, un messaggio può essere consegnato più volte. Il messaggio deve essere memorizzato localmente dal mittente finché non riceve la conferma che il messaggio è stato pubblicato dal ricevente. Il messaggio viene memorizzato nel caso in cui debba essere inviato nuovamente.

### Esattamente una volta (QoS2)

Il livello 2 QOS (quality of service) "Esattamente una volta" (QoS2) è il più sicuro, ma la modalità di trasferimento più lenta. Il messaggio viene sempre consegnato almeno una volta e deve anche essere archiviato localmente dal mittente finché non riceve la conferma che il messaggio è stato pubblicato dal ricevente. Il messaggio viene memorizzato nel caso in cui debba essere inviato nuovamente. Con il livello di QOS (quality of service) 2, viene utilizzata una sequenza di ricezione e sincronizzazione più sofisticata che per il livello 1 per assicurare che i messaggi non vengano duplicati.

**Suggerimento:** quando invii i comandi, se desideri la conferma che solo il comando specificato sarà avviato e che lo sarà solo una volta, utilizza il livello QOS (quality of service) 2. Questo è un esempio di quando il sovraccarico del livello 2 può essere vantaggioso rispetto agli altri livelli.

## Sottoscrizione buffer e ripulitura sessione
{: #subscription-buffers-and-clean-session}

A ogni sottoscrizione da un dispositivo o da applicazione viene assegnato un buffer di 5000 messaggi.  Il buffer consente ad ogni applicazione o dispositivo di stare dietro all'elaborazione dei dati live e anche di creare un backlog che comprende fino a 5000 messaggi in sospeso per ogni sottoscrizione fatta. Quando il buffer è pieno, i messaggi più vecchi vengono scartati quando viene ricevuto un nuovo messaggio.

Utilizza l'opzione della sessione di pulitura MQTT per accedere al buffer della sottoscrizione. Quando la sessione di pulitura è impostata su false, il sottoscrittore riceve i messaggi dal buffer. Quando la sessione di pulitura è impostata su true, il buffer viene reimpostato.

**Nota:** i limite del buffer della sottoscrizione si applica indipendentemente dall'impostazione QOS (quality of service) utilizzata. È possibile che un messaggio inviato al livello 1 o 2 possa non essere consegnato a un'applicazione che non riesce a stare dietro alla frequenza dei messaggi per la sottoscrizione fatta.

## Limitazioni payload del messaggio
{: #message-payload}

{{site.data.keyword.iot_short_notm}} supporta l'invio e la ricezione dei messaggi in qualsiasi formato consentito dallo standard MQTT. MQTT è indipendente dai dati per cui è possibile inviare immagini, testo con qualsiasi codifica, dati crittografati e virtualmente qualsiasi tipo di dati nel formato binario. Tuttavia, esistono alcune limitazioni per casi di utilizzo specifici.   

Esistono anche delle limitazioni di dimensione per il payload del messaggio in {{site.data.keyword.iot_short_notm}}.

### Restrizioni del formato del payload del messaggio

Il payload del messaggio può contenere qualsiasi stringa valida, tuttavia i formati JSON ("json"), testo ("text") e binario ("bin") sono i formati comunemente più utilizzati rispetto agli altri tipi di formato.

La seguente tabella illustra le restrizioni del payload del messaggio per diversi tipi di formato:

Formato payload  | Linee guida per casi di utilizzo specifici
--------- | ----------  
JSON | JSON è il formato standard per {{site.data.keyword.iot_short_notm}}. Se prevedi di utilizzare le analisi, le tabelle, le schede e i dashboard {{site.data.keyword.iot_short_notm}} integrati, assicurati che il formato del payload del messaggio sia conforme al testo JSON con formato corretto.
Testo | Utilizza una codifica del carattere UTF-8 valida.
Binario | Nessuna restrizione.


### Dimensione del payload del messaggio massima

**Importante:** la dimensione del payload massima in {{site.data.keyword.iot_short_notm}} è 131072 byte. I messaggi con un payload maggiore del limite sono rifiutati. Il client collegato viene inoltre scollegato e viene visualizzato un messaggio nei log di diagnostica, come descritto nel seguente esempio di messaggio del dispositivo:

`Connessione da x.x.x.x chiusa. La dimensione del messaggio è troppo elevata per questo endpoint.`

## Intervallo keepalive MQTT
{: #mqtt-keep-alive}

L'intervallo keepalive MQTT, misurato in secondi, definisce il tempo massimo che può passare senza comunicazione tra il client e il broker. Il client MQTT deve assicurare che, in assenza di qualsiasi altra comunicazione con il broker, sia inviato un pacchetto PINGREQ. L'intervallo keepalive consente al client e al broker di individuare la rete malfunzionante, determinando una connessione broker, senza attendere che venga raggiunto il periodo di timeout TCP/IP.

Se i tuoi client {{site.data.keyword.iot_short_notm}} MQTT utilizzano le sottoscrizioni condivise, il valore dell'intervallo keepalive può essere impostato solo tra 1 e 3600 secondi. Se viene richiesto un valore di 0 o maggiore di 3600, il broker {{site.data.keyword.iot_short_notm}} imposta l'intervallo keepalive su 3600 secondi.
