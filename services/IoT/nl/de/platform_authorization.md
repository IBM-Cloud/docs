---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Anwendungsverbindung

Um eine Verbindung zwischen Ihrer Anwendung und {{site.data.keyword.iot_full}} herzustellen, müssen Sie die Verbindung über API-Schlüssel und Token herstellen oder Ihre Anwendung in {{site.data.keyword.Bluemix_notm}} direkt mit {{site.data.keyword.iot_short_notm}} verbinden. Verwenden Sie das Zugriffsdashboard, um Zugriff zu erteilen.
{:shortdesc}

## Verbindung über API-Schlüssel
{: #api-key}
Beim Herstellen einer Verbindung zwischen Anwendungen und Ihrer {{site.data.keyword.iot_short_notm}}-Organisation werden API-Schlüssel verwendet. Anwendungen benötigen einen API-Schlüssel, um mit einer Organisation verbunden zu werden, sowie ein eindeutiges Authentifizierungstoken, das mit diesem API-Schlüssel verwendet werden muss.  

Weitere Informationen zu Anwendungsverbindungen finden Sie in der Entwicklerdokumentation in [MQTT-Konnektivität für Anwendungen ![Symbol für externen Link](../../icons/launch-glyph.svg "Symbol für externen Link")](https://docs.internetofthings.ibmcloud.com/applications/mqtt.html){: new_window}.

Gehen Sie wie folgt vor, um eine neue Kombination aus API-Schlüssel und Authentifizierungstoken zu erstellen:  
1.	Wechseln Sie im {{site.data.keyword.iot_short_notm}}-Dashboard zu **Apps > API-Schlüssel**.  
2.	Klicken Sie auf **API-Schlüssel generieren**.  
**Wichtig:** Notieren Sie sich die Kombination aus API-Schlüssel und Authentifizierungstoken. Authentifizierungstokens sind nicht wiederherstellbar. Wenn Sie dieses Token verlieren oder vergessen, müssen Sie den API-Schlüssel erneut registrieren, um ein neues Authentifizierungstoken zu generieren.
 - Beispiel für einen API-Schlüssel: `a-organization_id-a84ps90Ajs`.  
 - Beispiel für ein Token: `MP$08VKz!8rXwnR-Q*`.  
3.	Fügen Sie einen Kommentar hinzu, um den API-Schlüssel im Dashboard anzugeben: Schlüssel zum Verbinden meiner Anwendung.
4.	Klicken Sie auf **Fertigstellen**.



## Verbindung für Bluemix-Bindung
{: #bluemix-binding}
Sie können Anwendungen über {{site.data.keyword.Bluemix_notm}} an Ihre {{site.data.keyword.iot_short_notm}}-Organisation binden. Durch Binden der Anwendung kann sie nur mit Serviceinstanzen im selben Bereich bzw. derselben Organisation kommunizieren. Sie können alle Daten, die für die Kommunikation zwischen der Anwendung und der Serviceinstanz erforderlich ist, in der Umgebungsvariable VCAP_SERVICES finden. Wenn Ihre Anwendung an mehrere Services gebunden ist, umfasst die Variable Verbindungsinformationen zu jeder einzelnen Serviceinstanz.  

Sie können jedoch Serviceinstanzen aus anderen Bereichen oder Organisationen auf dieselbe Weise verwenden, wie auch eine externe App sie verwenden würde. Verwenden Sie die Berechtigungsnachweise, um eine App-Instanz direkt zu konfigurieren, anstatt eine Bindung zu erstellen. Weitere Informationen finden Sie in der {{site.data.keyword.Bluemix_notm}}-Dokumentation in [Neue Serviceinstanz anfordern](https://console.{DomainName}/docs/services/reqnsi.html#req_instance).

Wechseln Sie zu **Apps > Bluemix-Apps**, um Details für die Bluemix-Anwendungen anzuzeigen, die an die Ihrer Organisation zugeordnete Serviceinstanz gebunden sind.  
