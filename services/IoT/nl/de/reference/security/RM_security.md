---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-22"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risiko- und Sicherheitsmanagement
{: #RM_security}

Mit dem Add-on für das Risiko- und Sicherheitsmanagement können Organisationen die Sicherheit von {{site.data.keyword.iot_full}} durch das Erstellen, Durchsetzen und Melden der Verbindungssicherheit von Geräten verbessern. Im Rahmen dieses Add-ons werden neben den von {{site.data.keyword.iot_short_notm}} verwendeten Benutzer-IDs und Tokens Zertifikate und die TLS-Authentifizierung (TLS, Transport Layer Security) verwendet, um festzulegen, wie und wo Geräte eine Verbindung zu der Plattform herstellen. Während der Kommunikation zwischen Geräten und dem Server wird allen Geräten, die nicht über gültige Zertifikate mit Serverzugriff verfügen, wie im Add-on für Risiko- und Sicherheitsmanagement festgelegt, der Zugriff verweigert, selbst dann, wenn sie gültige Benutzer-IDs und Kennwörter verwenden.

## Verbindungssicherheitsrichtlinie
{: #connect_policy}

Die Verbindungssicherheitsrichtlinie legt fest, wie Geräte eine Verbindung zur Plattform herstellen und wie sie mit den gebührenfreien und erweiterten Sicherheitsplänen verwendet werden. Sie können Standardverbindungsrichtlinien für alle Gerätetypen sowie angepasste Einstellungen für bestimmte Gerätetypen festlegen. Die Richtlinie kann so eingerichtet werden, dass unverschlüsselte Verbindungen möglich sind, nur TLS-Verbindungen zulässig sind oder Geräte sich mit clientseitigen Zertifikaten authentifizieren müssen.

Wenn Sie einen Standardsicherheitsplan verwenden, sind keine Verbindungsrichtlinien verfügbar. Informationen zum Konfigurieren von Sicherheitsrichtlinien für Verbindungen finden Sie in [Sicherheitsrichtlinien konfigurieren](set_up_policies.html).

Die Verbindungssicherheit kann auch so eingerichtet werden, dass Clients anstelle des bereitgestellten Standardzertifikats ihr eigenes serverseitiges Zertifikat verwenden. Dies kann beispielsweise hilfreich sein, wenn die Benutzergeräte den Server während des TLS-Handshakes authentifizieren. In diesem ersten Release des Add-ons für das Risiko- und Sicherheitsmanagement kann der Domänenname des {{site.data.keyword.iot_short_notm}}-Servers nicht geändert werden und muss im Serverzertifikat wie vorgegeben verwendet werden.



## Clientzertifikate
{: #certificates}

Um Clientzertifikate und den Serverzugriff für Geräte zu konfigurieren, importiert der Systembediener die zugehörigen Zertifikate der Zertifizierungsstelle (CA-Zertifikate) und des Messaging-Servers in {{site.data.keyword.iot_short_notm}}. Der Sicherheitsanalyst konfiguriert dann die Verbindungssicherheitsrichtlinien so, dass die Standardverbindungen zwischen Geräten und der Plattform entweder die Sicherheitsebene 'Nur Zertifikate' oder 'Zertifikate mit Authentifizierungstoken' verwenden. Der Analyst kann verschiedene Richtlinien für unterschiedliche Gerätetypen hinzufügen.

Informationen zum Konfigurieren von Zertifikaten finden Sie in [Zertifikate konfigurieren](set_up_certificates.html).

## Richtlinien für Blacklists und Whitelists
{: #wl_bl}

Mit Richtlinien für Blacklists und Whitelists können die Positionen gesteuert werden, von denen aus Geräte eine Verbindung zum Konto der Organisation herstellen dürfen. Eine Blacklist gibt alle IP-Adressen, CIDRs oder Länder an, für die der Serverzugriff verweigert wird, während eine Whitelist bestimmten IP-Adressen expliziten Zugriff einräumt.

Informationen zum Konfigurieren von Richtlinien für Blacklists und Whitelists finden Sie in [Blacklists und Whitelists konfigurieren](set_up_policies.html#config_black_white).

## Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement
{: #dashboard}

Abschließend können der Systembediener und der Sicherheitsanalyst über das Dashboard des Add-ons für das Risiko- und Sicherheitsmanagement den allgemeinen Sicherheitsstatus anzeigen. Karten auf dem Dashboard können einen umfassenden Überblick über die Einhaltung von Richtlinien sowie über den Verbindungsstatus von Geräten liefern.
