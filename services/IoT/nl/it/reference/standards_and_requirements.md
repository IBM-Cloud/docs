---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}
# Requisiti e standard
{: #standards_and_requirements}

{{site.data.keyword.iot_full}} supporta vari standard e requisiti per la messaggistica e lo sviluppo dell'applicazione e del dispositivo generale.
{:shortdesc}


<!-- ## Blockchain
{: #blockchain}

{{site.data.keyword.iot_short_notm}} supports the following versions of the Hyperledger fabric:
- 0.5

## Python
{: #python}

Support for MQTT over SSL requires at least Python v2.7.9 or v3.4, and OpenSSL v1.0.1.
-->

## MQTT
{: #mqtt}

{{site.data.keyword.iot_short_notm}} supporta le seguenti versioni del protocollo di messaggistica MQTT.

Versione MQTT | Note
--- | --- | ---
[3.1.1 ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](https://www.oasis-open.org/standards#mqttv3.1.1){: new_window} (recommended)  | <ul><li>Standard OASIS<li>Standard ISO (ISO/IEC PRF 20922) <li>Migliore interoperabilità tra vari client e server grazie a una definizione più accurata del protocollo in confronto alla V3.1.   <li>La lunghezza massima dell'identificativo client MQTT (ClientId) è stata aumentata a 256 rispetto al limite di 23 caratteri imposto dalla V3.1. </br>Il servizio {{site.data.keyword.iot_short_notm}} spesso richiede ID client più lunghi. </br>Gli ID client lunghi sono supportati indipendentemente dalla versione del protocollo MQTT. Tuttavia alcune librerie client V3.1 controllano la lunghezza del valore ClientId e forzano il limite di 23 caratteri.</ul>
3.1 | MQTT V3.1 è la versione del protocollo maggiormente utilizzata oggi.

{{site.data.keyword.iot_short_notm}} supporta tutto il contenuto consentito dallo standard MQTT. MQTT è indipendente dai dati, per cui è possibile inviare immagini, testo con qualsiasi codifica, dati crittografati e virtualmente qualsiasi tipo di dati nel formato binario. Per ulteriori informazioni sullo standard MQTT, consulta le seguenti risorse:
- [MQTT.org ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://mqtt.org/){: new_window}
- [HiveMQ: Introducing MQTT ![Icona link esterno](../../../icons/launch-glyph.svg "Icona link esterno")](http://www.hivemq.com/blog/mqtt-essentials-part-1-introducing-mqtt){: new_window}

Per informazioni sui limiti di dimensione del payload del messaggio e le restrizioni del formato per casi di utilizzo specifici di {{site.data.keyword.iot_short_notm}}, consulta [Messaggistica MQTT](mqtt/index.html).
