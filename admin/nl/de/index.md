{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

#{{site.data.keyword.Bluemix_notm}} verwalten
{: #administer}
*Letzte Aktualisierung: 20. Januar 2016*

Verwalten Sie Organisationen, Bereiche und zugeordnete Benutzer, indem Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) klicken und anschließend die Option **Organisationen verwalten** auswählen. Wenn Sie ein Benutzer von {{site.data.keyword.Bluemix_notm}} Local oder {{site.data.keyword.Bluemix_notm}} Dedicated sind, finden Sie unter [{{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten](index.html#mng) weitere Informationen zur Verwaltung einer lokalen oder dedizierten Instanz.
{:shortdesc}

##Konto verwalten
{: #mngacct}

In der öffentlichen {{site.data.keyword.Bluemix}}-Umgebung (Public) können Sie Organisationen und Bereiche, einschließlich des Benutzerzugriffs, über das Dashboard in der Benutzerschnittstelle verwalten. Sie können darüber hinaus Ihre Nutzung und Abrechnung überwachen.
{:shortdesc}

###Organisationen und Bereiche
{: #orgsandspaces}

Als Organisationsmanager können Sie die Einstellungen der Organisation oder des Bereichs, einschließlich des Benutzerzugriffs, auf der Seite 'Organisationen verwalten' anzeigen und verwalten. Zum Öffnen der Seite 'Organisationen verwalten' klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen **Organisationen verwalten** aus.

####Organisationen

Eine Organisation wird durch die folgenden Elemente definiert:

<dl>
<dt>Benutzer</dt>
<dd>Die Rolle mit Basisberechtigungen in Organisationen und Bereichen. Sie müssen einer Organisation zugewiesen sein, bevor Ihnen weitere Berechtigungen für Bereiche innerhalb der Organisation erteilt werden können. Detaillierte Informationen hierzu finden Sie unter [Benutzer und Rollen](index.html#userroles).</dd>
<dt>Domänen</dt>
<dd>Stellen die Route im Internet bereit, die der Organisation zugeordnet ist. Eine Route hat eine Unterdomäne und eine Domäne. Eine Unterdomäne ist in der Regel der Anwendungsname. Eine Domäne kann eine Systemdomäne oder eine angepasste Domäne sein, die Sie für Ihre Anwendung registriert haben.<br/>
<p>**Hinweis**: Wenn Sie eine angepasste Domäne hinzufügen, müssen Sie Ihren DNS-Server so konfigurieren, dass er Ihre angepasste Domäne in einen Verweis auf die {{site.data.keyword.Bluemix_notm}}-Systemdomäne auflöst. Auf diese Weise kann {{site.data.keyword.Bluemix_notm}} eine aus Ihrer angepassten Domäne empfangene Anforderung ordnungsgemäß an Ihre Anwendung weiterleiten.</p></dd>
<dt>Kontingent</dt>
<dd>Stellt die Ressourcengrenzwerte für die Organisation dar, einschließlich der Anzahl der Services und die Speicherkapazität, die für die Verwendung durch Ihre Organisation zugeordnet werden können. Kontingente werden bei der Erstellung von Organisationen zugeordnet. Jede Anwendung und jeder Service in einem Bereich der Organisation trägt zur Nutzung des Kontingents bei. Sowohl mit dem nutzungsabhängigen Plan als auch dem Abonnementplan können Sie Ihr Kontingent für Cloud Foundry-Anwendungen und -Container anpassen, sobald sich die Bedürfnisse für Ihre Organisation ändern.</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}} können Sie Organisation auf folgende Arten dazu verwenden, die Zusammenarbeit unter Benutzern zu ermöglichen und eine logische Gruppierung von Projektressourcen einzurichten:

<ul>
<li>Sie können eine Reihe von Bereichen, Anwendungen, Services, Domänen, Routen und Benutzern in Organisationen zusammen gruppieren.</li>
<li>Sie können den Zugriff auf die Bereiche und Organisationen auf Benutzerbasis verwalten.</li>
</ul>

Wenn Sie eine Organisation erstellen, muss der Organisationsname in {{site.data.keyword.Bluemix_notm}} eindeutig sein. Wenn Sie die Organisation erstellt haben, wird Ihnen automatisch die Berechtigung einer *Organisationsmanagers* zugewiesen, mit der Sie den Organisationsnamen bearbeiten, die Organisation löschen und Bereiche in der Organisation erstellen können.

Wenn Sie eine Organisation löschen, werden alle Bereiche, Anwendungen und Services in der Organisation gelöscht.

{{site.data.keyword.Bluemix_notm}} ermöglicht die Zusammenarbeit an Projekten durch das Zuordnen von Benutzern innerhalb einer Organisation und innerhalb der Bereiche der Organisation. Auf der Registerkarte **Benutzer** können Sie Benutzer der Organisation anzeigen und verwalten. Darüber hinaus können Sie Benutzer in Ihre Organisation einladen, indem Sie auf den Link **Neuen Benutzer einladen** auf der Registerkarte **Benutzer** klicken. Benutzern in der Organisation können die folgenden Berechtigungen zugeordnet werden:

<ul>
<li>Organisationsbenutzer</li>
<li>Organisationsmanager</li>
<li>Abrechnungsmanager der Organisation</li>
<li>Organisationsauditor</li>
</ul>

####Bereiche

Innerhalb einer Organisation können Sie Bereiche verwenden, um eine Reihe von Anwendungen, Services und Benutzern zusammen zu gruppieren.

Wenn Sie einer Organisation Benutzer hinzugefügt haben, können Sie ihnen Berechtigungen für Bereiche innerhalb der Organisation erteilen. Ähnlich wie Organisationen haben auch Bereiche eine Reihe von Berechtigungen, die Benutzern zugeordnet werden können:

<ul>
<li>Bereichsmanager</li>
<li>Bereichsentwickler</li>
<li>Bereichsauditor</li>
</ul>

**Hinweis**: Einem Benutzer muss mindestens eine der Berechtigungen im Bereich zugeordnet werden.

Die Registerkarte **Domänen** für einen Bereich enthält eine schreibgeschützte Liste der Domänen, die dem Bereich zugeordnet sind. Die Systemdomäne ist für einen Bereich immer verfügbar. Außerdem können dem Bereich angepasste Domänen zugeordnet werden. Anwendungen, die in dem Bereich erstellt wurden, können eine beliebige der für den Bereich aufgelisteten Domänen verwenden.

###Benutzer und Rollen
{: #userroles}

Kontoeigner führen alle Operationen an Organisationen und Bereichen aus.

####Benutzertypen

Sie können entweder ein Mitglied oder ein Collaborator eines Kontos sein.

<dl>
<dt>Mitglied</dt>
<dd>Sie sind ein Mitglied eines {{site.data.keyword.Bluemix_notm}}-Kontos, wenn Sie das Konto erstellt haben oder wenn Sie als Einstieg in {{site.data.keyword.Bluemix_notm}} zu dem Konto eingeladen wurden und sich dann auf der Basis der Einladung angemeldet haben. </dd>
<dt>Collaborator</dt>
<dd>Sie sind ein Collaborator eines {{site.data.keyword.Bluemix_notm}}-Kontos, wenn Sie {{site.data.keyword.Bluemix_notm}} zuvor mit einem anderen Konto verwendet haben, dann jedoch zu diesem Konto eingeladen wurden und die Einladung akzeptiert haben.</dd>
</dl>

####Benutzerrollen

Benutzern können die folgenden Berechtigungen für verschiedene Benutzerrollen in einer Organisation oder einem Bereich zugewiesen werden:

<dl>
<dt>Organisationsmanager</dt>
<dd>Organisationsmanager verfügen über die folgenden Berechtigungen:
<ul>
<li>Erstellen oder Löschen von Bereichen innerhalb der Organisation.</li>
<li>Laden Sie Benutzer zur Organisation ein, falls Sie selbst ein Mitglied der Organisation oder der Kontoeigner sind.</li>
<li>Verwalten Sie vorhandene Benutzer, die bereits Mitglieder der Organisation sind.</li>
<li>Verwalten von Domänen der Organisation.</li>
</ul>
<p>**Hinweis**: Wenn Ihnen der Benutzertyp 'Collaborator' zugewiesen ist und Sie {{site.data.keyword.Bluemix_notm}} zuvor mit einem anderen Konto verwendet haben, können Sie keine Benutzer zur Organisation einladen, selbst wenn Ihnen die Organisationsmanagerrolle zugewiesen wird. Zum Einladen von Benutzern müssen Sie über den Benutzertyp 'Mitglied' verfügen. Weitere Informationen zur Umgehung dieses Problems finden Sie unter <a href="../troubleshoot/index.html#ts_adduser">Hinzufügen von Benutzern zu Organisation nicht möglich</a>.</p>
</dd>
<dt>Abrechnungsmanager</dt>
<dd>Fakturierungsmanager sind berechtigt, Informationen zur Laufzeit- und Servicenutzung für die Organisation anzuzeigen.</dd>
<dt>Organisationsauditoren</dt>
<dd>Organisationsauditoren sind berechtigt, Anwendungs- und Serviceinhalt in dem Bereich anzuzeigen.</dd>
<dt>Bereichsmanager</dt>
<dd>Bereichsmanager verfügen über die folgenden Berechtigungen:
<ul>
<li>Fügen dem Bereich Benutzer hinzu und verwalten Benutzer. </li>
<li>Aktivieren Features (Funktionen) für den Bereich.</li>
</ul>
</dd>
<dt>Bereichsentwickler</dt>
<dd>Bereichsentwickler verfügen über die folgenden Berechtigungen:
<ul>
<li>Erstellen, löschen und verwalten Anwendungen und Services innerhalb des Bereichs.</li>
<li>Haben Zugriff auf Protokolle im Bereich.</li>
</ul>
</dd>
<dt>Bereichsauditoren</dt>
<dd>Bereichsauditoren verfügen über Berechtigungen für den Lesezugriff auf alle Informationen über den Bereich, wie zum Beispiel auf Informationen zu Anwendungen und Services sowie auf Einstellungen, Berichte und Protokolle.</dd>
</dl>

###Organisation verwalten
{: #orgmng}

Als Organisationsmanager oder Kontoeigner können Sie Ihre Organisationen verwalten. Management-Tasks beinhalten die Erstellung einer Organisation, die Umbenennung einer Organisation, die Erstellung eines Bereichs, die Einladung von Benutzen in einen Bereich, die Änderung von Benutzerrollen sowie das Löschen einer vorhandenen Organisation.

<ul>
<li>Eine Organisation erstellen
<p>Es können nur Benutzer mit einem Zahlungskonto eine Organisation erstellen. Mit einem Zahlungskonto können Sie durch Ausführen der folgenden Schritte eine Organisation erstellen:</p>
<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Klicken Sie auf **Organisation erstellen** und befolgen Sie die Eingabeaufforderungen, um Ihre Organisation zu erstellen.</li>
</ol>
</li>
<li>Eine Organisation umbenennen
<p>Führen Sie die folgenden Schritte aus, um Ihre Organisation umzubenennen:</p>
<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Wählen Sie die Organisation aus, die Sie umbenennen möchten.</li>
<li>Geben Sie im Feld **Organisation** einen neuen Namen ein und klicken Sie auf **Speichern**.</li>
</ol>
</li>
<li>Mitglieder auflisten
<p>Führen Sie die folgenden Schritte aus, um die Mitglieder Ihrer Organisation oder Ihres Bereichs aufzulisten:</p>
<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus. Auf der Registerkarte **Benutzer** werden die Mitglieder Ihrer Organisation und ihre Rollen angezeigt.</li>
<li>Klicken Sie auf den Bereichsnamen in Ihrer Organisation, um die Mitglieder dieses Bereichs und deren Rollen anzuzeigen.</li>
</ol>
</li>
<li>Einen Bereich erstellen
<p>Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen:</p>
<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Klicken Sie auf **Bereich erstellen** hinter Ihrem Organisationsnamen und befolgen Sie die Eingabeaufforderungen, um Ihren Bereich zu erstellen.</li>
</ol>
</li>
<li>Benutzer in einen Bereich einladen
<p>Sie können Benutzer in Ihre Organisation als Teilnehmer einladen. Sie können außerdem Benutzer Ihrer Organisation zu verschiedenen Bereichen hinzufügen. Die Benutzer können nur auf den Bereich zugreifen, zu dem sie hinzugefügt wurden. Führen Sie die folgenden Schritte aus, um einen Benutzer zu einem Bereich hinzuzufügen:</p>
<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus. Klicken Sie anschließend auf **Benutzer hinzufügen** in Ihrer Organisation und befolgen Sie die Eingabeaufforderungen, um den Benutzer zu Ihrer Organisation hinzuzufügen.</li>
<li>Fügen Sie den Benutzer zu einem Bereich hinzu. Wählen Sie den Bereich im Navigationsfenster aus, klicken Sie auf **Benutzer hinzufügen** und befolgen Sie die Eingabeaufforderungen, um den Benutzer zu dem Bereich hinzuzufügen.</li>
</ol>
</li>
<li>Benutzerrollen ändern
<p>Führen Sie die folgenden Schritte aus, um Benutzerrollen zu ändern:</p>
<ol>
<li>Klicken Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Wählen Sie das Kontrollkästchen **Manager**, **Abrechnungsmanager** oder **Auditor** auf der Registerkarte **Benutzer** aus, um Rollen von Benutzern in Ihrer Organisation zu ändern. Oder wählen Sie einen Bereich im Navigationsbereich und anschließend das Kontrollkästchen **Manager**, **Entwickler** oder **Auditor** auf der Registerkarte **Benutzer** aus, um Rollen von Benutzern in dem Bereich zu ändern.</li>
<li>Klicken Sie auf **Speichern**.</li>
</ol>
</li>
<li>Eine vorhandenen Organisation löschen
<p>Wenn Sie Ihre Organisation löschen möchten, wenden Sie sich an die Unterstützung für {{site.data.keyword.Bluemix_notm}}-Registrierungen und -IDs.</p>
<p>**Hinweis**: Das Löschen von Operationen kann nicht rückgängig gemacht werden. Alle der Organisation zugeordneten Anwendungen und Services gehen verloren.</p>
</li>
</ul>

## {{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten
{: #mng}

Wenn Sie über Administratorzugriff für {{site.data.keyword.Bluemix_notm}} Local oder {{site.data.keyword.Bluemix_notm}} Dedicated verfügen, können Sie über die Verwaltungsseite (**Administration**) Ressourcen verwalten, die Kontingentnutzung überwachen, Benutzerberechtigungen verwalten, Upgradebenachrichtigungen planen, Sicherheitsberichte und Protokolle anzeigen und vieles mehr. Sie können Ihre Organisationen verwalten, indem Sie Bereiche erstellen und Benutzerrollen und Berechtigungen festlegen. Weitere Informationen finden Sie unter [Organisation verwalten](index.html#orgmng).
{:shortdesc}

*Tabelle 1. Verwaltungstasks zur Verwaltung einer {{site.data.keyword.Bluemix_notm}} Local- oder Dedicated-Instanz*

| Verwaltungstask | Details |    
|----------------|---------|
|Systemnutzung überwachen | Klicken Sie auf **ADMINISTRATION &gt; USAGE**. Zeigen Sie Systeminformationen an, überwachen Sie die CPU-Nutzung und planen Sie die Nutzung, um die besten Entscheidungen für Ihr Unternehmen zu treffen.|
|Eigenen Katalog verwalten | Klicken Sie auf **ADMINISTRATION &gt; CATALOG MANAGEMENT**. Legen Sie fest, welche Services für Ihre Benutzer sichtbar sind.|
|Organisationen verwalten | Klicken Sie auf **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**. Erstellen Sie Organisationen, überwachen Sie Kontigente für Organisationen und treffen Sie rasch bedarfsorientierte Entscheidungen.|
|Bereiche erstellen und Benutzerrollen zuweisen | Klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und anschließend auf **Organisationen verwalten**. Erstellen Sie Bereiche in Ihren Organisationen. Fügen Sie Benutzer hinzu und weisen Sie Benutzern Organisations- und Bereichsrollen zu. |
|Administratorberechtigungen verwalten | Klicken Sie auf **ADMINISTRATION &gt; USER ADMINISTRATION**. Fügen Sie Benutzer hinzu, entfernen Sie Benutzer und passen Sie Benutzerberechtigungen an. |
|Berichte und Protokolle prüfen | Klicken Sie auf **ADMINISTRATION &gt; REPORTS AND LOGS**. Zeigen Sie Sicherheitsberichte und Prüfprotokolle für Ihre Instanz an.|
|Systeminformationen anzeigen | Klicken Sie auf **ADMINISTRATION &gt; SYSTEM INFORMATION**. Zeigen Sie Systeminformationen an. Beispiele: anstehende Aktualisierungen, Name und Version Ihrer Instanz, Region, API-URL, CLI-URL, LDAP-Konfigurationsdetails, Gruppen- und Benutzerzuordnungen, Statistiken und gemeinsam genutzte Domänen.  |

### Systeminformationen anzeigen
{: #oc_system}

Klicken Sie zum Anzeigen von Systeminformationen auf **ADMINISTRATION &gt; SYSTEM INFORMATION**.

Sie können verschiedene Bereiche zu anstehenden Aktualisierungen, allgemeinen Systeminformationen und LDAP-Konfigurationsdetails erweitern und anzeigen.

* Im Bereich für die Aktualisierungen werden alle anstehenden Aktualisierungen angezeigt, für die Sie eine Aktion durchführen müssen. Sie können die Aktualisierungen auch leicht über den Kalender-Link überwachen, um geplante Aktualisierungen in eine Kalender-App zu importieren.

<ol>
<li>Um für eine bestimmte Aktualisierung eine Aktion auszuführen, führen Sie die folgenden Schritte durch:
<ol type="a">
<li>Klicken Sie auf die Anzahl der anstehenden Aktualisierungen, um alle anstehenden Aktualisierungen anzuzeigen.</li>
<li>Wählen Sie eine Aktualisierung aus, für die eine Aktion ausgeführt werden soll, oder zeigen Sie die Details zu dieser Aktualisierung an, darunter das Aktualisierungsfenster, das geplante Datum oder den Unterbrechungsstatus.</li>
<li>Klicken Sie auf die Option zum Festlegen nicht verfügbarer Daten, um im Aktualisierungsfenster bestimmte Tage anzugeben, an denen die Aktualisierung nicht angewendet werden sollte. Wenn Sie solche Daten angeben, genehmigt und plant IBM die Aktualisierung basierend auf Ihrer Auswahl. Sie erhalten eine Benachrichtigung, wenn die Aktualisierung genehmigt und geplant wurde.</li>
<li>Wenn Sie keine Datumseinschränkungen haben, klicken Sie auf die Schaltfläche zum Genehmigen, um die Aktualisierung zu genehmigen. Wenn Sie die Aktualisierung genehmigen, wird die Aktualisierung im geplanten Aktualisierungsfenster angewendet. IBM sendet eine Benachrichtigung, wenn die Bereitstellung der Aktualisierung startet und endet.</li>
</ol>
</li>
<li>Um die geplanten Aktualisierungen in eine Kalender-App Ihrer Wahl zu importieren, führen Sie die folgenden Schritte aus:
<ol type="a">
<li>Öffnen Sie die Kalender-App.</li>
<li>Importieren Sie den Kalender für die Aktualisierungen, indem Sie die auf der Seite mit den Systeminformationen aufgeführte Kalender-URL in Ihre App importieren. Alternativ laden Sie die Kalenderdatei herunter, indem Sie auf die Kalender-URL klicken und diese dann mithilfe der `ICS`-Datei in die Kalender-App importieren.</li>
<li>Geben Sie Ihre Berechtigungsnachweise ein.</li>
<li>Zeigen Sie die geplanten Aktualisierungen an.</li>
</ol>
</li>
</ol>

* Der Bereich für allgemeine Informationen enthält die folgenden Angaben:
    * Basisinformationen zum {{site.data.keyword.Bluemix_notm}}-Build
    * API-Informationen wie Version, URL und Region sowie einen Link zur CLI-Dokumentation
    * Informationen der gemeinsamen Domäne zu Ihrem System und Service
    * Statistiken zur Gesamtzahl der Anwendungen, Benutzer und Organisationen
* Im Bereich für die LDAP-Konfigurationsdetails können Sie den LDAP-Server
auswählen und Informationen zu Benutzer- und Gruppenzuordnungen anzeigen. Wenn Sie
{{site.data.keyword.IBM}} WebID verwenden, wird dies im Bereich für die
LDAP-Konfigurationsdetails angezeigt.

### Nutzungsinformationen anzeigen
{: #oc_resource}

Klicken Sie zum Anzeigen von Ressourceninformationen auf **ADMINISTRATION &gt; USAGE**.

Im Bereich für die Ressourcenüberwachung können Sie die folgenden Informationen anzeigen:

* Informationen zur Ressourcennutzung, z. B. der Umfang des belegten Hauptspeichers und
Plattenspeicherplatzes in GB. Sie können die durchschnittliche CPU-Auslastung für alle
DEA (Droplet Execution Agent) anzeigen. Klicken Sie auf die Kachel **CPU**, um die CPU-Auslastung für die
einzelnen DEA anzuzeigen. Der DEA mit dem höchsten Wert für die Auslastung
steht an erster Stelle und jeder einzelne DEA wird durch den zugehörigen Job und die IP-Adresse näher
spezifiziert. Die CPU-Auslastung ist in drei Kategorien unterteilt: der für Systemprozesse
aufgewendete Umfang der CPU-Auslastung, der für Benutzerprozesse
aufgewendete Umfang der CPU-Auslastung und der für Prozesse mit Wartestatus
aufgewendete Umfang der CPU-Auslastung.
* Informationen zur Netzauslastung für die Bandbreite bei Ein- und Ausgang, über einen vergangenen Tag, eine vergangene Woche oder einen vergangenen Monat hinweg.
Die angezeigten Daten basieren auf dem Gesamtwert zum ankommenden und abgehenden Datenverkehr für öffentliche und private Netze.
* Durchschnittliche Antwortzeit für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.
* Durchschnittliche Transaktionen pro Sekunde für {{site.data.keyword.Bluemix_notm}} über die letzten 10 Minuten, die letzte Stunde und den vergangenen Tag.

### Berichte anzeigen
{: #oc_report}

Sie können Sicherheitsberichte und -protokolle, wie DataPower&trade;-, Firewall- und Anmeldeprüfberichte für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz anzeigen.

Klicken Sie zum Anzeigen von Berichten und Protokollen auf **ADMINISTRATION &gt; REPORTS AND LOGS**.

Es stehen Ihnen nun verschiedene Möglichkeiten zur Auswahl:

* Sie können in den Feldern Start- und Enddatum auswählen, um die Berichte und Protokolle zu filtern, die angezeigt werden.
* Sie können im Navigationsbereich verschiedene Berichte einblenden und anzeigen.
* Sie können Ihre Berichte und Protokolle durchsuchen. Bei der Suche werden die
Berichtsnamen ebenso wie der Textinhalt in den Berichten und Protokollen einbezogen. Sie können bei
der Suche auch Filter für Administrationsereignisse, DataPower-, Firewall- und
Anmeldeprüfungsberichte einsetzen.
* Beim Anzeigen eines Berichts oder eines Protokolls können Sie auf das Symbol ![Download](images/icon_download.svg) klicken, um den Bericht bzw. das Protokoll herunterzuladen. 

### Status anzeigen
{: #oc_status}

Sie können den Status für Ihre {{site.data.keyword.Bluemix_notm}}-Instanz über die {{site.data.keyword.Bluemix_notm}}-Statusseite überwachen. Die Seite 'Status' ist der zentrale Ort zum Suchen nach Benachrichtigungen und Ankündigungen in Bezug auf bedeutende Ereignisse, die die {{site.data.keyword.Bluemix_notm}}-Plattform und die übergeordneten Services in {{site.data.keyword.Bluemix_notm}} betreffen. 

Sie können einen RSS-Feed abonnieren, damit Sie nicht immer überprüfen müssen, ob Sie eine Benachrichtigung erhalten haben. Weitere Informationen zur Seite 'Status' und zur Einrichtung des RSS-Feeds finden Sie in [{{site.data.keyword.Bluemix_notm}} anzeigen](../troubleshoot/getting_customer_support.html#status).

### Eigenen Katalog verwalten
{: #oc_catalog}

Sie können die {{site.data.keyword.Bluemix_notm}}-Services und -Starter festlegen, die für Benutzer im {{site.data.keyword.Bluemix_notm}}-Katalog sichtbar sein sollen. Klicken Sie auf **ADMINISTRATION &gt; CATALOG MANAGEMENT**. 

Wählen Sie eine Kachel für einen Service oder einen Starter aus, um die Sichtbarkeit der betreffenden Service- oder Starterpläne zu bearbeiten. In Bezug auf die Sichtbarkeit stehen folgende Bearbeitungsoptionen zur Auswahl:
* Wählen Sie **ENABLE ALL PLANS** aus, wenn der ausgeblendete Service oder Starter für Benutzer im Katalog sichtbar sein soll.
* Wählen Sie **DISABLE ALL PLANS** aus, wenn ein Service oder Starter ausgeblendet sein soll, damit er für die Benutzer im {{site.data.keyword.Bluemix_notm}}-Katalog nicht sichtbar ist.
* Soll die Sichtbarkeit eines einzelnen Plans gesteuert werden, wählen Sie den Namen des
betreffenden Plans aus. Wählen Sie dann im Dropdown-Menü zum Anzeigen des Plans für alle Organisationen die
Option **Enable for all organizations**, zum Ausblenden des Plans
bei allen Organisationen die Option **Disable for all organizations** und zum
Anzeigen des Plans für bestimmte Organisationen die Option **Enable plan for specific
organizations** aus.

### Organisationen verwalten
{: #oc_organizations}

Sie können Ihre Organisationen verwalten, indem Sie Organisationen erstellen und löschen, Manager zu Organisationen hinzufügen und die Kontingentnutzung überwachen.

Klicken Sie auf **ADMINISTRATION &gt; ORGANIZATION ADMINISTRATION**. 

Sie können verschiedene Bereiche erweitern und anzeigen. Darüber hinaus können Sie
Kontingentpläne für Ihre Organisationen überprüfen und verwalten.

* Klicken Sie zum Erstellen einer neuen Organisation und Hinzufügen von Managern auf <strong>CREATE ORGANISATION</strong>.
Geben Sie einen Namen für die Organisation ein und
anschließend den Namen oder eine E-Mail-Adresse einer Person, die als Manager hinzugefügt
werden soll. Geben Sie
mehrere Namen ein bzw. wählen Sie mehrere Namen aus, wenn Sie mehrere Manager hinzufügen
möchten. Klicken Sie auf <strong>CREATE ORGANIZATION</strong>, um die Änderungen zu speichern und die Organisation zu erstellen.
* Erweitern Sie den Bereich für die Kontingentüberwachung, um Informationen
zu den folgenden Punkten anzuzeigen:
    * Speicherbelegung der Umgebung. In diesem Bereich finden Sie Details zur Speicherbelegung für die gesamte Systemumgebung.
Das Diagramm enthält Informationen zum belegten Systemspeicher, gesamten Systemspeicher,
ausgeschöpften Kontingent und zum insgesamt zugeordneten Kontingent. Die folgende Liste definiert die Typen der Speicherbelegung, die im Diagramm angezeigt werden.
	<dl>
	<dt><strong>Belegter Systemspeicher</strong></dt>
	<dd>Der physische Speicher, der von der Umgebung belegt wird.</dd>
	<dt><strong>Gesamtsystemspeicher</strong></dt>
	<dd>Der gesamte physische Speicher, der für die Umgebung zur Verfügung steht.</dd>
	<dt><strong>Bereitgestelltes Kontingent</strong></dt>
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
	* Speicherbelegung der Organisationen. Dieser Bereich enthält Details zur Speicherbelegung auf
Organisationsebene. Sie können das gesamte verfügbare Kontingent anzeigen sowie das Kontingent, das
jeweils für die einzelnen Organisationen verfügbar ist. Das Diagramm liefert Informationen, die nach
der höchsten Speicherbelegung pro Organisation geordnet sind. Die Organisation, die den größten
Speicherumfang belegt, wird standardmäßig an erster Stelle angezeigt. Sie können die Liste nach
der höchsten Speicherbelegung und der überschüssigen Speicherzuordnung sortieren.
	<dl>
	<dt><strong>Highest Memory Usage</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option für die höchste Speicherbelegung die Organisation, die den
meisten Speicher belegt. Sortieren Sie die Liste nach der höchsten
	Speicherbelegung, um die Organisationen zu ermitteln, die den meisten
Speicher belegen. Die Liste ist nach dem bereitgestellten Kontingent sortiert. </dd>
	<dt><strong>Excess Memory Allocation</strong></dt>
	<dd>Ermitteln Sie mithilfe dieser Option für überschüssige Speicherzuordnung
Organisationen mit einem Kontingentplan, der mehr Speicher als erforderlich zuordnet.
	Sortieren Sie die Liste nach der überschüssigen Speicherzuordnung, um Organisationen zu
ermitteln,
die im Verhältnis zu dem jeweils zugeordneten Speicher am wenigsten Speicher belegen. </dd>
	</dl>
* Ändern Sie den Kontingentplan für eine Organisation, indem Sie im Diagramm im Bereich für die
Speicherbelegung der Organisationen auf den Balken für die Organisation klicken, die bearbeitet werden
soll, oder den Namen der Organisation im Bereich mit der Organisationsliste auswählen. Auf der Seite zum Bearbeiten von Organisationen können Sie den Kontingentplan und
den Organisationsnamen ändern und Manager hinzufügen oder entfernen. Wenn Sie einen Kontingentplan
auswählen, der für die aktuelle Speichernutzung einer Organisation nicht ausreicht, erhalten Sie eine
entsprechende Nachricht. Speichern Sie Ihre Änderungen auf der Seite zum Bearbeiten von
Organisationen, indem Sie auf die Schaltfläche zum Speichern klicken.
* Im Bereich mit der Organisationsliste werden alle Organisationen in der
{{site.data.keyword.Bluemix_notm}}-Umgebung angezeigt.
	* Löschen Sie eine Organisation, indem Sie in der Aktionsspalte auf ![Löschen](images/icon_trash.svg) klicken.
	* Klicken Sie auf den Namen einer Organisation in der Liste, wenn Sie den Kontingentplan für die
jeweilige Organisation anzeigen oder bearbeiten möchten.
	* Klicken Sie auf den Namen einer Organisation in der Liste, wenn Sie den Namen der jeweiligen
Organisation bearbeiten oder Manager hinzufügen oder löschen möchten.

### Benutzer und Berechtigungen verwalten
{: #oc_useradmin}

Sie können Ihrer {{site.data.keyword.Bluemix_notm}}-Instanz aus der Benutzerregistry Ihres Unternehmens über LDAP
Benutzer hinzufügen. Sie können
Benutzer einzeln oder in Gruppen hinzufügen und die Benutzerberechtigungen anzeigen. Wenn Ihnen die
Berechtigung `admin` zugewiesen ist, können Sie auch Berechtigungen für andere Benutzer festlegen
und verwalten. Klicken Sie auf **ADMINISTRATION &gt; USER ADMINISTRATION**. 

Auf der Seite für die Benutzerverwaltung werden alle Benutzer für die lokale oder dedizierte Instanz angezeigt.
Die Berechtigungen für jeden Benutzer werden angezeigt. Die folgenden Berechtigungen sind verfügbar: None,
`Admin`, `Catalog`, `Login`,
`Reports` und `Users`. Berechtigungen können aktiviert werden oder dem Benutzer kann die Funktionalität `view` bzw.
`write` für diese Berechtigung erteilt werden; diese werden durch Symbole dargestellt. Beschreibungen der
einzelnen Typen und Erläuterungen der Symbole finden Sie unter [Berechtigungen](#permissions).

Es stehen verschiedene Optionen zur Auswahl:
* Nach Benutzern suchen. Sie können mithilfe des Feldes **Suchen** Benutzer in der Tabelle suchen. 
* Fügen Sie Benutzer hinzu. Wenn Sie die Berechtigung `admin` oder die
Berechtigung `users` mit der Funktionalität `write` besitzen, können
Sie Benutzer hinzufügen. Klicken Sie auf **Einzelnen Benutzer hinzufügen** oder **Benutzergruppe hinzufügen**,
um einen Benutzer oder eine Benutzergruppe hinzuzufügen. Geben Sie im Suchfeld einen Benutzernamen oder den Namen
einer Gruppe für die Suche ein und wählen Sie die Organisation aus der Organisationsliste aus, der der
Benutzer oder die Benutzergruppe hinzugefügt werden soll. Wenn Sie den Benutzer oder die Gruppe gefunden haben, den bzw. die
Sie hinzufügen möchten, klicken Sie auf den Benutzernamen und dann zum Hinzufügen auf
**Benutzer hinzufügen** oder **Mehrere Benutzer hinzufügen**.
Gruppen oder mehr als 50 Benutzer werden über einen Stapeljob im Hintergrund hinzugefügt. Wenn die Hinzufügeoperation erfolgreich war, wird der Benutzer bzw. die Gruppe
zur Tabelle hinzugefügt und Sie können ihn bzw. sie anzeigen und durchsuchen. Wenn Benutzer hinzugefügt werden,
sind ihnen keine Berechtigungen zugewiesen.
* Bearbeiten Sie Berechtigungen und Organisationen. Wenn Sie die Berechtigung `admin`
besitzen, können Sie Berechtigungen und Organisationen für andere Benutzer bearbeiten. Um Berechtigungen zu bearbeiten,
suchen Sie den gewünschten Benutzer und klicken Sie auf den Benutzernamen. Um Berechtigungen zu aktivieren oder zu
inaktivieren, wählen Sie in dem daraufhin angezeigten Fenster die folgenden Optionen aus:
	* Wählen Sie **On** in der Liste aus, um eine Berechtigung zu aktivieren.
	* Wählen Sie **Lesen** in der Liste aus, um dem Benutzer die Funktionalität `view` (schreibgeschützt) für diese Berechtigung zu erteilen, oder **Schreiben**,
um die Funktionalität `write` (Schreiben, d. h. Bearbeiten, Hinzufügen und Entfernen) für diese Berechtigung zu erteilen.
	* Wählen Sie **Off** aus, um die Berechtigung zu inaktivieren. Um Organisationen zu bearbeiten, wählen Sie die folgenden Optionen aus:
	* Fügen Sie den Benutzer zu einer Organisation hinzu, indem Sie über das Suchfeld eine Organisation
suchen und durch Klicken unter den verfügbaren Optionen die Option **HINZUFÜGEN** auswählen.
	* Entfernen Sie einen Benutzer aus einer Organisation, indem Sie auf das Symbol ![Minuszeichen als Symbol für 'Entfernen'](images/icon_remove.svg) klicken.
Klicken Sie zum Abschluss auf die Schaltfläche zum Speichern.
* Entfernen Sie Benutzer. Wenn Sie die Berechtigung `admin` oder die Berechtigung
`users` mit der Funktionalität `write` besitzen, können Sie
Benutzer entfernen.
Um einen Benutzer zu entfernen, suchen Sie den Benutzer und klicken Sie zunächst auf das Symbol ![Löschen](images/icon_trash.svg) und anschließend auf **Entfernen**.

### Berechtigungen
{: #permissions}

Benutzern können die folgenden Berechtigungen zugewiesen werden:

| **Benutzerberechtigung** | **Beschreibung** |       
|-----------------|-------------------|
| Admin | Benutzer mit der Berechtigung `admin` können Berechtigungen für andere Benutzer bearbeiten. |
| Catalog | Benutzern mit der Berechtigung `catalog` kann die Funktionalität `view` (Anzeigen) oder `write` (Ändern) zugewiesen werden, und zwar für die in der lokalen oder dedizierten Instanz verfügbaren Services. |  
| Login | Benutzer mit der Berechtigung `login` sind berechtigt, die Verwaltungsseite ('Administration') anzuzeigen. Ohne diese Berechtigung wird Benutzern die Menüoption 'Administration' nicht angezeigt. |
| Reports | Benutzern mit der Berechtigung `reports` kann für Sicherheitsberichte die Funktionalität `view` (Anzeigen) oder `write` (Ändern) zugewiesen werden. |
| Users | Benutzern mit der Berechtigung `users` kann die Funktionalität `view` (Anzeigen) für die Benutzerliste oder `write` (Hinzufügen oder Entfernen) für Benutzer zugewiesen werden. Diese Berechtigung erlaubt es Ihnen nicht, Berechtigungen für andere Benutzer festzulegen.|

*Tabelle 2. Berechtigungen*

Berechtigungen können aktiviert werden oder dem Benutzer kann die Funktionalität `view` bzw.
`write` für diese Berechtigung erteilt werden; dies wird durch die folgenden Symbole dargestellt:

* Das Symbol ![Aktiviert; dargestellt durch ein Hakensymbol](images/icon_enabled.svg) neben einer Berechtigung bedeutet, dass diese Berechtigung aktiviert ist.
* Das Symbol ![Anzeigen; dargestellt durch ein Augensymbol](images/icon_read.svg) bedeutet, dass der Benutzer für diese Berechtigung über die Funktionalität `view` (schreibgeschützt) verfügt.
* Das Symbol ![Schreiben; dargestellt durch ein Stiftsymbol](images/icon_write.svg) bedeutet, dass der Benutzer für diese Berechtigung über die Funktionalität `write` (Bearbeiten, Hinzufügen oder Entfernen) verfügt.

### Benutzer mit der Admin-REST-API verwalten
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

#### Bei der Administrationskonsole anmelden

Vor dem Ausführen von `Admin`-API-Anforderungen müssen Sie sich
bei der Administrationskonsole anmelden. Wenn Sie die Berechtigung `admin` oder die
Berechtigung `users` mit der Funktionalität `write` besitzen, können Sie
Benutzer hinzufügen und Benutzer entfernen. Zum Bearbeiten der Berechtigungen anderer Benutzer
benötigen Sie die Berechtigung `admin`.

Zum Anmelden bei der Administrationskonsole können Sie die Basiszugriffsauthentifizierung am Endpunkt
`https://<eigener Host>.ibm.com/login` verwenden. Der Server gibt ein Cookie mit Ihrer Sitzung zurück. Dieses Cookie verwenden Sie für alle
Operationen mit der Administrationskonsole.

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

#### Organisationen auflisten
{: #listingorg}

Beim Hinzufügen eines Benutzers müssen Sie eine Organisation angeben. Sie können die
`Admin`-REST-API verwenden, um alle Organisationen aufzulisten. Zum Auflisten der Organisationen müssen Sie die Berechtigung `users` mit der Funktionalität
`read` besitzen. Führen Sie zum Auflisten von Organisationen den folgenden Befehl aus:

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

#### Benutzer auflisten
{: #listingusr}

Sie können feststellen, ob ein Benutzer bereits zu Ihrer
{{site.data.keyword.Bluemix_notm}}-Umgebung hinzugefügt wurde, und zwar mithilfe der REST-API `Admin` zum
Auflisten der registrierten Benutzer. Zum Auflisten der registrierten Benutzer müssen Sie die Berechtigung `users` mit der Funktionalität `read` besitzen. Um alle Benutzer aufzulisten, führen Sie den folgenden Befehl aus:

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

#### Benutzer hinzufügen

Sie können die REST-API `Admin` verwenden, um
Benutzer zur {{site.data.keyword.Bluemix_notm}}-Instanz
hinzuzufügen. Zum Hinzufügen von Benutzern müssen Sie die Berechtigung `users`
mit der Funktionalität `write` besitzen.

Sie können einen Benutzer oder eine Liste von Benutzern hinzufügen. Dabei können Benutzer zu einer einzelnen Organisation oder zu mehreren Organisationen hinzugefügt werden. Zum Hinzufügen eines Benutzers müssen Sie die folgenden Informationen bereitstellen:

* Vorname (fist_name) und Familienname (last_name) des Benutzers. Geben Sie den Vornamen
(`"first_name"`) und den Familiennamen (`"last_name"`) aus [Listing users](index.html#listingusr) an.
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
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
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

#### Benutzer entfernen

Sie können die REST-API `Admin` verwenden, um
Benutzer aus der {{site.data.keyword.Bluemix_notm}}-Instanz
zu entfernen. Zum Entfernen von Benutzern müssen Sie die Berechtigung
`users` mit der Funktionalität `write` besitzen.

Beim Entfernen eines Benutzers müssen Sie die Benutzer-ID des Benutzers angeben. Führen Sie den folgenden Befehl aus:

`curl -v -b ./cookies.txt -X DELETE https://<eigener Host>.ibm.com/codi/v1/users?user_id=<Benutzer-ID@domain.com>`
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

### API für angepasster Services
{: #servicebrokerapi}

Es gibt drei APIs, die Sie zum Registrieren oder Erstellen eines neuen Service, zum Aktualisieren eines Service und zum Löschen eines Service verwenden können.

Alle APIs beziehen sich auf <code>https://opsconsole.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;Unterdomäne&gt;</strong></dt>
<dd>Dieser Wert steht für den Namen der lokalen oder dedizierten Instanz. Der Unterdomänenname für Ihre {{site.data.keyword.Bluemix}}-Instanz wurde beim Onboarding zugeordnet.</dd>
</dl>

### Neuen Service registrieren

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Registrieren eines neuen Service.

#### Route

```
POST /codi/v1/serviceBrokers
```
{: screen}

#### Anforderung

*Tabelle 3. Felder*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |

##### Hauptteil

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

##### Header

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Antwort

##### Status

```
201 Created
```
{: screen}

##### Hauptteil

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

### Service aktualisieren

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Aktualisieren eines Service.

#### Route

`PUT /codi/v1/serviceBrokers`
{: screen}

#### Anforderung

*Tabelle 4. Felder*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |
| auth_username | Benutzername für die Verbindung mit dem Service-Broker. |
| auth_password | Kennwort für die Verbindung mit dem Service-Broker. |
| broker_url | URL für die Verbindung zum Service-Broker. |
| owningOrganization | Anfangsorganisation, bei der der Service in die Whitelist eingetragen werden soll. |

##### Hauptteil

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

##### Header

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Antwort

##### Status

```
201 Created
```
{: screen}

##### Hauptteil

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

### Service löschen

Verwenden Sie die folgende API und die folgenden Codebeispiele zum Löschen eines Service.

*Tabelle 5. Parameter*

| **Name** | **Beschreibung** |
|-----------------|-------------------|
| name | Name des Service-Brokers. Dieser Name kann in keinen anderen Namen als den Erstellungsnamen des Service geändert werden. |

#### Route

```
DELETE /codi/v1/serviceBrokers?name=Name des Service-Brokers
```
{: screen}

#### Anforderung

##### Header

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

#### Antwort

##### Status

```
204 No Content
```
{: screen}

### Benutzer mit der Befehlszeilenschnittstelle 'cf' verwalten
{: #usingadmincli}

Sie können Benutzer für Ihre {{site.data.keyword.Bluemix_notm}} Local- oder
{{site.data.keyword.Bluemix_notm}} Dedicated-Umgebung über die Cloud
Foundry-Befehlszeilenschnittstelle mit dem
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in verwalten. Sie können Benutzer beispielsweise aus einer LDAP-Registry
hinzufügen.

Vor dem Beginn müssen Sie die Befehlszeilenschnittstelle 'cf' installieren. Für das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
ist cf Version 6.11.2 oder höher erforderlich. [Cloud Foundry-Befehlszeilenschnittstelle herunterladen](https://github.com/cloudfoundry/cli/releases){: new_window}

**Einschränkung:** Die
Cloud Foundry-Befehlszeilenschnittstelle wird nicht von Cygwin unterstützt. Verwenden Sie
die Cloud Foundry-Befehlszeilenschnittstelle in einem
Befehlszeilenfenster, das sich von dem Befehlszeilenfenster von Cygwin unterscheidet.

#### Das {{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in hinzufügen

Nach der Installation der Befehlszeilenschnittstelle 'cf' können Sie das
{{site.data.keyword.Bluemix_notm}}-Administrator-CLI-Plug-in
hinzufügen.

Führen Sie die folgenden Schritte aus, um das Repository hinzuzufügen und
das Plug-in zu installieren:

<ol>
<li>Führen Sie zum Hinzufügen des {{site.data.keyword.Bluemix_notm}}-Administrator-Plug-in-Repositorys den folgenden Befehl aus:<br/><br/>
<code> cf add-plugin-repo BluemixAdmin https://opsconsole.&lt;subdomain&gt;.bluemix.net/cli </code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;Unterdomäne&gt;</dt>
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
