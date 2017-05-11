---

copyright:

  years: 2015, 2017
lastupdated: "2017-03-08"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Benutzer einladen, Zugriff zuweisen und verwalten
{: #iamuserinv}

Sie können Benutzer von {{site.data.keyword.Bluemix_notm}}-Services, von Anwendungen und in der gesamten {{site.data.keyword.Bluemix_notm}}-Infrastruktur von einer einzigen Position aus einladen. Bei der Einladung weisen Sie den Benutzern Zugriffsrechte, Rollen und Richtlinien sowie die Konten oder Organisationen (oder beides) zu, auf die sie zugreifen können. Abhängig von den Zugriffsoptionen, zu deren Verwaltung Sie berechtigt sind, können Sie Benutzer aus dem gesamten Konto oder der gesamten Organisation einladen und mit Zugriffsrechten ausstatten. Als Kontoeigner können Sie Ihrem Konto Zugriffsoptionen für einen Benutzer unabhängig von der Rolle zuweisen, wenn sowohl Sie als auch der Benutzer Mitglieder sind. 
{:shortdesc}

Zum Einladen von Benutzern oder zur Verwaltung von Benutzereinladungen in Ihrem Konto klicken Sie in der Menüleiste auf **Verwalten** &gt; **Konto** &gt; **Benutzer**. Das Fenster 'Benutzer' zeigt eine Liste der Benutzer mit den zugehörigen E-Mail-Adressen und Angaben zum aktuellen Status in den Konten an, die Sie verwalten. 

Zum Einladen von Benutzern und Verwalten ausstehender Benutzer müssen Sie entweder ein Kontoeigner oder ein Organisationsmanager sein oder über die Infrastrukturberechtigungen zum Hinzufügen von Benutzern verfügen.  Sie können Benutzer einladen, Einladungen abbrechen und anstehende Einladungen erneut an eingeladene Benutzer senden. Sie können einen einzelnen Benutzer einladen, wenn Sie denselben Zugriff für alle Mitglieder in einer Gruppe bereitstellen, und Sie können mehrere Benutzer gleichzeitig einladen.

Zum Einladen von Benutzern klicken Sie auf die Option **Benutzer einladen**, geben die E-Mail-Adresse oder die IBMid (IBM ID) des Benutzers an und fügen ihn einer oder mehreren Zugriffsoptionen hinzu, die Sie verwalten. Sie müssen mindestens eine Zugriffsoption zuweisen und die Einstellungen für den Benutzer in jeder zugewiesenen Zugriffsoption konfigurieren. Für alle weiteren Zugriffsoptionen, die Sie nicht hinzufügen und konfigurieren, wird der Standardwert *Kein Zugriff* zugewiesen. Abhängig von den Zugriffsoptionen, zu deren Verwaltung Sie berechtigt sind, können Ihnen die folgenden Optionen angezeigt werden:

**Durch Identity and Access aktivierte Services**:
Wählen Sie diese Option aus, um die Services, Regionen, Serviceinstanzen und Rollen für die Benutzer zuzuweisen, die Sie einladen.
**Hinweis:** Wenn Sie die Option **Der Zugriff wird automatisch erteilt, wenn neue Services hinzugefügt werden** auswählen, werden Sie nicht benachrichtigt, um jeden neuen {{site.data.keyword.Bluemix_notm}}-Service für diesen Benutzer abwählen zu können, wenn Services später hinzugefügt werden.

**Cloud Foundry-Zugriff:**
Wählen Sie diese Option aus, um die Services, Regionen, Bereiche und Bereichsrollen für Benutzer zuzuweisen, die Sie einladen. Weitere spezielle Informationen zu diesen Einstellungen finden Sie unter [Benutzerrollen](/docs/admin/users_roles.html#userrolesinfo). Sie können mehrere Rollen hinzufügen, jedoch jeweils nur eine gleichzeitig.

**Infrastructure-Zugriff:**
Sie können dem Benutzer die folgenden Infrastrukturberechtigungen zuweisen: 
<dl>
<dt>Nur anzeigen</dt>
<dd>Benutzer mit dieser Berechtigung können Elemente im System nur anzeigen.</dd>
<dt>Basisbenutzer</dt>
<dd>Benutzer mit dieser Berechtigung können Basisaktionen im System ausführen, wie zum Beispiel Tickets hinzufügen und Geräte verwalten.</dd>
<dt>Superuser</dt>
<dd>Benutzer mit dieser Berechtigung können alle verfügbaren Aktionen im System ausführen.</dd>
</dl>
**Hinweis:** Die tatsächlichen zugewiesenen Berechtigungen werden automatisch auf die Untergruppe von Berechtigungen eingeschränkt, die Sie haben.

Wenn Sie mehreren Benutzern denselben Zugriff erteilen, können Sie die Option **Mehrere Benutzer einladen** auswählen, um eine Liste der einzuladenden Benutzer einzugeben. Trennen Sie die Benutzer-IDs durch Kommas.  

Wenn Sie entscheiden, dass ein Benutzer keinen Zugriff benötigt, können Sie eine Einladung für beliebige Benutzer abbrechen, die mit dem Status **Verarbeitung läuft** (Processing) oder **Anstehend** (Pending) in der Spalte  **Status** angezeigt werden. Wenn ein eingeladener Benutzer keine Einladung empfangen hat, können Sie die Einladung an jeden Benutzer mit dem Status **Anstehend** erneut senden.  Diese Optionen sind für Benutzer im entsprechenden Status über das Menü **Aktionen** im Fenster 'Benutzer' verfügbar.

Spezielle Informationen zur Konfiguration von Zugriffsrechten für Benutzer, einschließlich Rollen und Richtlinien, finden Sie unter [Benutzerkonten und Benutzerzugriff verwalten](/docs/admin/iamusermanage.html).
