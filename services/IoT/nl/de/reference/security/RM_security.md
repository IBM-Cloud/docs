---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risiko- und Sicherheitsmanagement
{: #RM_security}
Letzte Aktualisierung: 15. November 2016
{: .last-updated}

Mit dem Add-on für das Risiko- und Sicherheitsmanagement können Organisationen die IBM Watson IoT Platform-Sicherheit durch das Erstellen und Durchsetzen der Verbindungssicherheit von Geräten verbessern. Im Rahmen dieses Add-ons werden neben den von Watson IoT Platform verwendeten Benutzer-IDs und Tokens Zertifikate und die TLS-Authentifizierung (TLS, Transport Layer Security) verwendet, um festzulegen, wie und wo Geräte mit der Plattform eine Verbindung herstellen. Während der Kommunikation zwischen Geräten und dem Server wird allen Geräten, die nicht über gültige Zertifikate mit Serverzugriff verfügen, wie im Add-on für Risiko- und Sicherheitsmanagement festgelegt, der Zugriff verweigert, selbst dann, wenn sie gültige Benutzer-IDs und Kennwörter verwenden.

**Hinweis:** Unter 'https://developer.ibm.com/iotplatform/2016/11/02/experience-the-latest-iot-security-capabilities-sign-up-to-our-november-beta-today/' können Sie sich für das Risiko- und Sicherheitsmanagement (Betaprogramm) von IBM Watson IoT registrieren und das Programm aktivieren.

## Verbindungssicherheitsrichtlinie

Die Verbindungssicherheitsrichtlinie legt fest, wie Geräte eine Verbindung zur Plattform herstellen. Sie können Standardverbindungsrichtlinien für alle Gerätetypen sowie angepasste Einstellungen für bestimmte Gerätetypen festlegen. Die Richtlinie kann so eingerichtet werden, dass unverschlüsselte Verbindungen möglich sind, nur TLS-Verbindungen zulässig sind oder Geräte sich mit clientseitigen Zertifikaten authentifizieren müssen. Wenn clientseitige Zertifikate verwendet werden, stellt die Sicherheitsrichtlinie eine zusätzliche Option für die ausschließliche Verwendung des Zertifikats für die Clientauthentifizierung oder einer Kombination aus Clientzertifikat und Client-ID/Authentifizierungstoken bereit.   

Die Verbindungssicherheit kann auch so eingerichtet werden, dass Clients anstelle des bereitgestellten Standardzertifikats ihr eigenes serverseitiges Zertifikat verwenden. Dies kann beispielsweise hilfreich sein, wenn die Benutzergeräte den Server während des TLS-Handshake authentifizieren. In diesem ersten Release des Add-ons für das Risiko- und Sicherheitsmanagement kann der Domänenname des Watson IoT Platfor-Servers nicht geändert werden und muss im Serverzertifikat wie vorgegeben verwendet werden.

## Clientzertifikate

Um Clientzertifikate und den Serverzugriff für Geräte zu konfigurieren, importiert der Systembediener die zugehörigen Zertifikate der Zertifizierungsstelle und des Messaging-Servers in die Watson IoT Platform-Instanz. Der Sicherheitsanalyst konfiguriert dann die Verbindungssicherheitsrichtlinien so, dass die Standardverbindungen zwischen Geräten und der Plattform entweder die Sicherheitsebene 'Nur Zertifikate' oder 'Zertifikate mit Authentifizierungstoken' verwenden. Der Analyst kann verschiedene Richtlinien für unterschiedliche Gerätetypen hinzufügen.

## Richtlinien für Whitelists und Blacklists

Mit Richtlinien für Whitelists und Blacklists können die Positionen gesteuert werden, von denen aus Geräte eine Verbindung zum Unternehmenskonto herstellen dürfen. Eine Blacklist gibt alle IP-Adressen, CIDRs oder Länder an, für die der Serverzugriff verweigert wird, während eine Whitelist bestimmten IP-Adressen expliziten Zugriff einräumt.

## Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement

Abschließend können der Systembediener und der Sicherheitsanalyst über das Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement den allgemeinen Sicherheitsstatus anzeigen. Karten auf dem Dashboard können einen umfassenden Überblick über die Einhaltung von Richtlinien sowie über den Verbindungsstatus von Geräten liefern.
