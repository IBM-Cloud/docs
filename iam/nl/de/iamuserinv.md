---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-17"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Benutzer einladen
{: #iamuserinv}

Sie können Benutzer von {{site.data.keyword.Bluemix_notm}}-Services, von Anwendungen und in der gesamten {{site.data.keyword.Bluemix_notm}}-Infrastruktur von einer einzigen Position aus einladen. Zum Einladen von Benutzern und Verwalten ausstehender Benutzer müssen Sie entweder ein Kontoeigner oder ein Organisationsmanager sein oder über die Infrastructure-Berechtigungen zum Hinzufügen von Benutzern verfügen. Sie können Benutzer einladen, Einladungen abbrechen und anstehende Einladungen erneut an eingeladene Benutzer senden. Sie können einen einzelnen Benutzer einladen, wenn Sie denselben Zugriff für alle Mitglieder in einer Gruppe bereitstellen, und Sie können mehrere Benutzer gleichzeitig einladen.
{:shortdesc}

Führen Sie die folgenden Schritte aus, um Benutzer einzuladen oder Einladungen in Ihrem Konto zu verwalten:

1. Klicken Sie in der Menüleiste auf **Verwalten** &gt; **Sicherheit** &gt; **Identity & Access** &gt; **Benutzer**. Das Fenster 'Benutzer' zeigt eine Liste der Benutzer mit den zugehörigen E-Mail-Adressen und Angaben zum aktuellen Status in den Konten an, die Sie verwalten. 
2. Klicken Sie auf **Benutzer einladen**. 
3. Geben Sie die E-Mail-Adresse oder IBMid des Benutzers an. Wenn Sie mehreren Benutzern denselben Zugriff erteilen, können Sie die Option **Mehrere Benutzer einladen** auswählen, um eine Liste der einzuladenden Benutzer einzugeben. Trennen Sie die Benutzer-IDs durch Kommas. 
4. Fügen Sie eine oder mehrere der von Ihnen verwalteten Zugriffsoptionen hinzu. Sie müssen mindestens eine Zugriffsoption zuweisen und die Einstellungen für den Benutzer in jeder zugewiesenen Zugriffsoption konfigurieren. Für alle weiteren Zugriffsoptionen, die Sie nicht hinzufügen und konfigurieren, wird der Standardwert *Kein Zugriff* zugewiesen. Abhängig von den Zugriffsoptionen, zu deren Verwaltung Sie berechtigt sind, können Ihnen die folgenden Optionen angezeigt werden: **Durch Identity and Access aktivierte Services**, **Cloud Foundry-Zugriff**, **Infrastructure-Zugriff**. Weitere Informationen finden Sie unter [Benutzerzugriff zuweisen](/docs/iam/assignaccess.html).

Wenn Sie entscheiden, dass ein Benutzer keinen Zugriff benötigt, können Sie eine Einladung für beliebige Benutzer abbrechen, die mit dem Status **Verarbeitung läuft** (Processing) oder **Anstehend** (Pending) in der Spalte **Status** angezeigt werden. Wenn ein eingeladener Benutzer keine Einladung empfangen hat, können Sie die Einladung an jeden Benutzer mit dem Status **Anstehend** erneut senden.  
