---

Copyright:
  Jahre: 2015, 2016
Letzte Aktualisierung: 01.11.2016
---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# Einführung in IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #getting_started}

{{site.data.keyword.IBM}} WebSphere Application Server for {{site.data.keyword.Bluemix}} ist ein Service, mit dem Sie ohne Zeitverlust eine vorkonfigurierte WebSphere Application Server Liberty-, eine klassische Network Deployment- oder eine klassische WebSphere Java EE-Instanz in einer gehosteten Cloudumgebung in {{site.data.keyword.Bluemix_notm}} einrichten können.
{: shortdesc}

## Übersicht zu WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}
{: #overview}

WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} bietet Nutzern vorkonfigurierte klassische WebSphere- und Liberty Profile-Server. Das Programm wird auf virtuellen Gastmaschinen mit Rootzugriff auf das Gastbetriebssystem gehostet. Wenn Sie einen eigenen Service erstellen, müssen Sie zwischen *Liberty*, *klassischem ND* und *klassischem WebSphere* wählen.

**Anmerkung:** Kunden können nun bei der Erstellung einer neuen Instanz von *klassischem ND* oder *klassischem WebSphere* zwischen V8.5 und V9.0 wählen.

Sie erhalten eine vertraute WebSphere-Administrationserfahrung und uneingeschränkten Zugriff auf das zugrunde liegende Betriebssystem. Sie können bereits vorhandene Scripts weiterverwenden und am System die für die Arbeit mit eigenen Frameworks oder Frameworks von Dritten erforderlichen Optimierungsschritte vornehmen. Admin Center und Admin Consoles werden ähnlich Ihren lokalen WebSphere-Konfigurationen zur Verwaltung Ihrer WebSphere Application Server Liberty-, ND- oder klassischen Services bereitgestellt.

Der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment-Plan besteht aus einer WebSphere Application Server Network Deployment-Zellenumgebung mit mindestens zwei virtuellen Maschinen. Die erste virtuelle Maschine enthält den Deployment Manager und IBM HTTP Server und die übrigen virtuellen Maschinen enthalten angepasste Knoten (Knotenagenten), die in den Deployment Manager integriert sind. Mithilfe der vorhandenen wsadmin-Scripts können Sie eine eigene WebSphere-Konfiguration erstellen oder Sie können WebSphere Admin Console verwenden, um die Umgebung manuell zu konfigurieren. Mit diesen neuen Funktionen können Benutzer eine Clusterumgebung konfigurieren, die ein entscheidender Aspekt einer Middleware-Unternehmensanwendung ist. Kunden können nun auswählen, dass für eine Topologie ein Cluster gebildet werden soll, um in zwei oder mehr Instanzen einen Lastausgleich für Anforderungen durchzuführen.

Der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Liberty Core-Plan beinhaltet die Nutzung eines Liberty-Verbunds. Der Liberty-Verbund ist eine Verwaltungsdomäne für eine Gruppe von Liberty-Profilen (Servern), die aus mindestens zwei virtuellen Maschinen besteht. Die erste virtuelle Maschine enthält den Liberty-Server für den Verbundcontroller, einen Steuerpunkt für den Liberty-Verbund. Zusätzlich zum Liberty-Verbund enthält diese virtuelle Maschine auch IBM HTTP Server, wodurch Zugriff auf Ihre Anwendungen über einen Web-Browser ermöglicht wird. Die übrigen virtuellen Maschinen sind Verbundhosts, in denen sich die Verbundmember befinden (Liberty Profile-Server). Das Feature Liberty Admin Center ist auf dem Liberty-Controller-Server ebenfalls aktiviert.

In der folgenden Abbildung ist die Architektur der WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} Network Deployment-Zelle sowie der Liberty-Verbundumgebungen zu sehen.

Abbildung 1. Architektur der Network Deployment-Zelle sowie des Liberty-Verbunds

![Abbildung 1. Architektur der Network Deployment-Zelle sowie des Liberty-Verbunds](images/CellCollectiveDiagram.gif)

**Anmerkung**: In *Abbildung 1* dient das Muster, das die Kollokation des Deployment Managers oder des Verbundcontrollers mit dem IBM HTTP Server darstellt, Entwicklungs- und Testzwecken. Mit WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} haben Sie außerdem die Möglichkeit, die vorinstallierte Software den Erfordernissen der Produktionsanwendung und den betrieblichen Anforderungen entsprechend anzupassen, wie es vor Ort in der Regel der Fall ist. Wenn es ausschließlich um Produktionsanforderungen geht, können Sie sich an den IBM Vertriebsbeauftragten wenden, der Sie gerne über das IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Single-Tenant-Angebot informiert, das isolierte Netz- und Rechenressourcen umfasst.


## Betriebsumgebung
{: #operational_environment}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} ist ein Service, mit dem Gäste (virtuelle Maschinen) in einer gemeinsam genutzten Umgebung zur Verfügung gestellt werden, mit denen Nutzer Anwendungen bereitstellen können. Der öffentliche Service wird mithilfe eines VPNs vor generischen Port-Scans und anderen unerwünschten netzbasierten Angriffen geschützt. Es ist jedoch wichtig zu wissen, dass das Service-VPN, das Sie für den Zugriff auf Ihre Serviceinstanz nutzen, möglicherweise mit mehreren {{site.data.keyword.Bluemix_notm}}-Organisationen und -Benutzern gemeinsam genutzt wird. Auf den virtuellen Maschinen werden Berechnungs-, Speicher- und Ein-/Ausgaberessourcen bereitgestellt, die sich in einem gemeinsamen Pool von IaaS-Ressourcen befinden.

Da bestimmte Berechnungs-, Speicher- und Ein-/Ausgaberessourcen von virtuellen Maschinen in einer gemeinsam genutzten Umgebung ausgeführt werden, können die Servicekonfigurationen variieren. Die Konfigurationen für die einzelnen Serviceinstanzen können über die Service-Dashboards und -Portale für IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} angezeigt werden.

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} stellt VM-Instanzen bereit. Mit diesen Instanzen nutzen Kunden für die Erstellung und Verwaltung von WebSphere Application Server-Bereitstellungen für Unternehmen ein einfaches Portal; dabei ist für die Optimierung von Anwendungen neben Konsistenz und wiederholter Anwendbarkeit auch eine erhebliche Flexibilität von Bedeutung. Benutzer können mit vorkonfigurierten WebSphere Application Server Liberty-, ND- oder konventionellen VMs in einer gehosteten Cloudumgebung arbeiten. Benutzer können vorhandene WebSphere Application Server-Anwendungen nach {{site.data.keyword.Bluemix_notm}} migrieren und das zugrunde liegende Betriebssystem und die Middleware uneingeschränkt nutzen.

## Strategie für die Preisermittlung
{: #pricing_strategy}

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} bietet Clients mit speicherintensiven Anwendungen nach T-Shirt-Größen unterteilte Instanzen, sodass diese ihre Umgebung mit größeren virtuellen Maschinen in der geeigneten Größe einrichten können. Kunden können die jeweilige Ressourcengröße einer angegebenen WebSphere Application Server-Komponente oder eines einzelnen Systems bis zu 32 GB RAM VM auswählen.

In den folgenden Tabellen sind die Preise für IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Pläne zum 01. April 2016 in US-Dollar (USD) dargestellt.

*Tabelle 1. Liberty Core-Plan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **FP (GB)** | **Preis/Std** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $ 0,21 |
| M | 2 | 4 | 25 | $ 0,42 |
| L | 4 | 8 | 50 | $ 0,84 |
| XL | 8 | 16 | 100 | $ 1,68 |
| XXL | 16 | 32 | 200 | $ 3,36 |

*Tabelle 2. WebSphere Application Server-Basisplan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **FP (GB)** | **Preis/Std** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $ 0,30 |
| M | 2 | 4 | 25 | $ 0,60 |
| L | 4 | 8 | 50 | $ 1,20 |
| XL | 8 | 16 | 100 | $ 2,40 |
| XXL | 16 | 32 | 200 | $ 4,80 |

*Tabelle 3. WebSphere Application Server-ND-Plan*

| **T-Shirt** | **vCPU** | **RAM (GB)** | **FP (GB)** | **Preis/Std** |       
|:-------------:|:----------:|:--------------:|:-------------:|:--------------:|
| S | 1 | 2 | 12 | $ 0,70 |
| M | 2 | 4 | 25 | $ 1,40 |
| L | 4 | 8 | 50 | $ 2,80 |
| XL | 8 | 16 | 100 | $ 5,60 |
| XXL | 16 | 32 | 200 | $ 11,20 |

<p></p>

IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}} wird der folgenden Gebührenmetrik entsprechend angeboten:

*  *Instanz-Stunde*: Eine Instanz wird definiert als Zugriff auf eine bestimmte Konfiguration des IBM WebSphere Application Server for {{site.data.keyword.Bluemix_notm}}-Service. Kunden wird jede volle Stunde oder jede Teilstunde pro Instanz des Service in Rechnung gestellt, der im Abrechnungszeitraum bereitgestellt wird. Jede Instanz-Stunde wird monatlich in Rechnung stellen und wenn eine Instanz in diesem Montat nur teilweise genutzt wurde, wird die Nutzung anteilmäßig berechnet.

Beispiel: Bei Nutzung des ND-Plans entspricht eine einzige Instanz 1vCPU mit 2 GB RAM und 12 GB Festplattenspeicher. Wenn Sie sich also für die Konfiguration Ihrer Zelle mit einem einzigen Steuerknoten und acht angepassten Knoten entscheiden, werden Ihnen neun Knoten (Instanzen) berechnet.

**Anmerkung**: Die Mindestabrechungseinheit sind 0,25 Instanz-Stunden pro angepassten Knoten oder Liberty-Host. Für das oben stehende Beispiel gilt, dass ein Steuerknoten und ein angepasster Knoten, der für mindestens 15 Minuten konfiguriert ist, einer Mindestgebühr von (.25 * Anzahl der Instanzen) entspricht.

**Hinweis**: Aufgrund einer bestimmten Menge an Rechen-, Speicher- und E/A-Ressourcen werden für Clients Gebühren für die Summe der Instanzen im Status GESTOPPT mit einer reduzierten Rate von 5 % berechnet. Clients werden mit einer festen Anzahl von Instanzen im Status GESTOPPT mit maximal 10 IP-Adressen oder 64 GB Speicherplatz verwaltet.

# Zugehörige Links
{: #rellinks}
## Allgemein
{: #general}
* [WASdev](https://developer.ibm.com/wasdev/){: new_window}
* [Dokumentation zu WebSphere Application Server V9](http://www.ibm.com/support/knowledgecenter/SSEQTP_9.0.0/as_ditamaps/was900_welcome_base.html){: new_window}
