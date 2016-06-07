---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten
{: #mng}
*Letzte Aktualisierung: 16. Mai 2016*

Wenn Sie über Administratorzugriff für {{site.data.keyword.Bluemix_notm}} Local oder {{site.data.keyword.Bluemix_notm}} Dedicated verfügen, können Sie über die Seite **Verwaltung** Ressourcen verwalten, die Kontingentnutzung überwachen, Benutzerberechtigungen verwalten, Upgradebenachrichtigungen planen, Sicherheitsberichte und Protokolle anzeigen und vieles mehr. Sie können Ihre Organisationen verwalten, indem Sie Bereiche erstellen und [Benutzerrollen und Berechtigungen festlegen](index.html#oc_useradmin). Weitere Informationen finden Sie in [Organisationen verwalten](../admin/orgs_spaces.html).
{:shortdesc}

*Tabelle 1. Verwaltungstasks zur Verwaltung einer {{site.data.keyword.Bluemix_notm}} Local- oder Dedicated-Instanz*

| Verwaltungstask | Details |    
|----------------|---------|
|Systemnutzung überwachen | Klicken Sie auf **Verwaltung &gt; Nutzung**. Zeigen Sie Systeminformationen an, überwachen Sie die CPU-Nutzung und planen Sie die Nutzung, um die besten Entscheidungen für Ihr Unternehmen zu treffen. Siehe [Nutzungsinformationen anzeigen](index.html#oc_resource).|
|Eigenen Katalog verwalten | Klicken Sie auf **Verwaltung &gt; Katalogverwaltung**, um die Services zu verwalten, die für Ihre Benutzer und Organisationen sichtbar sind. Siehe [Eigenen Katalog verwalten](index.html#oc_catalog).|
|Organisationen verwalten | Klicken Sie auf **Verwaltung &gt; Organisationsadministration**, um Organisationen zu erstellen, Kontingente für Organisationen zu überwachen und rasch bedarfsorientierte Entscheidungen zu treffen. Siehe [Organisationen verwalten](index.html#oc_organizations).|
|Bereiche erstellen und Benutzerrollen zuweisen | Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus, um Bereiche in Ihren Organisationen zu erstellen. Fügen Sie Benutzer hinzu und weisen Sie Benutzern Organisations- und Bereichsrollen zu. Siehe [Organisationen verwalten](../admin/orgs_spaces.html). |
|Administratorberechtigungen verwalten | Klicken Sie auf **Verwaltung &gt; Benutzeradministration**, um Benutzer hinzuzufügen, Benutzer zu entfernen und Benutzerberechtigungen anzupassen. Siehe [Benutzer und Berechtigungen verwalten](index.html#oc_useradmin). |
|Berichte und Protokolle prüfen | Klicken Sie auf **Verwaltung &gt; Berichte und Protokolle**, um Sicherheitsberichte und Prüfprotokolle für Ihre Instanz anzuzeigen. Siehe [Berichte anzeigen](index.html#oc_report). |
|Systeminformationen anzeigen | Klicken Sie auf **Verwaltung &gt; Systeminformationen**, um Systeminformationen wie anstehende Aktualisierungen, Name und Version Ihrer Instanz, Region, API-URL, CLI-URL, LDAP-Konfigurationsdetails, Gruppen- und Benutzerzuordnungen, Statistiken und gemeinsam genutzte Domänen anzuzeigen. Sie können außerdem auf den Kalenderfeed und die Ereignisabonnements zur Erweiterung Ihrer Benachrichtigungen im Abschnitt 'Anstehende Aktualisierungen' zugreifen. Siehe [Systeminformationen anzeigen](index.html#oc_system). |
|Benachrichtigungen erweitern und Ereignisabonnements einrichten | Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* Aktualisierungen stehen an**. Sie können Web-Hooks zur Integraion in einen Web-Service Ihrer Wahl verwenden, um ein Abonnement für Ereignisbenachrichtigungen für eine Aktualisierung oder eine Störung einzurichten. Siehe [Benachrichtigungen und Ereignisabonnements](index.html#oc_eventsubscription). |


## Benachrichtigungen und Ereignisabonnements
{: #oc_eventsubscription}

Sie können den Status Ihrer Umgebung jederzeit über die Seite 'Status' ermitteln. {{site.data.keyword.Bluemix_notm}} sendet außerdem Benachrichtigungen in den Bereich 'Benachrichtigungen' für die Seite 'Verwaltung' über Ereignisse wie geplante Wartungen und Aktualisierungen. Störungen (Vorfälle) werden auf der Seite 'Status' gemeldet.

### Benachrichtigungen

Sie können Benachrichtigungen von IBM für Ihre lokale oder dedizierte Umgebung anzeigen, um den Status Ihrer Umgebung zu überwachen. Die folgende Tabelle enthält Informationen zu den verschiedenen Typen von Benachrichtigungen und zu den Positionen, an die diese gesendet werden.

*Tabelle 2. Ereignistypen und Benachrichtigungsmethoden*

| **Ereignistyp** | **Benachrichtigungsmethode** |       
|-----------------|-------------------|
| Wartungsaktualisierungen | Sie werden über bevorstehende Wartungsaktualisierungen in den Benachrichtigungen für die Seite 'Verwaltung' benachrichtigt. Wechseln Sie zur Seite **Verwaltung** und wählen Sie das Symbol **Benachrichtigungen** ![Benachrichtigungen](images/icon_announcement.svg) aus. Zum Anzeigen einer vollständigen Liste und des Verlaufs der anstehenden und abgeschlossenen Benachrichtigungen klicken Sie auf **Verwaltung &gt; Systeminformationen** &gt; *Anzahl* **Aktualisierungen stehen an**. Sie können die Benachrichtigungsfunktion erweitern, indem Sie ein Ereignisabonnement einrichten, das die Wartungsaktualisierungsalerts von der Seite 'Verwaltung' in einen Web-Service Ihrer Wahl integriert, um die Nachrichten an eine E-Mail-Adresse eines Help-Desks zu leiten oder eine SMS-Nachricht an eine Telefonnummer Ihrer Wahl zu senden. |
| Kritische Vorfälle | Sie werden über kritische Vorfälle auf der Seite 'Status' benachrichtigt. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Status** aus. Sie können die Benachrichtigungsfunktion erweitern, indem Sie ein Ereignisabonnement einrichten, das die Vorfallalerts von der Seite 'Status' in einen Web-Service Ihrer Wahl integriert, um die Nachrichten an eine E-Mail-Adresse eines Help-Desks zu leiten oder eine SMS-Nachricht an eine Telefonnummer Ihrer Wahl zu senden. |  
| Status | Sie können den neuesten Status für die Plattform, die Services und Ihre {{site.data.keyword.Bluemix_notm}}-Instanz anzeigen. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Status** aus.  |

### Ereignisabonnements einrichten

Sie können die Funktionalität der Benachrichtigungen, die an die Seiten 'Verwaltung' und 'Status' gesendet werden, durch Ereignisabonnements erweitern, die Web-Hooks implementieren. Web-Hooks leiten Ihre Benachrichtigungen direkt an ein Ziel Ihrer Wahl, wie zum Beispiel an eine E-Mail-Adresse eines Help-Desks (per E-Mail) oder an eine Telefonnummer (durch eine SMS-Nachricht). Sie können den Typ von Benachrichtigung, insbesondere Wartungsaktualisierungen oder Alerts über kritische Vorfälle, sowie die Informationen, die in der Benachrichtigung enthalten sind, anpassen.

Führen Sie die folgenden Schritte aus, um mithilfe von Web-Hooks ein bestimmtes Ereignisabonnement einzurichten:

* Für Benachrichtigungen über Wartungsaktualisierungen wechseln Sie zu **Systeminformationen** &gt; *Anzahl* **Aktualisierungen stehen an** und klicken auf das Symbol **Abonnieren** ![Abonnieren](images/icon_subscribe.svg).
* Für Benachrichtigungen über Vorfallalerts klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) &gt; **Status** und anschließend auf das Symbol **Abonnieren** ![Abonnieren](images/icon_subscribe.svg).

**Hinweis:** Sie können auf die Seite für Ereignisabonnements für beide Typen von Benachrichtigungen mit jeder der beiden beschriebenen Methoden zugreifen.

1. Klicken Sie auf **Abonnement hinzufügen**.

2. Füllen Sie das Formular für das Ereignisabonnement aus. Informationen zu den Feldern des Formulars und zu den Werten, die für den Abschnitt mit den Nutzdaten verwendet werden können, enthält die folgende Tabelle:

*Tabelle 3. Formularfelder für das Ereignisabonnement*

| **Feld** | **Beschreibung** |
|-----------------|-------------------|
| Typ | Wählen Sie Web-Hook aus. |
| Methode | Wählen Sie GET oder POST aus. |
| Ereignis | Wählen Sie aus, ob Benachrichtigungen für Aktualisierungen oder Vorfälle abonniert werden sollen. |
| URL | Geben Sie die URL ein, an die Ihr Web-Service angebunden werden soll. |
| Beschreibung | Fügen Sie eine Beschreibung für das Ereignisabonnement hinzu, das Sie erstellen. |
| Benutzername | Geben Sie Ihren Benutzernamen für den Web-Service ein. Wenn Sie nicht Ihre persönlichen Berechtigungsnachweise verwenden möchten, können Sie eine Funktions-ID speziell zur Verwendung mit {{site.data.keyword.Bluemix_notm}} einrichten. |
| Kennwort | Geben Sie das Kennwort für Ihren Web-Service ein. |
| Nutzdaten | Wenn Sie die Methode POST ausgewählt haben, geben Sie die Eigenschaften, die für den bestimmten Web-Service gelten, den Sie verwenden, gepaart mit den Werten, die für die IBM Benachrichtigung verwendet werden, ein. In der folgenden Tabelle finden Sie IBM Werte, die Sie für das Füllen Ihrer Benachrichtigungen verwenden können. Wenn Sie keine Informationen in diesem Abschnitt eingeben, empfangen Sie die Benachrichtigung ganz ohne zusätzliche Informationen. |

*Tabelle 4. Werte zum Abschnitt mit den Nutzdaten*

| **IBM Wert** | **Beschreibung** | **Ereignistyp** |
|----------------|----------------|------------------------|
| {{content.title}} | Nachrichtentitel |  Aktualisierung und Störung  |
| {{status}} | Status von Aktualisierung und Störung. | Aktualisierung und Störung |
| {{type}} | Aktualisierung und Störung | Aktualisierung und Störung | 
| {{region}} | Betroffene Region | Aktualisierung und Störung |
| {{content.message}} | Nachrichtenbeschreibung |   Aktualisierung und Störung  |
| {{content.severity}} | Sicherheitseinstufung | Störung |
| {{content.category}} | Betroffene Services | Störung |
| {{content.subCategoryName}} | Betroffene Komponenten | Störung |
| {{content.scheduleWindow}} | Das geplante Datum für die Aktualisierung | Aktualisierung |
| {{content.disruption}} | Betroffene Komponenten | Aktualisierung |

Nach dem Speichern des Ereignisabonnements empfangen Sie Benachrichtigungen durch die Methode, die Sie durch Ihren Web-Service eingerichtet haben. Benachrichtigungen werden weiterhin auf der Seite 'Status' für Vorfälle und im Bereich 'Benachrichtigungen' der Seite 'Verwaltung' für Wartungsaktualisierungen angezeigt.

Sie können ein beliebiges gespeichertes Ereignisabonnement auswählen und die letzte Aktivität anzeigen. Sie können auf einen Eintrag für eine kürzliche Aktivität klicken, um die zugehörigen Details anzuzeigen. Die Details beinhalten im Abschnitt 'Nutzdaten' die IBM Werte für die Benachrichtigung, die Sie verwenden können. Zum Anzeigen dieser Werte erweitern Sie den Eintrag für die kürzliche Aktivität, erweitern den Eintrag **Ereignis** und erweitern anschließend **Objekt**.

## Wartungsaktualisierungen
{: #oc_schedulemaintenance}

Sie können geplante und ausstehende Wartungsaktualisierungen anzeigen, indem Sie über **Verwaltung &gt; Systeminformation &gt; *Anzahl* Aktualisierungen stehen an
** auf die Seite **Systemaktualisierungen** zugreifen.  

**Hinweis**: Lesen Sie als Einführung den folgenden Abschnitt zur Einstellung vorab genehmigter Wartungszeiten. Diese Fenster müssen definiert sein, damit IBM die Wartungszeiten für Ihre Umgebung planen kann. 

<dl>
<dt>Unterbrechungsfreie Aktualisierungen</dt>
<dd>Eine unterbrechungsfreie Aktualisierung hat keine Auswirkungen auf Ihre Umgebung, Ihre aktiven Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen. Dieser Aktualisierungstyp erfordert keine fallspezifische Genehmigung und wird während der vorab genehmigten, verfügbaren Wartungszeiten angewendet, die Sie auf der Seite 'Systemaktualisierungen' festgelegt haben. </dd>
<dt>Aktualisierung mit Unterbrechungen</dt>
<dd>Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie müssen jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen. Sie können das vorgeschlagene Datum und die vorgeschlagene Uhrzeit auswählen, die auf den vorab genehmigten Aktualisierungsfenstern basieren, oder Sie können zwei weitere Uhrzeiten und Daten auswählen, aus denen IBM dann bei der Terminierung der Aktualisierung auswählt. </dd>
</dl>


### Vorab genehmigte Wartungszeiten einstellen
{: #preapprovedmaintenance}

Bevor Sie mit der Terminierung und Prüfung von Aktualisierungen beginnen, müssen Sie ihre vorab genehmigten Zeitfenster festlegen. Unterbrechungsfreie Aktualisierungen werden innerhalb der vorab genehmigten Zeiten geplant. Eine unterbrechungsfreie Aktualisierung hat keine Auswirkungen auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen. Dieser Aktualisierungstyp erfordert keine fallspezifische Genehmigung und wird innerhalb der vorab genehmigten, verfügbaren Wartungszeiten angewendet, die Sie auf der Seite 'Systemaktualisierungen' festgelegt haben. 

Sie müssen mindestens 24 verfügbare Stunden pro Woche an mindestens 3 Tagen der Woche festlegen. Sie können zum Beispiel drei 8-Stunden-Zeitfenster an drei verschiedenen Tagen festlegen oder an vier Tagen 6-Stunden-Zeitfenster. Um sicherzustellen, dass die Zeiträume ausreichend Zeit für das Anwenden einer Aktualisierung bieten, muss jeder Zeitraum mindestens 4 Stunden lang sein. 

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* Aktualisierungen stehen an &gt; Verfügbarkeit verwalten**.
2. Erweitern Sie den Abschnitt zum Thema **Verfügbare Aktualisierungszeiten verwalten**.
3. Klicken Sie auf **Neues hinzufügen** ![Neues hinzufügen](images/add-new.png).
4. Legen Sie das erste verfügbare Zeitfenster fest, indem Sie die Häufigkeit, die Dauer und die Anfangszeit für das Fenster auswählen. 
5. Klicken Sie auf **Abschicken**.
6. Wiederholen Sie diesen Vorgang, bis Sie die Mindestanforderungen für die wöchentlichen Zeitfenster erfüllt haben. 

### Nicht verfügbare Wartungszeiten festlegen

Nachdem Sie Ihre bereits genehmigten verfügbaren Wartungszeiten festgelegt haben, können Sie bestimmte Daten und Uhrzeiten festlegen, in denen Ihre Umgebung nicht für Aktualisierungen verfügbar ist. Sie möchten zum Beispiel ein Wochenende oder einen Feiertag mit hohem Datenverkehr auswählen, an denen Sie keine Wartung wünschen, damit die Anwendungen für Ihre Benutzer zur Verfügung stehen. 

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* Aktualisierungen stehen an &gt; Verfügbarkeit verwalten**.
2. Erweitern Sie den Abschnitt zum Thema **Nicht verfügbare Aktualisierungszeiten verwalten**.
3. Klicken Sie auf **Neues hinzufügen** ![Neues hinzufügen](images/add-new.png).
4. Legen Sie das erste nicht verfügbare Zeitfenster fest, indem Sie die Häufigkeit, die Dauer und die Anfangszeit für das Fenster auswählen. 
5. Klicken Sie auf **Abschicken**.

### Aktualisierungen planen und genehmigen
{: #scheduleandapprove}

Nachdem Sie Ihre vorab genehmigten Wartungszeiten festgelegt haben, werden unterbrechungsfreie Aktualisierungen automatisch während dieser Zeiten geplant. Ihre explizite Genehmigung für diese Aktualisierungstypen ist nicht erforderlich. Sie können jedoch die Details für jede Wartungsaktualisierung einschließlich der aktualisierten Komponenten, der Dauer der Aktualisierung und des geplanten Aktualisierungstermins anzeigen.  

Um die Details für eine unterbrechungsfreie Aktualisierung anzuzeigen, führen Sie die folgenden Schritte aus: 

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* Aktualisierungen stehen an**.
2. Suchen Sie Aktualisierungszeilen, bei denen für **Angepasste Terminplanung erforderlich** die Einstellung **Nein** festgelegt ist.
3. Wählen Sie die Zeile für die Aktualisierung aus, um die Details anzuzeigen.

Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie müssen jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen. Sie können die vorgeschlagenen Daten und die vorgeschlagenen Uhrzeiten auswählen, die auf den vorab genehmigten Aktualisierungsfenstern basieren, oder Sie können zwei weitere Uhrzeiten und Daten auswählen, aus denen IBM dann bei der Terminierung der Aktualisierung auswählt. 

Führen Sie für Aktualisierungen mit Unterbrechung, die Ihre Genehmigung erfordern, folgende Schritte durch: 

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* Aktualisierungen stehen an**.
2. Suchen Sie Aktualisierungszeilen, bei denen für **Angepasste Terminplanung erforderlich** die Einstellung **Ja** festgelegt ist.
3. Wählen Sie die Zeile für die Aktualisierung aus, um die Details für die Aktualisierung einschließlich der Aktualisierungsbeschreibung, des vorgeschlagenen Datums und der vorgeschlagenen Uhrzeit für die Aktualisierung, die betroffenen Komponenten sowie die Dauer der Aktualisierung zu überprüfen. 
4. Wählen Sie **Planen und Genehmigen** aus.
5. Wählen Sie aus den folgenden Optionen: **Vorgeschlagenes Datum**, **Alternative Daten** oder **Alle vorab genehmigten Zeiten** aus.
6. Wählen Sie **Abschicken** aus. 

Die Aktualisierung wird auf Grundlage Ihrer Auswahl an dem vorgeschlagenen Datum, das Sie genehmigt haben, während einer der von Ihnen vorab genehmigten Wartungszeiten oder an einem der alternativen Daten und zu einer der alternativen Uhrzeiten angewendet. Wenn das Plandatum für Ihre Aktualisierung durch IBM abgeschlossen ist, sehen Sie das geplante Datum in den Details zur Aktualisierung auf der Seite **Systemaktualisierungen**.

### Kalenderfeed für geplante Aktualisierungen einrichten

Sie können auf der Seite 'Systemaktualisierungen' auswählen, dass Ihr Plan für die Aktualisierung verfolgt wird, indem Sie auf das Symbol **Kalender** ![Kalender](images/icon_calendar.svg) klicken und die Datei mit der Erweiterung `.ics` herunterladen, um Ihre geplanten Aktualisierungen in eine Kalender-App mit vier Auswahloptionen zu importieren: 

<ol>
<li>Öffnen Sie die Kalender-App.</li>
<li>Laden Sie die Kalenderdatei herunter, indem Sie auf das Symbol **Kalender** ![Kalender](images/icon_calendar.svg) klicken und die Datei dann mithilfe der ICS-Datei (`.ics`) in Ihre Kalender-App importieren.</li>
<li>Geben Sie Ihre Berechtigungsnachweise ein.</li>
<li>Zeigen Sie die geplanten Aktualisierungen an.</li>
</ol>

Sie können die Benachrichtigungsfunktionalität für die Seite 'Verwaltung' auch durch Ereignisabonnements erweitern, um sie in einen Web-Service Ihrer Wahl zu integrieren. Informationen zur Einrichtung eines Abonnements für Ereignisbenachrichtigungen für eine Aktualisierung oder einen Vorfall finden Sie unter [Benachrichtigungen und Ereignisabonnements](index.html#oc_eventsubscription).

## Systeminformationen anzeigen
{: #oc_system}

Klicken Sie zum Anzeigen von Systeminformationen auf **Verwaltung &gt; Systeminformationen**.

Sie können verschiedene Abschnitte zu den anstehenden Wartungsaktualisierungen, allgemeinen Systeminformationen und LDAP-Konfigurationsdetails erweitern und anzeigen. 

### Anstehende Systemaktualisierungen

Im Bereich für die Aktualisierungen wird die Anzahl der Benachrichtigungen über anstehende Aktualisierungen angezeigt,
für die eine Aktion Ihrerseits erforderlich ist. Es gibt zwei Typen von Wartungsaktualisierungen, die Ihnen möglicherweise angezeigt werden: 

<dl>
<dt>Unterbrechungsfreie Aktualisierungen</dt>
<dd>Eine unterbrechungsfreie Aktualisierung hat keine Auswirkunge auf Ihre Umgebung, Ihre aktiven Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen. Dieser Aktualisierungstyp erfordert keine fallspezifische Genehmigung. Diese Aktualisierungen werden in den vorab genehmigten, verfügbaren Wartungszeiten, die Sie auf der Seite 'Systemaktualisierungen' festgelegt haben, angewendet. </dd>
<dt>Aktualisierung mit Unterbrechungen</dt>
<dd>Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie können jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen, um sicherzustellen, dass die Aktualisierung nicht während kritischer Geschäftszeiten angewendet wird. Sie können das vorgeschlagene Implementierungsdatum und die vorgeschlagene Uhrzeit auswählen, die auf den von Ihnen vorab genehmigten Aktualisierungszeiten basieren, oder Sie können zwei weitere Uhrzeiten und Daten auswählen, aus denen IBM dann bei der Anwendung der Aktualisierung auswählt. </dd>
</dl>

Weitere Informationen zum Festlegen vorab genehmigter Wartungszeiten, zum Festlegen bestimmter Zeiten, die für die Wartung nicht verfügbar sind und zum Festlegen eines Kalenderfeeds, finden Sie im Abschnitt zu [Wartungsaktualisierungen](index.html#oc_schedulemaintenance).

### Allgemeines Systeminformationen

Der Bereich für allgemeine Informationen enthält die folgenden Angaben:

- Basisinformationen zum {{site.data.keyword.Bluemix_notm}}-Build
- API-Informationen wie Version, URL und Region sowie einen Link zur CLI-Dokumentation
- Informationen der gemeinsamen Domäne zu Ihrem System und Service
- Statistiken zur Gesamtzahl der Anwendungen, Benutzer und Organisationen

### LDAP-Konfigurationsdetails

Im Bereich für die LDAP-Konfigurationsdetails können Sie den LDAP-Server
auswählen und Informationen zu Benutzer- und Gruppenzuordnungen anzeigen. Wenn Sie {{site.data.keyword.IBM}} WebID verwenden, wird dies in diesem Bereich angezeigt.

## Nutzungsinformationen und Berichte anzeigen
{: #oc_resource}

Sie können verschiedene Typen von Nutzungsinformationen für Ihre lokale oder dedizierte Instanz und das {{site.data.keyword.Bluemix_notm}}-Konto anzeigen. Sie können ferner Sicherheitsberichte und Protokolle für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz herunterladen und anzeigen. 

- Ressourceninformationen wie Plattenspeicher, CPU-Auslastung, Netzauslastung und durchschnittliche Antwortzeiten. Siehe [Ressourcennutzung](index.html#resourceusage).
- Kontonutzung pro Organisation, zum Beispiel die Anzahl von Laufzeit-Apps mit Nutzung, Gesamtzahl GB-Stunden für Laufzeiten und die Anzahl von Serviceinstanzen mit Nutzung. Siehe [Kontonutzung](index.html#accountusage).
- Speicherkontingentnutzung für Organisationen, zugeordneter App-Speicher auf der Basis des verwendeten Gesamtspeicherkontingents und Anzeige der GB-Stundennutzung pro App für eine bestimmte Organisation. Sie können außerdem die Kontingentnutzung für alle Organisationen auf der Seite 'Organisationsadministration' im Abschnitt 'Kontingentüberwachung' anzeigen. Siehe [Organisationsadministration](../admin/index.html#orgusage).


### Ressourcennutzung
{: #resourceusage}

Klicken Sie zum Anzeigen von Informationen zur Ressourcennutzung auf **Verwaltung &gt; Nutzung**.

Im Bereich für die Ressourcenüberwachung können Sie die folgenden Informationen anzeigen:

- Informationen zur Ressourcennutzung, z. B. der Umfang des belegten Hauptspeichers und
Plattenspeicherplatzes in GB. Sie können die durchschnittliche CPU-Auslastung für alle
DEA (Droplet Execution Agent) anzeigen. Klicken Sie auf die Kachel **CPU**, um die CPU-Auslastung für die
einzelnen DEA anzuzeigen. Der DEA mit dem höchsten Wert für die Auslastung
steht an erster Stelle und jeder einzelne DEA wird durch den zugehörigen Job und die IP-Adresse näher
spezifiziert. Die CPU-Auslastung ist in drei Kategorien unterteilt: der für Systemprozesse
aufgewendete Umfang der CPU-Auslastung, der für Benutzerprozesse
aufgewendete Umfang der CPU-Auslastung und der für Prozesse mit Wartestatus
aufgewendete Umfang der CPU-Auslastung.
- Informationen zur Netzauslastung für die Bandbreite bei Ein- und Ausgang, über einen vergangenen Tag, eine vergangene Woche oder einen vergangenen Monat hinweg.
Die angezeigten Daten basieren auf dem Gesamtwert zum ankommenden und abgehenden Datenverkehr für öffentliche und private Netze.
- Durchschnittliche Antwortzeit für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.
- Durchschnittliche Transaktionen pro Sekunde für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.

### Kontonutzung
{: #accountusage}

Sie können die monatliche Nutzung für Ihr Konto für Ihre dedizierte oder lokale Umgebung anzeigen. Mithilfe dieser Daten können Sie ermitteln, wie viel bestimmten Organisationen auf Grundlage ihrer Nutzung zu berechnen ist.

<ol>
<li>Klicken Sie auf das Symbol <strong>Konto und Unterstützung</strong> ![Konto und Unterstützung](../support/images/account_support.svg) &gt; <strong>Konto</strong> &gt; <strong>Nutzungsdetails</strong>.</li>
<li>Wählen Sie die Organisation aus, für die Daten angezeigt werden sollen.</li>
<li>Sie können Nutzungsdetails für die folgenden Kategorien anzeigen:
<ul>
<li>Laufzeit-Apps, für die Nutzung anfällt</li>
<li>Gesamtnutzung von Laufzeit-Apps in GB-Stunden</li>
<li>Serviceinstanzen, für die Nutzung anfällt</li>
</ul>
</li>
<li>Optional: Zeigen Sie Ihre Daten für einen bestimmten Monat an, indem Sie über das Menü <strong>Ihre Cloud-Aktivität</strong> einen gewünschten Monat auswählen.</li>
<li>Optional: Klicken Sie auf <strong>Daten exportieren</strong> und wählen Sie <strong>CSV</strong> oder <strong>JSON</strong> aus, um Ihre Daten für den ausgewählten Monat in eine <code>CSV</code>- oder <code>JSON</code>-Datei zu exportieren.</li>
</ol>

Sie können auch die monatliche Nutzung und die damit verbundenen Gebühren auf Kontoebene für Ihre Laufzeiten, Apps und Services anzeigen, die aus {{site.data.keyword.Bluemix_notm}} Public syndiziert wurden. Mithilfe dieser Daten können Sie ermitteln, wie viel bestimmten Organisationen auf Grundlage ihrer Nutzung zu berechnen ist.

<ol>
<li>Klicken Sie auf das Symbol <strong>Konto und Unterstützung</strong> ![Konto und Unterstützung](../support/images/account_support.svg) &gt; <strong>Konto</strong> &gt; <strong>Nutzungsdetails</strong>.</li>
<li>Klicken Sie auf <strong>Öffentlich</strong>.</li>
<li>Wählen Sie die Organisation aus, für die Daten angezeigt werden sollen, oder wählen Sie <strong>Alle Organisationen</strong> aus, um die Daten für alle Organisationen auf einmal anzuzeigen.</li>
<li>Sie können Nutzungsdetails für die folgenden Kategorien anzeigen:
<ul>
<li>Laufzeit-Apps, für die Nutzung anfällt</li>
<li>Gesamtnutzung von Laufzeit-Apps in GB-Stunden</li>
<li>Serviceinstanzen, für die Nutzung anfällt</li>
<li>Eine Gebührenzusammenfassung für alle syndizierten Laufzeiten, Services und Apps</li>
</ul>
</li>
<li>Optional: Zeigen Sie Ihre Daten für einen bestimmten Monat an, indem Sie den gewünschten Monat im Balkendiagramm auswählen. Standardmäßig werden die Daten für den aktuellen Monat angezeigt.</li>
<li>Optional: Klicken Sie auf <strong>Daten exportieren</strong> und wählen Sie <strong>CSV</strong> oder <strong>JSON</strong> aus, um Ihre Daten für den ausgewählten Monat in eine <code>CSV</code>- oder <code>JSON</code>-Datei zu exportieren.</li>
</ol>


### Organisationsnutzung
{: #orgusage}

Zum Anzeigen der Nutzung pro Organisation klicken Sie auf **Verwaltung &gt; Organisationsadministration** und wählen anschließend eine Organisation in der **Organisationsliste** aus. Auf der Seite **Organisationen verwalten** für die ausgewählte Organisation können Sie die folgenden Nutzungsinformationen anzeigen:

- Anzahl der Services, die zurzeit verwendet werden.
- Anzahl der Routen, die zurzeit verwendet werden.
- Speicherkontingentdiagramm, das zeigt, wie viel des Kontingents zurzeit verwendet und wie viel nicht verwendet wird.
- Diagramm zur Anwendungszuordnung, das zeigt, welche Anwendungen in dem Wert für das genutzte Speicherkontingent enthalten sind.
- Diagramm zur gemessenen Anwendungsnutzung, das einen dreimonatigen Bericht zu den genutzten GB-Stunden pro bereitgestellter App zeigt. Sie können die **Listenansicht** auswählen, um Daten für alle Apps mit Speicherzuordnung pro App und gemessener GB-Stundennutzung für die vergangenen drei Monate anzuzeigen.

Weitere Informationen zum Anzeigen der Nutzung pro Organisation, zum Anpassen von Kontingentplänen und zum Verwalten der Organisationen finden Sie unter [Organisationen verwalten](../admin/index.html#oc_organizations).

### Reports
{: #oc_report}

Sie können Sicherheitsberichte und -protokolle, wie DataPower&trade;-, Firewall- und Anmeldeprüfberichte für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz anzeigen. Klicken Sie zum Anzeigen von Berichten und Protokollen auf **Verwaltung &gt; Berichte und Protokolle**.

Es stehen Ihnen nun verschiedene Möglichkeiten zur Auswahl:

- Sie können in den Feldern Start- und Enddatum auswählen, um die Berichte und Protokolle zu filtern, die angezeigt werden.
- Sie können im Navigationsbereich verschiedene Berichte einblenden und anzeigen.
- Sie können Ihre Berichte und Protokolle durchsuchen. Bei der Suche werden die
Berichtsnamen ebenso wie der Textinhalt in den Berichten und Protokollen einbezogen. Sie können bei
der Suche auch Filter für Administrationsereignisse, DataPower-, Firewall- und
Anmeldeprüfungsberichte einsetzen.
- Beim Anzeigen eines Berichts oder eines Protokolls können Sie auf das Symbol ![Download](images/icon_download.png) klicken, um den Bericht bzw. das Protokoll herunterzuladen.

In der folgenden Tabelle sind Sicherheitsberichte aufgelistet, die für {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated generiert werden.

*Tabelle 5. Liste der Sicherheitsberichte*

| **Kategorie** | **Bericht** | **Beschreibung** |      
|-----------------|-------------------|---------------------|
| Firewall | Firewall-Anmeldungen | Ereignisse im Zusammenhang mit der Administratoranmeldung an den Vyatta-Firewall-Geräten. |
| Firewall | Firewall-Ablehnungen | Ereignisse, die von den Vyatta-Firewall-Geräten generiert werden, wenn eine Zugriffsanforderung im Einklang mit den bestehenden Firewallregeln abgelehnt wird. |
| {{site.data.keyword.Bluemix_notm}}-Administrator-Anmeldeereignisse | {{site.data.keyword.Bluemix_notm}}-Administratoranmeldung | Ereignisse, die vom Betriebssystem generiert werden, wenn ein Administrator eine SSH-Sitzung auf einem beliebigen {{site.data.keyword.Bluemix_notm}}-System startet. |
| {{site.data.keyword.Bluemix_notm}}-Anwendungsentwickler-Anmeldeereignisse | {{site.data.keyword.Bluemix_notm}}-Anwendungsentwickleranmeldung | Ereignisse, die von der Anmeldungskomponente der {{site.data.keyword.Bluemix_notm}}-Plattform generiert werden, wenn ein {{site.data.keyword.Bluemix_notm}}-Plattformbenutzer eine Sitzung über die Befehlszeile, die REST-APIs oder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle startet. |
| {{site.data.keyword.Bluemix_notm}}-Administrator-Verwaltungsereignisse | {{site.data.keyword.Bluemix_notm}}-Administrator-Verwaltungsereignisse des Betriebssystems | Ereignisse, die vom Betriebssystem generiert werden, wenn ein Administrator eine Aktion innerhalb einer aktuellen Arbeitssitzung ausführt. |
| {{site.data.keyword.Bluemix_notm}}-Anwendungsentwickler-Verwaltungsereignisse | {{site.data.keyword.Bluemix_notm}}-Verwaltungsereignisse (Cloud Foundry) | Ereignisse im Zusammenhang mit Operationen, die vom {{site.data.keyword.Bluemix_notm}}-Plattformbenutzer über die Befehlszeile, die REST-APIs oder die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle ausgeführt werden. |
| {{site.data.keyword.Bluemix_notm}}-Administrator-Datenbankverwaltungsereignisse | Datenbankverwaltungsereignisse | Ereignisse im Zusammenhang mit Operationen, die von einem Datenbankadministrator in den internen {{site.data.keyword.Bluemix_notm}}-Datenbanken ausgeführt werden. |
| Verwaltungsereignisse | Benutzerverwaltungsereignisse | Ereignisse im Zusammenhang mit Benutzerverwaltungsaktionen, die auf der Verwaltungsseite ausgeführt werden. |
| Verwaltungsereignisse | Catalog | Ereignisse im Zusammenhang mit Änderungen am Servicekatalog |
| Verwaltungsereignisse | Sicherheitsbericht-Verwaltungsereignisse | Ereignisse im Zusammenhang mit Sicherheitsbericht-Verwaltungsaktionen, die auf der Verwaltungsseite ausgeführt werden. |
| Zugriffsprüfungen | Bericht über Zugriffsprüfungen | Prüfungen für berechtigte Zugriffe. |
| Änderungsmanagement | Management von Softwareänderungen | Änderungsmanagementaktivität. |
| Schlüsselmanagement | Verwaltung von angepassten SSL-Zertifikaten | Angepasste SSL-Zertifikate, die hochgeladen und gespeichert wurden. |
| Verschlüsselung | Verschlüsselung von Daten bei der Übertragung | Konfigurierte Verschlüsselung von Daten bei der Übertragung. |
| Virenschutz | Bericht zum Virenscan | Installierte Virenschutzsoftware. |
| Software-Fix-Management | Patchanwendungsbericht | Angewendete Software-Fixes. |
| Verwaltung von Sicherheitsvorfällen | Bericht zur Korrektur von Sicherheitsvorfällen | Nachweis von Sicherheitsvorfällen für die Verwaltung von Sicherheitsvorfällen. |

## Status anzeigen
{: #oc_status}

Sie können den Status für die {{site.data.keyword.Bluemix_notm}}-Umgebung und für die Administrationskonsole anzeigen. 

### {{site.data.keyword.Bluemix_notm}}-Umgebungsstatus

Sie können den Status für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz über die {{site.data.keyword.Bluemix_notm}}-Statusseite anzeigen. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Status** aus.

Die Seite 'Status' ist die zentrale Position für die Suche nach Benachrichtigungen und Ankündigungen in Bezug auf bedeutende Ereignisse, die die {{site.data.keyword.Bluemix_notm}}-Plattform und die übergeordneten Services in {{site.data.keyword.Bluemix_notm}} betreffen. Sie können einen RSS-Feed abonnieren, damit Sie nicht immer überprüfen müssen, ob Sie eine Benachrichtigung erhalten haben. Weitere Informationen zur Seite 'Status' und zur Einrichtung des RSS-Feeds finden Sie in [{{site.data.keyword.Bluemix_notm}} anzeigen](../support/index.html#viewing-bluemix-status).

### Status der Administrationskonsole

Nach der ursprünglichen Implementierung Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung wird automatisch eine Verifizierungsprüfung für die Komponenten ausgeführt, die für die Verwaltung Ihrer Umgebung verwendet werden. Sie können auf die Seite 'Verifizierungsprüfung für Administratorkonsole' wechseln, um den Status der Komponenten nach dem Ausführen der Verifizierungsprüfung zu überprüfen. Um auf die Seite zuzugreifen, wechseln Sie zu <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>, wobei `<subdomain>` der Name Ihrer lokalen oder dedizierten Instanz ist. 

Sie können eine Verifizierung jederzeit ausführen. Sie müssen angemeldet sein, um die Option zur Ausführung der Verifizierung auszuführen. Wenn Fehler auftreten, während Sie einen Benutzer hinzufügen, eine Organisation bearbeiten oder Ihre Services verwalten, führen Sie diese Prüfung aus, um festzustellen, ob Komponenten fehlschlagen oder nicht verbunden sind. Sie können ein Support-Ticket mit den Informationen aus der Prüfung öffnen, um das Problem schnell zu beheben. 

## Eigenen Katalog verwalten
{: #oc_catalog}

Sie können die {{site.data.keyword.Bluemix_notm}}-Services und -Starter festlegen, die für Benutzer im {{site.data.keyword.Bluemix_notm}}-Katalog sichtbar sein sollen. Klicken Sie auf **Verwaltung &gt; Katalogverwaltung**.

Wählen Sie eine Kachel für einen Service oder einen Starter aus, um die Sichtbarkeit der betreffenden Service- oder Starterpläne zu bearbeiten. In Bezug auf die Sichtbarkeit stehen folgende Bearbeitungsoptionen zur Auswahl:

- Wählen Sie **Alle Pläne aktivieren** aus, wenn der ausgeblendete Service oder Starter für Benutzer im Katalog sichtbar sein soll.
- Wählen Sie **Alle Pläne inaktivieren** aus, wenn ein Service oder Starter ausgeblendet sein soll, damit er für die Benutzer im {{site.data.keyword.Bluemix_notm}}-Katalog nicht sichtbar ist.
- Soll die Sichtbarkeit eines einzelnen Plans gesteuert werden, wählen Sie den Namen des
betreffenden Plans aus. Wählen Sie dann im Dropdown-Menü zum Anzeigen des Plans für alle Organisationen die
Option **Für alle Organisationen aktivieren**, zum Ausblenden des Plans
bei allen Organisationen die Option **Für alle Organisationen inaktivieren** und zum
Anzeigen des Plans für bestimmte Organisationen die Option **Plan für bestimmte Organisationen aktivieren** aus.

<!-- staging only start -->

### Service-Broker registrieren
{: #servicebrokerui}

Wenn Sie einen Service haben, den Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Katalog anzeigen wollen, müssen sie einen Service-Broker implementieren und registrieren. Nach der Registrierung des Brokers können Sie die Organisationen auswählen, die auf den Service in Ihrer lokalen oder dedizierten Instanz zugreifen können.

Die Methoden zur Arbeit mit Ihrem Service-Broker variieren abhängig von der Anzahl der durch den Service-Broker verwalteten Services sowie davon, ob er bereits in {{site.data.keyword.Bluemix_notm}} registriert wurde.

- Wenn Ihr Service-Broker nur einen Service verwaltet, können Sie die Benutzerschnittstelle zum Registrieren des Brokers verwenden, nachdem Sie die [Service-Broker-API](http://docs.cloudfoundry.org/services/api.html){: new_window} implementiert haben. Siehe [Service-Broker registrieren, der nur einen Service verwaltet](index.html#registerbrokerui).
- Wenn Ihr Service-Broker mehrere Services gleichzeitig verwaltet, können Sie ihn nach der Implementierung der Service-Broker-API nicht registrieren. Verwenden Sie stattdessen die Befehlszeilenschnittstelle 'cf' mit dem [{{site.data.keyword.Bluemix_notm}}-Administrator-CLI](../cli/plugins/bluemix_admin/index.html)-Plug-in (Unterbefehl `ba`) oder die [API für angepasste Services](index.html#servicebrokerapi).
- Wenn Ihr Service-Broker bereits registriert ist und Sie ihn aktualisieren oder löschen wollen, verwenden Sie die Befehlszeilenschnittstelle mit dem [{{site.data.keyword.Bluemix_notm}}-Administrator-CLI](../cli/plugins/bluemix_admin/index.html)-Plug-in (Unterbefehl `ba`) oder die [API für angepasste Services](index.html#servicebrokerapi).

#### Service-Broker registrieren, der nur einen Service verwaltet
{: #registerbrokerui}

Führen Sie die folgenden Schritte aus, um Ihren Service-Broker zu registrieren:

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implementieren Sie die Cloud Foundry-Service-Broker-API</a>, um die Kommunikation zwischen Ihrem Service und {{site.data.keyword.Bluemix_notm}} einzurichten. Die Service-Broker-API besteht aus einer Gruppe von REST-Endpunkten, die von {{site.data.keyword.Bluemix_notm}} genutzt werden.<br />
<br />
<p>Wenn Sie den Service-Broker implementieren, müssen Sie in der JSON-Antwort von <code>GET /v2/catalog</code> die Definitionen für Ihren Service und Ihre Servicepläne, einschließlich der Serviceinformationen, die angezeigt werden sollen, angeben. Sehen Sie sich als Beispiel den folgenden JSON-Beispielcode der GET-Antwort für den Katalog an.</p>
<p><pre>
"services":[
   {
      "bindable":true,
      "description":"Cool Service ist eine Lösung für Data Warehousing und Analyse.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags":[
         "customer_dedicated"
      ],
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool",
         "longDescription":"Cool Service ist eine Lösung für Data Warehousing und Analyse. Sie können Ihre Daten rasch in eine speicherinterne spaltenbasierte Datenbank der nächsten Generation versetzen, um komplexe analytische Abfragen auszuführen.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service arbeitet mit dynamischer, speicherinterner und spaltenbasierter Technologie sowie mit Innovationen, wie paralleler Vektorverarbeitung und verlässlicher Komprimierung, um relevante Daten schnell zu scannen und zurückzugeben."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service ermöglicht schnelle Verbindungen zu all Ihren Services und Anwendungen. Sie können Ihre Daten sofort und mit leicht bedienbaren Tools analysieren."
            }
         ],
         "featuredImageUrl":"http://path/to/icon_64x64.png",
         "imageUrl":"http://path/to/icon_50x50.png",
         "mediumImageUrl":"http://path/to/icon_32x32.png",
         "smallImageUrl":"http://path/to/icon_24x24.png",
         "documentationUrl":"http://path/to/documentation.html",
         "instructionsUrl":"http://path/to/servicesample.md",
         "termsUrl":"http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type":"youtube",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/youtube/video",
               "caption":"Verwendung von Cool Service in 60 Sekunden"
            },
            {
               "type":"image",
               "thumbnailUrl":"http://path/to/thumbnail.png",
               "url":"http://path/to/image_file.png",
               "caption":"Cool Service verbindet Anwendungen"
            },
            {
               "type":"video",
               "thumbnailUrl":"http://path/to/thumb.png",
               "caption":"Cool Service arbeitet mit Tabelle",
               "source":[
                  {
                     "type":"video/mp4",
                     "url":"http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Dediziertes Schema und dedizierter Tabellenbereich pro Serviceinstanz auf einem gemeinsam genutzten Server. 1 GB und 10 GB komprimierter Datenbankspeicher kann bis zu 5 GB bzw. 50 GB unkomprimierter Daten nach typischen Komprimierungsverhältnissen aufnehmen.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata":{
               "bullets":[
                  "1 GB Minimum pro Instanz. 10 GB Maximum pro Instanz."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>Hinweis:</strong> Wenn Sie einen Service-Broker für eine lokale oder dedizierte Umgebung erstellen, müssen Sie den Wert `customer_dedicated` im Feld "tags" Ihrer JSON-Servicedefinitionsdatei angeben.</p>
</li>
<li>Wechseln Sie nach der Implementierung der Service-Broker-API zu <strong>Verwaltung</strong> &gt; <strong>Katalogverwaltung</strong>.</li>
<li>Klicken Sie auf <strong>Service-Broker registrieren</strong>.</li>
<li>Füllen Sie das Formular aus, indem Sie Werte in die folgenden Felder eingeben:
<ul>
<li>Name des Service-Brokers</li>
<li>URL des Service-Brokers</li>
<li>Benutzername des Service-Brokers</li>
<li>Kennwort des Service-Brokers</li>
</ul>
</li>
<li>Klicken Sie auf <strong>Verbindung herstellen</strong>.</li>
<li>Prüfen Sie die Informationen für Ihren Service, einschließlich verfügbarer Pläne, Symbol und Servicebeschreibung.<br />
<p><strong>Hinweis:</strong> Wenn Sie die Kataloginformationen für den Service ändern müssen, aktualisieren Sie Ihren Service-Broker und starten Sie den Registrierungsprozess erneut, indem Sie das Formular ausfüllen.</p>
</li>
<li>Klicken Sie auf <strong>Registrierung</strong>.</li>
<li>Aktivieren Sie alle Pläne oder nur bestimmte Pläne für den Service. Alle Pläne sind standardmäßig inaktiviert.</li>
<li>Aktivieren Sie die Serviceinstanz für alle Organisationen oder für bestimmte Organisationen.</li>
</ol>

Sie können jetzt Ihren Service in der Kategorie 'Angepasste Services' Ihres {{site.data.keyword.Bluemix_notm}}-Katalogs anzeigen. Wechseln Sie zu **Verwaltung &gt; Katalogverwaltung** und wählen Sie die Kachel im Katalog aus. Sie können verschiedene Pläne aktivieren und die Plansichtbarkeit jederzeit für Ihre Organisation bearbeiten.

## Organisationen verwalten
{: #oc_organizations}

Sie können Ihre Organisationen verwalten, indem Sie Organisationen erstellen und löschen, Manager für Organisationen hinzufügen oder entfernen und die Kontingentnutzung überwachen, um optimale Entscheidungen für Ihr Geschäft zu treffen.

Klicken Sie auf **Verwaltung &gt; Organisationsadministration**.

Sie können verschiedene Bereiche erweitern und anzeigen. Darüber hinaus können Sie
Kontingentpläne für Ihre Organisationen überprüfen und verwalten.

### Organisationen erstellen

Führen Sie zum Erstellen einer neuen Organisation sowie zum Hinzufügen von Managern die folgenden Schritte aus:

1. Klicken Sie auf <strong>Organisation erstellen</strong>.
2. Geben Sie einen Namen für die Organisation ein.
3. Geben Sie den Namen oder die E-Mail-Adresse der Person ein, die als Manager hinzugefügt werden soll. Geben Sie
mehrere Namen ein bzw. wählen Sie mehrere Namen aus, wenn Sie mehrere Manager hinzufügen möchten.
4. Klicken Sie auf <strong>Organisation erstellen</strong>, um die Änderungen zu speichern und die Organisation zu erstellen.

### Bereiche erstellen

Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps den Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Wählen Sie die Organisation aus, der Sie einen Bereich hinzufügen möchten. 
3. Klicken Sie auf **Bereich erstellen**.
4. Geben Sie einen Bereichsnamen ein.
5. Klicken Sie auf **Erstellen**.

### Kontingentüberwachung

Erweitern Sie den Bereich für die Kontingentüberwachung, um Informationen zu den folgenden Punkten anzuzeigen:

- Hauptspeichernutzung für Umgebung. In diesem Bereich finden Sie Details zur Speicherbelegung für die gesamte Systemumgebung.
	Das Diagramm enthält Informationen zum belegten Systemspeicher, gesamten Systemspeicher,
ausgeschöpften Kontingent und zum insgesamt zugeordneten Kontingent. Die folgende Liste definiert die Typen der Speicherbelegung, die im Diagramm angezeigt werden.

	<dl>
	<dt><strong>Belegter Systemspeicher</strong></dt>
	<dd>Der physische Speicher, der von der Umgebung belegt wird.</dd>
	<dt><strong>Gesamter Systemspeicher</strong></dt>
	<dd>Der gesamte physische Speicher, der für die Umgebung zur Verfügung steht.</dd>
	<dt><strong>Kontingent bereitgestellt</strong></dt>
	<dd>Die Summe des Speichers, der für alle bereitgestellten Apps in allen Organisationen zugeordnet
ist. Die Summe für
	das bereitgestellte Kontingent kann über dem Wert für den gesamten physischen Systemspeicher für die Umgebung liegen. Wenn der gesamte Systemspeicher z. B. eine Größe von 16 GB
aufweist und Sie jeweils 4 GB an Speicher für fünf verschiedene Organisationen zuordnen, liegt die
Summe der Kontingente über dem Wert für den gesamten Systemspeicher, der Ihnen für alle Organisationen
zugeordnet wurde. In vielen Fällen wird das Kontingent, das
den einzelnen Organisationen zugeordnet ist, von den Organisationen jedoch gar nicht in vollem Umfang
genutzt. Darüber hinaus gilt auch, dass
nicht alle Organisationen gleichzeitig das gesamte Kontingent an Speicher nutzen, das ihnen zugeordnet
ist. </dd>
	<dt><strong>Gesamtkontingent</strong></dt>
	<dd>Der gesamte Speicher, der für die Organisationen zugeordnet ist.</dd>
	</dl>

- Hauptspeichernutzung für Organisation. Dieser Bereich enthält Details zur Speicherbelegung auf
Organisationsebene. Sie können das gesamte verfügbare Kontingent anzeigen sowie das Kontingent, das
jeweils für die einzelnen Organisationen verfügbar ist. Das Diagramm liefert Informationen, die nach
der höchsten Speicherbelegung pro Organisation geordnet sind. Die Organisation, die den größten
Speicherumfang belegt, wird standardmäßig an erster Stelle angezeigt. Sie können die Liste nach
der höchsten Speicherbelegung und der überschüssigen Speicherzuordnung sortieren.

	<dl>
	<dt><strong>Höchste Speichernutzung</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option für die höchste Speicherbelegung die Organisation, die den
meisten Speicher belegt. Sortieren Sie die Liste nach der höchsten
	Speicherbelegung, um die Organisationen zu ermitteln, die den meisten
Speicher belegen. Die Liste ist nach dem bereitgestellten Kontingent sortiert. </dd>
	<dt><strong>Überschüssige Hauptspeicherzuordnung</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option für überschüssige Speicherzuordnung
Organisationen mit einem Kontingentplan, der mehr Speicher als erforderlich zuordnet.
	Sortieren Sie die Liste nach der überschüssigen Speicherzuordnung, um Organisationen zu ermitteln,
die im Verhältnis zu dem jeweils zugeordneten Speicher am wenigsten Speicher belegen. </dd>
	</dl>

### Kontingentpläne anpassen

Führen Sie die folgenden Schritte aus, um den Kontingentplan für eine Organisation zu ändern:

<ol>
<li>Klicken Sie im Abschnitt 'Hauptspeichernutzung für Organisation' auf den Balken im Diagramm für die Organisation, die bearbeitet werden
soll, oder wählen Sie den Namen der Organisation im Bereich 'Organisationsliste' aus.</li>
<li>Auf der Seite 'Organisation verwalten' können Sie den Kontingentplan und
den Organisationsnamen ändern und Manager hinzufügen oder entfernen.<br />
<p><strong>Hinweis:</strong> Wenn Sie einen Kontingentplan auswählen, der für die aktuelle Speichernutzung
einer Organisation nicht ausreicht, erhalten Sie eine Nachricht.</p>
</li>
<li>Speichern Sie Ihre Änderungen auf der Seite 'Organisation verwalten', indem Sie auf <strong>Speichern</strong> klicken.</li>
</ol>

### Organisationen über die Organisationsliste verwalten

Im Bereich der Organisationsliste werden alle Organisationen in der
{{site.data.keyword.Bluemix_notm}}-Umgebung angezeigt und Sie können Aktionen für einzelne
Organisationen durch Klicken auf den Organisationsnamen ausführen.

- Löschen Sie eine Organisation, indem Sie auf das Symbol **Löschen** ![Löschen](images/icon_trash.svg) in der Spalte 'Aktionen' klicken.
- Zeigen Sie den Kontingentplan für eine Organisation an, indem Sie auf den Namen der Organisation in der Liste klicken. Auf der Seite **Organisationen verwalten** für die ausgewählte Organisation können Sie die folgenden Nutzungsinformationen anzeigen:

  - Anzahl der Services, die zurzeit verwendet werden.
  - Anzahl der Routen, die zurzeit verwendet werden.
  - Speicherkontingentdiagramm, das zeigt, wie viel des Kontingents zurzeit verwendet und wie viel nicht verwendet wird.
  - Diagramm zur Anwendungszuordnung, das zeigt, welche Anwendungen in dem Wert für das genutzte Speicherkontingent enthalten sind.
  - Diagramm zur gemessenen Anwendungsnutzung, das einen dreimonatigen Bericht zu den genutzten GB-Stunden pro bereitgestellter App zeigt. Sie können die **Listenansicht** auswählen, um Daten für alle Apps mit Speicherzuordnung pro App und gemessener GB-Stundennutzung für die vergangenen drei Monate anzuzeigen.

- Zum Bearbeiten des Namens der Organisation sowie zum Hinzufügen oder Entfernen von Managern klicken Sie auf den Namen
der Organisation in der Liste und folgen den Anweisungen auf der Anzeige.

## Benutzer und Berechtigungen verwalten
{: #oc_useradmin}

Sie können Ihrer {{site.data.keyword.Bluemix_notm}}-Instanz aus der Benutzerregistry Ihres Unternehmens über LDAP
Benutzer hinzufügen. Sie können
Benutzer einzeln oder in Gruppen hinzufügen und die Benutzerberechtigungen anzeigen. Wenn Ihnen die
Berechtigung `admin` zugewiesen ist, können Sie auch Berechtigungen für andere Benutzer festlegen
und verwalten. Klicken Sie auf **Verwaltung &gt; Benutzeradministration**.

Auf der Seite für die Benutzerverwaltung werden alle Benutzer für die lokale oder dedizierte Instanz angezeigt.
Die Berechtigungen für jeden Benutzer werden angezeigt. Die folgenden Berechtigungen sind verfügbar: None,
`Admin`, `Catalog`, `Login`,
`Reports` und `Users`. Berechtigungen können aktiviert werden oder dem
Benutzer kann der Zugriff `view` bzw. `write` für diese Berechtigung
erteilt werden; diese werden durch Symbole dargestellt. Beschreibungen der
einzelnen Typen und Erläuterungen der Symbole finden Sie unter [Berechtigungen](index.html#permissions).

### Mit Benutzern arbeiten

Sie können nach vorhandenen Benutzern suchen, Benutzer entfernen und Benutzer einzeln oder in Gruppen hinzufügen. Es stehen verschiedene Optionen zur Auswahl:

* Nach Benutzern suchen. Sie können mithilfe des Feldes **Suchen** Benutzer in der Tabelle suchen.

* Fügen Sie einen einzelnen Benutzer hinzu. Wenn Sie die Berechtigung `admin` oder die Berechtigung
`users` mit dem Zugriff `write` besitzen, können Sie Benutzer hinzufügen.

  1. Um einen einzelnen Benutzer aus Ihrem LDAP-Verzeichnis hinzuzufügen, klicken Sie auf **Benutzer hinzufügen**.
  2. Geben Sie im Feld **Suche** die E-Mail-Adresse für den Benutzer ein und wählen Sie anschließend den Benutzer aus der gefüllten Liste aus.
  3. Wählen Sie neben dem Feld **Organisation** die Organisation aus, zu der Sie den Benutzer hinzufügen möchten, indem Sie den Namen der Organisation eingeben und diesen aus der gefüllten Liste auswählen. 
  4. Klicken Sie auf **Benutzer hinzufügen**, um den Benutzer zur ausgewählten Organisation hinzuzufügen.

  **Hinweis**: Wenn die Operation zum Hinzufügen erfolgreich ist, wird der Benutzer für Sie zum Anzeigen und zum Durchsuchen zu der Tabelle hinzugefügt. Wenn Benutzer hinzugefügt werden,
sind ihnen keine Berechtigungen zugewiesen.

* Fügen Sie eine Benutzergruppe aus Ihrem LDAP-Verzeichnis hinzu. 

  1. Klicken Sie auf **Benutzergruppe hinzufügen**.
  2. Geben Sie im Feld **Suche** einen Gruppennamen für die Suche ein und wählen Sie den Gruppennamen aus der gefüllten Liste aus. 
  3. Wählen Sie neben dem Feld **Organisation** die Organisation aus, zu der Sie die Benutzergruppe hinzufügen möchten, indem Sie den Namen der Organisation eingeben und diesen aus der gefüllten Liste auswählen. 
  4. Klicken Sie auf **Benutzer hinzufügen**, um die Benutzergruppe zu der ausgewählten Organisation hinzuzufügen.
  **Hinweis**: Gruppen oder mehr als 50 Benutzer werden über einen Stapeljob im Hintergrund hinzugefügt. Wenn die Hinzufügeoperation erfolgreich war, wird der Benutzer bzw. die Gruppe
zur Tabelle hinzugefügt und Sie können ihn bzw. sie anzeigen und durchsuchen. Wenn Benutzer hinzugefügt werden,
sind ihnen keine Berechtigungen zugewiesen.

* Eine Gruppe von Benutzern hinzufügen, indem ein Arbeitsblatt importiert wird, das die Benutzer-IDs, E-Mail-Adressen und die Organisation enthält, zu der Sie die Benutzer hinzufügen möchten. 

  1. Klicken Sie auf **Benutzer importieren**.
  2. Klicken Sie auf **Vorlage herunterladen (.CSV)**, um ein Arbeitsblatt mit den erforderlichen Spalten herunterzuladen, das Sie ausfüllen können, oder um Ihre eigenes Arbeitsblatt zu erstellen, das mindestens die folgenden erforderlichen Spaltenüberschriften enthält: **Benutzer-ID**, **E-Mail**, **Organisation**.
  3. Geben Sie die Benutzerwerte in die erforderlichen Spalten ein. Falls Sie kein LDAP-Verzeichnis verwenden, verwenden Sie die erforderlichen Spaltenüberschriften **Vorname** und **Nachname** für Ihren Benutzerimport. 
  4. Speichern Sie Ihre Datei und klicken Sie auf **Datei hochladen**.
 

  **Hinweis**: Geben Sie die Benutzer-IDs ein, die mit den in Ihrer Benutzerregistry verwendeten Werten übereinstimmen. Die Spalten innerhalb des Arbeitsblatts können in beliebiger Reihenfolge angeordnet sein, solange Sie über alle erforderlichen Spalten verfügen. Sie empfangen eine Bestätigungsnachricht, die besagt, dass alle Benutzer hinzugefügt wurden, wenn der Import erfolgreich war. Wenn der Import für einige Benutzer erfolgreich war, für andere hingegen nicht, prüfen Sie die Fehlernachricht, um Aktionen für die Benutzer zu ergreifen, die nicht hinzugefügt werden konnten. 

* Entfernen Sie Benutzer. Wenn Sie die Berechtigung `admin` oder die Berechtigung
`users` mit dem Zugriff `write` besitzen, können Sie Benutzer entfernen.

    1. Suchen Sie den Benutzer und klicken Sie auf das Symbol ![Löschen](images/icon_trash.svg). 
    2. Klicken Sie auf **Entfernen**.

### Berechtigungen
{: #permissions}

Benutzern können die folgenden Berechtigungen zugewiesen werden:

*Tabelle 6. Berechtigungen*

| **Benutzerberechtigung** | **Beschreibung** |       
|-----------------|-------------------|
| Admin | Benutzer mit der Berechtigung `admin` können Berechtigungen für andere Benutzer bearbeiten. |
| Catalog | Benutzern mit der Berechtigung `catalog` kann der Zugriff auf `view` (Anzeigen) oder `write` (Ändern) zugewiesen werden, und zwar für die in der lokalen oder dedizierten Instanz verfügbaren Services. |  
| Login | Benutzer mit der Berechtigung `login` sind berechtigt, die Verwaltungsseite anzuzeigen. Ohne diese Berechtigung wird Benutzern die Menüoption 'Verwaltung' nicht angezeigt. |
| Reports | Benutzern mit der Berechtigung `reports` kann für Sicherheitsberichte der Zugriff `view` (Anzeigen) oder `write` (Ändern) zugewiesen werden. |
| Users | Benutzern mit der Berechtigung `users` kann der Zugriff `view` (Anzeigen) für die Benutzerliste oder `write` (Hinzufügen oder Entfernen) für Benutzer zugewiesen werden. Diese Berechtigung erlaubt es Ihnen nicht, Berechtigungen für andere Benutzer festzulegen.|


Berechtigungen können aktiviert werden oder dem Benutzer kann der Zugriff `view` bzw.
`write` für diese Berechtigung erteilt werden; dies wird durch die folgenden Symbole dargestellt:

* Das Symbol ![Aktiviert; dargestellt durch ein Hakensymbol](images/icon_enabled.svg) neben einer Berechtigung bedeutet, dass diese Berechtigung aktiviert ist.
* Das Symbol ![Anzeigen: dargestellt durch ein Augensymbol](images/icon_read.svg) bedeutet, dass der Benutzer für diese Berechtigung über den Zugriff `view` (schreibgeschützt) verfügt.
* Das Symbol ![Schreiben: dargestellt durch ein Stiftsymbol](images/icon_write.svg) bedeutet, dass der Benutzer für diese Berechtigung über den Zugriff `write` (Bearbeiten, Hinzufügen oder Entfernen) verfügt.

Die Bearbeitung von Berechtigungen und Organisationen für andere Benutzer erfordert, dass Sie über die Berechtigung `admin` verfügen. Um Berechtigungen zu bearbeiten,
suchen Sie den gewünschten Benutzer und klicken Sie auf den Benutzernamen. Auf der Seite **Benutzer bearbeiten** können Sie die Berechtigungen aktivieren oder inaktivieren. 

* Wählen Sie **On** in der Liste aus, um eine Berechtigung zu aktivieren.
* Wählen Sie in der Liste **Lesen** (Read) aus, um dem Benutzer Lesezugriff `view` für diese Berechtigung zu erteilen, oder wählen Sie **Schreiben** (Write) aus, um dem Benutzer Schreibzugriff `write` zum Bearbeiten, Hinzufügen und Entfernen für diese Berechtigung zu erteilen. 
* Wählen Sie **Off** aus, um die Berechtigung zu inaktivieren.

Wählen Sie die folgenden Optionen aus, um einen Benutzer zu einer Organisation hinzuzufügen oder zu entfernen: 

* Wählen Sie den Benutzernamen in der Tabelle aus, um auf die Anzeige **Benutzer bearbeiten** zuzugreifen und einen Benutzer zu einer Organisation hinzuzufügen. Verwenden Sie anschließend das Suchfeld, um eine Organisation zu lokalisieren, und wählen Sie die Organisation aus der Liste aus. Klicken Sie anschließend auf **Speichern**.
* Wählen Sie den Benutzernamen in der Tabelle aus, um auf die Anzeige **Benutzer bearbeiten** zuzugreifen und einen Benutzer aus einer Organisation zu entfernen. Klicken Sie anschließend für die Organisation, aus der der Benutzer entfernt werden soll, auf ![Entfernen](images/icon_remove.svg) und dann auf **Speichern**.


## Benutzer mit der Admin-REST-API verwalten
{: #usingadminapi}

Sie können die REST-API `Admin` verwenden, um Benutzer für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz hinzuzufügen und zu entfernen.
Die Endpunkte und JSON-Antworten der `Admin`-REST-API
werden probeweise zu Verfügung gestellt, um Basisoperationen über eine
Befehlszeile zu ermöglichen. Die in den vorliegenden Informationen zu den Beispielen
enthaltenen Endpunkte und URLs können jederzeit geändert oder entfernt werden.

Die folgenden Tools sind Voraussetzungen für die Verwendung der nachfolgenden Beispiele. Wenn Sie möchten, können Sie auch andere Tools verwenden.
* cURL für die Eingabe von REST-API-Anforderungen als Befehle. cURL ist
ein Dienstprogramm zur freien Verwendung, mit dessen Hilfe Sie über eine Befehlszeilenschnittstelle
HTTP-Anforderungen an einen Server senden und Antworten vom Server empfangen können. Sie können
cURL von der [cURL Download-Site](http://curl.haxx.se/download.html){: new_window} herunterladen.
* Python für die Verwendung des Python-Tools für JSON-Schöndruck. Dieses optionale
Tool akzeptiert JSON-Text als Eingabe und stellt eine übersichtliche Ausgabe zur Verfügung. Sie können Python von der [Python Download-Site](https://www.python.org/downloads){: new_window} herunterladen.

### Bei der Administrationskonsole anmelden

Vor dem Ausführen von `Admin`-API-Anforderungen müssen Sie sich
bei der Administrationskonsole anmelden. Wenn Sie die Berechtigung `admin` oder die
Berechtigung `users` mit dem Zugriff `write` besitzen, können Sie
Benutzer hinzufügen und Benutzer entfernen. Zum Bearbeiten der Berechtigungen anderer Benutzer
benötigen Sie die Berechtigung `admin`.

Zum Anmelden bei der Administrationskonsole können Sie die Basiszugriffsauthentifizierung am Endpunkt
`https://<eigener Host>.ibm.com/login` verwenden. Der Server gibt ein Cookie mit Ihrer Sitzung zurück. Dieses Cookie verwenden Sie für alle Operationen mit der Administrationskonsole.

**Anmerkung:** Die Sitzung wird ungültig, wenn Sie mehrere Stunden lang nicht genutzt wird.

Führen Sie zum Anmelden bei der Administrationskonsole den folgenden Befehl aus:

`curl --user <Benutzer-ID>:<Kennwort> -c ./cookies.txt --header "Accept: application/json" https://<eigener Host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>Benutzer-ID</em>:<em>Kennwort</em></dt>
<dd class="pd">Akzeptiert die Benutzer-ID und das Kennwort und sendet einen Header für die Basisauthentifizierung.</dd>


<dt class="pt dlterm">-c <em>Dateiname</em></dt>
<dd class="pd">Speichert die angegebene Benutzer-ID und das angegebene Kennwort als Cookie in der angegebenen Datei.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Sendet einen Akzeptanzheader.</dd>

</dl>

Das folgende Beispiel zeigt die Ausgabe dieses Befehls:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*Nachname*",
        "givenName": "*Vorname*"
    }
}
```
{: screen}

### Organisationen auflisten
{: #listingorg}

Beim Hinzufügen eines Benutzers müssen Sie eine Organisation angeben. Sie können die
`Admin`-REST-API verwenden, um alle Organisationen aufzulisten. Zum Auflisten der
Organisationen müssen Sie die Berechtigung `users` mit dem Zugriff `read`
besitzen. Führen Sie zum Auflisten von Organisationen den folgenden Befehl aus:

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option
<samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>

</dl>

Für jede Organisation werden die folgenden Informationen zurückgegeben:
* `"guid"`, die GUID der Organisation
* `"name"`, der Name der Organisation

Das folgende Beispiel zeigt die Ausgabe dieses Befehls:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### Benutzer auflisten
{: #listingusr}

Sie können feststellen, ob ein Benutzer bereits zu Ihrer
{{site.data.keyword.Bluemix_notm}}-Umgebung hinzugefügt wurde, und zwar mithilfe der REST-API `Admin` zum
Auflisten der registrierten Benutzer. Zum Auflisten der registrierten Benutzer müssen Sie die Berechtigung
`users` mit dem Zugriff `read` besitzen. Zum Auflisten aller Benutzer
führen Sie den folgenden Befehl aus:

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option
<samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>
</dl>

Für jeden registrierten Benutzer werden die folgenden Informationen zurückgegeben:
* `"first_name"` (Vorname) und `"last_name"` (Familienname)
* `"user_id"`, die Benutzer-ID und die E-Mail-Adresse
* `"guid"`, die GUID der Organisation
* `"permissions"`, die dem Benutzer erteilten Berechtigungen für die Administrationskonsole

Das folgende Beispiel zeigt die Ausgabe dieses Befehls:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Benutzer hinzufügen

Sie können die REST-API `Admin` verwenden, um
Benutzer zur {{site.data.keyword.Bluemix_notm}}-Instanz
hinzuzufügen. Zum Hinzufügen von Benutzern müssen Sie die Berechtigung `users`
mit dem Zugriff `write` besitzen.

Sie können einen Benutzer oder eine Liste von Benutzern hinzufügen. Dabei können Benutzer einer
einzelnen Organisation oder mehreren Organisationen hinzugefügt werden. Zum Hinzufügen eines Benutzers
müssen Sie die folgenden Informationen angeben:

* Vorname (fist_name) und Familienname (last_name) des Benutzers. Geben Sie den Vornamen
(`"first_name"`) und den Familiennamen (`"last_name"`) aus [Benutzer auflisten](index.html#listingusr) an.
* E-Mail-Adresse und Benutzer-ID: Geben Sie die Benutzer-ID (`"user_id"`) aus [Benutzer auflisten](index.html#listingusr) für die E-Mail-Adresse und für die Benutzer-ID an.
* `"guid"`. Geben Sie die GUID der Organisation aus [Organisationen auflisten](index.html#listingorg) an.

Diese Informationen werden in einer JSON-Datei angegeben.

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option
<samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>
</dl>

<ol>
<li>Erstellen Sie eine JSON-Datei, die die Informationen in einem ordnungsgemäßen JSON-Format enthält.
<p>Erstellen Sie beispielsweise eine Datei namens `user.json` mit dem
folgenden Inhalt:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "eine_benutzer-id@domäne.com"
            ],
            "first_name": "ein_vorname",
            "last_name": "ein_nachname",
            "user_id": "eine_benutzer-id@domäne.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Führen Sie den folgenden Befehl aus, um den Inhalt der JSON-Datei an den
Endpunkt des Benutzers zu übergeben:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<Ihr Host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Gibt die Ausgabe mit ausführlichen Informationen an.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Gibt eine POST-Anforderung an, die die standardmäßige GET-Anforderung außer Kraft setzt.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Gibt den Inhaltstypheader an (in diesem Beispiel JSON).</dd>


<dt class="pt dlterm">-d *daten*</dt>
<dd class="pd">Gibt die Daten an (in diesem Beispiel die Datei `user.json`),
die in der POST-Anforderung an den HTTP-Server gesendet werden sollen.</dd>

</dl>



Das folgende Beispiel zeigt die Ausgabe dieses Befehls:

```
* Connected to localhost (127.0.0.1) port 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completely sent off: 333 out of 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Benutzer entfernen

Sie können die REST-API `Admin` verwenden, um
Benutzer aus der {{site.data.keyword.Bluemix_notm}}-Instanz
zu entfernen. Zum Entfernen von Benutzern müssen Sie die Berechtigung
`users` mit dem Zugriff `write` besitzen.

Beim Entfernen eines Benutzers müssen Sie die Benutzer-ID des Benutzers angeben. Führen Sie den folgenden Befehl aus:

`curl -v -b ./cookies.txt -X DELETE https://<eigener Host>.ibm.com/codi/v1/users?user_id=<Benutzer-ID@Domäne.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Gibt eine DELETE-Anforderung an.</dd>
</dl>

Das folgende Beispiel zeigt die Ausgabe dieses Befehls:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Connected to localhost (127.0.0.1) port 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}


## API für angepasste Services
{: #servicebrokerapi}

Es gibt drei APIs, die Sie zum Registrieren oder Erstellen eines neuen Service, zum Aktualisieren eines Service und zum Löschen eines Service verwenden können.

Alle APIs beziehen sich auf <code>https://console.&lt;Unterdomäne&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;Unterdomäne&gt;</strong></dt>
<dd>Dieser Wert steht für den Namen der lokalen oder dedizierten Instanz. Der Unterdomänenname für Ihre {{site.data.keyword.Bluemix}}-Instanz wurde beim Onboarding zugeordnet.</dd>
</dl>

## Neuen Service registrieren

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Registrieren eines neuen Service.

### Route
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Anforderung
{: #registerrequest}

*Tabelle 7. Felder*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |


#### Hauptteil
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Header
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Antwort
{: #registerresponse}

#### Status
{: #registerstatus}

```
201 Created
```
{: screen}

#### Hauptteil
{: #registerbody2}

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

## Service aktualisieren

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Aktualisieren eines Service.

### Route
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Anforderung
{: #updaterequest}

*Tabelle 8. Felder*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |


#### Hauptteil
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Header
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Antwort
{: #updateresponse}

#### Status
{: #updatestatus}

```
201 Created
```
{: screen}

#### Hauptteil
{: #updatebody2}

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## Service löschen

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Löschen eines Service.

*Tabelle 9. Parameter*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |


### Route

```
DELETE /codi/v1/serviceBrokers?name=Name des Service-Brokers
```
{: screen}

### Anforderung
{: #deleterequest}

#### Header
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Antwort
{: #deleteresponse}

#### Status
{: #deletestatus}

```
204 No Content
```
{: screen}

## Benutzer mit der Befehlszeilenschnittstelle 'cf' verwalten
{: #usingadmincli}

Sie können Benutzer für Ihre {{site.data.keyword.Bluemix_notm}}-Umgebung über die Cloud Foundry-Befehlszeilenschnittstelle mit dem
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwalten. Sie können Benutzer beispielsweise aus einer LDAP-Registry
hinzufügen.

Vor dem Beginn müssen Sie die Befehlszeilenschnittstelle 'cf' installieren. Für das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
ist cf Version 6.11.2 oder höher erforderlich. [Cloud Foundry-Befehlszeilenschnittstelle herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet.

### {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in hinzufügen

Nach der Installation der Befehlszeilenschnittstelle 'cf' können Sie das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
hinzufügen.

**Hinweis:** Wenn Sie das {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in zuvor installiert haben, müssen Sie das Plug-in möglicherweise deinstallieren, das Repository löschen und anschließend das Plug-in erneut installieren, um die neuesten Aktualisierungen zu erhalten.

Führen Sie die folgenden Schritte aus, um das Repository hinzuzufügen und
das Plug-in zu installieren:

<ol>
<li>Führen Sie zum Hinzufügen des {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in-Repositorys den folgenden Befehl aus:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Die Unterdomäne der URL für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz.</dd>
</dl>
</li>
<li>Führen Sie zum Installieren des {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-ins den folgenden Befehl aus:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Führen Sie den folgenden Befehl aus,
um eine Liste der Befehle anzuzeigen:

`cf plugins`
{: codeblock}

Wenn Sie weitere Hilfe zu einem Befehl benötigen, verwenden Sie die Option `-help`.

Weitere Informationen zur Arbeit mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Admin](../cli/plugins/bluemix_admin/index.html).
