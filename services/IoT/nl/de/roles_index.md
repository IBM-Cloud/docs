---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Rollen für Benutzer, Anwendungen und Gateways

Rollen sind Gruppen von Berechtigungen, die Sie zum Erteilen oder Einschränken von Zugriff auf bestimmte Operationen verwenden können. Sie können Rollen verwenden, um Berechtigungen für Gruppen aus Benutzern, Anwendungen und Gateways zu verwalten.
{:shortdesc}

## Benutzerrollen
{: #user_roles}

Sie können Benutzerrollen zuordnen, wenn Sie einen Benutzer in {{site.data.keyword.iot_full}} hinzufügen, einladen oder registrieren. Sie können Benutzerrollen mithilfe des {{site.data.keyword.iot_short_notm}}-Dashboards auch jederzeit zuordnen oder ändern. Weitere Informationen zur Zuordnung einer Rolle zu einem Benutzer finden Sie in [Benutzerrollen verwalten](managing_user_roles.html).

Folgende standardmäßigen Benutzerrollen sind verfügbar:

Benutzerrolle | Beschreibung
------------- | -------------
Administrator | Eine 'Superuser'-Rolle, die Zugriff auf alle benutzerbezogenen APIs gewährt. Administratoren können nicht auf Operationen zugreifen, die auf Geräte und Anwendungen eingeschränkt sind.
Operator | Für Front-End-Benutzer der Organisation bestimmt. Gewährt Zugriff auf den größten Teil der Organisationsoperationen, Zugriffssteuerungsoperationen, Analyseoperationen, Operationen von Drittanbietern und Risikomanagementoperationen.
Entwickler | Gewährt unbeschränkten Zugriff auf Geräteoperationen, Protokolloperationen, Operationen der Archivierungsfunktion, Analyseoperationen und Operationen von Drittanbieterservices. Die Rolle bietet eingeschränkten Zugriff auf Operationen der Organisation, der Zugriffssteuerung und des Risikomanagements.
Analyst | Gewährt Zugriff auf Analyseoperationen, einschließlich der Erstellung, Aktualisierung und dem Löschen von Regeln, Aktionen und Schemas.
Leser | Die Rolle des Standardbenutzers. Gewährt eingeschränkten Zugriff auf Operationen, die für alle Benutzer verfügbar sind.

Weitere Informationen zu den Benutzerrollen finden Sie in [Benutzerrollen](reference/roles_access.html).

## Anwendungsrollen
{: #application_roles}
Sie können Anwendungsrollen zuordnen, um Ihren Anwendungen den Zugriff auf bestimmte Operationen zu gewähren oder zu verweigern. Alle Anwendungsrollen verweigern Zugriff auf folgende Operationen:

- Alle Operationen des Risikomanagements
- Konfigurieren von Speicherparametern
- Konfigurieren von Authentifizierungsprovidern
- Erstellung, Aktualisierung oder Löschen der E-Mail-Konfiguration

Folgende standardmäßigen Benutzerrollen sind verfügbar:

Anwendungsrolle | Beschreibung
------------- | -------------
Standard | Die standardmäßige Anwendungsrolle. Gewährt Zugriff auf den größten Teil der Anwendungsoperationen, jedoch nicht auf Benutzer- oder Rollenoperationen.   
Operationen | Gewährt Zugriff auf ein breites Spektrum an Operationen, verweigert jedoch den Zugriff auf Subskriptions- oder Publizierungsoperationen.
Vertrauenswürdige Backend-Anwendung | Bestimmt für Anwendungen, die keine Interaktion vom Systemoperator erfordern. Verweigert Zugriff auf Operationen des Gerätemanagements, auf Organisationsoperationen, Rollenoperationen oder Erweiterungsoperationen.
Datenprozessor | Bestimmt für Anwendungen, die Analysen und Datenverarbeitung ausführen. Datenprozessoranwendungen wird eingeschränkter Zugriff auf Organisationsoperationen und Benutzeroperationen gewährt; sie haben jedoch vollständigen Zugriff auf Analyseoperationen einschließlich dem Erstellen und Verwalten von Rollen, Aktionen und Schemas.
Visualisierung | Bestimmt für Anwendungen, die für das Generieren von Datenvisualisierungen zuständig sind. Visualisierungsanwendungen haben Zugriff auf Live-Datenoperationen und Live-Dashboard-Operationen sowie auf gespeicherte Datenoperationen bzw. Dashboardoperationen.
Gerät | Bestimmt für Anwendungen, die die Rolle von Geräten annehmen; das bedeutet, sie stellen eine Quelle von Daten bereit, die an {{site.data.keyword.iot_short_notm}} in einer Form gesendet werden, als handele es sich bei den Anwendungen um ein Gerät. Geräteanwendungen wird nur eingeschränkter Zugriff auf Operationen gewährt.

Weitere Informationen dazu, welchen Zugriff auf Operationen Anwendungsrollen haben, finden Sie in [Anwendungsrollen](reference/app_roles_access.html).

## Gateway-Rollen
{: #gateway_roles}
Gateways haben eine begrenzte Anzahl von Rollen, die die Definition des Gateways sowie die Möglichkeit regeln, Geräte für {{site.data.keyword.iot_short_notm}} zu registrieren.

Folgende standardmäßige Gateway-Rollen sind verfügbar:

Gateway-Rolle | Beschreibung
------------- | -------------
Standard | Die Rolle des Standardgateways. Hiermit wird eingeschränkter Zugriff auf Operationen gewährt.
Privilegiert | Für vertrauenswürde Gateways bestimmt, ermöglicht privilegierten Gateways, Geräte zu {{site.data.keyword.iot_short_notm}} hinzuzufügen. Gewährt Zugriff auf die relevanten Operationen zum Hinzufügen, Aktualisieren und Verwalten von Geräten und Geräteeigenschaften, bietet jedoch keinen Zugriff auf andere Operationen.  

Weitere Informationen dazu, welchen Zugriff auf Operationen Gateway-Rollen haben, finden Sie in [Gateway-Rollen](reference/gateway_roles_access.html).
