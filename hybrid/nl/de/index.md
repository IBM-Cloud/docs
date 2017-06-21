---


copyright:
  years: 2015, 2017
lastupdated: "2017-04-18"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}
{:pre: .pre}
{:table: .aria-labeledby="caption"}

# {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten
{: #mng}

Wenn Sie über Administratorzugriff für {{site.data.keyword.Bluemix}} Local oder {{site.data.keyword.Bluemix_notm}} Dedicated verfügen, können Sie über die Seite **Verwaltung** Ressourcen verwalten, die Kontingentnutzung überwachen, Benutzerberechtigungen verwalten, Upgradebenachrichtigungen planen, Sicherheitsberichte und Protokolle anzeigen und vieles mehr. Sie können Ihre Organisationen verwalten, indem Sie Bereiche erstellen und [Benutzerrollen und Berechtigungen festlegen](/docs/admin/index.html#oc_useradmin). Weitere Informationen finden Sie in [Organisationen verwalten](/docs/admin/orgs_spaces.html).
{:shortdesc}

{: #ld_table1}

| Verwaltungstask | Details |    
|----------------|---------|
|Systemnutzung überwachen | Klicken Sie auf **Verwaltung &gt; Nutzung**. Zeigen Sie Systeminformationen an, überwachen Sie die CPU-Nutzung und planen Sie die Nutzung, um die besten Entscheidungen für Ihr Unternehmen zu treffen. Siehe [Nutzungsinformationen anzeigen](/docs/admin/index.html#oc_resource).|
|Eigenen Katalog verwalten | Klicken Sie auf **Verwaltung &gt; Katalogverwaltung**, um die Services zu verwalten, die für Ihre Benutzer und Organisationen sichtbar sind. Siehe [Eigenen Katalog verwalten](/docs/admin/index.html#oc_catalog).|
|Organisationen verwalten | Klicken Sie auf **Verwaltung &gt; Organisationsadministration**, um Organisationen zu erstellen, Kontingente für Organisationen zu überwachen und rasch bedarfsorientierte Entscheidungen zu treffen. Siehe [Organisationen verwalten](/docs/admin/index.html#oc_organizations).|
|Bereiche erstellen und Benutzerrollen zuweisen | Klicken Sie auf **Konto** &gt; **Organisationen verwalten**, um in Ihren Organisationen Bereiche zu erstellen. Fügen Sie Benutzer hinzu und weisen Sie Benutzern Organisations- und Bereichsrollen zu. Siehe [Organisationen verwalten](/docs/admin/orgs_spaces.html). |
|Administratorberechtigungen verwalten | Klicken Sie auf **Verwaltung &gt; Benutzeradministration**, um Benutzer hinzuzufügen, Benutzer zu entfernen und Benutzerberechtigungen anzupassen. Siehe [Benutzer und Berechtigungen verwalten](/docs/admin/index.html#oc_useradmin). |
|Berichte und Protokolle prüfen | Klicken Sie auf **Verwaltung &gt; Berichte und Protokolle**, um Sicherheitsberichte und Prüfprotokolle für Ihre Instanz anzuzeigen. Siehe [Berichte anzeigen](/docs/admin/index.html#oc_report). |
|Systeminformationen anzeigen | Klicken Sie auf **Verwaltung &gt; Systeminformationen**, um Systeminformationen wie anstehende Wartungsaktualisierungen, Name und Version Ihrer Instanz, Region, API-URL, CLI-URL, LDAP-Konfigurationsdetails, Gruppen- und Benutzerzuordnungen, Statistiken und gemeinsam genutzte Domänen anzuzeigen. Siehe [Systeminformationen anzeigen](/docs/admin/index.html#oc_system). |
|Benachrichtigungen erweitern und Benachrichtigungsabonnements einrichten | Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* anstehend**. Sie können Web-Hooks zur Integration in einen Web-Service Ihrer Wahl verwenden, um ein Abonnement für Ereignisbenachrichtigungen für eine Aktualisierung oder einen Vorfall einzurichten. Siehe [Benachrichtigungen und Benachrichtigungsabonnements](/docs/admin/index.html#oc_eventsubscription). |
{: caption="Tabelle 1. Verwaltungstasks zur Verwaltung Ihrer Bluemix Local oder Dedicated-Instanz" caption-side="top"}

<!-- staging only for WoW start -->

**Tipp:** Das Infrastruktur-Dashboard in der {{site.data.keyword.Bluemix_notm}}-Konsole steht nur in verknüpften Konten in {{site.data.keyword.Bluemix_notm}} Public-Umgebungen zur Verfügung.


<!-- staging only for WoW end -->


## Benachrichtigungen und Benachrichtigungsabonnements
{: #oc_eventsubscription}

Sie können den Status Ihrer Umgebung jederzeit über die Seite 'Status' ermitteln. Vorfälle sowie geplante Wartungsaktualisierungsereignisse mit Unterbrechungen werden auf der Seite 'Status' gemeldet. {{site.data.keyword.Bluemix_notm}} sendet außerdem Benachrichtigungen in den Bereich 'Benachrichtigungen' auf der Seite 'Verwaltung' über Ereignisse wie geplante oder anstehende Wartungsaktualisierungen.

### Benachrichtigungen

Sie können Benachrichtigungen für Ihre lokale oder dedizierte Umgebung anzeigen, um den Status Ihrer Umgebung zu überwachen. Die folgende Tabelle enthält Informationen zu den verschiedenen Typen von Benachrichtigungen und zu den Positionen, an die die verschiedenen Benachrichtigungstypen gesendet werden.

{: #ld_table2}

| **Ereignistyp** | **Benachrichtigungsmethode** |       
|-----------------|-------------------|
| Wartungsaktualisierungen | Zum Anzeigen einer vollständigen Liste und des Verlaufs der anstehenden und abgeschlossenen Benachrichtigungen klicken Sie auf **Verwaltung &gt; Systeminformationen** &gt; *Anzahl* **Anstehend**. Sie werden auch über geplante Wartungsaktualisierungsereignisse mit Unterbrechungen auf der Seite 'Status' benachrichtigt. Klicken Sie auf **Support** &gt; **Status**. Sie können die Benachrichtigungsfunktion erweitern, indem Sie ein Abonnement einrichten, das eine E-Mail an die Empfänger Ihrer Wahl sendet. Sie können auch ein Abonnement einrichten, das die Benachrichtigungen auf der Seite 'Verwaltung' mithilfe von Web-Hooks in einen Web-Service Ihrer Wahl integriert.|
| Kritische Vorfälle | Sie werden über kritische Vorfälle auf der Seite 'Status' benachrichtigt. Klicken Sie auf **Support** &gt; **Status**. Sie können die Benachrichtigungsfunktion erweitern, indem Sie ein Benachrichtigungsabonnement einrichten, das eine E-Mail an einen Empfänger Ihrer Wahl sendet. Sie können auch ein Abonnement einrichten, das die Benachrichtigungen auf der Seite 'Verwaltung' mithilfe von Web-Hooks in einen Web-Service Ihrer Wahl integriert.  |  
| Schwellenwertereignisse | Sie können ein Benachrichtigungsabonnement einrichten, das eine E-Mail an einen Empfänger Ihrer Wahl sendet, wenn in Ihrer Umgebung Schwellenwerte für Organisationskontingent, physische Platte, physischen Speicher, reservierte Platte oder reservierten Speicher erreicht wurden. Alternativ können Sie ein Abonnement einrichten, das die Benachrichtigungen mithilfe von Web-Hooks in einen Web-Service Ihrer Wahl integriert.  |  
| {{site.data.keyword.Bluemix_notm}}-Status | Sie können den neuesten Status für die Plattform, die Services und Ihre {{site.data.keyword.Bluemix_notm}}-Instanz immer auf der Seite 'Status' anzeigen. Klicken Sie auf **Support** &gt; **Status**.  |
{: caption="Tabelle 2. Ereignistypen und Benachrichtigungsmethoden" caption-side="top"}

### Benachrichtigungsabonnements einrichten
{: #seteventsub}

Sie können die Funktionalität der Benachrichtigungen, die an die Seiten 'Verwaltung' und 'Status' gesendet werden, durch Benachrichtigungsabonnements erweitern. Verwenden Sie Benachrichtigungsabonnements, um eine benutzerdefinierte E-Mail zu erstellen oder die Benachrichtigungen mithilfe von Web-Hooks in ein Tool Ihrer Wahl zu integrieren.
 * Wenn Sie die E-Mail-Option auswählen, werden die Benachrichtigungen an die von Ihnen angegebene E-Mail-Adresse gesendet. Sie haben die Wahl zwischen Benachrichtigungen für Vorfälle, Wartungsaktualisierungen oder Schwellenwerte. Eine erste E-Mail-Benachrichtigung wird gesendet. Wenn dann am Ereignis eine Änderung vorgenommen wird, wird für jede Änderung jeweils eine weitere Benachrichtigung gesendet.  
 * Bei Auswahl von Web-Hooks werden Ihre Benachrichtigungen direkt an ein Ziel Ihrer Wahl weitergeleitet, wie zum Beispiel an eine Telefonnummer (durch eine SMS-Nachricht). Sie können den Typ der Benachrichtigung für Wartungsaktualisierungen, Alerts über kritische Vorfälle oder Schwellenwerte anpassen. Außerdem können Sie festlegen, ob neue Benachrichtigungen oder Benachrichtigungen zu Änderungen an Abonnements empfangen werden sollen, sowie die Art der Informationen, die in den Hauptteil der jeweiligen Benachrichtigung eingeschlossen werden.

**Hinweis:** Nur Benutzer mit Superuserberechtigung (`ops.admin`) können Benachrichtigungsabonnements einrichten.

Führen Sie folgende Schritte aus, um ein E-Mail- oder Web-Hook-Abonnement auf der Seite **Benachrichtigungsabonnements** zu erstellen:

1. Navigieren Sie zur Seite **Benachrichtigungsabonnements**.  Klicken Sie auf **Systeminformationen&gt; Umgebung&gt; Abonnements**.
2. Klicken Sie auf **Abonnement hinzufügen**.
3. Füllen Sie das Formular für das Benachrichtigungsabonnement aus.

  * Informationen zum Erstellen von Abonnements für E-Mail-Benachrichtigungen über Wartungsaktualisierungen oder Vorfälle finden Sie in [Tabelle 3](index.html#emailnotmaintinc).
  * Informationen zum Erstellen von Abonnements für E-Mail-Benachrichtigungen über Schwellenwerte finden Sie in [Tabelle 4](index.html#emailnottrhesh).
  * Informationen zum Erstellen von Abonnements für Web-Hook-Benachrichtigungen über Wartungsaktualisierungen oder Vorfälle finden Sie in [Tabelle 5](index.html#webhooknotsub).
  * Informationen zum Erstellen von Abonnements für Web-Hook-Benachrichtigungen über Schwellenwerte finden Sie in [Tabelle 6](index.html#webhooknotthresh).

4. Nachdem Sie das Formular ausgefüllt haben, können Sie eine der folgenden Optionen auswählen:

  * Klicken Sie auf **Speichern**, um das Abonnement in Ihrer Benachrichtigungs-Abonnementliste zu speichern.
  * Klicken Sie auf **Speichern und testen**, um die Benachrichtigung zu speichern und zu testen.
  * Klicken Sie auf **Speichern und schließen**, um das Abonnement in Ihrer Benachrichtigungs-Abonnementliste zu speichern, und kehren Sie zur vorherigen Seite zurück.

{: #emailnotmaintinc}

| **Feld** | **Beschreibung** |
|-----------------|-------------------|
| Aktiviert | Wählen Sie diese Option aus, um E-Mail-Benachrichtigungen zu aktivieren. Nehmen Sie die Auswahl zurück, um E-Mail-Benachrichtigungen zu inaktivieren. Abonnements sind standardmäßig aktiviert. |
| Typ | Wählen Sie **E-Mail** aus. |
| Ereignis | Wählen Sie aus, ob Benachrichtigungen für ein **Wartungs-** oder **Vorfalls**ereignis abonniert werden sollen. |
| Benachrichtigungen kombinieren | Wählen Sie diese Option aus, um die Benachrichtigungen zu Vorfällen für alle Regionen in einer einzigen Benachrichtigung zu kombinieren. Diese Option ist nur für Vorfälle verfügbar. |
| Betreff | Geben Sie die Betreffzeile für die E-Mail ein. Dies ist ein erforderliches Feld.  |
| Hauptteil | Geben Sie den Nachrichtentext für die E-Mail ein. Sie können die IBM Nutzdaten verwenden, um relevante Informationen in die E-Mail-Benachrichtigung einzugeben. In der Tabelle [Werte für den Abschnitt 'Nutzdaten zu Wartungen und Vorfällen'](index.html#payload) finden Sie die Werte, die Sie verwenden können. Verwenden Sie zum Strukturieren der E-Mail HTML-Basistags. Dies ist ein erforderliches Feld. |
| An | Geben Sie die E-Mail-Adresse(n) der Empfänger der E-Mail-Benachrichtigung in Form einer durch Kommas getrennte Liste ein. Erweitern Sie die Optionen "cc" bzw. "bcc", um andere Benutzer auf Kopie zu setzen. Dies ist ein erforderliches Feld. |
| Beschreibung | Fügen Sie eine eindeutige Beschreibung für das Abonnement hinzu, das Sie erstellen. |
{: caption="Tabelle 3. Felder für E-Mail-Benachrichtigungs-Abonnements für Schwellenwerte" caption-side="top"}


{: #emailnottrhesh}

| **Feld** | **Beschreibung** |
|-----------------|-------------------|
| Aktiviert | Wählen Sie diese Option aus, um E-Mail-Benachrichtigungen zu aktivieren. Nehmen Sie die Auswahl zurück, um E-Mail-Benachrichtigungen zu inaktivieren. Abonnements sind standardmäßig aktiviert. |
| Typ | Wählen Sie **E-Mail** aus. |
| Ereignis | Wählen Sie **Schwellenwert** aus. |
| Schwellenwert | Wählen Sie die Art der Schwellenwerte aus, über die Sie benachrichtigt werden wollen: Organisationskontingent, physische Platte, physischer Speicher, reservierte Platte oder reservierter Speicher. |
| Schwellenwertrichtung | Wählen Sie die Richtung aus, in der die Daten verschoben werden sollen (aufsteigend oder absteigend), wenn sie den von Ihnen festgelegten Wert für 'Benachrichtigung bei Überschreitung' überschreiten. Wenn der Wert für 'Benachrichtigung bei Überschreitung' beispielsweise bei 50% liegt und die Richtung 'absteigend' ist, werden Sie nur dann benachrichtigt, wenn der Nutzungs-Prozentsatz von mindestens 50% auf unter 50% fällt. Wenn die Richtung auf 'aufsteigend' festgelegt ist, werden Sie benachrichtigt, sobald der Nutzungs-Prozentsatz von unter 50 % auf über 50 % steigt.
| Benachrichtigung bei Überschreitung (%) | Geben Sie den Schwellenwert-Prozentsatz ein, bei dem Sie benachrichtigt werden möchten. Wenn Sie im Feld 'Schwellenwertrichtung' die Eigenschaft 'aufsteigend' angegeben haben, werden die E-Mail-Benachrichtigungen gesendet, sobald der Schwellenwert diesen Prozentsatz übersteigt. |
| Benachrichtigung bei Unterschreitung (%) | Geben Sie den Schwellenwert-Prozentsatz ein, bei dem Sie benachrichtigt werden möchten. Wenn Sie im Feld 'Schwellenwertrichtung' die Eigenschaft 'absteigend' angegeben haben, werden die E-Mail-Benachrichtigungen gesendet, sobald der Schwellenwert diesen Prozentsatz unterschreitet. |
| Beschreibung | Fügen Sie eine eindeutige Beschreibung für das Abonnement hinzu, das Sie erstellen. |
| Betreff | Geben Sie die Betreffzeile für die E-Mail ein. Dies ist ein erforderliches Feld.  |
| Nachrichtentext | Geben Sie den Nachrichtentext für die E-Mail ein. Sie können die IBM Nutzdaten verwenden, um relevante Informationen in die E-Mail-Benachrichtigung einzugeben. In der Tabelle [Werte für den Abschnitt 'Nutzdaten zu Schwellenwerten'](index.html#threshpayload) finden Sie die Werte, die Sie verwenden können. Verwenden Sie zum Strukturieren der E-Mail HTML-Basistags. Dies ist ein erforderliches Feld. |
| An | Geben Sie die E-Mail-Adresse(n) der Empfänger der E-Mail-Benachrichtigung in Form einer durch Kommas getrennte Liste ein. Erweitern Sie die Optionen "cc" bzw. "bcc", um andere Benutzer auf Kopie zu setzen. Dies ist ein erforderliches Feld. |
{: caption="Tabelle 4. Felder für E-Mail-Benachrichtigungs-Abonnements für Wartungsaktualisierungen oder Vorfälle" caption-side="top"}

Schwellenwertdaten werden alle 6 Stunden erfasst. Eine Benachrichtigung wird nur einmal gesendet, wenn der Wert den von Ihnen festgelegten Schwellenwert über- oder unterschreitet. Wenn Sie 'aufsteigend' gewählt haben, wird nur dann eine neue Benachrichtigung gesendet, wenn der Wert den Schwellenwert unterschreitet und dann wieder überschreitet. Wenn Sie 'absteigend' gewählt haben, werden Sie entsprechend nur dann benachrichtigt, wenn der Wert den von Ihnen festgelegten Schwellenwert überschreitet und dann wieder unterschreitet. 

Wenn Sie nicht 6 Stunden warten möchten, bis die Benachrichtigung über das Erreichen des Schwellenwerts gesendet wird, können Sie nach dem Ausfüllen der Felder im Formular auf **Speichern und testen** klicken, um eine Testbenachrichtigung mit Beispieldaten zu empfangen.  

Eine Benachrichtigung über einen Organisationskontingentschwellenwert enthält nur die Organisationen, die den angegebenen Schwellenprozentwert in dem 6-Stunden-Zeitraum, der dieser Benachrichtigung entspricht, über- oder unterschritten haben. Organisationen, die einen Schwellenwert während vorheriger 6-Stunden-Zeiträume über- oder unterschritten haben, werden nicht eingeschlossen, auch wenn sie über bzw. unter dem Schwellenwert verbleiben.  Die drei Ressourcen, die ein Kontingent der Organisation bilden (reservierter Speicher, Services und Routen) werden bei der Ermittlung, ob eine Benachrichtigung über ein Organisationskontingent gesendet werden soll, unabhängig bewertet. Wenn zum Beispiel die Menge an reserviertem Speicher, die von einer Organisation genutzt wird, den Wert von 50 % des Kontingents der Organisation über- oder unterschreitet, hat ein Schwellenwert für das Organisationskontingent, der mit 50 % konfiguriert ist, zur Folge, dass eine Benachrichtigung gesendet wird.  Wenn die Anzahl der Services, die von derselben Organisation genutzt werden, den Wert von 50 % des Kontingents der Organisation zu einem späteren Zeitpunkt überschreitet, führt dies ebenfalls dazu, dass eine Benachrichtigung gesendet wird, selbst wenn die Menge an genutztem Speicher unverändert bleibt.

{: #webhooknotsub}

| **Feld** | **Beschreibung** |
|-----------------|-------------------|
| Aktiviert | Wählen Sie diese Option aus, um die Benachrichtigung zu aktivieren. Nehmen Sie die Auswahl zurück, um die Benachrichtigung zu inaktivieren. Abonnements sind standardmäßig aktiviert. |
| Typ | Wählen Sie **Web-Hook** aus. |
| Ereignis | Wählen Sie aus, ob Benachrichtigungen für ein **Wartungs-** oder **Vorfalls**ereignis abonniert werden sollen. |
| Autorisierung | Wählen Sie aus, ob die Autorisierung aktiviert werden soll.  Es gibt folgende Optionen: **Basis** oder **Ohne**. |
| Benutzername | Wenn Sie die **Basis**-Autorisierung ausgewählt haben, geben Sie den Benutzernamen für Ihren Web-Service ein. Wenn Sie nicht Ihre persönlichen Berechtigungsnachweise verwenden möchten, können Sie eine Funktions-ID speziell zur Verwendung mit {{site.data.keyword.Bluemix_notm}} einrichten. |
| Kennwort | Wenn Sie die **Basis**-Autorisierung ausgewählt haben, geben Sie das Kennwort für Ihren Web-Service ein. |
| Beschreibung | Fügen Sie eine eindeutige Beschreibung für das Abonnement hinzu, das Sie erstellen. |
| Neues Ereignis | Wählen Sie diese Option aus, um Benachrichtigungen zu neuen Wartungs- oder Vorfallereignissen zu aktivieren. Nehmen Sie die Auswahl zurück, um die Benachrichtigung zu inaktivieren. |
| Methode | Wählen Sie **GET**, **POST** oder **PUT** aus. |
| URL | Geben Sie die URL für die Verbindung mit dem Web-Service ein. |
| Antworteigenschaft | Dieses optionale Feld enthält den Eigenschaftsnamen, der die Ressource angibt, die von Ihrem Web-Service beim Senden einer POST- oder PUT-Anforderung erstellt wird. Wenn Sie eine Antworteigenschaft für ein neues Ereignis bereitstellen und dann ein Abonnement für Änderungen an einem Ereignis erstellen wollen, müssen Sie die Antworteigenschaft auch für das Abonnement 'Änderung an Ereignis' angeben. Je nachdem, welchen Web-Service Sie verwenden, könnten Sie sie als Teil der URL oder als Nutzlastwert angeben.  |
| Nutzdaten | Wenn Sie die Methode POST oder PUT ausgewählt haben, geben Sie die Eigenschaften ein, die für den von Ihnen verwendeten Web-Service gelten, gepaart mit den Nutzdatenwerten, die für die IBM Benachrichtigung verwendet werden. In der Tabelle [Werte für den Abschnitt 'Nutzdaten zu Wartungen und Vorfällen'](index.html#payload) finden Sie die Werte, die Sie verwenden können. Wenn Sie in diesem Abschnitt keine Informationen eingeben, empfangen Sie die Benachrichtigung ganz ohne zusätzliche Informationen. |
| Änderung an Ereignis | Wählen Sie diese Option aus, um Abonnements für Benachrichtigungen über Änderungen an Wartungs- oder Vorfallereignissen zu erstellen, für die Sie Abonnements erstellt haben. Nehmen Sie die Auswahl zurück, um die Benachrichtigung zu inaktivieren. |
| Werte und Nutzdaten aus 'Neues Ereignis' verwenden | Verwendet den Inhalt der Felder für Methode, URL und Nutzdaten aus dem Abschnitt 'Neues Ereignis'. Beachten Sie, dass bei Aktivieren dieser Option diese Felder nicht für die weitere Bearbeitung im Abschnitt 'Änderung an Ereignis' zur Verfügung stehen. |
| Methode | Wählen Sie **GET**, **POST** oder **PUT** aus. |
| URL | Geben Sie die URL für die Verbindung mit dem Web-Service ein. |
| Nutzdaten | Wenn Sie die Methode POST oder PUT ausgewählt haben, geben Sie die Eigenschaften ein, die für den von Ihnen verwendeten Web-Service gelten, gepaart mit den Nutzdatenwerten, die für die IBM Benachrichtigung verwendet werden. In der Tabelle [Werte für den Abschnitt 'Nutzdaten zu Wartungen und Vorfällen'](index.html#payload) finden Sie die Werte, die Sie verwenden können. Wenn Sie in diesem Abschnitt keine Informationen eingeben, empfangen Sie die Benachrichtigung ganz ohne zusätzliche Informationen. |
| Benachrichtigungen kombinieren | Wählen Sie diese Option aus, um die Benachrichtigungen zu Vorfällen für alle Regionen in einer einzigen Benachrichtigung zu kombinieren. Diese Option ist nur für Vorfälle verfügbar. |
{: caption="Tabelle 5. Formularfelder für ein Abonnement für Web-Hook-Benachrichtigungen über Wartung oder Vorfälle" caption-side="top"}


{: #webhooknotthresh}

| **Feld** | **Beschreibung** |
|-----------------|-------------------|
| Aktiviert | Wählen Sie diese Option aus, um die Benachrichtigung zu aktivieren. Nehmen Sie die Auswahl zurück, um die Benachrichtigung zu inaktivieren. Abonnements sind standardmäßig aktiviert. |
| Typ | Wählen Sie **Web-Hook** aus. |
| Ereignis | Wählen Sie **Schwellenwert** aus. |
| Schwellenwert | Wählen Sie die Art der Schwellenwerte aus, über die Sie benachrichtigt werden wollen: Organisationskontingent, physische Platte, physischer Speicher, reservierte Platte oder reservierter Speicher.|
| Schwellenwertrichtung | Wählen Sie aus, ob die Schwellenwertdaten in aufsteigender oder in absteigender Reihenfolge angezeigt werden sollen.  |
| Benachrichtigung bei Unterschreitung (%) | Wenn Sie **Schwellenwertrichtung** mit **Absteigend** angegeben haben, geben Sie den Schwellenwert-Prozentsatz ein, bei dem Sie benachrichtigt werden wollen. Fällt der Schwellenwert unterhalb dieses Prozentsatzes, wird die Web-Hook-Benachrichtigung gesendet. |
| Benachrichtigung bei Überschreitung (%) | Wenn Sie **Schwellenwertrichtung** mit **Aufsteigend** angegeben haben, geben Sie den Schwellenwert-Prozentsatz ein, bei dem Sie benachrichtigt werden wollen. Überschreitet der Schwellenwert diesen Prozentsatz, wird die Web-Hook-Benachrichtigung gesendet. |
| Beschreibung | Fügen Sie eine eindeutige Beschreibung für das Abonnement hinzu, das Sie erstellen. |
| Autorisierung | Wählen Sie aus, ob die Autorisierung aktiviert werden soll.  Es gibt folgende Optionen: **Basis** oder **Ohne**. |
| Benutzername | Wenn Sie die Basisautorisierung gewählt haben, geben Sie den Benutzernamen für Ihren Web-Service ein. Wenn Sie nicht Ihre persönlichen Berechtigungsnachweise verwenden möchten, können Sie eine Funktions-ID speziell zur Verwendung mit {{site.data.keyword.Bluemix_notm}} einrichten. |
| Kennwort | Wenn Sie die Basisautorisierung ausgewählt haben, geben Sie das Kennwort für Ihren Web-Service ein. |
| Methode | Wählen Sie **GET**, **POST** oder **PUT** aus. |
| URL | Geben Sie die URL für die Verbindung mit dem Web-Service ein. |
{: caption="Tabelle 6. Formularfelder für ein Abonnement für Web-Hook-Benachrichtigungen über Schwellenwerte" caption-side="top"}

Schwellenwertdaten werden alle 6 Stunden erfasst. Eine Benachrichtigung wird nur einmal gesendet, wenn der Wert den von Ihnen festgelegten Schwellenwert über- oder unterschreitet. Eine neue Benachrichtigung wird nur dann gesendet, wenn Sie 'absteigend' gewählt haben, der Wert den Schwellenwert unterschreitet und dann wieder überschreitet. Wenn Sie 'absteigend' gewählt haben, werden Sie entsprechend nur dann benachrichtigt, wenn der Wert den von Ihnen festgelegten Schwellenwert überschreitet und dann wieder unterschreitet. 

Wenn Sie nicht 6 Stunden warten möchten, bis die Benachrichtigung über das Erreichen des Schwellenwerts gesendet wird, können Sie nach dem Ausfüllen der Felder im Formular auf **Speichern und testen** klicken, um die Benachrichtigung mit Beispieldaten zu speichern und zu testen.

Eine Benachrichtigung über einen Organisationskontingentschwellenwert enthält nur die Organisationen, die den angegebenen Schwellenprozentwert in dem 6-Stunden-Zeitraum, der dieser Benachrichtigung entspricht, über- oder unterschritten haben. Organisationen, die einen Schwellenwert während vorheriger 6-Stunden-Zeiträume über- oder unterschritten haben, werden nicht eingeschlossen, auch wenn sie über bzw. unter dem Schwellenwert verbleiben.  Die drei Ressourcen, die ein Kontingent der Organisation bilden, nämlich reservierter Speicher, Services und Routen, werden bei der Ermittlung, ob eine Benachrichtigung über ein Organisationskontingent gesendet werden soll, unabhängig bewertet. Wenn zum Beispiel die Menge an reserviertem Speicher, die von einer Organisation genutzt wird, den Wert von 50 % des Kontingents der Organisation über- oder unterschreitet, hat ein Schwellenwert für das Organisationskontingent, der mit 50 % konfiguriert ist, zur Folge, dass eine Benachrichtigung gesendet wird.  Wenn die Anzahl der Services, die von derselben Organisation genutzt werden, den Wert von 50 % des Kontingents der Organisation zu einem späteren Zeitpunkt überschreitet, führt dies ebenfalls dazu, dass eine Benachrichtigung gesendet wird, selbst wenn die Menge an genutztem Speicher unverändert bleibt.

{: #payload}

| **IBM Wert** | **Beschreibung** | **Ereignistyp** |
|----------------|----------------|------------------------|
| {{content.category}} | Betroffene Services | Vorfall |
| {{content.disruption}} | Betroffene Komponenten | Wartungsaktualisierung |
| {{content.message}} | Nachrichtenbeschreibung |   Wartungsaktualisierung und Vorfall |
| {{content.scheduleWindow.start}} | Geplantes Startdatum für die Aktualisierung | Wartungsaktualisierung |
| {{content.scheduleWindow.end}} | Geplante Endzeit für die Aktualisierung | Wartungsaktualisierung |
| {{content.severity}} | Sicherheitseinstufung | Vorfall |
| {{content.subCategoryName}} | Betroffene Komponenten | Vorfall |
| {{content.title}} | Nachrichtentitel | Wartungsaktualisierung und Vorfall |
| {{region}} | Betroffene Region | Wartungsaktualisierung und Vorfall |
| {{status}} | Status der Aktualisierung | Wartungsaktualisierung |
| {{type}} | Aktualisierung und Vorfall | Wartungsaktualisierung und Vorfall |
{: caption="Tabelle 7. Werte im Abschnitt 'payload' für Wartung und Vorfälle" caption-side="top"}


{: #threshpayload}

| **IBM Wert** | **Beschreibung** | **Ereignistyp** |
|----------------|----------------|------------------------|
| {{content.org_quota}} | Schwellenwert für Organisationskontingent | Schwellenwert |
| {{content.physical_disk}} | Schwellenwert für physische Platte | Schwellenwert |
| {{content.physical_memory}} | Schwellenwert für physischen Speicher | Schwellenwert |  
| {{content.reserved_disk}} | Schwellenwert für reservierte Platte | Schwellenwert |
| {{content.reserved_memory}} | Schwellenwert für reservierten Speicher | Schwellenwert |
{: caption="Tabelle 8. Werte im Abschnitt 'payload' für Schwellenwerte" caption-side="top"}

Nach dem Speichern des Benachrichtigungsabonnements empfangen Sie Benachrichtigungen über die Methode, die Sie eingerichtet haben. Benachrichtigungen werden weiterhin an die folgenden Positionen gesendet:  
 * Für Vorfälle auf der Seite 'Status'
 * Für geplante Wartungsaktualisierungsereignisse mit Unterbrechungen auf der Seite 'Status'
 * Für Wartungsaktualisierungen im Bereich 'Benachrichtigungen' der Seite 'Verwaltung'

Sie können ein beliebiges gespeichertes Benachrichtigungsabonnement auswählen, die letzte Aktivität anzeigen oder bei Bedarf Änderungen vornehmen. Sie können auf einen Eintrag für eine kürzliche Aktivität klicken, um die zugehörigen Verlaufsdetails anzuzeigen.

## Wartungsaktualisierungen
{: #oc_schedulemaintenance}

Wenn Sie die Superuserberechtigung (`ops.admin`) besitzen, können Sie geplante und ausstehende Wartungsaktualisierungen anzeigen, indem Sie über **VERWALTUNG &gt; SYSTEMINFORMATIONEN &gt; *Anzahl* anstehend** auf die Seite **Systemaktualisierungen** zugreifen.  Alle Benutzer Ihrer Umgebung können die geplanten Wartungsaktualisierungsereignisse mit Unterbrechungen anzeigen, indem sie auf **Support** &gt; **Status** klicken.

**Hinweis:** Lesen Sie als Einführung den Abschnitt [Vorab genehmigte Wartungszeiten einstellen](index.html#preapprovedmaintenance). Diese Fenster müssen definiert sein, damit IBM die Wartungszeiten für Ihre Umgebung planen kann.

<dl>
<dt>Unterbrechungsfreie Aktualisierungen</dt>
<dd>Eine unterbrechungsfreie Aktualisierung hat keine Auswirkungen auf Ihre Umgebung, Ihre aktiven Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen. Dieser Aktualisierungstyp erfordert keine fallspezifische Genehmigung und wird während der vorab genehmigten, verfügbaren Wartungszeiten angewendet, die Sie auf der Seite 'Systemaktualisierungen' festgelegt haben.</dd>
<dt>Aktualisierung mit Unterbrechungen</dt>
<dd>Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie müssen jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen. Sie können den vorgeschlagenen Bereitstellungszeitpunkt (Datum und Uhrzeit) oder die Option für ein zuvor genehmigtes Fenster auswählen. Alternativ können Sie auch den Kalender öffnen, um drei bestimmte Daten und Uhrzeiten auszuwählen, aus denen IBM dann bei der Planung der Aktualisierung auswählt.</dd>
</dl>


### Vorab genehmigte Wartungszeiten einstellen
{: #preapprovedmaintenance}

Die Ausführung unterbrechungsfreier Wartungsaktualisierungen wird für zuvor genehmigte Zeitfenster geplant. Standardmäßig werden für Ihr System zwei wöchentlich verfügbare Aktualisierungs-Zeitfenster erstellt. Diese Zeitfenster sind normalerweise auf samstags abends und sonntags abends festgelegt. Zum Ändern der Standardeinstellungen stehen Ihnen folgende Möglichkeiten zur Verfügung:
 * Bearbeiten Sie die Standard-Aktualisierungszeitfenster, indem Sie einen anderen Wochentag oder eine andere Startzeit oder beides auswählen.
 * Erstellen Sie ein Aktualisierungszeitfenster und löschen Sie dann das Standard-Aktualisierungszeitfenster.

Um Ihre Änderungen speichern zu können, müssen Sie immer noch für jede Woche die mindestens erforderliche Zeit festlegen.

Sie müssen mindestens 12 verfügbare Stunden pro Woche an mindestens zwei Tagen der Woche festlegen. Sie können zum Beispiel 6-Stunden-Zeitfenster an zwei verschiedenen Tagen oder an drei Tagen 4-Stunden-Zeitfenster festlegen. Um sicherzustellen, dass die Zeiträume ausreichend Zeit für das Anwenden einer Aktualisierung bieten, muss jeder Zeitraum mindestens vier Stunden andauern.  

**Hinweis:** Nur Benutzer mit der Superuserberechtigung (`ops.admin`) können Wartungsaktualisierungen planen und genehmigen.

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* anstehend &gt; Verfügbarkeit verwalten**.
2. Erweitern Sie den Abschnitt zum Thema **Verfügbare Aktualisierungszeiten verwalten**.
3. Klicken Sie auf **Neues hinzufügen** ![Neues hinzufügen](images/add-new.png).
4. Legen Sie das erste verfügbare Zeitfenster fest, indem Sie die Häufigkeit, die Dauer und die Anfangszeit für das Fenster auswählen.
5. Optional: Wählen Sie **Als bevorzugt markieren** aus, um das wiederkehrende Zeitfenster als bevorzugtes Zeitfenster für geplante Bereitstellungen festzulegen. Bevorzugte Zeitfenster haben Priorität, sofern dies möglich ist.
6. Klicken Sie auf **Abschicken**.
7. Wiederholen Sie diesen Vorgang, bis Sie die Mindestanforderungen für die wöchentlichen Zeitfenster erfüllt haben.

### Nicht verfügbare Wartungszeiten festlegen
{: #blockpreapprovedmaintenance}

Sie können bestimmte nicht verfügbare Aktualisierungsfenster festlegen, in der Ihre Umgebung nicht für unterbrechungsfreie Wartungsaktualisierungen zur Verfügung steht. So können Sie zum Beispiel ein Wochenende oder einen Feiertag mit hohem Datenverkehr auswählen, an denen Sie keine Wartung wünschen, um sicherzugehen, dass Ihre Anwendungen für Ihre Benutzer zur Verfügung stehen.

Sie müssen mindestens 12 verfügbare Stunden pro Woche an mindestens zwei Tagen der Woche festlegen. Wenn Sie versuchen, ein nicht verfügbares Aktualisierungsfenster zu erstellen, können Sie Ihre Änderungen möglicherweise nicht speichern, wenn dieses neue Fenster dazu führen würde, dass Ihr System das wöchentlich mindestens erforderliche Zeitfenster nicht einhält. In diesem Fall müssen Sie zunächst entweder einige der vorhandenen nicht verfügbaren Aktualisierungsfenster entfernen oder weitere verfügbare Aktualisierungsfenster hinzufügen, bevor Sie das neue nicht verfügbare Aktualisierungsfenster speichern können. Weitere Informationen hierzu finden Sie unter [Vorab genehmigte Wartungszeiten einstellen](index.html#preapprovedmaintenance).

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* anstehend &gt; Verfügbarkeit verwalten**.
2. Erweitern Sie den Abschnitt zum Thema **Nicht verfügbare Aktualisierungszeiten verwalten**.
3. Klicken Sie auf **Neues hinzufügen** ![Neues hinzufügen](images/add-new.png).
4. Legen Sie das erste nicht verfügbare Zeitfenster fest, indem Sie die Häufigkeit, die Dauer und die Anfangszeit für das Fenster auswählen.
5. Klicken Sie auf **Abschicken**.

### Aktualisierungen planen und genehmigen
{: #scheduleandapprove}

Nachdem Sie Ihre vorab genehmigten Wartungszeiten festgelegt haben, werden unterbrechungsfreie Aktualisierungen automatisch während dieser Zeiten geplant. Ihre explizite Genehmigung für diese Aktualisierungstypen ist nicht erforderlich. Sie können jedoch die Details für jede Wartungsaktualisierung einschließlich der aktualisierten Komponenten, der Dauer der Aktualisierung und des geplanten Aktualisierungstermins anzeigen.

Um die Details für eine unterbrechungsfreie Aktualisierung anzuzeigen, führen Sie die folgenden Schritte aus:

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* anstehend**.
2. Suchen Sie Zeilen, bei denen für **Angepasste Terminplanung erforderlich** die Einstellung **Nein** festgelegt ist.
3. Wählen Sie die Zeile für die Aktualisierung aus, um die Details anzuzeigen.

Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie müssen jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen. Sie können den vorgeschlagenen Bereitstellungszeitpunkt (Datum und Uhrzeit) oder die Option für ein zuvor genehmigtes Fenster auswählen. Alternativ können Sie auch den Kalender öffnen, um drei bestimmte Daten und Uhrzeiten auszuwählen, aus denen IBM dann bei der Planung der Aktualisierung auswählt.

Führen Sie für Aktualisierungen mit Unterbrechung, die Ihre Genehmigung erfordern, folgende Schritte durch:

1. Klicken Sie auf **Verwaltung &gt; Systeminformationen &gt; *Anzahl* anstehend**.
2. Suchen Sie Zeilen, bei denen für **Angepasste Terminplanung erforderlich** die Einstellung **Ja** festgelegt ist.
3. Wählen Sie die Zeile für die Aktualisierung aus, um die Details für die Aktualisierung einschließlich der Aktualisierungsbeschreibung, des vorgeschlagenen Datums und der vorgeschlagenen Uhrzeit für die Aktualisierung, die betroffenen Komponenten sowie die Dauer der Aktualisierung zu überprüfen.
4. Wählen Sie **Planen und Genehmigen** aus.
5. Wählen Sie aus den folgenden Optionen aus: **Datumsvorschlag**, **Alternative Datumsangaben** oder **Alle zuvor genehmigten Fenster**. Bei Auswahl von **Alternative Datumsangaben** können Sie den Kalender öffnen, um drei Optionen zu bestimmen, aus denen IBM auswählen kann.
6. Optional: Wählen Sie in der Liste der ausgewählten alternativen Datumsangaben im Kalender die Angaben aus, die Sie als bevorzugte Datumsangaben für die Bereitstellung festlegen möchten. Jedes ausgewählte Datum wird für den Bereitsteller, der die Bereitstellung plant, als bevorzugt markiert. IBM versucht, Wartungen innerhalb der bevorzugten Aktualisierungsfenster zu planen.
7. Wenn der Vorgang abgeschlossen ist, wählen Sie **Abschicken** aus.

Das Bereitstellen der Aktualisierung wird auf Grundlage Ihrer Auswahl an dem vorgeschlagenen Datum, das Sie genehmigt haben, in einem vorab genehmigten Zeitfenster oder an einem von Ihnen ausgewählten Datum zur ausgewählten Uhrzeit geplant. Wenn das Bereitstellen der Aktualisierung von IBM geplant wird, sehen Sie das geplante Datum in den Details zur Aktualisierung auf der Seite **Systemaktualisierungen**. Die erneute Planung einer bereits geplanten Bereitstellung ist nur dann möglich, wenn zwischen dem geplanten Startzeitpunkt ein Tag (24 Stunden) liegt. Nach der erneuten Planung einer Bereitstellung kann diese nicht mehr neu geplant werden.


## Systeminformationen anzeigen
{: #oc_system}

Klicken Sie zum Anzeigen von Systeminformationen auf **Verwaltung &gt; Systeminformationen**.

Sie können verschiedene Abschnitte anzeigen, darunter anstehende Systemaktualisierungen, allgemeine Systeminformationen, API- und CLI-Informationen sowie LDAP-Konfigurationsdetails.

### Anstehende Systemaktualisierungen

Im Bereich für die Aktualisierungen wird die Anzahl der Benachrichtigungen über anstehende Aktualisierungen angezeigt,
für die eine Aktion Ihrerseits erforderlich ist. Es gibt zwei Typen, die Ihnen möglicherweise angezeigt werden:

<dl>
<dt>Unterbrechungsfreie Aktualisierungen</dt>
<dd>Eine unterbrechungsfreie Aktualisierung hat keine Auswirkungen auf Ihre Umgebung, Ihre aktiven Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen. Dieser Aktualisierungstyp erfordert keine fallspezifische Genehmigung. Diese Aktualisierungen werden in den vorab genehmigten, verfügbaren Wartungszeiten, die Sie auf der Seite 'Systemaktualisierungen' festgelegt haben, angewendet.</dd>
<dt>Aktualisierung mit Unterbrechungen</dt>
<dd>Eine Aktualisierung mit Unterbrechungen kann sich auf Ihre Umgebung, die Ausführung von Anwendungen oder den Zugriff der Benutzer auf Ihre Anwendungen auswirken. Sie können jede dieser Wartungsaktualisierungen innerhalb des zugeteilten Wartungszeitraums von 21 Tagen terminieren und genehmigen, um sicherzustellen, dass die Aktualisierung nicht während kritischer Geschäftszeiten angewendet wird. Sie können das vorgeschlagene Implementierungsdatum und die vorgeschlagene Uhrzeit auswählen, die auf Ihren vorab genehmigten Aktualisierungsfenstern basieren, oder Sie können zwei weitere Uhrzeiten und Daten auswählen, aus denen IBM dann bei der Anwendung der Aktualisierung auswählen kann.</dd>
</dl>

Weitere Informationen zum Festlegen vorab genehmigter Wartungszeiten und zum Festlegen bestimmter Zeiten, die für die Wartung nicht verfügbar sind, finden Sie im Abschnitt zu [Wartungsaktualisierungen](index.html#oc_schedulemaintenance).

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
- Speicherkontingentnutzung für Organisationen, zugeordneter App-Speicher auf Basis des verwendeten Gesamtspeicherkontingents und Anzeige der GB-Stundennutzung pro App für eine bestimmte Organisation. Sie können außerdem die Kontingentnutzung für alle Organisationen auf der Seite 'Organisationsadministration' im Abschnitt **Kontingentüberwachung** anzeigen. Siehe [Organisationsadministration](../admin/index.html#orgusage).


### Ressourcennutzung
{: #resourceusage}

Klicken Sie zum Anzeigen von Informationen zur Ressourcennutzung auf **VERWALTUNG &gt; Ressourcennutzung**.

Im Abschnitt **Ressourcennutzung** können Sie die folgenden Informationen anzeigen:

- Informationen zur Ressourcennutzung, beispielsweise wie viel Speicher und Plattenspeicher reserviert und physisch zur Verfügung gestellt werden kann, wie viel Speicher und Plattenspeicher tatsächlich reserviert und physisch verfügbar ist.  Sie können auch Informationen zur durchschnittlichen CPU-Auslastung für alle DEAs (Droplet Execution Agent) anzeigen. Ausführliche Informationen zur Nutzung von Speicher, Platte und CPU finden Sie im Abschnitt [Details zu Speicher, Platte und CPU](index.html#resourceusagedetails).
- Informationen zur Netzauslastung für die Bandbreite bei Ein- und Ausgang über die letzten 6 Stunden oder einen vergangenen Tag. Die angezeigten Daten basieren auf dem Gesamtwert zum ankommenden und abgehenden Datenverkehr für öffentliche und private Netze.
- Durchschnittliche Antwortzeit für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.
- Durchschnittliche Transaktionen pro Sekunde für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.


#### Details zu Systemspeicher, Platte und CPU
{: #resourceusagedetails}

Im Abschnitt **Ressourcennutzung** können Sie eine Zusammenfassung für Speicher- und Plattennutzung, unterteilt in **Reserviert** und **Physisch**, anzeigen.    
	<dl>
	<dt><strong>Physisch</strong></dt>
	<dd>Die Speicher- oder Plattenkapazität, die für Ihre Umgebung gekauft wurde.</dd>
	<dt><strong>Reserviert</strong></dt>
	<dd>Die gesamte Speicher- oder Plattenkapazität, die verfügbar ist und von allen bereitgestellten und aktiven Anwendungen in Ihrer Umgebung reserviert werden kann. Da Anwendungen selten den gesamten Speicher nutzen, der für sie reserviert wurde, ist der Wert für den physischen Speicher in der Regel kleiner als der Wert für den reservierten Speicher.</dd>
	</dl>

Neben der grafischen Darstellung wird der Prozentsatz der Speicher- und Plattenkapazität angezeigt, die Ihre Umgebung verwendet. Sowohl die reservierte als auch die physische Kapazität wird in Gigabyte im Vergleich zur verfügbaren Kapazität angezeigt.

Um die Nutzung Ihres Speichers, Ihrer Platte, Ihrer CPU oder Ihres DEA anzuzeigen, klicken Sie auf **Aufgliederung**.  

Um weitere Informationen zur physischen und reservierten Speicher- oder Plattennutzung im Zeitverlauf anzuzeigen, klicken Sie auf **Protokoll**. Sie können einen wöchentlichen oder monatlichen Zeitrahmen auswählen. In der Ansicht für die vergangene Nutzung wird ein Diagramm zur Speicher- oder Plattennutzung im ausgewählten Zeitraum angezeigt.  
	<dl>
	<dt><strong>Reservierter Grenzwert</strong></dt>
	<dd>Zeigt eine horizontale, gepunktete Linie an. Der Grenzwert für den reservierten Speicher ist die gesamte Speicher- oder Plattenkapazität, die von allen aktiven Anwendungen in Ihrer Umgebung gemeinsam reserviert werden kann.</dd>
	<dt><strong>Reserviert</strong></dt>
	<dd>Im Abschnitt 'Reserviert' wird die Speicher- oder Plattenkapazität angezeigt, die zurzeit von allen aktiven Anwendungen in Ihrer Umgebung reserviert ist.
	<p>Um anzuzeigen, welche Organisationen zu einem bestimmten Zeitpunkt den meisten Speicher reserviert haben, bewegen Sie den Mauszeiger im reservierten Bereich über einen Punkt, der den gewünschten Zeitpunkt darstellt. Klicken Sie dann im angezeigten Kreisdiagramm auf eine Organisation, um weitere Informationen zu dieser Organisation anzuzeigen.</p></dd>
	<dt><strong>Physischer Speicher - Grenzwert</strong></dt>
	<dd>Zeigt eine horizontale, gepunktete Linie an. Der Grenzwert für den physischen Speicher ist die gesamte physische Speicher- oder Plattenkapazität, die für Ihre Umgebung erworben wurde.</dd>
	<dt><strong>Physisch</strong></dt>
	<dd>Im Bereich 'Physisch' wird die Speicher- oder Plattenkapazität angezeigt, die zurzeit tatsächlich genutzt wird.</dd>
	</dl>
	
#### Details zur Verwendung des Service
{: #servicesresourceusage}

Die Registerkarte **Service** zeigt die Gesamtnutzung des Service in Bezug auf die maximale Kapazität, die für einen dedizierten Service zur Verfügung steht. Wenn Sie beispielsweise einen dedizierten Cloudant-Service haben und 500 GB der Gesamtkapazität von 1000 GB verwenden, wird anhand einer Grafik gezeigt, dass Sie 50 % der Gesamtkapazität verwendet haben. Die Farbe der Grafik ändert sich in Abhängigkeit davon, wie nah Sie an der Kapazitätsgrenze sind. Gelb gibt an, dass Sie 70 bis 84 % Ihrer Kapazität verwendet haben, und Rot wird verwendet, wenn Sie 85 % oder mehr der verfügbaren Kapazität erreicht haben.

**Hinweis**: Die Informationen zur Servicenutzung sind möglicherweise zu diesem Zeitpunkt nicht in allen Umgebungen vorhanden. Dieses Feature ist für Cloudant, MessageHub, API Connect und Session Cache verfügbar.


### Kontonutzung
{: #accountusage}

Sie können die monatliche Nutzung für Ihr Konto für Ihre dedizierte oder lokale Umgebung anzeigen. Mithilfe dieser Daten können Sie ermitteln, wie viel bestimmten Organisationen auf Grundlage ihrer Nutzung zu berechnen ist. Alle Administrationskonsolenbenutzer mit der Berechtigung **Benutzer** und mit dem Zugriffsrecht **Lesen** können die Kontonutzungsdaten anzeigen. Abrechnungsmanager der Organisation können außerdem die Kontonutzungsdaten für ihre Organisationen anzeigen, selbst wenn Abrechnungsmanagern die Administrationskonsolenberechtigung **Benutzer** nicht zugewiesen wurde. Administratoren der Administrationskonsole (Superuserberechtigung) können Organisationen die Rolle eines Abrechnungsmanagers zuweisen, indem sie auf **Konto** &gt; **Organisationen verwalten** klicken.

Führen Sie die folgenden Schritte durch, um die Kontonutzungsdaten anzuzeigen:

<ol>
<li>Klicken Sie auf <strong>Konto</strong> &gt; <strong>Nutzungsdashboard</strong>.</li>
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
<li>Klicken Sie auf <strong>Konto</strong> &gt; <strong>Nutzungsdashboard</strong>.</li>
<li>Klicken Sie auf <strong>Öffentlich</strong>.</li>
<li>Wählen Sie die Organisation aus, für die Daten angezeigt werden sollen.</li>
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

In der folgenden Tabelle sind Sicherheitsberichte aufgelistet, die für {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated generiert werden. Die meisten Berichte werden täglich generiert. Die Berichte zur Verschlüsselung und zu den wichtigsten Verwaltungsereignissen werden jedoch monatlich generiert. Alle Berichte werden in der Administrationskonsole gespeichert und können 90 Tage lang abgerufen werden. Nach Ablauf dieser 90 Tage sind die Berichte auf Anforderung an {{site.data.keyword.Bluemix_notm}} 9 Monate lang offline verfügbar. Insgesamt sind die Berichte bis zu 1 Jahr verfügbar.


{: #ld_table9}

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
{: caption="Tabelle 9. Liste der Sicherheitsberichte" caption-side="top"}

## Status anzeigen
{: #oc_status}

Sie können den Status für die {{site.data.keyword.Bluemix_notm}}-Umgebung und für die Administrationskonsole anzeigen.

### {{site.data.keyword.Bluemix_notm}}-Umgebungsstatus

Sie können den Status für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz über die {{site.data.keyword.Bluemix_notm}}-Statusseite anzeigen. Klicken Sie auf **Support** &gt; **Status**.

Die Seite 'Status' ist die zentrale Position für die Suche nach Benachrichtigungen und Ankündigungen in Bezug auf bedeutende Ereignisse, die die {{site.data.keyword.Bluemix_notm}}-Plattform und die übergeordneten Services in {{site.data.keyword.Bluemix_notm}} betreffen. Sie können einen RSS-Feed abonnieren, damit Sie nicht immer überprüfen müssen, ob Sie eine Benachrichtigung erhalten haben. Weitere Informationen zur Seite 'Status' und zur Einrichtung des RSS-Feeds finden Sie in [{{site.data.keyword.Bluemix_notm}} anzeigen](../support/index.html#viewing-bluemix-status).

### Status der Administrationskonsole

Nach der ursprünglichen Implementierung Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung wird automatisch eine Verifizierungsprüfung für die Komponenten ausgeführt, die für die Verwaltung Ihrer Umgebung verwendet werden. Sie können auf die Seite 'Verifizierungsprüfung für Administratorkonsole' wechseln, um den Status der Komponenten nach dem Ausführen der Verifizierungsprüfung zu überprüfen. Um auf die Seite zuzugreifen, wechseln Sie zu <code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>, wobei `<subdomain>` der Name Ihrer lokalen oder dedizierten Instanz ist.

Sie können eine Verifizierung jederzeit ausführen. Sie müssen angemeldet sein, um die Option zur Ausführung der Verifizierung auszuführen. Wenn Fehler auftreten, während Sie einen Benutzer hinzufügen, eine Organisation bearbeiten oder Ihre Services verwalten, führen Sie diese Prüfung aus, um festzustellen, ob Komponenten fehlschlagen oder nicht verbunden sind. Sie können ein Support-Ticket mit den Informationen aus der Prüfung öffnen, um das Problem schnell zu beheben.

## Eigenen Katalog verwalten
{: #oc_catalog}

Sie können die {{site.data.keyword.Bluemix_notm}}-Services festlegen, die den Benutzern im {{site.data.keyword.Bluemix_notm}}-Katalog angezeigt werden sollen. Klicken Sie auf **Verwaltung &gt; Katalogverwaltung**.

Wählen Sie eine Service-Kachel aus, um die Sichtbarkeit des Serviceplans zu bearbeiten. In Bezug auf die Sichtbarkeit stehen folgende Bearbeitungsoptionen zur Auswahl:

- Wählen Sie **Alle Pläne aktivieren** aus, wenn der ausgeblendete Service für Benutzer im Katalog sichtbar sein soll.
- Wählen Sie **Alle Pläne inaktivieren** aus, wenn ein Service ausgeblendet sein soll, damit er für die Benutzer im {{site.data.keyword.Bluemix_notm}}-Katalog nicht sichtbar ist.
- Soll die Sichtbarkeit eines einzelnen Plans gesteuert werden, wählen Sie den Namen des
betreffenden Plans aus. Wählen Sie dann im Dropdown-Menü zum Anzeigen des Plans für alle Organisationen die
Option **Für alle Organisationen aktivieren**, zum Ausblenden des Plans
bei allen Organisationen die Option **Für alle Organisationen inaktivieren** und zum
Anzeigen des Plans für bestimmte Organisationen die Option **Plan für bestimmte Organisationen aktivieren** aus.

<!-- staging only start -->

Sie können auch die Priorität der verfügbaren Buildpacks festlegen, die beim Erstellen von Apps für die Entwickler basierend auf der Kompatibilität ausgewählt werden.

1. Klicken Sie auf **Verwaltung &gt; Katalogverwaltung**.
2. Rufen Sie den Abschnitt **Compute** auf.
3. Wählen Sie **Buildpack-Priorität** aus.
4. Wählen Sie die Buildpack-Option aus, der innerhalb der Liste höhere oder niedrigere Priorität eingeräumt werden soll.
5. Verschieben Sie die ausgewählte Option innerhalb der Liste, indem Sie die Pfeile verwenden.

<!-- staging only end -->

### Service-Broker registrieren
{: #servicebrokerui}

Wenn Sie über einen Service verfügen, den Sie in Ihrem {{site.data.keyword.Bluemix_notm}}-Katalog anzeigen möchten, müssen Sie einen [Service-Broker ![Symbol für externen Link](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window} implementieren und registrieren. Nach der Registrierung des Brokers können Sie die Organisationen auswählen, die auf den Service in Ihrer lokalen oder dedizierten Instanz zugreifen können.

Die Methoden zur Arbeit mit Ihrem Service-Broker variieren abhängig von der Anzahl der durch den Service-Broker verwalteten Services sowie davon, ob er bereits in {{site.data.keyword.Bluemix_notm}} registriert wurde.

- Wenn Ihr Service-Broker nur einen Service verwaltet, können Sie die Benutzerschnittstelle zum Registrieren des Brokers verwenden, nachdem Sie die [Service-Broker-API ![Symbol für externen Link](../icons/launch-glyph.svg)](http://docs.cloudfoundry.org/services/api.html){: new_window} implementiert haben. Siehe [Service-Broker registrieren, der nur einen Service verwaltet](index.html#registerbrokerui).
- Verwenden Sie die Befehlszeilenschnittstelle 'cf' mit dem [{{site.data.keyword.Bluemix_notm}}-Administrator-CLI](../cli/plugins/bluemix_admin/index.html)-Plug-in (Unterbefehl `ba`) oder die [API für angepasste Services](index.html#servicebrokerapi).
- Wenn Ihr Service-Broker bereits registriert ist und Sie ihn aktualisieren oder löschen wollen, verwenden Sie die Befehlszeilenschnittstelle mit dem [{{site.data.keyword.Bluemix_notm}}-Administrator-CLI](../cli/plugins/bluemix_admin/index.html)-Plug-in (Unterbefehl `ba`) oder die [API für angepasste Services](index.html#servicebrokerapi).

#### Service-Broker registrieren, der nur einen Service verwaltet
{: #registerbrokerui}

<!-- staging only start -->

Prüfen Sie die folgenden Informationen und führen Sie diese Schritte aus, um Ihren Service-Broker zu registrieren:

**Vorbereitende Schritte:** <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implementieren Sie die Cloud Foundry-Service-Broker-API <img src="../icons/launch-glyph.svg" alt="Symbol für externen Link"></a>, um die Kommunikation zwischen Ihrem Service und {{site.data.keyword.Bluemix_notm}} einzurichten. Die Service-Broker-API besteht aus einer Gruppe von REST-Endpunkten, die von {{site.data.keyword.Bluemix_notm}} genutzt werden.

Wenn Sie den Service-Broker implementieren, müssen Sie in der JSON-Antwort von <code>GET /v2/catalog</code> die Definitionen für Ihren Service und Ihre Servicepläne, einschließlich der Serviceinformationen, die angezeigt werden sollen, angeben. Sehen Sie sich als Beispiel den folgenden JSON-Beispielcode der GET-Antwort für den Katalog an:

```
{
"services":[
   {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Cool company",
         "longDescription":"Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
         "bullets":[
            {
               "title":"Fast and Simple",
               "description":"Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title":"Connectivity",
               "description":"Cool Service is built to let you connect easily and to all of your services and applications. Sie können mit vertrauten Tools Ihre Daten sofort analysieren."
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
            "description":"Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
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
```
{: codeblock}

Mithilfe der folgenden Tabellen können Sie die JSON-Datei füllen.


{: #ld_table10}

| **JSON-Felder** | **Beschreibung** |
|-----------------|-----------------|
|bindable   | Ein boolescher Wert, der angibt, ob Serviceinstanzen an Anwendungen gebunden werden können.  |
|description | Die Beschreibung des Service, der angezeigt wird, wenn Sie den Befehl 'cf marketplace' verwenden oder wenn Sie den Mauszeiger über das Servicesymbol im Katalog der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle bewegen. Sie können für die Beschreibung einen einzelnen Satz oder Ausdruck hinzufügen. |
|name | Der Name des Service, der in der cf-Befehlszeilenschnittstelle angezeigt wird. Dieser Name muss in {{site.data.keyword.Bluemix_notm}} eindeutig sein und muss aus Kleinbuchstaben ohne Leerzeichen bestehen. Sie können den Namen des Service nicht mehr ändern, nachdem Sie den Service mit {{site.data.keyword.Bluemix_notm}} registriert haben. |
|id  | Die ID des Service. Diese ID muss in {{site.data.keyword.Bluemix_notm}} eindeutig und eine global eindeutige ID (GUID; Globally Unique Identifier) sein. Sie können die ID des Service nicht mehr ändern, nachdem Sie den Service mit {{site.data.keyword.Bluemix_notm}} registriert haben. |
|metadata | Die Metadaten des Serviceplans, die im Katalog und in der Preisliste für {{site.data.keyword.Bluemix_notm}} angezeigt werden. Das Feld für die Metadaten ist ein optionales Feld. Sie können für die Metadaten weitere Felder angeben. Weitere Informationen zu [Metadatenfeldern](index.html#metadatafields) finden Sie in der folgenden Tabelle. |
|plans | Ein Array von Serviceplandefinitionen. Weitere Informationen zu [Planfeldern](index.html#planfields) finden Sie in der folgenden Tabelle. |
{: caption="Tabelle 10. JSON-Felder" caption-side="top"}


{: #metadatafields}

| **Metadatenwerte** | **Beschreibung** |
|---------------------|-----------------|
|displayName          | Der Name des Plans, der in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle angezeigt wird. Dieser Name wird auf der Seite mit den Servicedetails sowohl im Katalog als auch in der Preisliste angezeigt. Schreiben Sie den ersten Buchstaben des Plannamens groß. Verwenden Sie nicht "Default" als Standardplannamen, sondern stattdessen "Standard". |
|providerDisplayName | Der Name des Service-Providers. |
|longDescription | Die detaillierte Beschreibung des Service. Schreiben Sie mindestens zwei Sätze für eine ausführliche Beschreibung. |
|plans                | Ein Array von Serviceplandefinitionen. Jeder Array-Eintrag in den Planfeldern besteht aus den folgenden Feldern: Name, Beschreibung, kostenlos, ID und Metadaten. Weitere Informationen zu [Planfeldern](index.html#planfields) finden Sie in der folgenden Tabelle. |
|bullets | Ein Array von Zeichenfolgen, die für einen Service angezeigt werden. Sie können Aufzählungszeichen verwenden, um neben der ausführlichen Beschreibung weitere Informationen hinzuzufügen. Das Feld für die Aufzählungszeichen muss mindestens zwei Aufzählungselemente haben. Jedes Aufzählungszeichen enthält das Titel- und Beschreibungsfeld. |
|imageUrl | Die URL eines großen Bilds im PNG-Format (50 x 50 Pixel). |
|smallImageUrl | Die URL eines kleinen Bilds im PNG-Format (24 x 24 Pixel). |
|mediumImageUrl | Die URL eines mittleren Bilds im PNG-Format (32 x 32 Pixel). |
|featuredImageUrl | Die URL eines unterstützten Bilds (64 x 64 Pixel). |
|documentationUrl | Die URL zur Dokumentation des Service. |
|termsUrl | Die URL zu den PDF-Dateien mit den Vereinbarungsbedingungen. |
|media (optional) | Ein Array von Elementen, um Videos und Screenshots anzuzeigen, die in den Service in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle einführen. Ein Medienelement kann die folgenden Felder haben: type (Bild, YouTube-Video, Video), thumbnailUrl (URL des Vorschaubilds für das Medienelement), url (URL des Screenshots oder des YouTube-Videos), source (Quellen der Videos, die nicht auf YouTube gehostet werden; der Typ "type" der Videoquelle muss von HTML5 unterstützt werden; schließen Sie "type" und "url" für das Video ein)sowie caption (Beschriftung des Medienelements; Beschriftungen unterstützen die behindertengerechte Bedienung, um die Medienelemente zu verstehen). |
|serviceKeysSupported | Ein boolescher Wert, der angibt, ob die Serviceschlüssel-API unterstützt wird. Die Serviceschlüssel-API wird verwendet, um einen Service zu aktivieren, der außerhalb von {{site.data.keyword.Bluemix_notm}} verwendet wird. Der Standardwert ist 'false'. |
|plan_updateable | Ein boolescher Wert, der angibt, ob der Service Planänderungen unterstützt. Der Standardwert ist 'false'. |
|embeddableDashboard (optional) | Ein Feld, das angibt, wie das Service-Dashboard in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle angezeigt wird. Wenn Sie keinen Wert für dieses Feld angeben, wird das Dashboard zwar integriert, aber auf eine Breite von 960 Pixel beschränkt, und das Dashboard hat eine zusätzliche horizontale Füllung um den I-Frame. Sie können 'true', 'false', 'drilldown' oder 'launch' verwenden. Sie können für dieses Feld die folgenden Werte verwenden: true, false, drilldown und launch.  |
|notCreatable (optional) | in boolescher Wert, der angibt, ob die Instanzen für den Service mit der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle und mit der cf-Befehlszeilenschnittstelle erstellt werden können. Der Wert 'true' bedeutet, dass Serviceinstanzen weder mit der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle noch mit der cf-Befehlszeilenschnittstelle erstellt werden können. Der Standardwert ist 'false'. |
|notCreatableMessage (optional) | Eine Nachricht, die in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle angezeigt wird, wenn die Serviceinstanzen nicht erstellt werden können. Wenn Sie keinen Wert für dieses Feld angeben, wird folgende Standardnachricht angezeigt: Wenn Sie benachrichtigt werden möchten, wenn er verfügbar ist, bestätigen Sie Ihre E-Mail-Adresse oder geben Sie eine neue Adresse ein. |
|notCreatableRobotMessage (optional) | Eine Nachricht, die in der Sprechblase auf der Seite mit den Servicedetails in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle angezeigt wird. Die Nachricht gibt an, ob ein Problem mit einem Service aufgetreten ist oder ob eine andere Ursache der Grund für die Nichtverfügbarkeit ist. Sie können eine Nachricht angeben, um die Ursache zu erklären. Wenn Sie keinen Wert für dieses Feld angeben, wird folgende Standardnachricht angezeigt: Der Service ist zurzeit nicht verfügbar. |
|apiReferenceUrl (optional) | Die URL von I-Frame in API-Referenzbereich, die auf der Seite mit den Servicedetails im Katalog angezeigt wird. Wenn die URL nicht für die Seite mit den Servicedetails im Katalog verwendet wird, können Sie den numerischen Wert eingeben, der Ihrer REST-API-Dokumentation für Ihren Service zugewiesen wurde, als er im Mikroservice für die REST-API-Dokumentation von {{site.data.keyword.Bluemix_notm}} registriert wurde. Daraufhin wird Ihre REST-API-Dokumentation im Service-Dashboard angezeigt. |
|sdkDownloadUrl (optional) | Die URL der Webseite, die geöffnet wird, wenn Sie auf die Schaltfläche 'SDKs herunterladen' klicken. Die Schaltfläche 'SDKs herunterladen' befindet sich in der Service-Kachel auf der Seite mit der Anwendungsübersicht im Dashboard. Die Webseite wird daraufhin in einer neuen Browserregisterkarte geöffnet. |
|serviceMonitorApi    | Die URL zu einer API, die die JSON-Daten zurückgibt, wie im folgenden Beispiel, das den Servicezustand auflistet. Dazu muss 'serviceMonitorApi' oder 'serviceMonitorApp' in Ihren Servicemetadaten vorhanden sein. Siehe folgendes Codebeispiel. |
|serviceMonitorApp    | Die URL zu einer Anwendung, die {{site.data.keyword.Bluemix_notm}} bereitgestellt und an einen Service gebunden werden kann, um die spezifische Ausgabe des Servicestatus bereitzustellen. Die Anwendung muss dasselbe JSON-Datenformat wie 'serviceMonitorApi' zurückgeben. Dazu muss 'serviceMonitorApi' oder 'serviceMonitorApp' in Ihren Servicemetadaten vorhanden sein. Siehe folgendes Codebeispiel. |
{: caption="Tabelle 11. Metadatenfelder" caption-side="top"}


```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

Im folgenden Beispiel wird dargestellt, wie eine JSON-Antwort von 'GET /v2/catalog' der Seite mit den Servicedetails im {{site.data.keyword.Bluemix_notm}}-Katalog zugeordnet wird:

![Servicedetails im Katalog.](images/metadata.png "Ansicht der Servicedetails im Bluemix-Katalog")


{: #planfields}

| **Planwerte** | **Beschreibung** |
|---------------------|-----------------|
|name       | Der Name des Serviceplans, der in der cf-Befehlszeilenschnittstelle verwendet wird. Der Planname wird beispielsweise in der Ausgabe des Befehls 'cf marketplace' angezeigt. Der Planname muss in Kleinbuchstaben und ohne Leerzeichen geschrieben sein. Er muss auch innerhalb des Service eindeutig sein.  |
|description       | Die Beschreibung des Serviceplans. Die Beschreibung wird angezeigt, nachdem Sie auf der Seite mit den Servicedetails im {{site.data.keyword.Bluemix_notm}}-Katalog einen Plan ausgewählt haben. |
|free      | Ein boolescher Wert, der angibt, ob der Serviceplan kostenfrei ist. Der Standardwert ist 'true'. |
|id       | Die ID des Serviceplans. Die ID muss eindeutig und eine GUID sein.  |
|metadata (optional)    | Die Metadaten des Serviceplans, die im Katalog und in der Preisliste für {{site.data.keyword.Bluemix_notm}} angezeigt werden. Das Feld für die Metadaten ist ein optionales Feld. Sie können im Metadatenfeld die folgenden Felder angeben: displayName, type (Abonnement, reservierbar, planDetails), bullets, costs (unitId, Einheit, partNumber) und paidOnly. Weitere Informationen zu [Planmetadatenfelder](index.html#planmetadata) finden Sie in der folgenden Tabelle. |
{: caption="Tabelle 12. Planfelder" caption-side="top"}


{: #planmetadata}

| **Planmetadatenwerte** | **Beschreibung** |
|------------------------|-----------------|
|displayName             | Der Name des Plans, der in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle angezeigt wird. Dieser Name wird auf der Seite mit den Servicedetails sowohl im Katalog als auch in der Preisliste angezeigt.   |
|type                    | Der Plantyp. Sie können für dieses Feld die folgenden Werte verwenden: subscription (Abonnementplan; Standardwert ist 'false'), reservable (reservierbarer Plan; wird nur verwendet, wenn es sich um einen Abonnementplan handelt und 'plan.metadata.subscription' den Wert 'true' hat; Standardwert ist 'false'), planDetails (detaillierte Quantität und Beschreibung der Ressourcen, die mit dem Plan verwendet werden können; wird nur verwendet, wenn der Plan reservierbar ist und 'plan.metadata.reserveable' den Wert 'true' hat) |
|bullets                 | Eine Beschreibung der Ressourcen, die mit dem Plan verwendet werden können. Die Beschreibung wird in der Spalte **Features** auf der Seite mit den Servicedetails im Katalog und in der Preisliste angezeigt. |
|costs                   | Die Informationen zu den Kosten des Service, der in der Spalte 'Preis' auf der Seite mit den Servicedetails im Katalog und in der Preisliste angezeigt  wird. Jedes Array enthält die folgenden Felder: unitId (ID der Einheit; Plural und nur Großbuchstaben verwenden; für kostenlose Pläne ist das Feld optional), unit (die Metrik, die zur Berechnung der Servicegebühren verwendet wird; Wert dieses Felds wird in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zur Darstellung der Gebührenmetrik verwendet)und partNumber (ID `part_number`, die im Abrechnungssystem verwendet wird; für kostenlose Pläne ist das Feld optional).   |
|paidOnly (optional)     | Ein boolescher Wert, der angibt, ob der Serviceplan nur für {{site.data.keyword.Bluemix_notm}}-Zahlungskonten verfügbar ist. Der Wert **true** gibt an, dass der Serviceplan nur für Zahlungskonten verfügbar ist und keinen Testkonten hinzugefügt werden kann. Der Wert **false** gibt an, dass der Serviceplan sowohl Zahlungskonten als auch Testkonten hinzugefügt werden kann. Der Standardwert ist **false**.	  |
{: caption="Tabelle 13. Planmetadatenfelder" caption-side="top"}

Im folgenden Beispiel wird dargestellt, wie eine JSON-Antwort von 'GET /v2/catalog' der Seite mit den Servicedetails im {{site.data.keyword.Bluemix_notm}}-Katalog zugeordnet wird. Es wird insbesondere dargestellt, wie die Planmetadatenfelder, die in der Tabelle oben beschrieben werden, der Benutzerschnittstelle zugeordnet werden:

![Planmetadatendetails im Katalog.](images/plan_metadata.png "Ansicht der Planmetadatenwerte im Bluemix-Katalog")


<!-- staging only end -->

<ol>
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

Führen Sie zum Erstellen einer Organisation und zum Hinzufügen von Managern die folgenden Schritte aus:

1. Klicken Sie auf <strong>Organisation erstellen</strong>.
2. Geben Sie einen Namen für die Organisation ein.
3. Geben Sie den Namen oder die E-Mail-Adresse der Person ein, die als Manager hinzugefügt werden soll. Geben Sie
mehrere Namen ein bzw. wählen Sie mehrere Namen aus, wenn Sie mehrere Manager hinzufügen möchten.
4. Klicken Sie auf <strong>Organisation erstellen</strong>, um die Änderungen zu speichern und die Organisation zu erstellen.

### Bereiche erstellen

Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps den Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen:

1. Klicken Sie in der Menüleiste auf **Konto** &gt; **Organisationen verwalten**.
2. Wählen Sie die Organisation aus, der Sie einen Bereich hinzufügen möchten.
3. Klicken Sie auf **Bereich erstellen**.
4. Geben Sie einen Bereichsnamen ein.
5. Klicken Sie auf **Erstellen**.

### Kontingentüberwachung

Sie können den Abschnitt **Kontingentüberwachung** erweitern, um folgende Informationen anzuzeigen:

- In der Hauptspeichernutzung für Umgebung finden Sie Details zur Speicherbelegung für die gesamte Systemumgebung. Im Diagramm werden folgende Informationen dargestellt:
<ul>
<li>Der belegte physische Hauptspeicher und die Begrenzung des verfügbaren physischen Hauptspeichers</li>
<li>Das derzeit reservierte Speicherkontingent und die Begrenzung des reservierbaren Hauptspeichers</li>
<li>Das gesamte Speicherkontingent für Ihre Organisationen</li>
</ul>
Die folgenden Typen der Speicherbelegung werden im Diagramm angezeigt.

	<dl>
	<dt><strong>Physischer Speicher - Belegung</strong></dt>
	<dd>Der physische Speicher, der von der Umgebung belegt wird.</dd>
	<dt><strong>Physischer Speicher - Grenzwert</strong></dt>
	<dd>Der gesamte physische Speicher, der für die Umgebung zur Verfügung steht.</dd>
	<dt><strong>Reservierter Speicher - Quote</strong></dt>
	<dd>Die Summe des Speichers, der für alle bereitgestellten Anwendungen in allen Organisationen reserviert ist. Die Summe des reservierten Speicherkontingents kann die physische Speicherbegrenzung für Ihre Umgebung überschreiten. Beispiel: Wenn Sie eine Begrenzung des physischen Hauptspeichers von 16 GB haben, können Sie für insgesamt fünf verschiedene Anwendungen jeweils 4 GB reservieren. Das reservierte Kontingent überschreitet die physische Speicherbegrenzung. In vielen Fällen wird das Kontingent, das von den einzelnen Anwendungen reserviert wurde, von den Anwendungen jedoch gar nicht in vollem Umfang genutzt. Darüber hinaus gilt auch, dass nicht alle Anwendungen gleichzeitig das gesamte Kontingent an reserviertem Speicher nutzen, das ihnen zugeordnet ist.</dd>
	<dt><strong>Grenzwert für Reserve</strong></dt>
	<dd>Der Gesamtspeicher, der für alle Anwendungen in Ihrer Umgebungen reserviert werden kann.</dd>
	<dt><strong>Gesamtkontingent</strong></dt>
	<dd>Das gesamte Speicherkontingent für alle Organisationen.</dd>
	</dl>
	**Hinweis:** Die Daten werden alle 4 Stunden automatisch aktualisiert. Klicken Sie auf **Neu berechnen**, wenn Sie die Daten auf der Seite vor der automatischen Aktualisierung aktualisieren möchten.

- Hauptspeichernutzung für Organisation. Dieser Bereich enthält Details zur Speicherbelegung auf
Organisationsebene. Sie können das gesamte Speicherkontingent, das reservierte Kontingent und den physischen Speicher anzeigen, die von jeder Organisation verwendet werden. Das Diagramm liefert Informationen, die nach der höchsten Speicherbelegung pro Organisation reserviert sind. Die Organisation, die den größten Speicherumfang reserviert, wird standardmäßig an erster Stelle angezeigt. Sie können die Liste nach
der höchsten Speicherbelegung und der überschüssigen Speicherzuordnung sortieren.

	<dl>
	<dt><strong>Höchste Speichernutzung</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option für die höchste Speicherbelegung die Organisation, die den meisten Speicher reserviert. Sortieren Sie die Liste nach der höchsten Speicherbelegung, um die Organisationen zu ermitteln, die den meisten Speicher reservieren. Die Liste ist nach dem reservierten Kontingent sortiert. </dd>
	<dt><strong>Überschüssige Hauptspeicherzuordnung</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option die Organisationen, die ein gesamtes Speicherkontingent haben, der mehr größer ist als erforderlich. Sortieren Sie die Liste nach der überschüssigen Speicherzuordnung, um Organisationen zu ermitteln, die im Verhältnis zu dem jeweils zugeordneten Speicher am wenigsten Speicher belegen. </dd>
	</dl>

### Kontingente verwalten
{: #manageorgquota}

Ein Kontingent stellt die Ressourcengrenzen für die Organisationen in Ihrer Umgebung dar, die beim Erstellen der Organisation zugeordnet wird. Jede Anwendung oder jeder Service in einem Bereich der Organisation trägt zur Nutzung des zugeordneten Kontingents bei. Führen Sie die folgenden Schritte aus, um das Kontingent für eine Organisation zu verwalten:

<ol>
<li>Klicken Sie im Abschnitt 'Hauptspeichernutzung für Organisation' auf den Balken im Diagramm für die Organisation, die bearbeitet werden soll, oder wählen Sie den Namen der Organisation im Bereich 'Organisationsliste' aus. Auf der Seite 'Informationen zu Organisation' können Sie die Organisation umbenennen oder Manager hinzufügen oder entfernen.
<p><strong>Hinweis:</strong> Wenn Sie einen Kontingentplan auswählen, der für die aktuelle Speichernutzung einer Organisation nicht ausreicht, erhalten Sie eine Nachricht.</p></li>
<li>Klicken Sie auf <strong>Cloud Foundry</strong> oder <strong>Container</strong>.  Standardmäßig wird die Kontingentseite 'Cloud Foundry' geöffnet. 
<ul>
<li>Auf der Seite 'Cloud Foundry' können Sie einen Plan auswählen und die Kontingentdetails für die folgenden Ressourcen anzeigen:
<ul>
<li>Services</li>
<li>Routen</li>
<li>Speicherkontingent</li>
<li>Anwendungszuordnung</li>
</ul>
</li>
<li>Auf der Seite <strong>Container</strong> können Sie für die folgenden Felder Werte zuweisen (diese müssen Ganzzahlen sein):
<dl class="parml">
<dt class="pt dlterm">Imagegrenzwert</dt>
<dd class="pd">Die maximale Anzahl von Container-Images, die in Ihrer privaten Registry vorhanden sein darf. Ein Container-Image ist die Basis für jeden von Ihnen erstellten Container. Ein Image wird aus einer Docker-Datei erstellt. Dabei handelt es sich um eine schreibgeschützte Datei, in der das Betriebssystem, die App und alle ihre Abhängigkeiten gespeichert sind, und in der beschrieben wird, wie ein Container konfiguriert wird. Images werden mit allen Mitgliedern einer Organisation gemeinsam genutzt.</dd>
<dt class="pt dlterm">Hauptspeicherzuordnung - Standard</dt>
<dd>Die Containerspeichermenge, die automatisch zugewiesen wird, wenn ein neuer Bereich erstellt wird. Beim Erstellen eines Containers müssen Sie eine Containergröße auswählen. Durch die Größe wird die Speichermenge bestimmt, die der Container auf dem Berechnungshost verwenden kann, und sie wird bei der Speicherbegrenzung für den Container berücksichtigt. </dd>
<dt class="pt dlterm">Hauptspeicherzuordnung - Maximum</dt>
<dd>Die maximale Containerspeichermenge, die bereichsübergreifend in einer Organisation zugeordnet verteilt werden kann.</dd>
<dt class="pt dlterm">Variable IPs - Standard</dt>
<dd>Die Anzahl öffentlicher IP-Adressen, die automatisch zugeordnet wird, wenn ein neuer Bereich erstellt wird. Sie können öffentliche IP-Adressen an einzelne Container und Containergruppen binden, damit über das Internet auf sie zugegriffen werden kann.</dd>
<dt class="pt dlterm">Variable IPs - Maximum</dt>
<dd>Die maximale Anzahl öffentlicher IP-Adressen, die Sie bereichsübergreifend in einer Organisation zuordnen können.</dd>
</dl>
<strong>Hinweis:</strong> Wenn in Ihrer Umgebung noch keine Container vorhanden oder konfiguriert sind, wird eine Fehlernachricht angezeigt.
<p>Weitere Informationen zu Containern finden Sie in den [Informationen zu IBM Containern](/docs/containers/container_ov.html). Weitere Informationen zu Containerkontingenten finden Sie unter [Kontingent und Bluemix-Konten](/docs/containers/container_planning_org_ov.html#container_planning_quota).</p>
<strong>Hinweis:</strong> In der {{site.data.keyword.Bluemix_notm}}-Region 'Sydney' stehen keine Container zur Verfügung.</li>
</ul>
<li>Speichern Sie Ihre Änderungen auf der Seite 'Organisation verwalten', indem Sie auf <strong>Speichern</strong> klicken.</li>
</ol>


### Organisationen über die Organisationsliste verwalten
{: #manageorgfrolis}

Im Bereich der Organisationsliste werden alle Organisationen in der {{site.data.keyword.Bluemix_notm}}-Umgebung angezeigt und Sie können Aktionen für einzelne Organisationen durch Klicken auf den Organisationsnamen ausführen.

- Löschen Sie eine Organisation, indem Sie auf das Symbol **Löschen** ![Löschen](images/icon_trash.svg) in der Spalte 'Aktionen' klicken.
- Zeigen Sie den Kontingentplan für eine Organisation an, indem Sie auf den Namen der Organisation in der Liste klicken. Auf der Seite **Organisationen verwalten** für die ausgewählte Organisation können Sie die folgenden Nutzungsinformationen anzeigen:

  - Anzahl der Services, die zurzeit verwendet werden.
  - Anzahl der Routen, die zurzeit verwendet werden.
  - Speicherkontingentdiagramm, das zeigt, wie viel des Kontingents zurzeit verwendet und wie viel nicht verwendet wird.
  - Diagramm zur Anwendungszuordnung, das zeigt, welche Anwendungen in dem Wert für das genutzte Speicherkontingent enthalten sind.
  - Diagramm zur gemessenen Anwendungsnutzung, das einen dreimonatigen Bericht zu den genutzten GB-Stunden pro bereitgestellter App zeigt. Sie können die **Listenansicht** auswählen, um Daten für alle Apps mit Speicherzuordnung pro App und gemessener GB-Stundennutzung für die vergangenen drei Monate anzuzeigen.

- Zum Bearbeiten des Namens der Organisation sowie zum Hinzufügen oder Entfernen von Managern klicken Sie auf den Namen der Organisation in der Liste und folgen den Anweisungen in der Anzeige.
- Um Informationen zu einem bestimmten Benutzer der angezeigten Organisation anzuzeigen, klicken Sie auf den Benutzernamen, um die Benutzerinformationen anzuzeigen. Anschließend können Sie auf den Namen der Organisation klicken, um zur Anzeige der Organisationsinformationen zurückzukehren. 

## Benutzer und Berechtigungen verwalten
{: #oc_useradmin}

Sie können Benutzer einzeln oder in Gruppen hinzufügen. Im Allgemeinen werden Benutzer zur {{site.data.keyword.Bluemix_notm}}-Instanz aus dem Benutzerregistry des Unternehmens über das LDAP-Protokoll hinzugefügt (LDAP - Lightweight Directory Access Protocol). Sie können auch Benutzerberechtigungen anzeigen. Wenn Ihnen die Berechtigung **Superuser** zugewiesen ist, können Sie auch Berechtigungen für andere Benutzer festlegen und verwalten. Klicken Sie auf **Verwaltung &gt; Benutzeradministration**.

Auf der Seite für die Benutzerverwaltung werden alle Benutzer für die lokale oder dedizierte Instanz angezeigt. Die Berechtigungen für jeden Benutzer werden über Symbole in der Tabelle angezeigt. Folgende Berechtigungen sind zulässig: None, **Superuser**, **Basic Access**, **Catalog**, **Reports** und **Users**.
Für die Berechtigungen **Superuser** und **Basic Access** kann **On** oder **Off** eingestellt werden; die restlichen Berechtigungen werden mithilfe bestimmter Zugriffstypen aktiviert oder inaktiviert, unter anderem durch den Zugriff **Lesen** oder **Schreiben** für die Berechtigung, die durch Symbole angezeigt wird. Beschreibungen der einzelnen Typen und Erläuterungen der Symbole finden Sie in [Berechtigungen](#permissions).

### Mit Benutzern arbeiten
{: #workwithusers}

Abhängig vom Zugriff **Lesen** oder **Schreiben** für die Berechtigungen des Benutzers können Sie nach vorhandenen Benutzern suchen, Benutzer entfernen und Benutzer einzeln oder in Gruppen hinzufügen. Sie verfügen über vollen Zugriff zum Ausführen jeder Task für die Benutzerverwaltung in der Umgebung, wenn Sie die Berechtigung **Superuser** besitzen. Überprüfen Sie die folgenden Benutzermanagement-Tasks sowie die zur Ausführung der einzelnen Tasks erforderlichen Zugriffsebenen:

* Suchen Sie Benutzer. Wenn Sie über den Zugriff **Lesen** oder **Schreiben** verfügen und den Benutzername ganz oder teilweise kennen, können Sie mithilfe des Felds **Suchen** Benutzer in der Tabelle suchen. Sie können die Benutzerliste auch nach Organisation und Berechtigung filtern. Führen Sie die folgenden Schritte aus, um eine Benutzerliste zu filtern:
  <ol>
  <li>Klicken Sie auf <strong>Filtern</strong>.</li>
  <li> Klicken Sie auf <strong>Organisationen</strong> oder <strong>Berechtigungen</strong>, je nachdem, nach was Sie filtern möchten.
  <dl>
	<dt><strong>Organisation</strong></dt>
	<dd>Um Benutzer nach ihrer Organisation zu filtern, geben Sie die ersten Buchstaben des Organisationsnamens in das Feld <strong>Organisation</strong> ein und wählen Sie aus der Liste die gewünschte Organisation aus. Wählen Sie dann die Rolle oder Rollen aus, dien den Benutzern in den Organisationen zugewiesen sind.</dd>
	<dt><strong>Berechtigungen</strong></dt>
	<dd>Um Benutzer nach ihren Berechtigungen zu filtern, wählen Sie zunächst den Benutzertyp aus. Sie können beispielsweise alle Superuser anzeigen. Für andere Berechtigungen als <strong>Superuser</strong> oder <strong>Basiszugriff</strong> können Sie auch den Zugriffstyp auswählen, z. B. <strong>Lesen</strong> oder <strong>Schreiben</strong>.</dd>
	</dl></li>
  <li>Klicken Sie auf <strong>Anwenden</strong>.</li>
   </ol>

   Im Fenster 'Benutzeradministration' werden die festgelegten Filter und die angezeigt, die den angegebenen Filtern entsprechen. Sie können dann in der gefilterten Tabelle nach einem Benutzer suchen. Sie können die Liste der angegebenen Filter bearbeiten, indem Sie eine Filteroption aus der Liste entfernen.

* Fügen Sie einen einzelnen Benutzer hinzu. Wenn Sie die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen, können Sie Benutzer hinzufügen.

  1. Um einen einzelnen Benutzer aus Ihrem LDAP-Verzeichnis hinzuzufügen, klicken Sie auf **Benutzer hinzufügen**.
  2. Geben Sie im Feld **Suche** die E-Mail-Adresse für den Benutzer ein und wählen Sie anschließend den Benutzer aus der gefüllten Liste aus.
  3. Wählen Sie neben dem Feld **Organisation** die Organisation aus, zu der Sie den Benutzer hinzufügen möchten, indem Sie den Namen der Organisation eingeben und diesen aus der gefüllten Liste auswählen.
  4. Klicken Sie auf **Benutzer hinzufügen**, um den Benutzer zur ausgewählten Organisation hinzuzufügen.

  **Hinweis:** Wenn die Operation zum Hinzufügen erfolgreich ist, wird der Benutzer für Sie zum Anzeigen und zum Durchsuchen zu der Tabelle hinzugefügt. Wenn Benutzer hinzugefügt werden, sind ihnen keine Berechtigungen zugewiesen.

* Fügen Sie eine Benutzergruppe aus Ihrem LDAP-Verzeichnis hinzu. Wenn Sie die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen, können Sie Benutzer hinzufügen.

  1. Klicken Sie auf **Benutzergruppe hinzufügen**.
  2. Geben Sie im Feld **Suche** einen Gruppennamen für die Suche ein und wählen Sie den Gruppennamen aus der gefüllten Liste aus.
  3. Wählen Sie neben dem Feld **Organisation** die Organisation aus, zu der Sie die Benutzergruppe hinzufügen möchten, indem Sie den Namen der Organisation eingeben und diesen aus der gefüllten Liste auswählen.
  4. Klicken Sie auf **Benutzer hinzufügen**, um die Benutzergruppe zu der ausgewählten Organisation hinzuzufügen.

  **Hinweis:** Gruppen oder mehr als 50 Benutzer werden über einen Stapeljob im Hintergrund hinzugefügt. Wenn die Hinzufügeoperation erfolgreich war, wird der Benutzer bzw. die Gruppe zur Tabelle hinzugefügt und Sie können ihn bzw. sie anzeigen und durchsuchen. Wenn Benutzer hinzugefügt werden, sind ihnen keine Berechtigungen zugewiesen.

* Eine Gruppe von Benutzern hinzufügen, indem ein Arbeitsblatt importiert wird, das die Benutzer-IDs, E-Mail-Adressen und die Organisation enthält, zu der Sie die Benutzer hinzufügen möchten. Wenn Sie die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen, können Sie Benutzer hinzufügen.

**Hinweis:** Geben Sie die Benutzer-IDs ein, die mit den in Ihrer Benutzerregistry verwendeten Werten übereinstimmen.

  1. Klicken Sie auf **Benutzer importieren**.
  2. Klicken Sie auf **Vorlage herunterladen (.CSV)**, um ein Arbeitsblatt mit den erforderlichen Spalten herunterzuladen, das Sie ausfüllen können, oder um Ihr eigenes Arbeitsblatt zu erstellen, das mindestens die folgenden erforderlichen Spaltenüberschriften enthält: **Benutzer-ID**, **E-Mail**, **Organisation**.  In der Vorlage sind zwei optionale Spalten enthalten: **Vorname** und **Nachname**.
  3. Geben Sie die Benutzerwerte in die erforderlichen Spalten ein. Falls Sie kein LDAP-Verzeichnis verwenden, verwenden Sie die erforderlichen und optionalen Spaltenüberschriften für die Benutzer, die Sie importieren.
  4. Speichern Sie Ihre Datei und klicken Sie auf **Datei hochladen**.

  **Hinweis:** Die Spalten innerhalb des Arbeitsblatts können in beliebiger Reihenfolge angeordnet sein, solange Sie über alle erforderlichen Spalten verfügen. Wenn der Import erfolgreich war, erhalten Sie eine Bestätigungsnachricht, in der bestätigt wird, dass alle Benutzer hinzugefügt wurden. Wenn der Import für einige Benutzer erfolgreich war, für andere hingegen nicht, prüfen Sie die Fehlernachricht, um Aktionen für die Benutzer zu ergreifen, die nicht hinzugefügt werden konnten.

* Entfernen Sie Benutzer. Wenn Sie die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen, können Sie Benutzer permanent aus der Umgebung entfernen.

    1. Suchen Sie den Benutzer und klicken Sie auf das Symbol ![Löschen](images/icon_trash.svg).
    2. Klicken Sie auf **Entfernen**.

* Damit Sie Berechtigungen und Organisationen, zu denen Benutzer gehören, bearbeiten können, müssen Sie über die Berechtigung **Superuser** verfügen. Um Berechtigungen für Benutzer zu bearbeiten, suchen Sie den gewünschten Benutzer und klicken Sie auf den Benutzernamen. Auf der Seite **Benutzer bearbeiten** können Sie die Berechtigungen aktivieren oder inaktivieren.

    * Wählen Sie **On** in der Liste aus, um die Berechtigung **Superuser** oder **Basic Access** (Basiszugriff) zu aktivieren.
    * Wählen Sie in der Liste **Lesen** (Read) aus, um dem Benutzer den Zugriff **Lesen** (schreibgeschützt) für diese Berechtigung zu erteilen, oder wählen Sie **Schreiben** (Write) aus, um dem Benutzer den Schreibzugriff **Schreiben** zum Bearbeiten, Hinzufügen und Entfernen für diese Berechtigung zu erteilen.
    * Wählen Sie **Off** aus, um alle Berechtigungen zu inaktivieren.

    **Hinweis:** Wenn für die Berechtigung **Superuser** die Einstellung **On** festgelegt wird, wird für alle anderen Berechtigungen **Schreiben** eingestellt.

* Wenn Sie einen Benutzer zu einer bestimmten Organisation hinzufügen oder aus ihr entfernen möchten, müssen Sie über die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** verfügen.

    1. Wählen Sie den Benutzernamen in der Tabelle aus, um auf die Seite **Benutzer bearbeiten** zuzugreifen und einen Benutzer zu einer Organisation hinzuzufügen. Verwenden Sie anschließend das Suchfeld, um eine Organisation zu lokalisieren, wählen Sie die Organisation aus der Liste aus und klicken Sie anschließend auf **Speichern**.
    2. Wählen Sie den Benutzernamen in der Tabelle aus, um auf die Seite **Benutzer bearbeiten** zuzugreifen und einen Benutzer aus einer Organisation zu entfernen. Klicken Sie anschließend für die Organisation, aus der der Benutzer entfernt werden soll, auf ![Entfernen](images/icon_remove.svg) und dann auf **Speichern**.
    
* Um Informationen zu der Organisation anzuzeigen, der der Benutzer zugewiesen ist, klicken Sie auf den Namen der Organisation, um die Organisationsinformationen anzuzeigen. Anschließend können Sie auf den Benutzernamen klicken, um zur Anzeige der Benutzerinformationen zurückzukehren. 

### Berechtigungen
{: #permissions}

Den Benutzern können die folgenden Berechtigungen mit bestimmten Zugriffsebenen (Lesen oder Schreiben) zugeordnet werden, die dem Benutzer die Ausführung bestimmter Tasks in der Administrationskonsole ermöglichen.


{: #ld_table14}

| **Benutzerberechtigung** | **Beschreibung** |       
|-----------------|-------------------|
| Superuser | Benutzer mit der Berechtigung **Superuser**, für die **On** eingestellt ist, können die Berechtigungen für andere Benutzer bearbeiten. Wenn für die Berechtigung 'On' festgelegt ist, ist automatisch der uneingeschränkte Zugriff auf alle anderen Berechtigungen aktiviert. Zusätzlich zu den Tasks, die für jede Berechtigung in dieser Tabelle beschrieben werden, kann der Superuser auch Benachrichtigungsabonnements einrichten, um direkt über Wartungen und Vorfälle benachrichtigt zu werden, Wartungen zu planen, Verifizierungsprüfungen für Konsolenkomponenten auszuführen und Organisationen und Bereiche für die Umgebung zu erstellen. Diese Berechtigung entspricht der Administratorrolle (admin) für die Administrationskonsole.  |
| Basic Access | Benutzer mit der Berechtigung **Basic Access**, für die **On** eingestellt ist, können die Option für die Verwaltungsseite in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle anzeigen. Benutzer, deren Berechtigung aktiviert ist, können auf die Kacheln [Systeminformationen](#oc_system) und [Ressourcennutzung](#oc_resource) zugreifen. Ohne diese Berechtigung können Benutzer die Menüoption 'Verwaltung' nicht anzeigen und nicht auf sie zugreifen. Diese Berechtigung entspricht der Administratorrolle (admin) für die Administrationskonsole. Diese Berechtigung entspricht der Administratorrolle (login) für die Administrationskonsole. |
| Catalog | Benutzern mit der Berechtigung **Catalog** kann der Zugriff auf **Lesen** oder **Schreiben** (Ändern) zugewiesen werden, und zwar für die in der lokalen oder dedizierten Instanz verfügbaren Services. Ein Benutzer mit Lesezugriff kann auf die Kachel 'Katalogverwaltung' zugreifen, um verfügbare Services anzuzeigen. Ein Benutzer mit Schreibzugriff kann auf die Kachel [Katalogverwaltung](#oc_catalog) zugreifen, um Services anzuzeigen, die Sichtbarkeit der Services zu bearbeiten, angepasste Services zu registrieren und die Liste für die Buildpack-Priorität zu steuern. |  
| Reports | Benutzern mit der Berechtigung **Reports** kann für Sicherheitsberichte der Zugriff **Lesen** oder **Schreiben** (Ändern) zugewiesen werden. Ein Benutzer mit Lesezugriff kann auf die Kachel 'Berichte und Protokolle' zugreifen, um Berichte herunterzuladen. Benutzer mit Schreibzugriff können die Kachel [Berichte und Protokolle](#oc_report) anzeigen und mithilfe der Befehlszeilenschnittstelle neue Berichte hochladen sowie neue Kategorien für den Zugriff durch die Benutzer erstellen. |
| Users | Benutzern mit der Berechtigung **Users** kann der Zugriff **Lesen** (Anzeigen) für die Liste der Benutzer oder **Schreiben** (Hinzufügen oder Entfernen) für Benutzer zugewiesen werden. Diese Berechtigung erlaubt es Ihnen nicht, Berechtigungen für andere Benutzer festzulegen. Benutzer mit Schreibzugriff können neue Benutzer zur Umgebung hinzufügen, Benutzer aus der Umgebung löschen und vorhandene Benutzer zu Organisationen hinzufügen, die in der Umgebung bereits vorhanden sind. Außerdem können Benutzer mit dem Zugriff **Schreiben** neue Organisationen hinzufügen, Organisationen löschen und die Benutzer in den Organisationen bearbeiten. |
{: caption="Tabelle 14. Berechtigungen" caption-side="top"}

## REST-APIs verwenden 
{: #auth_adminapi}

Für die Verwendung der REST-API-Befehle müssen Sie sich zunächst authentifizieren. Zur Generierung und Unterstützung von Sitzungen können Sie cURL-Befehle für die folgenden Tasks verwenden:

* [Bei der Administrationskonsole anmelden](#auth_loginapi) 
* [Benutzer-ID und Kennwort speichern](#auth_setuidpw)
* [Cookies speichern](#auth_apistorecook)
* [Cookies wiederverwenden](#auth_apireusecook)

### Bei der Administrationskonsole anmelden
{: #auth_loginapi}

Vor dem Ausführen von `Admin`-API-Anforderungen müssen Sie sich bei der Administrationskonsole anmelden. 

Zum Anmelden bei der Administrationskonsole können Sie die Basiszugriffsauthentifizierung am Endpunkt `https://console.<region>.bluemix.net/login` verwenden. Der Server gibt ein Cookie mit Ihrer Sitzung zurück. Dieses Cookie verwenden Sie für alle Operationen mit der Administrationskonsole.

**Anmerkung:** Die Sitzung wird ungültig, wenn Sie mehrere Stunden lang nicht genutzt wird.

Führen Sie zum Anmelden bei der Administrationskonsole den folgenden Befehl aus:

`curl --user <Benutzer-ID>:<Kennwort> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">--user <em>Benutzer-ID</em>:<em>Kennwort</em></dt>
<dd class="pd">Akzeptiert die Benutzer-ID und das Kennwort und sendet einen Header für die Basisauthentifizierung.</dd>
<dt class="pt dlterm">-c <em>Dateiname</em></dt>
<dd class="pd">Speichert die angegebene Benutzer-ID und das angegebene Kennwort als Cookie in der angegebenen Datei.</dd>
<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Ruft die angegebene Benutzer-ID und das angegebene Kennwort als Cookie in der angegebenen Datei ab.</dd>
<dt class="pt dlterm">--header</dt>
<dd class="pd">Sendet einen Akzeptanzheader.</dd>
</dl>

Das folgende Beispiel zeigt die Ausgabe dieses Befehls:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Benutzer-ID und Kennwort speichern
{: #auth_setuidpw}

Sie können Ihre Benutzer-ID und das zugehörige Kennwort auch speichern, sodass Sie es nicht bei jeder Anmeldung manuell eingeben müssen.  Verwenden Sie das folgende cURL-Beispiel, um Ihre Benutzer-ID und das Kennwort zur Wiederverwendung zu speichern:

`curl -X GET -H "Authorization: Basic <redacted>" -H "Accept: application/json" "http://localhost:3000/login"`
{: codeblock}

Wenn Sie Ihre Anmeldeinformationen in einer separaten Datei speichern und dann die Datei aufrufen wollen, sodass Sie die Informationen nicht für jede Authentifizierungsanforderung erneut eingeben müssen, verwenden Sie die Option `--netrc`, die mit dem cURL-Befehl zur Verfügung steht.

Wenn Sie die Option `--netrc` mit cURL verwenden wollen, erstellen Sie zunächst eine Datei im Ausgangsverzeichnis des Benutzers auf eine der folgenden Weisen:
* UNIX-System: Erstellen Sie eine Datei mit dem Namen '.netrc'. 
* Windows-System: Erstellen Sie eine Datei mit dem Namen '_netrc'. 

Geben Sie in dieser Datei die folgenden Informationen an:

`machine console.<Region>.bluemix.net
login <ID>
password <Kennwort>`
{: codeblock}

Fügen Sie im Aufruf eines cURL-Befehls das folgende Argument hinzu: `--netrc`.
<p>Wenn Sie mit einer netrc-Datei arbeiten wollen, die sich in einem anderen Verzeichnis befindet, verwenden Sie die Option `--netrc-file [Datei]`. Dabei ist `[Datei]` die Speicherposition der netrc-Datei.</p>
</li>
</ol>


### Cookies speichern
{: #auth_apistorecook}

Wenn Sie sich bei der Administratorkonsole anmelden, gibt der Server ein Cookie mit Ihrer Sitzung zurück. Dieses im Anmeldeprozess übergebene Cookie ist für zukünftige API-Aufrufe bei allen Operationen mit der Administrationskonsole erforderlich. Sie können Cookies zur späteren Verwendung speichern.

Zum Speichern von Cookies nach der Anmeldung verwenden Sie die Option `-c` wie im folgenden CURL-Beispiel:

`curl --user <Benutzer-ID>:<Kennwort> -c ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/login | python -m json.tool`
{: codeblock}

### Cookies wiederverwenden
{: #auth_apireusecook}

Zur Wiederverwendung von Cookies verwenden Sie die Option `-b` mit dem Dateinamen des Cookies, den Sie mit der Option `-c` zugewiesen haben, wie im folgenden CURL-Beispiel gezeigt:

`curl --user <Benutzer-ID>:<Kennwort> -b ./cookies.txt`
{: codeblock}

## Benutzer mit der Admin-REST-API verwalten

{: #usingadminapi}

Sie können die REST-API `Admin` verwenden, um Benutzer für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz hinzuzufügen und zu entfernen.
Die Endpunkte und JSON-Antworten der `Admin`-REST-API werden probeweise zu Verfügung gestellt, um Basisoperationen über eine Befehlszeile zu ermöglichen. Die in den vorliegenden Informationen zu den Beispielen enthaltenen Endpunkte und URLs können jederzeit geändert oder entfernt werden.

Wenn Sie die Berechtigung **Superuser** oder die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen, können Sie Benutzer hinzufügen oder entfernen. Zum Bearbeiten der Berechtigungen anderer Benutzer benötigen Sie die Berechtigung **Superuser**.

Sie können zwar auswählen, ob Sie andere Tools verwenden möchten, jedoch sind die folgenden Tools Voraussetzungen für die Verwendung der nachfolgenden Beispiele:
* cURL für die Eingabe von REST-API-Anforderungen als Befehle. cURL ist ein Dienstprogramm zur freien Verwendung, mit dessen Hilfe Sie über eine Befehlszeilenschnittstelle HTTP-Anforderungen an einen Server senden und Antworten vom Server empfangen können. Sie können
cURL von der [cURL-Download-Site ![Symbol für externen Link](../icons/launch-glyph.svg)](http://curl.haxx.se/download.html){: new_window} herunterladen.
* Python für die Verwendung des Python-Tools für JSON-Schöndruck. Dieses optionale Tool akzeptiert JSON-Text als Eingabe und stellt eine übersichtliche Ausgabe zur Verfügung. Sie können Python von der [Python-Download-Site ![Symbol für externen Link](../icons/launch-glyph.svg)](https://www.python.org/downloads){: new_window} herunterladen.


### Organisationen auflisten
{: #listingorg}

Beim Hinzufügen eines Benutzers müssen Sie eine Organisation angeben. Sie können die `Admin`-REST-API verwenden, um alle Organisationen aufzulisten. Zum Auflisten der Organisationen müssen Sie die Berechtigung **Users** mit dem Zugriff **Lesen** besitzen. Führen Sie zum Auflisten von Organisationen den folgenden Befehl aus:

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option <samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>

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

Sie können feststellen, ob ein Benutzer bereits zu Ihrer {{site.data.keyword.Bluemix_notm}}-Umgebung hinzugefügt wurde, und zwar mithilfe der REST-API `Admin` zum Auflisten der registrierten Benutzer. Zum Auflisten der registrierten Benutzer müssen Sie die Berechtigung **Users** mit dem Zugriff **Lesen** besitzen. Zum Auflisten aller Benutzer führen Sie den folgenden Befehl aus:

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option <samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>
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
            "first_name": "ein_vorname",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "ein_nachname",
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

Sie können die REST-API `Admin` verwenden, um Benutzer zur {{site.data.keyword.Bluemix_notm}}-Instanz hinzuzufügen. Zum Hinzufügen von Benutzern müssen Sie die Berechtigung **Users** mit dem Zugriff **Schreiben** oder die Berechtigung **Superuser** (ops.admin) für die Administrationskonsole besitzen. Ferner können Sie als Administrator den Mitglieder der Organisation, die nicht die allgemeinen Berechtigungen `Users` oder `Superuser` für die Administrationskonsole besitzen, die Berechtigung zum Hinzufügen neuer Benutzer für ihre Organisation erteilen. Verwenden Sie den folgenden API-Befehl, um diese Funktion für Organisationsmanager einzurichten:

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

Sie können einen Benutzer oder eine Liste von Benutzern hinzufügen. Dabei können Benutzer einer einzelnen Organisation oder mehreren Organisationen hinzugefügt werden. Zum Hinzufügen eines Benutzers müssen Sie die folgenden Informationen angeben:

* Vorname (fist_name) und Familienname (last_name) des Benutzers. Geben Sie den Vornamen (`"first_name"`) und den Familiennamen (`"last_name"`) aus [Benutzer auflisten](index.html#listingusr) an.
* E-Mail-Adresse und Benutzer-ID: Geben Sie die Benutzer-ID (`"user_id"`) aus [Benutzer auflisten](index.html#listingusr) für die E-Mail-Adresse und für die Benutzer-ID an.
* `"guid"`. Geben Sie die GUID der Organisation aus [Organisationen auflisten](index.html#listingorg) an.

Diese Informationen werden in einer JSON-Datei angegeben.

`curl -b ./cookies.txt https://<eigener Host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>Dateiname</em></dt>
<dd class="pd">Übergibt die Benutzer-ID und das zugehörige Kennwort, die zuvor mit der Option <samp class="ph codeph">-c</samp> in der Datei gespeichert wurden, als Cookie an den HTTP-Server.</dd>
</dl>

<ol>
<li>Erstellen Sie eine JSON-Datei, die die Informationen in einem ordnungsgemäßen JSON-Format enthält.
<p>Erstellen Sie beispielsweise eine Datei namens `user.json` mit dem folgenden Inhalt:</p>
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
<li>Übergeben Sie mit dem folgenden Befehl den Inhalt der JSON-Datei an den Endpunkt des Benutzers:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<eigener Host>.ibm.com/codi/v1/users
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
<dd class="pd">Gibt die Daten an (in diesem Beispiel die Datei `user.json`), die in der POST-Anforderung an den HTTP-Server gesendet werden sollen.</dd>
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

Sie können die REST-API `Admin` verwenden, um Benutzer aus der {{site.data.keyword.Bluemix_notm}}-Instanz zu entfernen. Zum Entfernen von Benutzern müssen Sie die Berechtigung **Users** mit dem Zugriff **Schreiben** besitzen.

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

## API für Metriken (experimentell)
{: #envappmetricsapi}

Zur Erfassung von Metriken über Ihre Umgebung oder Anwendungen können Sie drei experimentelle APIs verwenden. Diese APIs geben ein Array von Datenpunkten für die angeforderten Metriken und den von Ihnen angegebenen Zeitraum zurück.

Auf die in den folgenden Abschnitten beschriebenen Metrik-APIs kann über den regionsspezifischen Endpunkt zugegriffen werden. Beispiel: 

`https://console.<region>.bluemix.net/admin/metrics`
{: codeblock}

**Hinweise**:

1. Ein Benutzer kann pro Stunde bis zu 200 API-Anforderungen für Metriken absetzen.
2. Jede API-Anforderung gibt bis zu 200 Datenpunkte pro Anforderung zurück. Falls mehr Daten verfügbar sind, wird in der Antwort eine URL bereitgestellt, mit deren Hilfe die nächste Gruppe von Daten geladen werden kann.
3. Jede API-Anforderung erfordert mindestens Basiszugriff eines Benutzers auf die Administrationskonsole.  Weitere Berechtigungen können wie nachfolgend beschrieben erforderlich sein.

## Metriken über Ihre Umgebung erfassen 

Mit der experimentellen Umgebungs-API können Sie allgemeine Information zur Umgebung für einen von Ihnen angegebenen Zeitraum erfassen. Zurückgegeben werden die verfügbaren Datenpunkte im angegebenen Zeitraum. Daten werden ungefähr ein Mal pro Stunde aufgezeichnet. Falls Sie beispielsweise sechs Stunden von CPU-Daten für die Umgebung angefordert haben, würde die Antwort CPU-Daten für jede der angeforderten sechs Stunden enthalten.


### Umgebungsendpunkte 

Zum Aufrufen dieses API-Befehls können Sie den folgenden Endpunkt verwenden: `/api/v1/env`

**Hinweis:**  Eine der folgenden Berechtigungen ist für den Zugriff auf diese Endpunkte erforderlich: **Basiszugriff**, **Benutzerlesezugriff**, **Benutzerschreibzugriff** oder **Superuser**.

### Abfrageparameter für Umgebungsmetriken

Mit den folgenden Abfrageparametern können Sie Metriken für die CPU, die Platte, den Hauptspeicher, das Netz, das Kontingent und die Apps erfassen:

<dl class="parml">
<dt class="pt dlterm">metric</dt>
<dd class="pd">Einer oder mehrere der folgenden Werte, durch Kommas getrennt: `memory`, `disk`, `cpu`, `network`, `quota` und `apps`.</dd>
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Der früheste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'startTime' nicht angegeben ist, wird der früheste verfügbare Datenpunkt einbezogen. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Startzeit 14.00 Uhr an.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Der späteste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'endTime' nicht angegeben ist, wird der neueste Datenpunkt verwendet. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Endzeit 17.00 Uhr an.</dd>
<dt class="pt dlterm">sort</dt>
<dd class="pd">Die Reihenfolge, in der die Daten zurückgegeben werden. Gültige Werte sind: `asc` (aufsteigend) und `desc` (absteigend). Standardeinstellung ist die absteigende Reihenfolge; hierbei werden zuerst die neuesten Daten zurückgegeben. </dd>
</dl>

Im folgenden Beispiel werden die Abfrageparameter zum Erfassen von Metriken für die Umgebung verwendet:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<Region>.bluemix.net/admin/metrics/api/v1/env?metric=cpu,network,disk,apps,memory
```
{: codeblock}


### Datenformat für Umgebungsmetriken

Das Datenformat ist in den folgenden Abschnitten erläutert.

 * Um Datensätze über die Hauptspeicherbelegung zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "memory": {
    "total": {
      "physical": {
        "total_gb": 1728,
        "used": {
          "value_gb": 673.68,
          "percent": 38.99
        }
      },
    "allocated": {
        "reserved_gb": 3456,
        "total_allocated": {
          "value_gb": 2575.18,
          "percent": 74.51
        }
      },
    },
  	"cell": {
      "physical": {
        "total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "dea": {
      "physical": {
      	"total_gb": 864,
      "used": {
          "value_gb": 336.84,
        "percent": 38.99
      }
      },
    "allocated": {
        "reserved_gb": 1728,
      "total_allocated": {
          "value_gb": 1287.59,
        "percent": 74.51
      }
      },
    },
    "memory_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "47"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "51"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "45"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "43"
      }
    ]
  }
}
```
{: screen}

 * Um Datensätze über die Plattenbelegung zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "disk": {
    "total": {
      "physical": {
        "total_gb": 16200,
        "used": {
          "value_gb": 1614,
          "percent": 9.96
        }
      },
    "allocated": {
        "reserved_gb": 32400,
        "total_allocated": {
          "value_gb": 3979,
          "percent": 12.28
        }
      },
    },
    "cell": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "dea": {
      "physical": {
        "total_gb": 8100,
      "used": {
          "value_gb": 807,
        "percent": 9.96
      }
      },
    "allocated": {
        "reserved_gb": 16200,
      "total_allocated": {
          "value_gb": 1989.5,
        "percent": 12.28
      }
      },
    },
    "disk_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "percent": "13"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "percent": "14"
      },
      {
        "name": "dea_next/2",
        "type": "dea",
        "ip": "169.53.230.49",
        "percent": "13"
      },
      {
        "name": "dea_next/3",
        "type": "dea",
        "ip": "169.44.109.231",
        "percent": "12"
      }
    ]
  }
}
```
{: screen}

 * Um Datensätze über die CPU-Auslastung zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "cpu": {
    "total": {
      "average_percent_cpu_used": 14.725
    },
    "cell": {
      "average_percent_cpu_used": 19
    },
    "dea": {
      "average_percent_cpu_used": 10.45
    },
    "cpu_by_container": [
      {
        "name": "dea_next/0",
        "type": "dea",
        "ip": "169.53.225.93",
        "sys_percent": "8.4",
        "user_percent": "2.7",
        "wait_percent": "0.0"
      },
      {
        "name": "dea_next/1",
        "type": "dea",
        "ip": "169.53.225.89",
        "sys_percent": "7.4",
        "user_percent": "2.4",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/1",
        "type": "cell",
        "ip": "169.53.230.49",
        "sys_percent": "5.3",
        "user_percent": "1.9",
        "wait_percent": "0.0"
      },
      {
        "name": "cell/2",
        "type": "cell",
        "ip": "169.44.109.231",
        "sys_percent": "8.2",
        "user_percent": "22.6",
        "wait_percent": "0.0"
      }
    ]
  }
}
```
{: screen}

 * Um Datensätze über das Netz zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "network": {
    "datapower": {
    "response_times": [
      {
        "proxy": "custom_certificates",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "90",
        "one_minute_ms": "89",
        "ten_minutes_ms": "83",
        "one_hour_ms": "85",
        "one_day_ms": "95"
      }
      ],
        "transactions": [
      {
        "proxy": "custom_domains",
        "ten_seconds_ms": "0",
        "one_minute_ms": "0",
        "ten_minutes_ms": "0",
        "one_hour_ms": "0",
        "one_day_ms": "0"
      },
      {
        "proxy": "bluemix",
        "ten_seconds_ms": "697",
        "one_minute_ms": "747",
        "ten_minutes_ms": "802",
        "one_hour_ms": "794",
        "one_day_ms": "730"
      }
      ],
        "bandwidth": {
        "in_kbps": 10855,
        "out_kbps": 38090
      }
  }
}
```
{: screen}

* Um Datensätze über die Kontingentnutzung zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "quota": {
    "reserved_memory": {
      "total_bytes": 33176474877952
    },
    "services": {
      "total": 111650
    },
    "routes": {
      "total": 1675000
    }
  }
}
```
{: screen}

* Um Datensätze über Ihre Anwendungen zu erfassen, verwenden Sie das folgende Datenformat:
 
```
{
  "sample_time": 1477494000000,
  "apps": {
    "count": 1406,
    "allocation": {
      "memory_gb": 571.8,
      "disk_gb": 1204
    }
  }
}
```
{: screen}

### Antwortformat für Umgebungsmetriken

```
{
   docs: [],
   next_url:
}
```
{: screen}

## Metriken über Ihre Organisationen

Für alle Organisationen werden ungefähr ein Mal pro Stunde Daten aufgezeichnet. Eine Anforderung für eine bestimmte Metrik gibt Informationen zu allen Organisationen in jeder Datenstichprobe für den von Ihnen angeforderten Zeitraum zurück, die gemäß der angeforderten Metrik in absteigender Reihenfolge sortiert sind. Wenn Sie beispielsweise alle Organisationen nach Hauptspeicher für einen sechsstündigen Zeitraum in einer Umgebung anfordern, die 200 Apps enthält, werden 1200 Datensätze (jeweils 200 für jede Stunde) zurückgegeben.

Um die Menge der Informationen zu verringern, die für jede Datenstichprobe im angeforderten Zeitraum zurückgegeben werden, können Sie eine Option für die Anzahl angeben. Wenn Sie beim vorherigen Beispiel eine Option für die Anzahl mit dem Wert 5 hinzufügen, werden 30 Datensätze zurückgegeben, die für jede Datenstichprobe die 5 Organisationen mit der höchsten Hauptspeichernutzung darstellen.

### Organisationsendpunkte 

Zum Aufrufen dieses API-Befehls können Sie die folgenden Endpunkte verwenden:
* `/api/v1/org/memory/physical`
* `/api/v1/org/memory/reserved`
* `/api/v1/org/disk/physical`
* `/api/v1/org/disk/reserved`

**Hinweis:** Eine der folgenden Berechtigungen ist für den Zugriff auf diese Endpunkte erforderlich: **Benutzerlesezugriff**, **Benutzerschreibzugriff** oder **Superuser**.

### Abfrageparameter für Organisationen
 
Mit den folgenden Abfrageparametern können Sie Metriken für Ihre Organisationen erfassen:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Der früheste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'startTime' nicht angegeben ist, wird der früheste verfügbare Datenpunkt einbezogen. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Startzeit 14.00 Uhr an.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Der späteste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'endTime' nicht angegeben ist, wird der neueste Datenpunkt verwendet. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Endzeit 17.00 Uhr an.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">Die Anzahl der Datensätze in jeder Datenstichprobe, die zurückgegeben werden sollen.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Der kleinste Wert, der für die angegebene Metrik zurückgegeben werden soll.  Wenn minValue nicht angegeben wird, werden alle Werte zurückgegeben.  Beispiel: Zum Erfassen von Organisationen, die mindestens 20000 Byte physischen Speicher belegen, geben Sie für minValue den Wert 20000 an.
</dd>
</dl>

Mit dem folgenden Beispiel werden Metriken zu Ihren Organisationen erfasst:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<region>.bluemix.net/admin/metrics/api/v1/org/memory/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}

### Antwortformat für Organisationen

```
{
   docs: [],
   next_url:
}
```
{: screen}

Jedes zurückgegebene Dokument stellt die angeforderten Metriken für eine Organisation in jeder Datenstichprobe zum Zeitpunkt der Anforderung dar.

## Metriken über Ihre Anwendungen erfassen

Für alle Anwendungen werden ungefähr ein Mal pro Stunde Daten aufgezeichnet. Eine Anforderung für eine bestimmte Metrik gibt Informationen zu allen Apps in jeder Datenstichprobe für den von Ihnen angeforderten Zeitraum zurück, die gemäß der angeforderten Metrik in absteigender Reihenfolge sortiert sind. Wenn Sie beispielsweise alle Apps nach CPU für einen sechsstündigen Zeitraum in einer Umgebung anfordern, die 200 Apps enthält, werden 1200 Datensätze (jeweils 200 für jede Stunde) zurückgegeben.

Um die Menge der Informationen zu verringern, die für jede Datenstichprobe im angeforderten Zeitraum zurückgegeben werden, können Sie eine Option für die Anzahl angeben. Wenn Sie beim vorherigen Beispiel eine Option für die Anzahl mit dem Wert 5 hinzufügen, werden 30 Datensätze zurückgegeben, die für jede Datenstichprobe die 5 Anwendungen mit der höchsten CPU-Auslastung darstellen.

### Anwendungsendpunkte 

Zum Aufrufen dieses API-Befehls können Sie die folgenden Endpunkte verwenden:
* `/api/v1/app/cpu/physical` 
* `/api/v1/app/memory/physical`
* `/api/v1/app/memory/reserved`
* `/api/v1/app/disk/physical`
* `/api/v1/app/disk/reserved`

**Hinweis:** Eine der folgenden Berechtigungen ist für den Zugriff auf diese Endpunkte erforderlich: **Benutzerlesezugriff**, **Benutzerschreibzugriff** oder **Superuser**.

### Abfrageparameter für Anwendungen
 
Mit den folgenden Abfrageparametern können Sie Metriken für Ihre Anwendungen erfassen:

<dl class="parml">
<dt class="pt dlterm">startTime</dt>
<dd class="pd">Der früheste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'startTime' nicht angegeben ist, wird der früheste verfügbare Datenpunkt einbezogen. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Startzeit 14.00 Uhr an.</dd>
<dt class="pt dlterm">endTime</dt>
<dd class="pd">Der späteste Zeitpunkt, für den Daten zurückgegeben werden. Falls der Parameter 'endTime' nicht angegeben ist, wird der neueste Datenpunkt verwendet. Um beispielsweise Daten für den Zeitraum zwischen 14.00 und 17.00 Uhr zu erfassen, geben Sie als Endzeit 17.00 Uhr an.</dd>
<dt class="pt dlterm">count</dt>
<dd class="pd">Die Anzahl der Datensätze in jeder Datenstichprobe, die zurückgegeben werden sollen.
</dd>
<dt class="pt dlterm">minValue</dt>
<dd class="pd">Der kleinste Wert, der für die angegebene Metrik zurückgegeben werden soll. Wenn minValue nicht angegeben wird, werden alle Werte zurückgegeben. Beispiel: Zum Erfassen von Anwendungen, die mindestens 20000 Byte physischen Speicher belegen, geben Sie für minValue den Wert 20000 an.
</dd>
</dl>

Mit dem folgenden Beispiel werden Metriken zu Ihren Anwendungen erfasst:

```
curl -b ./cookies.txt --header "Accept: application/json" https://console.<Region>.bluemix.net/admin/metrics/api/v1/app/cpu/physical?count=5&startTime=2016-12-02T16:54:09.467Z
```
{: codeblock}


### Antwortformat für Anwendungen

```
{
   docs: [],
   next_url:
}
```
{: screen}

Jedes zurückgegebene Dokument stellt die angeforderten Metriken für eine Anwendung in jeder Datenstichprobe zum Zeitpunkt der Anforderung dar.


## API für angepasste Services
{: #servicebrokerapi}

Es gibt drei APIs, die Sie jeweils zum Registrieren oder Erstellen, zum Aktualisieren und zum Löschen eines Service verwenden können.

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

{: #ld_table15}

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |
{: caption="Tabelle 15. Felder" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
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

{: #ld_table16}

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |
{: caption="Tabelle 16. Anforderungen" caption-side="top"}

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
    "_id": "2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "proxy_broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-0ca80769-8e9e-4e1c-9b99-68bdcf1a2c68",
    "auth_username": "username",
    "created_on": "2016-09-30T16:45:56.304Z"
}
```
{: screen}

## Service löschen

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Löschen eines Service.


{: #ld_table17}

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |
{: caption="Tabelle 17. Parameter" caption-side="top"}

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

### Benutzer mit der Befehlszeilenschnittstelle 'cf' verwalten
{: #usingadmincli}

Sie können Benutzer für Ihre {{site.data.keyword.Bluemix_notm}}-Umgebung über die Cloud Foundry-Befehlszeilenschnittstelle mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwalten. Sie müssen dieses Plug-in für Ihre Cloud Foundry-CLI herunterladen.

Vor dem Beginn müssen Sie die Befehlszeilenschnittstelle 'cf' installieren. Für das {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in ist cf Version 6.11.2 oder höher erforderlich. [Laden Sie die Cloud Foundry-Befehlszeilenschnittstelle herunter. ![Symbol für externen Link](../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window}

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet.

#### {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in hinzufügen

Nach der Installation der Befehlszeilenschnittstelle 'cf' können Sie das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
hinzufügen.

**Hinweis:** Wenn Sie das {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in zuvor installiert haben, müssen Sie das Plug-in möglicherweise deinstallieren, das Repository löschen und anschließend das Plug-in erneut installieren, um die neuesten Aktualisierungen zu erhalten.

Führen Sie die folgenden Schritte aus, um das Repository hinzuzufügen und das Plug-in zu installieren:

<ol>
<li>Führen Sie den folgenden Befehl aus, um das Repository für das {{site.data.keyword.Bluemix_notm}}-Admin-Plug-in hinzuzufügen:<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Die Unterdomäne der URL für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz.</dd>
</dl>
</li>
<li>Führen Sie den folgenden Befehl aus, um das Plug-in für die {{site.data.keyword.Bluemix_notm}}-Administrator-CLI zu installieren:<br/><br/>
<code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Führen Sie den folgenden Befehl aus, um eine Liste der Unterbefehle anzuzeigen, die durch die installierten Plug-ins verfügbar sind:

```
cf plugins
```
{: codeblock}

Führen Sie den folgenden Befehl aus, um eine Liste der verfügbaren Befehlsgruppen für das {{site.data.keyword.Bluemix_notm}}-Admin-Plug-in anzuzeigen:

```
cf ba
```
{: codeblock}

Wenn Sie weitere Hilfe zu einem Befehl benötigen, verwenden Sie die Option `-help`.

Weitere Informationen zur Arbeit mit dem {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in finden Sie unter [{{site.data.keyword.Bluemix_notm}}-Admin](../cli/plugins/bluemix_admin/index.html).
