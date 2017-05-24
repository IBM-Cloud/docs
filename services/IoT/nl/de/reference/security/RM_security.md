---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risiko- und Sicherheitsmanagement
{: #RM_security}

Sie können die Sicherheit verbessern, um das Erstellen, Durchsetzen und Melden der Verbindungssicherheit von Geräten zu ermöglichen. Dank dieser erweiterten Sicherheit werden neben den von {{site.data.keyword.iot_short_notm}} verwendeten Benutzer-IDs und Tokens Zertifikate und die TLS-Authentifizierung (TLS, Transport Layer Security) verwendet, um festzulegen, wie und wo Geräte eine Verbindung zu der Plattform herstellen. Sind Zertifikate aktiviert, wird während der Kommunikation zwischen Geräten und dem Server allen Geräten, die nicht über gültige Zertifikate mit Serverzugriff verfügen, wie in den Sicherheitseinstellungen konfiguriert, der Zugriff verweigert, selbst wenn sie über gültige Benutzer-IDs und Kennwörter verfügen.

## Clientzertifikate
{: #certificates}

Um Clientzertifikate und den Serverzugriff für Geräte zu konfigurieren, importiert der Systembediener die zugehörigen Zertifikate der Zertifizierungsstelle (CA-Zertifikate) und des Messaging-Servers in {{site.data.keyword.iot_short_notm}}. Der Sicherheitsanalyst konfiguriert dann die Verbindungssicherheitsrichtlinien so, dass die Standardverbindungen zwischen Geräten und der Plattform entweder die Sicherheitsebene 'Nur Zertifikate' oder 'Zertifikate mit Authentifizierungstoken' verwenden. Der Analyst kann verschiedene Richtlinien für unterschiedliche Gerätetypen hinzufügen.

Informationen zum Konfigurieren von Zertifikaten finden Sie in [Zertifikate konfigurieren](set_up_certificates.html).

## Organisationspläne und Sicherheitsrichtlinien
Die erweiterten Sicherheitsrichtlinien ermöglichen Organisationen, mithilfe von Verbindungsrichtlinien sowie Blacklist- und Whitelist-Richtlinien festzulegen, wie Geräte verbunden und bei der Plattform authentifiziert werden. Welche Optionen für Sicherheitsrichtlinien in einer Organisation verfügbar sind, hängt vom Plantyp der Organisation ab:

**Standardplan:**
- Systembediener können Verbindungsrichtlinien mit den folgenden Optionen konfigurieren:
    - TLS Optional 
    - TLS mit Tokenauthentifizierung
    - TLS mit Token- und Clientzertifikatsauthentifizierung

**Advanced Security Plan (ASP) oder Lite-Plan:** 
- Systembediener können Verbindungsrichtlinien mit den folgenden Optionen konfigurieren:
    - TLS Optional 
    - TLS mit Tokenauthentifizierung
    - TLS mit Clientzertifikatsauthentifizierung
    - TLS mit Token- und Clientzertifikatsauthentifizierung
    - TLS mit Clientzertifikat oder Token
- Systembediener können Blacklists oder Whitelists konfigurieren.

## Verbindungsrichtlinien
{: #connect_policy}

Die Verbindungsrichtlinien geben vor, wie Geräte mit der Plattform verbunden werden. Sie können Standardverbindungsrichtlinien für alle Gerätetypen festlegen und angepasste Einstellungen für bestimmte Gerätetypen erstellen. Die Richtlinie kann so eingerichtet werden, dass unverschlüsselte Verbindungen möglich sind, nur TLS-Verbindungen zulässig sind oder Geräte sich mit clientseitigen Zertifikaten authentifizieren müssen.

Informationen zum Konfigurieren von Sicherheitsrichtlinien für Verbindungen finden Sie in [Sicherheitsrichtlinien konfigurieren](set_up_policies.html).

Die Verbindungssicherheit kann auch so eingerichtet werden, dass Systembediener anstelle des bereitgestellten Standardzertifikats ihr eigenes Messaging-Serverzertifikat verwenden. Dies kann beispielsweise hilfreich sein, wenn die Benutzergeräte den Server während des TLS-Handshakes authentifizieren. Es werden nur angepasste Messaging-Serverzertifikate unterstützt, die dieselbe Domäne wie der ursprüngliche IoTP-Messaging-Server verwenden (<Organisations-ID>.messaging.internetofthings.ibmcloud.com).

## Richtlinien für Blacklists und Whitelists
{: #wl_bl}

Mit Richtlinien für Blacklists und Whitelists können die Positionen gesteuert werden, von denen aus Geräte eine Verbindung zum Konto der Organisation herstellen dürfen. Eine Blacklist gibt alle IP-Adressen, CIDRs oder Länder an, für die der Serverzugriff verweigert wird, während eine Whitelist bestimmten IP-Adressen expliziten Zugriff einräumt.

Informationen zum Konfigurieren von Richtlinien für Blacklists und Whitelists finden Sie in [Blacklists und Whitelists konfigurieren](set_up_policies.html#config_black_white).

## Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement
{: #dashboard}

Abschließend können der Systembediener und der Sicherheitsanalyst über das Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement den allgemeinen Sicherheitsstatus anzeigen. Karten auf dem Dashboard können einen umfassenden Überblick über die Einhaltung von Richtlinien sowie über den Verbindungsstatus von Geräten liefern.
