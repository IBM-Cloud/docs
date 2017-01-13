---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Sicherheitsrichtlinien konfigurieren
{: #set_up_policies.md}
Letzte Aktualisierung: 15. November 2016
{: .last-updated}

Ein Sicherheitsanalyst kann die Verbindungssicherheitsrichtlinien sowie die Black- oder Whitelists konfigurieren.

## Verbindungsrichtlinien konfigurieren

Sie können die Standardsicherheitsebene festlegen, die auf alle Geräte angewendet wird. Anschließend können Sie angepasste Sicherheitseinstellungen für bestimmte Geräte hinzufügen.

1. Klicken Sie auf der Seite **Richtlinien** des Add-ons für Risiko- und Sicherheitsmanagement neben **Verbindungsmanagement** auf **Konfigurieren**.
2. Wählen Sie auf der Seite **Verbindungssicherheit** die Standardsicherheitsebene der Verbindung aus der Dropdown-Liste aus. Der von Ihnen hier ausgewählte Wert wird auf alle Geräte angewendet, mit Ausnahme von Geräten, die angepasste Verbindungseinstellungen aufweisen. Diese Richtlinien wirken sich auf die Art und Weise aus, wie Geräte eine Verbindung zum Server herstellen; dabei werden keine Einstellungen auf dem Gerät geändert oder Nachrichten an das Geräte gesendet. Sie können eine der folgenden Sicherheitsebenen als Standardeinstellung auswählen:
    - TLS Optional
    - TLS mit Tokenauthentifizierung
    - TLS mit Clientzertifikatsauthentifizierung
    - TLS mit Token- Clientzertifikatsauthentifizierung

Basierend auf der von Ihnen ausgewählten Sicherheitsebene enthält die Tabelle die Anzahl der betroffenen Geräte und den vorhergesagte Umfang der Einhaltung auf der angegebenen Sicherheitsebene.

3. Falls erforderlich, klicken Sie auf **Angepasste Verbindung hinzufügen** und wählen Sie die Gerätetypen und angepassten Sicherheitsebenen aus. Der vorhergesagte Wert wird so aktualisiert, dass er die durch die angepassten Sicherheitseinstellungen resultierenden Änderungen widerspiegelt.
4. Klicken Sie auf **Speichern**.  

## Blacklists und Whitelists konfigurieren

Schränken Sie den Zugriff auf den Server von bestimmten Geräten durch die Verwendung einer Blacklist ein oder gewähren Sie mithilfe einer Whitelist den Serverzugriff für bestimmte Geräte. Sie können entweder eine Blacklist oder eine Whitelist verwenden, nicht jedoch beide gemeinsam.

### Blacklist konfigurieren

1. Klicken Sie auf der Seite **Richtlinien** des Add-ons für Risiko- und Sicherheitsmanagement im Abschnitt **Blacklist** auf **Konfigurieren**.
2. Klicken Sie auf der Seite **Blacklist** auf **Zu Blacklist hinzufügen**.
3. Führen Sie im Fenster **Zu Blacklist hinzufügen** eine der folgenden Aktionen durch:
    - Geben Sie auf der Registerkarte **IP-Adresse/Bereich** die IP-Adressen der Geräte ein, die blockiert werden sollen, oder Bereiche von IP-Adressen für mehrere aufeinander folgende Geräte.
    - Geben Sie auf der Registerkarte **CIDR** einen notierten CIDR-Block (CIDR, Classless Inter-Domain Routing) ein.
    - Geben Sie auf der Registerkarte **Land** das Land an, für das Sie alle Geräte blockieren möchten. 
4. Klicken Sie im Fenster **Zu Blacklist hinzufügen** auf **Speichern**.
5. Überprüfen Sie die Liste der blockierten Geräte. Alle Geräte aus der Liste können basierend auf der IP-Adresse, CIDR oder dem Land keine Verbindung mit dem Watson IoT Platform-Server herstellen.
6. Klicken Sie auf **Speichern**.

### Whitelist konfigurieren
1. Klicken Sie auf der Seite **Richtlinien** des Add-ons für Risiko- und Sicherheitsmanagement neben **Whitelist** auf **Konfigurieren**.
2. Klicken Sie auf der Seite **Whitelist** auf **Zu Whitelist hinzufügen**.
3. Führen Sie im Fenster **Zu Whitelist hinzufügen** eine der folgenden Aktionen durch:
    - Geben Sie auf der Registerkarte **IP-Adresse/Bereich** die IP-Adressen der Geräte ein, auf die der Zugriff möglich sein soll, oder Bereiche von IP-Adressen für mehrere aufeinander folgende Geräte.
    - Geben Sie auf der Registerkarte **CIDR** einen notierten CIDR-Block (CIDR, Classless Inter-Domain Routing) ein.
    - Geben Sie auf der Registerkarte **Land** das Land an, für das Sie die Verbindung für alle Geräte zulassen möchten. 
4. Klicken Sie im Fenster **Zu Whitelist hinzufügen** auf **Speichern**.
5. Überprüfen Sie die Liste der zulässigen Geräte. Alle Geräte aus der Liste können basierend auf der IP-Adresse, CIDR oder dem Land eine Verbindung mit dem Watson IoT Platform-Server herstellen.
6. Klicken Sie auf **Speichern**.
