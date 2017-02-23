---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-29"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Server für angepasste Karten schützen
{: #securing_custom_cards}

Server für angepasste Karten sind standardmäßige Web-Server, auf dem der JavaScript-Code von angepassten Karten gehostet wird. Zum Sicherstellen der Integrität Ihrer {{site.data.keyword.iot_short_notm}}-Umgebung sollten Sie Ihren Server für angepasste Karten schützen, indem Sie Schritte vornehmen, mit denen die Kartenquelle wie in diesem Abschnitt beschrieben geschützt wird.
{:shortdesc}

**Wichtig:** Angepasste Karten werden zurzeit als experimentelles Feature angeboten und die Erweiterung für angepasste Karten wird pro Browsersitzung aktiviert. Kartenpakete und die Verbindungskonfiguration für angepasste Karten werden innerhalb Ihrer {{site.data.keyword.iot_short_notm}}-Organisation nicht global gemeinsam genutzt.

## Erforderliche {{site.data.keyword.Bluemix_notm}}-Rolle
{: #roles_requirements}

Sie müssen für {{site.data.keyword.iot_short_notm}} über Administratorrechte verfügen, um eine Verbindung für einen Server für angepasste Karten zu erstellen.

## Sicherheitsaspekte für Server für angepasste Karten
{: #server_requirements}

Folgende Anforderungen sind von {{site.data.keyword.iot_short_notm}} festgelegt:
- Für den Zugriff auf das Verzeichnis, in dem der Inhalt aus angepassten Karten auf dem Server bereitgestellt werden soll, dürfen keine Berechtigungsnachweise erforderlich sein.  
Für den Server für angepasste Karten ist beim Herstellen einer Verbindung für den Zugriff auf angepasste Karten und das Laden dieser Karten keine Authentifizierung erforderlich.
- Der Server muss das Protokoll HTTP Secure (HTTPS) verwenden.
- Der Server muss Cross-Origin Resource Sharing-Verbindungen (CORS) unterstützen.  

Um den Code für angepasste Karten und den Kartenserver selbst zu schützen, sollte der Kartenserver mithilfe der tiefengestaffelten Sicherheit positioniert und geschützt werden. Dies schließt den Schutz durch eine Firewall ein, um den Zugriff auf den Server für angepasste Karten einzuschränken.

Die Verarbeitung angepasster Karten findet stets zwischen dem Browser eines Benutzers und dem Server für angepasste Karten statt. Das {{site.data.keyword.iot_short_notm}}-Back-End wird zu keinem Zeitpunkt in die Verarbeitung oder Anpassung von Informationen und Code für angepasste Karten einbezogen.

Für den JavaScript-Code, mit dem Sie Ihre Karten auf Ihrem Server für angepasste Karten implementieren möchten, bestehen keine Einschränkungen. Mit Javascript-Code in angepassten Karten kann auf alle im Browser enthaltenen Informationen zugegriffen werden, genau wie dies bei allen anderen Karten möglich ist, die im Dashboard ausgeführt werden.  Stellen Sie sicher, dass der für den Browser angegebene Code zum Anzeigen und Verarbeiten der angepassten Karten vom richtigen Server für angepasste Karten bereitgestellt wird.

Der Code der Karten wird in Ihrer {{site.data.keyword.iot_short_notm}}-Browsersitzung genau so ausgeführt, wie er geschrieben wurde. Darüber hinaus wird die Verbindung zum Server für angepasste Karten hergestellt, ohne dass für den Server für angepasste Karten Berechtigungsnachweise bereitgestellt werden. Der Browser eines Benutzers kann eine Verbindung zu jedem konfigurierten Server für angepasste Karten herstellen.

Es ist wichtig, dass Sie zum Bereitstellen von angepassten Karten für die Dashboards Ihrer Benutzer nur bekannte und geschützte Server für angepasste Karten konfigurieren.   
