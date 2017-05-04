---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-03"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Organisationen und Bereiche verwalten
{: #orgsspacesusers}

Als Kontoeigner können Sie Ihre Organisationen und Bereiche über die Seite 'Organisationen verwalten' verwalten. Organisationsmanager können ferner die Seite 'Organisationen verwalten' verwenden, um beliebige Organisationen, für die sie als Manager festgelegt sind, zu verwalten.
{:shortdesc}

Zur Verwaltung von Organisationen und Bereichen klicken Sie in der {{site.data.keyword.Bluemix_notm}}-Menüleiste auf **Verwalten** &gt; **Konto** &gt; **Organisationen**.  

**Hinweis:** Sie müssen der Kontoeigner eines nutzungsabhängigen Kontos sein, um eine Organisation erstellen zu können.

## Organisationen verwalten
{: #orginfo}

Organisationen können mehrere Regionen umfassen und sind durch folgende Elemente definiert:

<dl>
<dt>Teammitglieder</dt>
<dd>Die Rolle mit Basisberechtigungen in Organisationen und Bereichen. Sie müssen einer Organisation zugewiesen sein, bevor Ihnen weitere Berechtigungen für Bereiche innerhalb der Organisation erteilt werden können. Detaillierte Informationen hierzu finden Sie unter [Benutzer und Rollen](/docs/admin/users_roles.html#userrolesinfo).</dd>
<dt>Domänen</dt>
<dd>Stellen die Route im Internet bereit, die der Organisation zugeordnet ist. Eine Route hat eine Unterdomäne und eine Domäne. Eine Unterdomäne ist in der Regel der Anwendungsname. Eine Domäne kann eine Systemdomäne oder eine angepasste Domäne sein, die Sie für Ihre Anwendung registriert haben. Siehe den Abschnitt zum Thema [Angepasste Domänen verwalten](/docs/admin/orgs_spaces.html#managedomains).<br/>
<p>**Hinweis:** Wenn Sie eine angepasste Domäne hinzufügen, müssen Sie Ihren DNS-Server so konfigurieren, dass er Ihre angepasste Domäne in einen Verweis auf die {{site.data.keyword.Bluemix_notm}}-Systemdomäne auflöst. Auf diese Weise kann {{site.data.keyword.Bluemix_notm}} eine aus Ihrer angepassten Domäne empfangene Anforderung ordnungsgemäß an Ihre Anwendung weiterleiten.</p></dd>
<dt>Kontingent</dt>
<dd>Stellt die Ressourcengrenzen für die Organisation dar, einschließlich der Anzahl der Services und die Speicherkapazität, die für die Verwendung durch Ihre Organisation zugeordnet werden können. Kontingente werden bei der Erstellung von Organisationen zugeordnet. Jede Anwendung und jeder Service in einem Bereich der Organisation trägt zur Nutzung des Kontingents bei. Sowohl mit dem nutzungsabhängigen Plan als auch dem Abonnementplan können Sie Ihr Kontingent für Cloud Foundry-Anwendungen und -Container anpassen, sobald sich die Anforderungen für Ihre Organisation ändern. Siehe den Abschnitt zum Thema [Kontingent verwalten](/docs/admin/orgs_spaces.html#managequota).</dd>
</dl>

In {{site.data.keyword.Bluemix_notm}} können Sie Organisationen verwenden, um die Onlinezusammenarbeit unter den Teammitgliedern zu ermöglichen und die logische Gruppierung von Projektressourcen auf folgende Weise zu erleichtern:

<ul>
<li>Sie können eine Reihe von Bereichen, Anwendungen, Services, Domänen, Routen und Teammitgliedern in Organisationen zusammen gruppieren.</li>
<li>Sie können den Zugriff auf die Bereiche und Organisationen auf Benutzerbasis verwalten.</li>
</ul>

Wenn Sie eine Organisation erstellen, muss der Organisationsname in {{site.data.keyword.Bluemix_notm}} eindeutig sein. Falls der Organisationsname bereits von einem anderen Benutzer von {{site.data.keyword.Bluemix_notm}} Public, Dedicated oder Local verwendet wird, müssen Sie einen neuen Namen angeben. Nachdem Sie die Organisation erstellt haben, wird Ihnen automatisch die Berechtigung *Organisationsmanager* zugeordnet, die es Ihnen ermöglicht, den Organisationsnamen zu bearbeiten, Teammitglieder hinzuzufügen und Bereiche in der Organisation zu erstellen oder zu löschen.

Sie müssen sich an den [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} wenden, um eine Organisation zu löschen. Wenn Sie das Unterstützungsteam auffordern, eine Organisation zu löschen, werden alle Bereiche, Anwendungen und Services innerhalb der Organisation gelöscht.

Die folgenden [Benutzerrollen](/docs/admin/users_roles.html#userrolesinfo) können Teammitgliedern in der Organisation zugeordnet werden:

<ul>
<li>Organisationsmanager</li>
<li>Abrechnungsmanager der Organisation</li>
<li>Organisationsauditor</li>
</ul>

<!-- Add info on Manage infrastructure option under a space -->

## Bereiche verwenden
{: #spaceinfo}

Innerhalb einer Organisation können Sie Bereiche verwenden, um eine Reihe von Anwendungen, Services und Teammitgliedern zu gruppieren. Bereiche sind an eine bestimmte Region in {{site.data.keyword.Bluemix_notm}} gebunden.

Nachdem Sie Teammitglieder zu einer Organisation hinzugefügt haben, können Sie ihnen Berechtigungen für die Bereich erteilen. Ähnlich wie Organisationen verfügen Bereiche über eine Reihe von [Benutzerrollen](/docs/admin/users_roles.html#userrolesinfo) mit bestimmten Berechtigungen, die Teammitgliedern zugeordnet sind:

<ul>
<li>Bereichsmanager</li>
<li>Bereichsentwickler</li>
<li>Bereichsauditor</li>
</ul>

**Hinweis:** Einem Teammitglied muss mindestens eine der Berechtigungen im Bereich zugeordnet sein.

## Organisationen und Bereiche erstellen
{: #createorg}

Nur Kontoeigner mit nutzungsabhängigen Konten können eine Organisation erstellen. Sie können eine Organisation erstellen, indem Sie die folgenden Schritte ausführen:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Klicken Sie auf **Neue Organisation hinzufügen**.
3. Geben Sie den Namen der Organisation ein.
4. Klicken Sie auf **Hinzufügen**.

Sie können in Ihrer Organisation Bereiche erstellen, z. B. einen Bereich *dev* als Entwicklungsumgebung, einen Bereich *test* als Testumgebung und einen Bereich *production* als Produktionsumgebung. Anschließend können Sie Ihre Apps den Bereichen zuordnen. Führen Sie die folgenden Schritte aus, um einen Bereich zu erstellen:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, der Sie einen Bereich hinzufügen möchten, und wählen Sie **Details anzeigen** aus. 
4. Klicken Sie auf **Bereich hinzufügen**.
5. Geben Sie den Bereichsnamen ein.
6. Klicken Sie auf **Hinzufügen**.

## Organisation umbenennen
{: #orgrename}

Führen Sie die folgenden Schritte aus, um Ihre Organisation umzubenennen:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, die Sie bearbeiten möchten, und wählen Sie **Details anzeigen** aus. 
3. Wählen Sie **Organisation bearbeiten** aus.
4. Wählen Sie **Bearbeiten** für den Titel der Organisation aus.
5. Geben Sie den neuen Organisationsnamen ein.
6. Klicken Sie auf **Speichern**.

## Vorhandene Organisation oder vorhandenen Bereich löschen
{: #deleteorgs}

Als Kontoeigner können Sie sich an den [{{site.data.keyword.Bluemix_notm}}-Support ![Symbol für externen Link](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} wenden, um eine Organisation zu löschen.

**Hinweis:** Das Löschen von Operationen kann nicht rückgängig gemacht werden. Alle der Organisation zugeordneten Anwendungen und Services gehen verloren.

Sie können einen Bereich von der Seite **Organisationen verwalten** löschen:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, die Sie bearbeiten möchten, und wählen Sie **Details anzeigen** aus. 
3. Ermitteln Sie den Bereich, den Sie löschen möchten, und wählen Sie **Bereich bearbeiten** aus.
4. Klicken Sie auf **Bereich löschen**.

## Mitglieder auflisten
{: #listmembers}

Führen Sie die folgenden Schritte aus, um die Mitglieder für eine bestimmte Organisation aufzulisten:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, deren Mitglieder Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Klicken Sie auf **Organisation bearbeiten**.
4. Sie können die Mitglieder Ihrer Organisation und deren Rollen auf der Registerkarte **Benutzer** anzeigen.

Führen Sie die folgenden Schritte aus, um die Mitglieder für einen bestimmten Bereich aufzulisten:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, deren Mitglieder Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Ermitteln Sie den Bereich, dessen Mitglieder Sie anzeigen möchten, und klicken Sie auf **Bereich bearbeiten**.
4. Sie können die Mitglieder Ihres Bereichs und deren Rollen auf der Registerkarte **Benutzer** anzeigen.

## Kontingent verwalten
{: #managequota}

Als {{site.data.keyword.Bluemix_notm}}-Kontoeigner oder -Organisationsmanager können Sie das verwendete und zugeordnete Kontingent für eine Organisation anzeigen. Das Kontingent stellt die Ressourcengrenzen für die Organisation dar, die beim Erstellen der Organisation zugeordnet wird. Abhängig davon, ob Sie über ein Testkonto oder ein belastbares Konto verfügen, können die für eine Organisation verfügbaren Ressourcen variieren. Jede Anwendung oder jeder Service in einem Bereich der Organisation trägt zur Nutzung des zugeordneten Kontingents bei.

Führen Sie die folgenden Schritte aus, um das verwendete und zugeordnete Kontingent für eine Organisation anzuzeigen:

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, deren Kontingent Sie anzeigen möchten, und klicken Sie auf **Details anzeigen**.
3. Klicken Sie auf **Organisation bearbeiten**.
4. Wenn Bereiche in mehreren Regionen definiert wurden, dann wählen Sie die Region aus, die Sie anzeigen möchten.
5. Klicken Sie auf **Kontingent**. 
6. Standardmäßig wird die Kontingentseite **Cloud Foundry** geöffnet. Sie können die Kontingentdetails für die folgenden Ressourcen anzeigen:
 * SPEICHER
 * SERVICES
 * PLAN
 * PREIS
7. Klicken Sie auf **Container**, um die verwendete und verfügbare Containerkontingentzuordnung anzuzeigen. Die Containerzuordnung variiert abhängig von Ihrem Preistarif. Sie können die Kontingentdetails für die folgenden Ressourcen anzeigen:
 * SPEICHER
 * ÖFFENTLICHE IP
 * DATEIFREIGABEN
8. Klicken Sie auf **Virtuelle Server**, um die virtuellen Maschinen anzuzeigen. 

**Hinweis:** In der {{site.data.keyword.Bluemix_notm}}-Region 'Sydney' stehen keine Container zur Verfügung. 

Weitere Informationen zu Containern finden Sie unter dem Thema [Kontingent](/docs/containers/container_planning_org_ov.html#container_planning_quota) in der Dokumentation zu Containern.
Um das Kontingent zu ändern, das einer Organisation zugeordnet ist, müssen Sie ein Support-Ticket öffnen. Weitere Informationen zum Öffnen eines Support-Tickets finden Sie unter dem Thema [Kundenunterstützung abrufen](/docs/support/index.html#contacting-support). 

## Domänen verwalten
{: #managedomains}

Als Kontoeigner oder Organisationsmanager können Sie die Systemdomäne anzeigen und angepasste Domänen für Anwendungen hinzufügen, die innerhalb der Organisation und ihren Bereichen erstellt wurden. Als Bereichsmanager enthält Ihre Registerkarte **Domänen** für einen Bereich eine schreibgeschützte Liste der Domänen, die dem Bereich zugeordnet sind.

1. Klicken Sie auf **Verwalten** &gt; **Konto** &gt; **Organisationen**. 
2. Ermitteln Sie die Organisation, für die Sie Domänen anzeigen oder bearbeiten möchten. 
3. Wählen Sie **Details anzeigen** für diese Organisation aus.
4. Klicken Sie auf **Organisation bearbeiten**.
5. Klicken Sie auf **Domänen**.

Wenn Sie eine angepasste Domäne hinzufügen möchten, müssen Sie Ihren DNS-Server so konfigurieren, dass er auf die {{site.data.keyword.Bluemix_notm}}-Systemdomäne verweist. Auf diese Weise kann {{site.data.keyword.Bluemix_notm}} eine aus Ihrer angepassten Domäne empfangene Anforderung ordnungsgemäß an Ihre Anwendung weiterleiten. Die Systemdomäne ist für einen Bereich immer verfügbar und angepasste Domänen können auch einem Bereich zugeordnet sein. In einem Bereich erstellte Anwendungen können eine der Domänen verwenden, die für diesen Bereich aufgelistet sind. Weitere Informationen zum Erstellen und Verwenden angepasster Domänen finden Sie unter [Angepasste Domäne verwenden](/docs/manageapps/updapps.html#domain).
