---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Status und Datenfluss überwachen
{: #monitor}  
*Letzte Aktualisierung: 17. März 2016*  

Mit der Überwachungsfunktion können Sie den Verbindungsstatus und die Geschwindigkeit des Datenflusses zwischen Ihrem lokal oder auf dem SoftLayer-Server vorhandenen VPN-Gateway und Ihrem {{site.data.keyword.vpn_short}}-Gateway anzeigen. 
{:shortdesc}  
##Im Service-Dashboard überwachen
{: #dashboard}

Wählen Sie die Registerkarte **Überwachung** aus, um die folgende Verbindungsstatistik anzuzeigen.

* **Verbindungsstatus:** Status der VPN-Verbindung zwischen Ihrem lokal oder auf dem SoftLayer-Server vorhandenen VPN-Gateway und dem IBM VPN-Gateway. Werte: 1=UP (aktiv), -1=DOWN (inaktiv) 
* **Geschwindigkeit des ausgehenden Datenverkehrs in Byte/Sekunde und Pakete/Sekunde:** Geschwindigkeit des Datenverkehrs vom IBM VPN-Gateway zu Ihrem lokal oder auf dem SoftLayer-Server vorhandenen VPN-Gateway.  
* **Geschwindigkeit des eingehenden Datenverkehrs in Byte/Sekunde und Pakete/Sekunde:** Geschwindigkeit des Datenverkehrs von Ihrem lokal oder auf dem SoftLayer-Server vorhandenen VPN-Gateway zum IBM VPN-Gateway.  

Die Überwachungsstatistik wird als Diagramme mit Daten aus den letzten 48 Stunden angezeigt. Die Diagramme werden alle 20 Minuten automatisch aktualisiert. Sie können jedoch die neuesten Daten jederzeit abrufen, indem Sie die Registerkarte 'Überwachung' verlassen und wieder zu ihr zurückkehren.

**Hinweis:** In den Diagrammen wird die koordinierte Weltzeit und nicht die Ortszeit verwendet.  
##Mit Logmet überwachen
{: #logmet}

Verwenden Sie [Logmet](https://logmet.{DomainName}), um eine detaillierte Verbindungsstatistik anzuzeigen. 

1. Melden Sie sich mit Ihren Bluemix-Berechtigungsnachweisen und dem Namen des Bereichs und der Organisation an, in der die Instanz des Service IBM VPN erstellt wurde.  
2. Wählen Sie in der rechten oberen Ecke das Ordnersymbol (![](images/folder.png)) aus.
3. Wählen Sie in der Liste der Dashboards **VPN-Service-Überwachung** aus, um die Diagramme anzuzeigen. Für die Diagramme wird die Ortszeit verwendet.  

**Hinweis:** Sie müssen die Registerkarte **Überwachung** im Dashboard des Service IBM VPN mindestens einmal auswählen, damit eine Abfrage an Logmet gesendet und das Dashboard des Service VPN in Logmet erstellt wird. Logmet benötigt nach dem Einrichten der VPN-Verbindung bis zu 10 Minuten, um die Verbindungsstatistik anzuzeigen.


