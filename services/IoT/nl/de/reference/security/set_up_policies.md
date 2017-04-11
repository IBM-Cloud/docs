---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-15"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Sicherheitsrichtlinien konfigurieren
{: #set_up_policies.md}

Wenn ein Advanced Security Plan (ASP) für eine Organisation verwendet wird, kann ein Sicherheitsanalyst die Verbindungssicherheitsrichtlinien sowie die Black- oder Whitelists konfigurieren. Wenn ein Standardplan verwendet wird, kann der Analyst Verbindungsrichtlinien - mit weniger Optionen - konfigurieren, aber er kann keine Blacklists oder Whitelists konfigurieren.

## Verbindungsrichtlinien für erweiterte Sicherheit konfigurieren
{: #config_connect}

Sie können die Standardsicherheitsebene festlegen, die auf alle Geräte angewendet wird. Anschließend können Sie angepasste Sicherheitseinstellungen für bestimmte Geräte hinzufügen.

1. Klicken Sie auf der Seite **Richtlinien** neben **Verbindungssicherheit** auf **Konfigurieren**.
2. Wählen Sie unter **Verbindungssicherheit** die Standardsicherheitsebene der Verbindung aus der Dropdown-Liste aus. Der von Ihnen hier ausgewählte Wert wird auf alle Geräte angewendet, mit Ausnahme von Geräten, die angepasste Verbindungseinstellungen aufweisen. Diese Richtlinien wirken sich auf die Art und Weise aus, wie Geräte eine Verbindung zum Server herstellen; dabei werden keine Einstellungen auf dem Gerät geändert oder Nachrichten an das Geräte gesendet. Sie können eine der folgenden Sicherheitsebenen als Standardeinstellung auswählen:
    - TLS Optional
    - TLS mit Tokenauthentifizierung
    - TLS mit Clientzertifikatsauthentifizierung
    - TLS mit Token- und Clientzertifikatsauthentifizierung
    - TLS mit Clientzertifikat oder Token
3. Falls erforderlich, klicken Sie auf **Angepasste Verbindung hinzufügen** und wählen Sie die Gerätetypen und angepassten Sicherheitsebenen aus. 
3. Klicken Sie auf die Option zum Aktualisieren der Einhaltung. Basierend auf der von Ihnen ausgewählten Sicherheitsebene enthält die aktualisierte Tabelle die Anzahl der betroffenen Geräte und den vorhergesagte Umfang der Einhaltung auf der angegebenen Sicherheitsebene.
4. Klicken Sie auf **Speichern**.  

**Hinweis:**
Sie können auch über die Seite **Allgemein** unter **Einstellungen** auf die Verbindungssicherheitseinstellungen zugreifen. Klicken Sie auf **Verbindungssicherheitsrichtlinie öffnen**.

## Verbindungsrichtlinien für Standardsicherheit konfigurieren
{: #config_connect_standard}

Für Organisationen, die Standardsicherheit verwenden, ändern Sie die Sicherheitseinstellungen auf der Seite **Allgemein** unter **Einstellungen**. Sie können die Standardsicherheitsebene festlegen, die auf alle Geräte angewendet wird.

1. Wählen Sie unter **Einstellungen** die Option **Allgemein** aus.
2. Wählen Sie unter **Verbindungssicherheit** die Standardsicherheitsebene der Verbindung aus der Dropdown-Liste aus. Der von Ihnen hier ausgewählte Wert wird auf alle Geräte angewendet. Diese Richtlinien wirken sich auf die Art und Weise aus, wie Geräte eine Verbindung zum Server herstellen; dabei werden keine Einstellungen auf dem Gerät geändert oder Nachrichten an das Geräte gesendet. Sie können eine der folgenden Sicherheitsebenen als Standardeinstellung auswählen:
    - TLS Optional
    - TLS mit Tokenauthentifizierung
    - TLS mit Token- und Clientzertifikatsauthentifizierung
4. Klicken Sie auf **Speichern**.  

## Blacklists und Whitelists konfigurieren
{: #config_black_white}

Organisationen, die erweiterte Sicherheit verwenden, können den Zugriff auf den Server von bestimmten Geräten durch die Verwendung einer Blacklist einschränken. Oder sie gewähren mithilfe einer Whitelist den Serverzugriff für bestimmte Geräte. Sie können entweder eine Blacklist oder eine Whitelist verwenden, nicht jedoch beide gemeinsam.

### Blacklist konfigurieren
{: #config_blacklist}

1. Klicken Sie auf der Seite **Richtlinien** im Abschnitt **Blacklist** auf **Konfigurieren**.
2. Klicken Sie auf der Seite **Blacklist** auf **Zu Blacklist hinzufügen**.
3. Führen Sie im Fenster **Zu Blacklist hinzufügen** eine der folgenden Aktionen durch:
    - Geben Sie auf der Registerkarte **IP-Adresse/Bereich** die IP-Adressen der Geräte ein, die blockiert werden sollen, oder Bereiche von IP-Adressen für mehrere aufeinander folgende Geräte.
    - Geben Sie auf der Registerkarte **CIDR** einen notierten CIDR-Block (CIDR, Classless Inter-Domain Routing) ein.
    - Geben Sie auf der Registerkarte **Land** das Land an, für das Sie alle Geräte blockieren möchten.
4. Klicken Sie im Fenster **Zu Blacklist hinzufügen** auf **Speichern**.
5. Überprüfen Sie die Liste der blockierten Geräte. Alle Geräte aus der Liste können basierend auf der IP-Adresse, CIDR oder dem Land keine Verbindung mit dem {{site.data.keyword.iot_short_notm}}-Server herstellen.
6. Klicken Sie auf **Speichern**.
7. Aktivieren Sie die Blacklist. War eine Whitelist aktiviert, wird diese inaktiviert.

### Whitelist konfigurieren
{: #config_whitelist}

1. Klicken Sie auf der Seite **Richtlinien** neben **Whitelist** auf **Konfigurieren**.
2. Klicken Sie auf der Seite **Whitelist** auf **Zu Whitelist hinzufügen**.
3. Führen Sie im Fenster **Zu Whitelist hinzufügen** eine der folgenden Aktionen durch:
    - Geben Sie auf der Registerkarte **IP-Adresse/Bereich** die IP-Adressen der Geräte ein, auf die der Zugriff möglich sein soll, oder Bereiche von IP-Adressen für mehrere aufeinander folgende Geräte.
    - Geben Sie auf der Registerkarte **CIDR** einen notierten CIDR-Block (CIDR, Classless Inter-Domain Routing) ein.
    - Geben Sie auf der Registerkarte **Land** das Land an, für das Sie die Verbindung für alle Geräte zulassen möchten.
4. Klicken Sie im Fenster **Zu Whitelist hinzufügen** auf **Speichern**.
5. Überprüfen Sie die Liste der zulässigen Geräte. Alle Geräte aus der Liste können basierend auf der IP-Adresse, CIDR oder dem Land eine Verbindung mit dem {{site.data.keyword.iot_short_notm}}-Server herstellen.
6. Klicken Sie auf **Speichern**.
7. Aktivieren Sie die Whitelist. War eine Blacklist aktiviert, wird diese inaktiviert.
