---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Organisationen und Bereiche verwalten
{: #orgsspacesusers}
*Letzte Aktualisierung: 16. Mai 2016*

Als Kontoeigner können Sie Ihre Organisationen verwalten, indem Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) klicken und die Seite **Organisationen verwalten** aufrufen. Organisationsmanager können ferner die Seite 'Organisationen verwalten' verwenden, um beliebige Organisationen, für die Sie als Manager festgelegt sind, zu verwalten.
{:shortdesc}

Die Management-Tasks umfassen folgende Tasks: 

* Eine Organisation oder einen Bereich erstellen
* Eine Organisation umbenennen
* Eine vorhandene Organisation oder einen vorhandenen Bereich löschen
* Die Teammitglieder auflisten, die Ihrem Konto oder Ihrer Organisation hinzugefügt wurden
* Kontingente verwalten oder anzeigen
* Angepasste Domänen verwalten

## Organisationen
{: #orginfo}

Organisationen können mehrere Regionen umfassen und sind durch folgende Elemente definiert: 

<dl>
<dt>Teammitglieder</dt>
<dd>Die Rolle mit Basisberechtigungen in Organisationen und Bereichen. Sie müssen einer Organisation zugewiesen sein, bevor Ihnen weitere Berechtigungen für Bereiche innerhalb der Organisation erteilt werden können. Detaillierte Informationen hierzu finden Sie unter [Benutzer und Rollen](users_roles.html#userrolesinfo).</dd>
<dt>Domänen</dt>
<dd>Stellen die Route im Internet bereit, die der Organisation zugeordnet ist. Eine Route hat eine Unterdomäne und eine Domäne. Eine Unterdomäne ist in der Regel der Anwendungsname. Eine Domäne kann eine Systemdomäne oder eine angepasste Domäne sein, die Sie für Ihre Anwendung registriert haben. Siehe den Abschnitt zum Thema [Angepasste Domänen verwalten](orgs_spaces.html#managedomains).<br/>
<p>**Hinweis**: Wenn Sie eine angepasste Domäne hinzufügen, müssen Sie Ihren DNS-Server so konfigurieren, dass er Ihre angepasste Domäne in einen Verweis auf die {{site.data.keyword.Bluemix_notm}}-Systemdomäne auflöst. Auf diese Weise kann {{site.data.keyword.Bluemix_notm}} eine aus Ihrer angepassten Domäne empfangene Anforderung ordnungsgemäß an Ihre Anwendung weiterleiten.</p></dd>
<dt>Kontingent</dt>
<dd>Stellt die Ressourcengrenzwerte für die Organisation dar, einschließlich der Anzahl der Services und die Speicherkapazität, die für die Verwendung durch Ihre Organisation zugeordnet werden können. Kontingente werden bei der Erstellung von Organisationen zugeordnet. Jede Anwendung und jeder Service in einem Bereich der Organisation trägt zur Nutzung des Kontingents bei. Sowohl mit dem nutzungsabhängigen Plan als auch dem Abonnementplan können Sie Ihr Kontingent für Cloud Foundry-Anwendungen und -Container anpassen, sobald sich die Bedürfnisse für Ihre Organisation ändern. Siehe den Abschnitt zum Thema [Kontingent verwalten](orgs_spaces.html#managequota).</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}} können Sie Organisationen verwenden, um die Onlinezusammenarbeit unter den Teammitgliedern zu ermöglichen und die logische Gruppierung von Projektressourcen auf folgende Weise zu erleichtern: 

<ul>
<li>Sie können eine Reihe von Bereichen, Anwendungen, Services, Domänen, Routen und Teammitgliedern in Organisationen zusammen gruppieren. </li>
<li>Sie können den Zugriff auf die Bereiche und Organisationen auf Benutzerbasis verwalten.</li>
</ul>

Wenn Sie eine Organisation erstellen, muss der Organisationsname in {{site.data.keyword.Bluemix_notm}} eindeutig sein. Falls der Organisationsname bereits von einem anderen Benutzer von {{site.data.keyword.Bluemix_notm}} Public, Dedicated oder Local verwendet wird, müssen Sie einen neuen Namen angeben. Nachdem Sie die Organisation erstellt haben, wird Ihnen automatisch die Berechtigung *Organisationsmanager* zugeordnet, die es Ihnen ermöglicht, den Organisationsnamen zu bearbeiten, Teammitglieder hinzuzufügen und Bereiche in der Organisation zu erstellen oder zu löschen. 

Sie müssen sich an die [Unterstützung für {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} wenden, um eine Organisation zu löschen. Wenn Sie das Unterstützungsteam auffordern, eine Organisation zu löschen, werden alle Bereiche, Anwendungen und Services innerhalb der Organisation gelöscht. 

Die folgenden [Benutzerrollen](users_roles.html#userrolesinfo) können Teammitgliedern in der Organisation zugeordnet werden: 

<ul>
<li>Organisationsmanager</li>
<li>Abrechnungsmanager der Organisation</li>
<li>Organisationsauditor</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Bereiche
{: #spaceinfo}

Innerhalb einer Organisation können Sie Bereiche verwenden, um eine Reihe von Anwendungen, Services und Teammitgliedern zu gruppieren. Bereiche sind an eine bestimmte Region in {{site.data.keyword.Bluemix_notm}} gebunden.

Nachdem Sie Teammitglieder zu einer Organisation hinzugefügt haben, können Sie ihnen Berechtigungen für die Bereich erteilen. Ähnlich wie Organisationen verfügen Bereiche über eine Reihe von [Benutzerrollen](users_roles.html#userrolesinfo) mit bestimmten Berechtigungen, die Teammitgliedern zugeordnet sind: 

<ul>
<li>Bereichsmanager</li>
<li>Bereichsentwickler</li>
<li>Bereichsauditor</li>
</ul>

**Hinweis**: Einem Teammitglied muss mindestens eine der Berechtigungen im Bereich zugeordnet sein. 

## Organisationen und Bereiche erstellen
{: #createorg}

Nur Kontoeigner mit nutzungsabhängigen Konten können eine Organisation erstellen. Sie können eine Organisation erstellen, indem Sie die folgenden Schritte ausführen: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Klicken Sie auf **Neue Organisation hinzufügen**.
3. Geben Sie den Namen der Organisation ein. 
4. Klicken Sie auf **Hinzufügen**.

Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps den Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, die Sie einem Bereich hinzufügen möchten, und wählen Sie **Details anzeigen** aus.
3. Klicken Sie auf **Bearbeiten**.
4. Klicken Sie auf **Bereich hinzufügen**.
5. Geben Sie den Bereichsnamen ein.
6. Klicken Sie auf **Hinzufügen**.


## Eine Organisation umbenennen
{: #orgrename}

Führen Sie die folgenden Schritte aus, um Ihre Organisation umzubenennen:

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, die Sie bearbeiten möchten, und wählen Sie **Details anzeigen** aus.
3. Wählen Sie **Bearbeiten** aus.
4. Wählen Sie **Bearbeiten** für den Titel der Organisation aus. 
5. Geben Sie den neuen Organisationsnamen ein. 
6. Klicken Sie auf **Speichern**.

## Eine vorhandene Organisation oder einen vorhandenen Bereich löschen
{: #deleteorgs}

Als Kontoeigner können Sie sich an die [Unterstützung für {{site.data.keyword.Bluemix_notm}}](http://ibm.biz/bluemixsupport){: new_window} wenden, um eine Organisation zu löschen.  

**Hinweis**: Das Löschen von Operationen kann nicht rückgängig gemacht werden. Alle der Organisation zugeordneten Anwendungen und Services gehen verloren.

Sie können einen Bereich von der Seite **Organisationen verwalten** löschen: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, die Sie bearbeiten möchten, und wählen Sie **Details anzeigen** aus.
3. Ermitteln Sie den Bereich, den Sie löschen möchten, und wählen Sie **Bearbeiten** aus.
4. Klicken Sie auf **Ihren Bereich löschen**.

## Mitglieder auflisten
{: #listmembers}

Führen Sie die folgenden Schritte aus, um die Mitglieder für eine bestimmte Organisation aufzulisten: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, deren Mitglieder Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Klicken Sie auf **Bearbeiten**.
4. Auf der Registerkarte **Benutzer** werden die Mitglieder Ihrer Organisation und ihre Rollen angezeigt.

Führen Sie die folgenden Schritte aus, um die Mitglieder für einen bestimmten Bereich aufzulisten: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, deren Mitglieder Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Ermitteln Sie den Bereich, dessen Mitglieder Sie anzeigen möchten und klicken Sie auf **Bearbeiten**.
4. Sie können die Mitglieder Ihres Bereichs und deren Rollen auf der Registerkarte **Benutzer** anzeigen.

## Kontingent verwalten
{: #managequota}

Als Kontoeigner oder Organisationsmanager können Sie das zugeordnete und das verwendete Kontingent für Ihre Organisation anzeigen. Das Kontingent stellt die Ressourcengrenzen für die Organisation dar, die beim Erstellen der Organisation zugeordnet wird. Jede Anwendung und jeder Service in einem Bereich der Organisation trägt zur Nutzung des Kontingents bei.

Führen Sie folgende Schritte aus, um das Kontingent für Ihre Organisation anzuzeigen: 

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, deren Kontingent Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Klicken Sie auf **Bearbeiten**.
4. Wählen Sie die Registerkarte **Kontingent** aus.

Um das Kontingent für Ihre Organisation zu aktualisieren, müssen Sie ein Support-Ticket öffnen. Weitere Informationen zum Öffnen eines Support-Tickets finden Sie unter dem Thema [Kundenunterstützung abrufen](../support/index.html#contacting-support). Weitere Informationen zum Kontingent für Container finden Sie unter dem Thema[Kontingent](../containers/container_creating_ov.html#container_quota) in der Dokumentation zu Containern. 

## Domänen verwalten
{: #managedomains}

Als Kontoeigner oder Organisationsmanager können Sie die Systemdomäne anzeigen und angepasste Domänen für Anwendungen hinzufügen, die innerhalb der Organisation und ihren Bereichen erstellt wurden. Als Bereichsmanager enthält Ihre Registerkarte **Domänen** für einen Bereich eine schreibgeschützte Liste der Domänen, die dem Bereich zugeordnet sind.  

1. Klicken Sie auf das Symbol **Konto und Unterstützung** ![Symbol 'Konto und Unterstützung'](../admin/images/account_support.svg) und rufen Sie die Seite **Organisationen verwalten** auf. 
2. Ermitteln Sie die Organisation, für die Sie Domänen anzeigen oder bearbeiten möchten. 
3. Wählen Sie **Details anzeigen** für diese Organisation aus. 
4. Klicken Sie auf **Bearbeiten**.
5. Klicken Sie auf **Domänen**.

Wenn Sie eine angepasste Domäne hinzufügen möchten, müssen Sie Ihren DNS-Server so konfigurieren, dass er auf die {{site.data.keyword.Bluemix_notm}}-Systemdomäne verweist. Auf diese Weise kann {{site.data.keyword.Bluemix_notm}} eine aus Ihrer angepassten Domäne empfangene Anforderung ordnungsgemäß an Ihre Anwendung weiterleiten. Die Systemdomäne ist für einen Bereich immer verfügbar und angepasste Domänen können auch einem Bereich zugeordnet sein. In einem Bereich erstellte Anwendung können eine der Domänen verwenden, die für diesen Bereich aufgelistet sind. Weitere Informationen zum Erstellen und Verwenden angepasster Domänen finden Sie unter [Angepasste Domäne verwenden](../manageapps/updapps.html#domain).
