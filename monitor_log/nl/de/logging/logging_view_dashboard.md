---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Protokoll über die Bluemix-Konsole analysieren
{: #analyzing_logs_bmx_ui}

In {{site.data.keyword.Bluemix}} können Sie Protokolle über die Registerkarte für Protokolle, die für jede Cloud Foundry-App bzw. jeden Docker-Container verfügbar ist, anzeigen, filtern und analysieren.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} Public bietet integrierte Protokollierungsfunktionen an. Wenn Sie Ihre Anwendungen zum Beispiel in Cloud Foundry (CF) ausführen, werden Protokolldaten aus Systemkomponenten, die mit Ihrer Anwendung interagieren, zu Ihrer Anwendung und sogar Protokolldaten aus Ihrer Anwendung erfasst, wenn Sie die Standardausgabe (STDOUT) und die Standard-Fehlerausgabe (STDERR) verwenden. 

Beachten Sie die folgenden Informationen zur Verfügbarkeit von Protokolldaten für die Analyse und Protokollspeicherung: 

* In {{site.data.keyword.Bluemix_notm}} Public werden Protokolldaten standardmäßig sieben Tage lang gespeichert.  
* Sie können bis zu 1 GB an Daten pro Tag speichern.  
* Die Protokolle, die für die Analyse über die {{site.data.keyword.Bluemix_notm}}-Konsole verfügbar sind, umfassen standardmäßig Daten für den Zeitraum der letzten 24 Stunden. 

**Tipp:** Wenn Sie Daten für einen angepassten Zeitraum analysieren wollen, der vor den letzten 24 Stunden liegt, finden Sie weitere Informationen unter [Erweiterte Protokollanalyse mit Kibana](logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana).  

##  Protokolle einer Cloud Foundry-App aufrufen
{: #launch_logs_tab_bmx_ui_cf}

Führen Sie die folgenden Schritte aus, um die Bereitstellungs- und Laufzeitprotokolle einer Cloud Foundry-App anzuzeigen: 

1. Klicken Sie im Dashboard 'Apps' auf den Namen Ihrer Cloud Foundry-App.  
    
2. Klicken Sie auf der App-Detailseite auf **Protokolle**. 
    
    Auf der Registerkarte **Protokolle** können Sie die letzten Protokolle für Ihre App oder Protokollendabschnitte in Echtzeit anzeigen. Darüber hinaus können Sie Protokolle nach Komponente (Protokolltyp), App-Instanz-ID und nach Fehler filtern.
    

##  Protokolle eines Docker-Containers aufrufen
{: #launch_logs_tab_bmx_ui_containers}

Führen Sie die folgenden Schritte aus, um Bereitstellungs- oder Laufzeitprotokolle eines Docker-Containers anzuzeigen: 

1. Klicken Sie im Dashboard 'Apps' auf einen einzelnen Container oder eine Containergruppe.  
    
2. Klicken Sie auf der App-Detailseite auf **Überwachung und Protokolle**. 

3. Wählen Sie **Protokollierung** aus. 
    
    Auf der Registerkarte **Protokollierung** können Sie die letzten Protokolle für Ihren Container oder Protokollendabschnitte in Echtzeit anzeigen.  

## Protokollformat für CF-App-Protokolle
{: #log_format_cf}

Protokolle für {{site.data.keyword.Bluemix_notm}}-Cloud Foundry-Apps werden in einem festen Format ähnlich dem folgenden Muster angezeigt: 

<code><var class="keyword varname">Komponente</var>/<var class="keyword varname">Instanz-ID</var>/<var class="keyword varname">Nachricht</var>/<var class="keyword varname">Zeitmarke</var></code>

Jeder Protokolleintrag enthält die folgenden Felder: 

| Feld | Beschreibung |
|-------|-------------|
| Zeitmarke | Die Zeit der Protokollanweisung. Die Zeitmarke ist bis auf die Millisekunde definiert. |
| Komponente | Die Komponente, die das Protokoll generiert. Eine Liste der verschiedenen Komponenten finden Sie unter [Protokollquellen für CF-Apps](logging_cf_apps.html#logging_bluemix_cf_apps_log_sources). <br> Auf jeden Komponententyp folgt ein Schrägstrich und eine Ziffer, die die Anwendungsinstanz angibt. 0 ist die Ziffer, die der ersten Instanz zugeordnet ist, 1 die der zweiten usw. |
| Nachricht | Die Nachricht, die von der Komponente ausgegeben wird. Die Nachricht variiert abhängig vom Kontext. |



## Protokollformat für Containerprotokolle
{: #log_format_containers}

Protokolle für Container werden in einem festen Format ähnlich dem folgenden Muster angezeigt: 

<code><var class="keyword varname">Zeitmarke</var>/<var class="keyword varname">Maschine</var>/<var class="keyword varname">Nachricht</var>  </code>

Jeder Protokolleintrag enthält die folgenden Felder: 

| Feld | Beschreibung |
|-------|-------------|
| Zeitmarke | Die Zeit der Protokollanweisung. Die Zeitmarke ist bis auf die Millisekunde definiert. |
| Maschine | Der Name des Hosts, auf dem der Container ausgeführt wird. |
| Nachricht | Die Nachricht, die ausgegeben wurde. Die Nachricht variiert abhängig vom Kontext. |


