---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Configurazione di host log esterni
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} conserva in memoria una quantità limitata di informazioni di log. Quando si registrano le informazioni, i dati precedenti vengono sostituiti con le informazioni più recenti. Per conservare tutte le informazioni di log, puoi salvare i tuoi log in un log host esterno, quale un servizio di gestione log di terze parti o un altro host.
{:shortdesc}

Per trasmettere i log dalla tua applicazione e dal sistema a un host log esterno, completa la seguente procedura:

  1. Determina l'endpoint di registrazione.

	 Puoi inviare i log a un aggregatore di log di terze parti, quale ad esempio Papertrail, Splunk o Sumologic. Puoi anche inviare i log a un host syslog, un host syslog crittografato con TLS (Transport Layer Security) o un endpoint HTTPS POST. I metodi per ottenere gli endpoint di registrazione variano per i diversi host log.

  2. Crea un'istanza del servizio fornito dall'utente.

	 Utilizza il comando `cf create-user-provided-service` (o `cups`, una versione breve del comando) per creare un'istanza del servizio fornita dall'utente:
	 ```
	 cf create-user-provided-service <nome_servizio> -l <endpoint_registrazione>
	 ```
	 &lt;service_name&gt;

	 Il nome dell'istanza di servizio fornita dall'utente.

	 &lt;endpoint_registrazione&gt;

	 L'endpoint di registrazione a cui invia i log {{site.data.keyword.Bluemix_notm}}. Fai riferimento alla seguente tabella per sostituire *endpoint_registrazine* con il tuo valore:

	 <table>
	 <caption>Tabella 1. Valori dell'endpoint di registrazione</caption>
     <thead>
     <tr>
     <th>Endpoint_registrazione</th>
     <th>Comando</th>
	 <th>Note</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog host</td>
     <td>`cf cups my-logs -l syslog://HOST:PORTA`</td>
	 <td>Ad esempio, per consentire la registrazione in Papertrail, immetti `cf cups my-logs -l syslog://<papertrail-url>`. Sostituisci `<papertrail-url>` con l'URL del tuo endpoint di registrazione proveniente da Papertrail.</td>
     </tr>
	 <tr>
     <td>syslog-tls host</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORTA`</td>
	 <td>Il certificato deve essere garantito da un'autorità di certificazione. Non utilizzare certificati autofirmati.</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORTA`</td>
	 <td>Questo endpoint deve trovarsi sull'Internet pubblico e deve essere accessibile da {{site.data.keyword.Bluemix_notm}}</td>
     </tr>
     </tbody>
     </table>
  3. Esegui il bind dell'istanza del servizio alla tua applicazione.

	 Utilizza il seguente comando per eseguire il bind dell'istanza del servizio alla tua applicazione:

	 ```
	 cf bind-service <appname> <nome_servizio>
	 ```
	 &lt;appname&gt;

	 Il nome della tua applicazione.

	 &lt;nome_servizio&gt;

	 Il nome dell'istanza di servizio fornita dall'utente.

  4. Riprepara l'applicazione.
     Immetti `cf restage appname` per rendere effettive le modifiche.

