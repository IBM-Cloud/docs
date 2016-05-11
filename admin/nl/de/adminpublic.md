---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Verwalten
{: #administer}
*Letzte Aktualisierung: 29. Februar 2016*

Sie können Organisationen, Bereiche und zugeordnete Benutzer verwalten, indem Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) klicken und anschließend die Option **Organisationen verwalten** auswählen. Wenn Sie ein Benutzer von {{site.data.keyword.Bluemix_notm}} Local oder {{site.data.keyword.Bluemix_notm}} Dedicated sind, finden Sie unter [{{site.data.keyword.Bluemix_notm}} Local und {{site.data.keyword.Bluemix_notm}} Dedicated verwalten](../admin/index.html#mng) weitere Informationen zur Verwaltung einer lokalen oder dedizierten Instanz.
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} Public verwalten
{: #mngacct}

In der öffentlichen {{site.data.keyword.Bluemix}}-Umgebung (Public) können Sie Organisationen und Bereiche, einschließlich des Benutzerzugriffs, über das Dashboard in der Benutzerschnittstelle verwalten. Sie können darüber hinaus Ihre Nutzung und Abrechnung überwachen.
{:shortdesc}

### Organisationen und Bereiche
{: #orgsandspaces}

Als Organisationsmanager können Sie die Einstellungen der Organisation oder des Bereichs, einschließlich des Benutzerzugriffs, auf der Seite 'Organisationen verwalten' anzeigen und verwalten. Zum Öffnen der Seite 'Organisationen verwalten' klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen **Organisationen verwalten** aus.

#### Organisationen

Eine Organisation wird durch die folgenden Elemente definiert:

<dl>
<dt>Benutzer</dt>
<dd>Die Rolle mit Basisberechtigungen in Organisationen und Bereichen. Sie müssen einer Organisation zugewiesen sein, bevor Ihnen weitere Berechtigungen für Bereiche innerhalb der Organisation erteilt werden können. Detaillierte Informationen hierzu finden Sie unter [Benutzer und Rollen](adminpublic.html#userroles).</dd>
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

#### Bereiche

Innerhalb einer Organisation können Sie Bereiche verwenden, um eine Reihe von Anwendungen, Services und Benutzern zusammen zu gruppieren.

Wenn Sie einer Organisation Benutzer hinzugefügt haben, können Sie ihnen Berechtigungen für Bereiche innerhalb der Organisation erteilen. Ähnlich wie Organisationen haben auch Bereiche eine Reihe von Berechtigungen, die Benutzern zugeordnet werden können:

<ul>
<li>Bereichsmanager</li>
<li>Bereichsentwickler</li>
<li>Bereichsauditor</li>
</ul>

**Hinweis**: Einem Benutzer muss mindestens eine der Berechtigungen im Bereich zugeordnet werden.

Die Registerkarte **Domänen** für einen Bereich enthält eine schreibgeschützte Liste der Domänen, die dem Bereich zugeordnet sind. Die Systemdomäne ist für einen Bereich immer verfügbar. Außerdem können dem Bereich angepasste Domänen zugeordnet werden. Anwendungen, die in dem Bereich erstellt wurden, können eine beliebige der für den Bereich aufgelisteten Domänen verwenden.

### Benutzer und Rollen
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

#### Benutzerrollen

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
<dd>Abrechnungsmanager sind berechtigt, Informationen zur Laufzeit- und Servicenutzung für die Organisation anzuzeigen.</dd>
<dt>Organisationsauditoren</dt>
<dd>Organisationsauditoren sind berechtigt, Anwendungs- und Serviceinhalt in dem Bereich anzuzeigen.</dd>
<dt>Bereichsmanager</dt>
<dd>Bereichsmanager verfügen über die folgenden Berechtigungen:
<ul>
<li>Fügen dem Bereich Benutzer hinzu und verwalten Benutzer.</li>
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

**Hinweis:** Benutzer, denen eine Manager- oder Entwicklerrolle zugewiesen ist, können auf die Umgebungsvariable VCAP_SERVICES zugreifen. Ein Benutzer, dem die Auditorrolle zugewiesen ist, kann jedoch nicht auf VCAP_SERVICES zugreifen.

### Organisationen verwalten
{: #orgmng}

Als Organisationsmanager oder Kontoeigner können Sie Ihre Organisationen verwalten. Management-Tasks beinhalten die Erstellung einer Organisation, die Umbenennung einer Organisation, die Erstellung eines Bereichs, die Einladung von Benutzen in einen Bereich, die Änderung von Benutzerrollen sowie das Löschen einer vorhandenen Organisation.

#### Eine Organisation erstellen

Es können nur Benutzer mit einem Zahlungskonto eine Organisation erstellen. Mit einem Zahlungskonto können Sie durch Ausführen der folgenden Schritte eine Organisation erstellen:

<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Klicken Sie auf **Organisation erstellen** und befolgen Sie die Eingabeaufforderungen, um Ihre Organisation zu erstellen.</li>
</ol>

#### Eine Organisation umbenennen

Führen Sie die folgenden Schritte aus, um Ihre Organisation umzubenennen:

<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Wählen Sie die Organisation aus, die Sie umbenennen möchten.</li>
<li>Geben Sie im Feld **Organisation** einen neuen Namen ein und klicken Sie auf **Speichern**.</li>
</ol>

#### Mitglieder auflisten 

Führen Sie die folgenden Schritte aus, um die Mitglieder Ihrer Organisation oder Ihres Bereichs aufzulisten:

<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](../support/images/account_support.svg) und wählen Sie **Organisationen verwalten** aus. Auf der Registerkarte **Benutzer** werden die Mitglieder Ihrer Organisation und ihre Rollen angezeigt.</li>
<li>Klicken Sie auf den Bereichsnamen in Ihrer Organisation, um die Mitglieder dieses Bereichs und deren Rollen anzuzeigen.</li>
</ol>

#### Einen Bereich erstellen

Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen:

<ol>
<li>Rufen Sie das {{site.data.keyword.Bluemix_notm}}-Dashboard auf, klicken Sie auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Klicken Sie auf **Bereich erstellen** hinter Ihrem Organisationsnamen und befolgen Sie die Eingabeaufforderungen, um Ihren Bereich zu erstellen.</li>
</ol>

#### Benutzer in einen Bereich einladen

Sie können Benutzer in Ihre Organisationen und Bereiche durch Angabe einer E-Mail-Adresse einladen. Die Benutzer können nur auf den Bereich zugreifen, dem sie hinzugefügt wurden. 

Abhängig davon, ob der Eingeladene eine IBM ID hat oder nicht, wird diesem Benutzer eine Rolle `Mitglied` oder `Collaborator` für das Konto zugewiesen. In der folgenden Tabelle wird erläutert, wie Kontorollen nach Einladungstyp zugewiesen werden.

*Tabelle 1. Zuweisungen von Kontorollen*

| **Eingeladener E-Mail-Typ** | **Zugewiesene Kontorolle** | 
|----------------|------------------|
|Benutzer hat IBM ID-Konto, das mit der eingeladenen E-Mail-Adresse verbunden ist.  | Mitglied  | 
|Benutzer hat keine IBM ID. | Eine IBM ID, die der übergebenen E-Mail-Adresse entspricht, wird erstellt und der Benutzer wird als Mitglied hinzugefügt. | 
|Eine E-Mail-Adresse für einen aktuellen {{site.data.keyword.Bluemix_notm}}-Benutzer. | Collaborator | 

Führen Sie die folgenden Schritte aus, um Benutzer mit zugewiesenen Rollen bestimmten Bereichen für eine ausgewählte Organisation hinzuzufügen:

<ol>
<li>Wechseln Sie zu **Konto und Unterstützung** &gt; **Konto** &gt; **Organisationen verwalten**.</li>
<li>Wählen Sie die Option **Benutzer einladen** aus.</li>
<li>Geben Sie die E-Mail-Adresse für die Person an, die Sie einladen wollen.</li>
<li>Wählen Sie die Rolle für die Organisation aus, in die der neue Benutzer eingeladen werden soll.</li>
<li>Wählen Sie die Rolle für den Bereich aus, in den der neue Benutzer eingeladen werden soll.</li>
<li>Wählen Sie **Einladen** aus.</li>
<li>Prüfen Sie die Bestätigung, das die Einladung gesendet wurde, im Abschnitt **Anstehend**. Wählen Sie **E-Mail-Einladung erneut senden** oder **Einladung abbrechen** aus, um eine Aktion für eine anstehende Einladung auszuführen.</li>
</ol>

#### Benutzerrollen ändern

Führen Sie die folgenden Schritte aus, um Benutzerrollen zu ändern:

<ol>
<li>Klicken Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle auf das Symbol **Konto und Unterstützung** ![Konto und Unterstützung](images/account_support.svg) und wählen Sie **Organisationen verwalten** aus.</li>
<li>Wählen Sie das Kontrollkästchen **Manager**, **Abrechnungsmanager** oder **Auditor** auf der Registerkarte **Benutzer** aus, um Rollen von Benutzern in Ihrer Organisation zu ändern. Oder wählen Sie einen Bereich im Navigationsbereich und anschließend das Kontrollkästchen **Manager**, **Entwickler** oder **Auditor** auf der Registerkarte **Benutzer** aus, um Rollen von Benutzern in dem Bereich zu ändern. </li>
<li>Klicken Sie auf **Speichern**.</li>
</ol>

#### Eine vorhandenen Organisation löschen

Wenn Sie Ihre Organisation löschen möchten, wenden Sie sich an die Unterstützung für {{site.data.keyword.Bluemix_notm}}-Registrierungen und -IDs.

**Hinweis**: Das Löschen von Operationen kann nicht rückgängig gemacht werden. Alle der Organisation zugeordneten Anwendungen und Services gehen verloren.

