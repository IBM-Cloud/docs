---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Esempio: trasmissione di log di applicazioni Cloud Foundry a Splunk
{: #splunk}

In questo esempio, uno sviluppatore di nome Jane crea un server virtuale utilizzando dei server virtuali IBM beta e l'immagine Ubuntu.  Jane tenta di trasmettere i log dell'applicazione Cloud Foundry da {{site.data.keyword.Bluemix_notm}} a Splunk.
{:shortdesc}

  1. Per iniziare, Jane configura Splunk.

     a. Jane scarica Splunk Light dal [sito di download di Splunk Light ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}, quindi lo installa utilizzando il seguente comando. Il software viene installato su */opt/splunk*.

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installa e applica le patch al componente aggiuntivo con tecnologia syslog RFC5424 da integrare con {{site.data.keyword.Bluemix_notm}}. Per ulteriori informazioni sulle istruzioni di installazione del componente aggiuntivo, consulta la [Guida Cloud Foundry ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installa il componente aggiuntivo utilizzando i seguenti comandi:

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Quindi, Jane applica la patch al componente aggiuntivo sostituendo */opt/splunk/etc/apps/rfc5424/default/transforms.conf* con un nuovo file *transforms.conf* che comprende il testo seguente:

	    ```
        [rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1

        [rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Una volta impostato Splunk, Jane deve aprire alcune porte sulla macchina Ubuntu per accettare lo scarico syslog in entrata (porta 5140) e Splunk Web UI (porta 8000), poiché il firewall del server virtuale {{site.data.keyword.Bluemix_notm}} è configurato con valori predefiniti.

	    **Nota:** la conferma iptable viene effettuata in questo punto per gli scopi di valutazione di Jane ed è temporanea. Per configurare l'impostazione del firewall nel server virtuale Bluemix produttivo, vedi la documentazione [Network Security Groups ![icona link esterno](../icons/launch-glyph.svg "External link icon")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} contenente informazioni dettagliate.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Quindi, Jane esegue Splunk utilizzando il seguente comando:

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane configura le impostazioni di Splunk in modo da accettare lo scarico syslog da {{site.data.keyword.Bluemix_notm}}. Deve creare un input di dati per lo scarico syslog.

     a. Dall'interfaccia Web Splunk, Jane fa clic su **Dati > Input di dati**. Viene visualizzato un elenco di tipi di input supportati da Splunk.

     b. Seleziona **TCP**, perché lo scarico syslog utilizza il protocollo TCP.

     c. Nel riquadro **TCP**, immette **5140** all'interno del campo **Porta**, lascia gli altri campi vuoti e fa clic su **Avanti**.

     d. Dall'elenco **Tipo di origine**, seleziona **Non categorizzato > rfc5424_syslog**.

     e. Per il tipo di **Metodo**, seleziona **IP**.

     f. Nel campo **Indice**, Jane fa clic su **Crea un nuovo indice**. Dopo aver rinominato il nuovo indice "bluemix", fa clic su **Salva**.

     g. Infine, nella finestra **Riesamina**, Jane conferma che l'impostazione è corretta e fa clic su **Invia** per abilitare l'input di dati.

  3. In {{site.data.keyword.Bluemix_notm}}, Jane crea un servizio di scarico syslog e lo collega a un'applicazione.

     a. Jane crea un servizio di scarico syslog utilizzando il seguente comando dalla cli cf:

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Nota:** *dummyhost* non è il nome reale. Viene utilizzato per nascondere il nome host effettivo.

     b. Jane associa il servizio di scarico syslog a un'applicazione nel proprio spazio, quindi riprepara l'applicazione.

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane testa l'applicazione, quindi digita la seguente stringa di query nell'interfaccia Web di Splunk:

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane visualizza un flusso di log nella propria interfaccia Web Splunk. Sebbene la versione di Splunk installata da Jane sia la Splunk Light, può comunque conservare 500 MB di registri al giorno.

