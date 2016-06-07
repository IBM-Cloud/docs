---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Public
{: #public}
*Letzte Aktualisierung: 22. Februar 2016*


{{site.data.keyword.Bluemix_notm}} abstrahiert und verbirgt den weitaus größten Teil der Komplexität, die mit dem Hosten und Verwalten von cloudbasierten Apps verbunden ist. Als Anwendungsentwickler können Sie sich auf die Entwicklung Ihrer App konzentrieren und müssen sich nicht um die Verwaltung der Infrastruktur kümmern, die für den Betrieb der App erforderlich ist.
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} bietet Cloudbereitstellungen, die Ihren Anforderungen entsprechen. Ob Sie als Kleinunternehmen eine Skalierung
planen oder als Großunternehmen eine zusätzliche Schutzisolierung benötigen, Sie können in einer Cloud praktisch
grenzenlos entwickeln und Ihre dedizierten Services mit den öffentlichen
{{site.data.keyword.Bluemix_notm}}-Services verbinden, die über
{{site.data.keyword.IBM_notm}} und Drittanbieter zur Verfügung gestellt werden. Alle Serviceinstanzen werden
von {{site.data.keyword.IBM_notm}} verwaltet und Sie erhalten nur eine Rechnung über die Leistungen, die Sie in Anspruch genommen haben.

Im
Wesentlichen ist {{site.data.keyword.Bluemix_notm}} eine Umgebung, in der Sie
Apps entwickeln und Services nutzen können, die gebrauchsfertige Funktionen bereitstellen. Zudem bietet {{site.data.keyword.Bluemix_notm}} eine Umgebung zum Betreiben von Anwendungsartefakten, die auf Anwendungsservern wie z. B. Liberty ausgeführt werden. Unter
Verwendung von SoftLayer setzt {{site.data.keyword.Bluemix_notm}} virtuelle
Container ein, um die einzelnen bereitgestellten Apps zu hosten. In dieser Umgebung kann die App
vorgefertigte Services (einschließlich Services von Drittanbietern) verwenden und die App-Assemblierung
somit vereinfachen.

Für mobile Apps und Web-Apps können Sie die vordefinierten Services verwenden, die von
{{site.data.keyword.Bluemix_notm}} bereitgestellt werden. Sie können Ihre Web-App in {{site.data.keyword.Bluemix_notm}} hochladen
und angeben, wie viele Instanzen ausgeführt werden sollen. Nach der Bereitstellung Ihrer Apps können Sie sie ohne großen Aufwand
herauf- oder herabskalieren, wenn sich die Nutzung oder die Auslastung der Apps ändert.

Durch das breite Angebot an Services und Laufzeiten in {{site.data.keyword.Bluemix_notm}} gewinnt der Entwickler mehr Steuerungsmöglichkeiten und Flexibilität. Er erhält Zugang zu verschiedenen Datenoptionen, von Vorhersageanalysen bis hin zu Big Data.

{{site.data.keyword.Bluemix_notm}} stellt die folgenden Funktionen bereit:

- Eine Auswahl von Services, die eine schnelle Erstellung und Erweiterung von mobilen Apps und Web-Apps ermöglichen
- Verarbeitungskapazität, die eine kontinuierliche Bereitstellung von Anwendungsänderungen ermöglicht
- Zweckmäßige Programmiermodelle und Services
- Verwaltungskomfort für Services und Apps
- Optimierte und elastische Workloads
- Kontinuierliche Verfügbarkeit

{{site.data.keyword.Bluemix_notm}} kann für eine rasche Entwicklung von Apps
in den gängigsten Programmiersprachen genutzt werden. Mobile Apps können Sie in iOS, Android und HTML
mit JavaScript entwickeln. Für Web-Apps können Sie Sprachen wie
Ruby, PHP, Java&trade;, Go und Python verwenden. Darüber hinaus können Sie vorhandene Apps nach {{site.data.keyword.Bluemix_notm}} migrieren und die von {{site.data.keyword.Bluemix_notm}} bereitgestellten Laufzeiten verwenden, um Ihre
Apps auszuführen.

{{site.data.keyword.Bluemix_notm}} stellt auch Middleware-Services für den Gebrauch
durch Ihre Apps bereit. {{site.data.keyword.Bluemix_notm}} agiert beim Bereitstellen
neuer Serviceinstanzen anstelle der App und bindet anschließend diese Services an die App. Auf diese Weise kann die App
ihre eigentlichen Aufgaben erledigen und die Verwaltung der Services der Infrastruktur überlassen.

## {{site.data.keyword.Bluemix_notm}} Public-Architektur
{: #publicarch}


Im Allgemeinen müssen Sie sich bei der Ausführung von Apps in
{{site.data.keyword.Bluemix_notm}} keine Gedanken über die Betriebssystem- und
Infrastrukturebenen machen. Die Ebenen wie Stammdateisysteme und
Middlewarekomponenten sind so abstrahiert, dass Sie sich auf Ihren Anwendungscode
konzentrieren können. Es gibt jedoch noch weitere Informationen zu diesen Ebenen, wenn Sie
spezielle Angaben dazu benötigen, wo Ihre App ausgeführt wird. Details finden Sie im Abschnitt zum [Anzeigen von {{site.data.keyword.Bluemix_notm}}-Infrastrukturebenen](../cli/vcapsvc.html#viewinfra).

Als Entwickler haben Sie die Möglichkeit, über eine browserbasierte Benutzerschnittstelle mit der
{{site.data.keyword.Bluemix_notm}}-Infrastruktur zu interagieren. Zum
Bereitstellen von Web-Apps können Sie außerdem die Cloud
Foundry-Befehlszeilenschnittstelle 'cf' verwenden.

Clients - mobile Apps, extern ausgeführte Apps,
auf {{site.data.keyword.Bluemix_notm}} aufbauende Apps oder auch Entwickler,
die gerade einen Browser verwenden -
können mit den von {{site.data.keyword.Bluemix_notm}} gehosteten
Apps interagieren. Mithilfe von REST- oder HTTP-APIs leiten Clients Anforderungen über
{{site.data.keyword.Bluemix_notm}} an eine der
App-Instanzen oder an die zusammengesetzten Services weiter.

Die folgende Abbildung stellt die allgemeine {{site.data.keyword.Bluemix_notm}}-Architektur dar.

![{{site.data.keyword.Bluemix_notm}}-Architektur](images/arch.png)

*Abbildung 1. {{site.data.keyword.Bluemix_notm}}-Architektur*

Sie können
Ihre Apps im Hinblick auf Latenz- und Sicherheitsaspekte für unterschiedliche
{{site.data.keyword.Bluemix_notm}}-Regionen
bereitstellen. Eine Bereitstellung
kann entweder in einer Region oder in mehreren Regionen stattfinden. Weitere Informationen finden Sie unter [Regionen](index.html#ov_intro_reg).


![Anwendungsentwicklung in mehreren Regionen](images/multi-region.png)

*Abbildung 2. Anwendungsbereitstellung in mehreren Regionen*

### Funktionsweise von {{site.data.keyword.Bluemix_notm}}
{: #howwork}

Wenn Sie
auf {{site.data.keyword.Bluemix_notm}} eine App bereitstellen, muss
{{site.data.keyword.Bluemix_notm}} mit genügend Informationen
konfiguriert sein, um die App unterstützen zu können.

* Für mobile Apps enthält {{site.data.keyword.Bluemix_notm}} ein
Artefakt, welches das Back-End für die mobilen Apps darstellt, z. B. die Services, die von
den mobilen Apps genutzt werden, um mit einem Server zu kommunizieren.
* Für Web-Apps muss sichergestellt werden, dass {{site.data.keyword.Bluemix_notm}}
Informationen zur geeigneten Laufzeit und zum geeigneten Framework enthält, sodass es die richtige Ausführungsumgebung
einrichten kann, in der die App ausgeführt wird.

Beide Ausführungsumgebungen, die für die mobile App
wie auch die für die Web-App, sind von den Ausführungsumgebungen anderer Apps isoliert. Die Ausführungsumgebungen werden isoliert, obwohl sich diese Apps auf derselben physischen Maschine befinden. Die folgende
Abbildung stellt die grundlegenden Abläufe für die Verwaltung der App-Bereitstellung durch
{{site.data.keyword.Bluemix_notm}} dar:

![App bereitstellen](images/deploy.png)

*Abbildung 5. App bereitstellen*

Wenn Sie eine App erstellen und auf {{site.data.keyword.Bluemix_notm}} bereitstellen, bestimmt die {{site.data.keyword.Bluemix_notm}}-Umgebung einen geeigneten virtuellen Server, an den die App oder die Artefakte gesendet werden, die die App darstellt. Für mobile Apps wird auf {{site.data.keyword.Bluemix_notm}} eine mobile Back-End-Projektion erstellt. Jeder Code für die in der Cloud ausgeführte mobile Anwendung wird letztendlich in der {{site.data.keyword.Bluemix_notm}}-Umgebung ausgeführt. Für Web-Apps ist der Code, der in der Cloud ausgeführt wird, die App selbst, die der Entwickler auf {{site.data.keyword.Bluemix_notm}} bereitstellt. Welcher virtuelle Server dafür ausgesucht wird, basiert auf mehreren Faktoren, wie zum Beispiel:

* Die bestehende Auslastung der Maschine
* Von diesem virtuellen Server unterstützte Laufzeiten oder Frameworks

Nachdem ein virtueller Server ausgesucht wurde, installiert ein Anwendungsmanager auf jedem virtuellen Server das passende Framework und die passende Laufzeit für die App. Anschließend kann die App in diesem Framework bereitgestellt werden. Sobald die Bereitstellung erfolgt ist, werden die Anwendungsartefakte gestartet.

Die folgende Abbildung zeigt die Struktur eines virtuellen Servers, auch als Droplet Execution Agent (DEA) bezeichnet, auf dem mehrere Apps bereitgestellt wurden:

![Struktur eines virtuellen Servers](images/container.png)

*Abbildung 6. Struktur eines virtuellen Servers*

In jedem virtuellen Server kommuniziert ein Anwendungsmanager mit der übrigen {{site.data.keyword.Bluemix_notm}}-Infrastruktur und verwaltet die Apps, die auf diesem virtuellen Server bereitgestellt sind. Jeder virtuelle Server verfügt über Container zum Trennen und Schützen der Apps. In jedem dieser Container installiert {{site.data.keyword.Bluemix_notm}} das geeignete Framework und die geeignete Laufzeit, die für die einzelnen Apps erforderlich sind.

Wenn die
App bereitgestellt wurde und über eine Webschnittstelle (wie für eine Java-Web-App)
oder andere REST-basierte Services (z. B. mobile Services, die für die mobile Anwendung öffentlich zugänglich sind)
verfügt, können Benutzer der App durch normale HTTP-Anforderungen mit ihr kommunizieren.

![Eine {{site.data.keyword.Bluemix_notm}}-App aufrufen](images/execute.png)

*Abbildung 7. Eine {{site.data.keyword.Bluemix_notm}}-App aufrufen*

Jeder App
kann mindestens eine URL zugeordnet sein, aber jede dieser URLs muss auf den {{site.data.keyword.Bluemix_notm}}-Endpunkt
verweisen. Wenn eine Anforderung eintrifft, prüft {{site.data.keyword.Bluemix_notm}} diese
Anforderung, stellt fest, an welche App sie gerichtet ist, und wählt eine der
Instanzen der App für den Empfang der Anforderung aus.


## Regionen
{: #ov_intro_reg}

Eine {{site.data.keyword.Bluemix_notm}}-Region ist ein definiertes geografisches Gebiet, in dem Sie Ihre Apps bereitstellen können. Sie können Apps und Serviceinstanzen in unterschiedlichen Regionen mit derselben {{site.data.keyword.Bluemix_notm}}-Infrastruktur für das Anwendungsmanagement und dieselbe Ansicht mit den Nutzungsdetails zur Gebührenabrechnung erstellen. Sie können die Region auswählen, die Ihren Kunden am nächsten ist, und Ihre
Anwendungen in dieser Region bereitstellen, um so eine geringe Anwendungslatenz zu erreichen. Es ist auch möglich,
die Region, in der Sie die Anwendungsdaten aufbewahren möchten, auszuwählen, um Sicherheitsproblemen
Rechnung zu tragen. Wenn Sie Apps in mehreren Regionen erstellen, werden
die Apps in den anderen Regionen weiter ausgeführt, falls eine Region ausfällt. Die verfügbaren Ressourcen
sind für jede verwendete Region gleich.

Wenn Sie mit der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle
arbeiten, können Sie in eine andere Region wechseln, um mit den Bereichen
in dieser Region zu arbeiten.

Wenn Sie mit der Befehlszeilenschnittstelle cf
arbeiten, müssen Sie eine Verbindung zu der {{site.data.keyword.Bluemix_notm}}-Region
herstellen, mit der Sie arbeiten möchten. Verwenden Sie hierzu den Befehl cf api und geben Sie den API-Endpunkt
der Region an. Geben Sie beispielsweise den folgenden Befehl ein, um eine Verbindung zu der
{{site.data.keyword.Bluemix_notm}}-Region 'Europe
United Kingdom' herzustellen:

```
cf api https://api.eu-gb.{{site.data.keyword.Bluemix_notm}}.net
```

Wenn Sie mit den Eclipse-Tools arbeiten,
müssen Sie eine Verbindung zu der {{site.data.keyword.Bluemix_notm}}-Region herstellen, mit der Sie
arbeiten möchten. Erstellen Sie hierzu einen {{site.data.keyword.Bluemix_notm}}-Server und geben Sie den
API-Endpunkt der Region an. Weitere Informationen zur Verwendung
der Eclipse-Tools finden Sie unter [Apps mit {{site.data.keyword.IBM_notm}} Eclipse Tools for {{site.data.keyword.Bluemix_notm}} bereitstellen](../manageapps/eclipsetools/eclipsetools.html#toolsinstall).

Jeder Region wird ein eindeutiges Präfix zugewiesen. Für {{site.data.keyword.Bluemix_notm}}
stehen die folgenden Regionen und Regionspräfixe zur Verfügung.

<!-- PRODUCTION ONLY: Ensure that URLs are production URLs, not stage1-->

| **Regionsname** | **Standort** | **Regionspräfix** | **cf-API-Endpunkt** | **Benutzerschnittstellenkonsole** |       
|-----------------|-------------------------|-------------------|---------------------|----------------|
| Region 'Vereinigte Staaten (Süden)' | Dallas, US | ng | api.ng.bluemix.net | console.ng.bluemix.net |
| Region 'United Kingdom' | London, England | eu-gb | api.eu-gb.bluemix.net | console.eu-gb.bluemix.net |
| Region 'Sydney' | Sydney, Australia | au-syd | api.au-syd.bluemix.net | console.au-syd.bluemix.net |

*Tabelle 1. Liste der {{site.data.keyword.Bluemix_notm}}-Regionen*


## {{site.data.keyword.Bluemix_notm}}-Ausfallsicherheit
{: #resiliency}

{{site.data.keyword.Bluemix_notm}}
wurde zum Hosten skalierbarer, ausfallsicherer Apps und Anwendungsartefakte
entworfen, die eine bedarfsorientierte Skalierung ermöglichen und gleichzeitig eine hohe Verfügbarkeit
sowie eine rasche Wiederherstellbarkeit nach Problemen bieten. {{site.data.keyword.Bluemix_notm}} unterscheidet zwischen
Komponenten, die den Zustand von Interaktionen verfolgen (mit Zustandsüberwachung) und Komponenten,
die den Zustand von Interaktionen nicht verfolgen (ohne Zustandsüberwachung). Diese Unterscheidung
ermöglicht es {{site.data.keyword.Bluemix_notm}}, Apps so flexibel
wie nötig zu versetzen, um Skalierbarkeit und Ausfallsicherheit zu erreichen.

Sie können für Ihre App eine oder mehrere Instanzen ausführen. Bei mehreren Instanzen für eine App wird die App nur einmal hochgeladen. {{site.data.keyword.Bluemix_notm}} implementiert jedoch die angeforderte Anzahl der App-Instanzen und verteilt sie auf so viele virtuelle Server wie möglich.

Sie müssen
alle persistenten Daten in einem Datenspeicher mit Zustandsüberwachung speichern, der sich außerhalb Ihrer App
befindet, wie z. B. einer der von {{site.data.keyword.Bluemix_notm}}
bereitgestellten Datenspeicherservices. Da alle im Hauptspeicher oder auf Platte zwischengespeicherten Daten selbst nach einem Neustart möglicherweise
nicht verfügbar sind, können Sie die Hauptspeicherkapazität oder das Dateisystem
einer einzelnen {{site.data.keyword.Bluemix_notm}}-Instanz als
Kurzzeitcache für eine einzelne Transaktion verwenden. Bei einem Einzelinstanzsetup wird die Anforderung
an Ihre App aufgrund der Tatsache, dass es für {{site.data.keyword.Bluemix_notm}}
keine Zustandsüberwachung gibt, möglicherweise unterbrochen. Bewährt hat sich die Verwendung von mindestens drei Instanzen für jede App, um die Verfügbarkeit
Ihrer App sicherzustellen.

Die gesamte
{{site.data.keyword.Bluemix_notm}}-Infrastruktur, die Cloud
Foundry-Komponenten und für {{site.data.keyword.IBM_notm}} spezifische Verwaltungskomponenten stellen eine hohe Verfügbarkeit sicher. Zum Lastausgleich
werden mehrere Instanzen der Infrastruktur verwendet.

## Integration mit Systems of Record (Kerndatensystemen)
{: #sor}

{{site.data.keyword.Bluemix_notm}} kann Entwicklern durch die Verbindung zweier Systemkategorien in einer Cloudumgebung Hilfestellung leisten: Systems of Record (Kerndatensysteme) und Systems of Engagement (mobile Interaktionssysteme).

*Systems of Record* umfassen Apps und Datenbanken, die Geschäftsberichte speichern und
standardisierte Prozesse automatisieren. *Systems of Engagement* sind Funktionen, die den Nutzen
von Systems of Record erweitern und für Benutzer attraktiver machen.
Durch die Integration eines System of Record in die App, die Sie in
{{site.data.keyword.Bluemix_notm}} erstellen,
können Sie die folgenden Aktionen durchführen:

 * Einrichten einer sicheren Kommunikation zwischen der App und der Back-End-Datenbank durch
Herunterladen und Installation eines lokalen sicheren Connectors
 * Aufrufen einer Datenbank mit einer sicheren Methode
 * Erstellen von APIs aus Integrationsflüssen mit Datenbanken und Back-End-Systemen wie z. B. einem System für Customer-Relationship-Management
 * Zugänglichmachen nur derjenigen Schemas und Tabellen, die Sie der App zugänglich machen wollen
 * Als {{site.data.keyword.Bluemix_notm}}-Organisationsmanager:
Veröffentlichen einer API als privaten Service, der nur für die Mitglieder Ihrer Organisation sichtbar ist

Um ein System of Record in die App zu integrieren, die Sie in {{site.data.keyword.Bluemix_notm}} erstellen,
können Sie den Cloud Integration-Service verwenden. Wenn Sie den Cloud Integration-Service
verwenden, können Sie eine Cloud Integration-API erstellen
und die API als privaten Service für Ihre Organisation veröffentlichen.

<dl>
<dt>Cloud Integration-API</dt>
    <dd>Mit einer Cloud Integration-API haben Sie über Web-APIs sicheren Zugriff auf die Systems of Record, die sich hinter einer Firewall befinden. Bei der Erstellung der
Cloud Integration-API wählen Sie die Ressource aus,
auf die Sie über die Web-API zugreifen möchten, geben die zulässigen Operationen
an und beziehen die SDKs und Beispiele für den Zugriff auf die API ein. Weitere Informationen zur Erstellung
einer Cloud Integration-API finden Sie
unter [Cloud Integration-APIs erstellen](../services/CloudIntegration/index.html#cloudint_add_service).</dd>
<dt>Privater Service</dt>
    <dd>Ein privater Service besteht aus einer Cloud Integration-API,
SDKs und Berechtigungsrichtlinien. Außerdem enthält der private Service
möglicherweise die Dokumentation oder andere Elemente des Service-Providers. Eine Cloud Integration-API kann nur vom Organisationsmanager als privater Service veröffentlicht werden. Wenn Sie die
für Sie zur Verfügung stehenden privaten Services anzeigen möchten, wählen Sie
im {{site.data.keyword.Bluemix_notm}}-Katalog das Kontrollkästchen 'Privat' aus. Sie können einen privaten Service auswählen und ihn an eine App binden, ohne dass eine Verbindung zum
Cloud Integration-Service erforderlich wäre. Private Services werden wie andere
{{site.data.keyword.Bluemix_notm}}-Services auch
an Ihre App gebunden. Weitere Informationen zur Veröffentlichung einer API als privaten Service finden Sie im Thema zur Veröffentlichung einer API als privaten Service.</dd>
</dl>

### Szenario: Erstellen einer umfangreichen mobilen App, die mit Ihrem System of Record verbunden werden soll
{: #scenario}

{{site.data.keyword.Bluemix_notm}} bietet eine Plattform,
auf der Sie ihre mobile App, Cloud-Services und Systems of Record von Unternehmen integrieren können, um eine App einzurichten,
die mit Ihren lokalen Daten interagiert.

Sie können beispielsweise eine mobile Anwendung aufbauen, die
mit Ihrem Customer-Relationship-Managementsystem interagiert, welches sich lokal hinter einer Firewall
befindet. Sie können auf sicherem Weg ein System of Record aufrufen und die mobilen Services in
{{site.data.keyword.Bluemix_notm}} zum Aufbau
einer umfangreichen mobilen App nutzen.

Zunächst erstellt Ihr Integrationsentwickler in {{site.data.keyword.Bluemix_notm}} die mobile Back-End-App. Er verwendet die Boilerplate aus Mobile Cloud mit der Node.js-Laufzeit, mit der er am besten vertraut ist.

Unter Verwendung des Cloud Integration-Service in der
{{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle
macht er über einen sicheren Connector eine API zugänglich. Ihr Integrationsentwickler lädt den sicheren
Connector herunter und installiert ihn lokal, um eine sichere Kommunikation zwischen seiner API und der
Datenbank zu ermöglichen. Nachdem er den Datenbankendpunkt erstellt hat, kann er sich alle Schemas ansehen
und diejenigen Tabellen extrahieren, die er der App als APIs zugänglich machen will.

Um
interessierten Kunden mobile Benachrichtigungen senden zu können, fügt der Integrationsentwickler den
Push-Service hinzu. Außerdem nimmt er
einen Geschäftspartnerservice auf, der über eine Twitter-API einen Tweet versendet, sobald ein neuer Satz von
Kundenstammdaten erstellt wird.

Als Nächstes können Sie sich als Anwendungsentwickler bei
{{site.data.keyword.Bluemix_notm}} anmelden,
das Android-Entwicklungstoolkit herunterladen und Code entwickeln, mit dem die APIs aufgerufen werden, die
Ihr Integrationsentwickler eingerichtet hat. Sie können eine mobile App entwickeln, die es dem Benutzer
ermöglicht, über sein mobiles Gerät Informationen einzugeben. Die mobile Anwendung erstellt daraufhin im
Customer-Managementsystem einen Kundenstammdatensatz. Nachdem der Datensatz erstellt ist, übermittelt die
App per Push-Operation eine Benachrichtigung an ein mobiles Gerät und leitet einen Tweet zu dem neuen
Datensatz ein.

# Zugehörige Links
## Allgemein
* [Neuerungen in {{site.data.keyword.Bluemix_notm}}](../whatsnew/index.html)
* [Voraussetzungen für {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#prereqs)
* [Bekannte Probleme in {{site.data.keyword.Bluemix_notm}}](https://developer.ibm.com/bluemix/support/#issues)
* [Konto verwalten](../admin/adminpublic.html#mngacct)
* [{{site.data.keyword.Bluemix_notm}}-Glossar](../overview/glossary/index.html)
