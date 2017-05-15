---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# Beispiel: Cloud Foundry-Anwendung durch Streaming an Splunk übertragen
{: #splunk}

In diesem Beispiel erstellt eine Entwicklerin namens Jane einen virtuellen Server unter Verwendung von IBM Virtual Servers Beta und dem Ubuntu-Image. Jane versucht, die Cloud Foundry-App-Protokolle aus {{site.data.keyword.Bluemix_notm}} an Splunk durch Streaming zu übertragen.
{:shortdesc}

  1. Zu Anfang richtet Jane Splunk ein. 

     a. Jane lädt Splunk Light von der Website [Download von Splunk Light ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window} herunter und installiert das Produkt mithilfe des folgenden Befehls. Die Software wird in */opt/splunk* installiert. 

	    ```
        dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane installiert und aktualisiert das Add-on RFC5424 für Syslog-Technologie, um Splunk in {{site.data.keyword.Bluemix_notm}} zu integrieren. Weitere Informationen zu den Anweisungen für die Installation des Add-ons finden Sie in der [Cloud Foundry-Anleitung ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}.

	    Jane installiert das Add-on mithilfe der folgenden Befehle: 

	    ```
        cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        Anschließend aktualisiert Jane das Add-on, indem Sie die Datei */opt/splunk/etc/apps/rfc5424/default/transforms.conf* durch eine neue Datei *transforms.conf* ersetzt, die den folgenden Text enthält: 

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

     c. Nach der Einrichtung von Splunk muss Jane einige Ports auf der Ubuntu-Maschine öffnen, um den eingehenden Syslog-Drain (Port 5140) und die Splunk-Webbenutzerschnittstelle (Web UI: Port 8000) zu akzeptieren, weil die Firewall für den virtuellen {{site.data.keyword.Bluemix_notm}}-Server standardmäßig konfiguriert ist. 

	    **Hinweis:** Die Konfiguration der IP-Tabelle ('iptable') erfolgt hier zu Auswertungszwecken für Jane und ist temporär. Details zur Konfiguration der Firewalleinstellung in der Produktionsumgebung des virtuellen Bluemix-Servers finden Sie in der Dokumentation [Network Security Groups ![Symbol für externen Link](../icons/launch-glyph.svg "Symbol für externen Link")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window}. 

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   Dann führt Jane Splunk mit dem folgenden Befehl aus: 

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane konfiguriert die Splunk-Einstellungen so, dass der Syslog-Drain aus {{site.data.keyword.Bluemix_notm}} akzeptiert wird. Sie muss eine Dateneingabe für den Syslog-Drain erstellen. 

     a. Jane klickt in der Splunk-Webschnittstelle auf **Data > Data inputs**. Eine Liste der von Splunk unterstützten Eingabetypen wird angezeigt. 

     b. Sie wählt **TCP** aus, weil der Syslog-Drain das TCP-Protokoll verwendet. 

     c. Im Fenster **TCP** gibt sie in das Feld **Port** den Wert **5140** ein und lässt die übrigen Felder leer. Anschließend klickt sie auf **Next**. 

     d. In der Liste **Source Type** wählt Sie den Quellentyp **Uncategorized > rfc5424_syslog** aus. 

     e. Für den Typ im Feld **Method** wählt sie **IP** aus. 

     f. Im Feld **Index** klickt sie auf **Create a new index**. Sie gibt dem neuen Index den Namen "bluemix" und klickt auf **Save**. 

     g. Schließlich bestätigt Jane im Fenster **Review**, dass die Einstellung korrekt ist, und klickt auf **Submit**, um diese Dateneingabe zu aktivieren. 

  3. In {{site.data.keyword.Bluemix_notm}} erstellt Jane einen Syslog-Drain-Service und bindet den Service an eine App. 

     a. Jane erstellt den Syslog-Drain-Service mithilfe des folgenden Befehls über die CF-CLI: 

     ```
     cf cups splunk -l syslog://dummyhost:5140
     ```

     **Hinweis:** *dummyhost* ist nicht der reale Name. Dies dient zur Verschleierung des tatsächlichen Hostnamens. 

     b. Jane bindet den Syslog-Drain-Service an eine App in ihrem Bereich und führt ein erneutes Staging der App durch. 

	 ```
     cf bind-service myapp splunk
     cf restage myapp
     ```


Jane probiert ihre App aus und gibt anschließend die folgende Abfragezeichenfolge in der Splunk-Webschnittstelle ein: 

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane wird ein Datenstrom von Protokollen in ihrer Splunk-Webschnittstelle angezeigt. Obwohl Jane Splunk Light installiert hat, kann sie 500 MB an Protokollen pro Tag aufbewahren. 

