---

copyright:
  years: 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Ressourcen
{: #dashboard_resources}
Letzte Aktualisierung: 16. März 2017
{: .last-updated}

Diese Anzeige enthält wichtige Netzdetails und Statusinformationen in Echtzeit für die Blockchain-Komponenten. Zu diesen Komponenten zählen Peer, Zertifizierungsstelle und Anordnungsknoten. Jede Komponente verfügt über vier spezielle Überschriften: **Name**, **URL**, **Status** und **Aktionen**.
{:shortdesc}

**Abbildung 1** zeigt die Anfangsanzeige des Dashboards mit den Netzkomponenten:

![Blockchain-Netz](images/myresources.png "Meine Ressourcen")
*Abbildung 1. Meine Ressourcen*

#### Name

Unter der Überschrift "Name" wird der formale Name auf Systemebene für die Komponente angezeigt. Im vorliegenden Beispiel heißen die Komponenten `order01`, `peer01` und `ca01`.  

#### URL

Unter der Überschrift "URL" wird der API-Endpunkt für jede Komponente angezeigt. Diese Endpunkte sind für die zielgerichtete Verwendung bestimmter Netzkomponenten von einer clientseitigen Anwendung erforderlich und ihre Definitionen befinden sich üblicherweise in einer JSON-modellierten Konfigurationsdatei als Bestandteil der App. Wenn Sie eine Anwendung anpassen, für die eine Billigung seitens von Peers erforderlich ist, die nicht Teil Ihrer Organisation sind, dann müssen Sie diese IP-Adressen von den entsprechenden Administratoren mit einer externen Operation abrufen. Clients müssen eine Verbindung zu allen Peers herstellen können, von denen sie eine Antwort benötigen.

#### Status

Unter der Überschrift "Status" wird der aktuelle Netzstatus der einzelnen Komponenten angezeigt (z. B. "Wird ausgeführt" oder "Gestoppt").

#### Aktionen

Unter der Überschrift "Aktionen" befinden sich Schaltflächen zum Starten oder Stoppen der Komponenten. Außerdem gibt es ein Dropdown-Feld mit Links zu den Komponentenprotokollen. Die Protokolle zeigen die Prozedurfernaufrufe zwischen verschiedenen Netzkomponenten und erweisen sich für die Fehlerbehebung als hilfreich. Experimentieren Sie ein wenig, indem Sie einen Peer stoppen und ihn als Ziel einer Transaktion auswählen, was jedoch zu gRPC-Verbindungfehlern führt. Starten Sie den Peer erneut und wiederholen Sie die Transaktion; es wird eine erfolgreiche Verbindung angezeigt. Sie können einen Peer auch für einen längeren Zeitraum inaktiv lassen, während über Ihre Kanäle weiterhin Transaktionen durchgeführt werden. Wenn der Peer wieder aktiviert wird, werden Sie bemerken, dass mithilfe des Gossip-Protokolls eine Synchronisierung des Kontos durchgeführt wird. Sobald der Peer das Konto vollständig synchronisiert hat, können Sie normale Aufrufe und Abfragen durchführen.  

#### Serviceberechtigungsnachweise

Rechts oben auf dieser Anzeige befindet sich die Registerkarte "Serviceberechtigungsnachweise". Klicken Sie auf diese Registerkarte, um eine JSON-Datei anzuzeigen, die Low-Level-Informationen zum Netzbetrieb für jede der Komponenten (z. B. 'enrollID/enrollSecret' für die Zertifizierungsstelle) enthält. Dies sind alle Konfigurationsinformationen, die Sie für eine Anwendung benötigen. Beachten Sie jedoch, dass diese Datei nur die Peer-IP enthält. Wenn Sie zusätzliche Peers als Ziel angeben müssen, müssen Sie diese Endpunkte abrufen.   
