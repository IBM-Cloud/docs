---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-02"
---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Zertifikate konfigurieren
{: #set_up_certificates}

Zertifikate werden für die Geräeteauthentifizierung oder zum Ersetzen des {{site.data.keyword.iot_full}}-Standardserverzertifikats für die MQTT-Nachrichtenübertragung verwendet. Geräten, die über keine gültigen und signierten Zertifikate verfügen, wird der Zugriff verweigert und eine Kommunikation mit dem Server ist nicht möglich.

Um Zertifikate und den Serverzugriff für Geräte zu konfigurieren, registriert der Systembediener die zugehörigen Zertifikate der Zertifizierungsstelle und optional die Zertifikate des Messaging-Servers in {{site.data.keyword.iot_short_notm}}.

## Zertifikatsanforderungen
{: #cert_reqs}

### Zertifikate einer Zertifizierungsstelle
Zertifikate einer Zertifizierungsstelle (CA-Zertifikate) ermöglichen der Organisation das Erkennen vertrauenswürdiger Clientzertifikate für Geräte und damit den betreffenden Geräten das Herstellen einer Verbindung zu dem Server. Ein CA-Zertifikat kann eine Zertifikatsperrliste (Certificate Revocation List, CRL) verwenden. Die CRL muss genau in dem Moment erreichbar sein, in dem die Zertifizierungsstelle zur Plattform hinzugefügt wird; andernfalls wird das CA-Zertifikat abgelehnt.

Wenn Sie ein CA-Zertifikat hinzufügen oder das Zertifikat des Messaging-Servers ersetzen, müssen alle Geräte mithilfe eines MQTT-Clients eine Verbindung herstellen, der SNI (Server Name Indication) unterstützt, damit der Server die entsprechenden Zertifizierungsstellen verwenden kann, um das Gerät zu authentifizieren.

Wenn Sie ein CA-Zertifikat hinzufügen und das Add-on für Risiko- und Sicherheitsmanagement nicht aktiviert ist, stellen alle Geräte mit der Verbindungsrichtlinie für TLS mit Token- und Clientzertifikatsauthentifizierung eine Verbindung her. Wenn das Add-on für Risiko- und Sicherheitsmanagement aktiviert ist, können Sie verschiedene Verbindungsrichtlinien konfigurieren. Informationen zum Konfigurieren von Sicherheitsrichtlinien für Verbindungen finden Sie in [Sicherheitsrichtlinien konfigurieren](set_up_policies.html).

### Client- oder Gerätezertifikate
Einzelclientzertifikate oder Gerätezertifikate verbleiben auf den Geräten und werden nicht in die Plattform hochgeladen. Das zum Signieren aller Gerätezertifikate verwendete Signaturzertifikat der Zertifizierungsstelle wird als einziges Zertifikat in die Plattform hochgeladen. Wenn Sie selbst signierte Serverzertifikate verwenden, müssen Sie die Stamm- und Zwischenzertifizierungsstelle (ca.pem) hochladen, die zum Signieren des Clientzertifikats (cert.pem) verwendet wird.

Für das Einzelgerätezertifikat, das Sie mit dem CA-Zertifikat signieren, muss die Geräte-ID entweder als allgemeiner Name (Common Name, CN) oder als 'SubjectAltName' im Zertifikat eingegeben werden. Das Format für das Feld *CN* lautet 'CN=d:devtype:devid'. Das Format für das Feld 'SubjectAltName' lautet 'SubjectAltName=email:d:devtype:devid'. Dabei ist 'devtype' der Gerätetyp und 'devid' die Client-ID des Geräts.

## Zertifikate der Zertifizierungsstelle für die Geräteauthentifizierung registrieren
{: #reg_ca_cert}

1. Melden Sie sich bei {{site.data.keyword.iot_short_notm}} an und navigieren Sie zu **Allgemeine Einstellungen**.
2. Klicken Sie im Abschnitt **Sicherheit** unter **CA-Zertifikate** auf **Zertifikat hinzufügen**.
3. Navigieren Sie zu der Zertifikatsdatei, die hochgeladen werden soll, oder legen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab. In der Datei darf nur ein Zertifikat enthalten sein, welches gültige Datumsangaben aufweisen muss. Nur Zertifikate im Format .pem oder .der werden akzeptiert. Sie können eine Vorschau der Zertifikatsinformationen in der ausgewählten Datei anzeigen.
4. Geben Sie eine Beschreibung für die Zertifikatsdatei ein.
5. Stellen Sie sicher, dass die richtige Datei ausgewählt ist, und klicken Sie auf **Speichern**. Das ausgewählte Zertifikat wird in die Tabelle aufgenommen und ist standardmäßig aktiviert.

## Messaging-Serverzertifikate registrieren
{: #reg_msg_cert}

Mit der Plattform wird ein Standardserverzertifikat bereitgestellt. Sie können dieses Standardzertifikat verwenden oder ein Zertifikat von Ihrer Organisation hochladen. Wenn Sie noch kein Zertifikat haben, können Sie eine Anforderung für ein neues Zertifikat erstellen. Nach dem Erhalt des neuen Zertifikats muss es signiert werden und anschließend zurück auf die Plattform hochgeladen werden.

Um das Standardzertifikat oder ein anderes Zertifikat zu verwenden, das bereits hochgeladen wurde, wählen Sie das gewünschte Zertifikat in der Dropdown-Liste in der Tabelle mit den Standardzertifikaten des Messaging-Servers**** unter **Messaging-Serverzertifikate** aus.

**Hinweis:** Die Dashboardseiten der Plattform stellen möglicherweise interne Verbindungen zum Messaging-Server her, um Geräteinformationen abzurufen. Beim Einrichten von selbst signierten Serverzertifikaten für eine Organisation, müssen Dashoardbenutzer das Serverzertifikat in Ihren Browsern als vertrauenswürdiges Zertifikat hinzufügen, um Verbindungsprobleme zu vermeiden, die entstehen können, weil die Browser den Messaging-Server standardmäßig nicht als vertrauenswürdigen Server erkennen.

### Zertifikat aus Ihrer Organisation hochladen
{: #upload_cert}
1. Klicken Sie unter **Allgemeine Einstellungen** im Abschnitt **Sicherheit** unter **Messaging-Serverzertifikate** auf **Zertifikat hinzufügen**.
2. Navigieren Sie zu der Zertifikatsdatei, die hochgeladen werden soll, oder legen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab.
3. Navigieren Sie zu der Datei mit privatem Schlüssel, die hochgeladen werden soll, oder fügen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab.  
4. Geben Sie die Kennphrase des privaten Schlüssels ein, wenn der private Schlüssel mit einer Kennphrase verschlüsselt wurde.
5. Stellen Sie sicher, dass die richtige Datei ausgewählt ist, und klicken Sie auf **Speichern**.
6. Wählen Sie das soeben hochgeladene Zertifikat aus der Dropdown-Liste mit den Standardzertifikaten des Messaging-Servers aus. Das ausgewählte Zertifikat wird in der Tabelle als das aktive Zertifikat angezeigt.

### Neues Zertifikat anfordern
{: #request_cert}

Wenn Sie ein neues Messaging-Serverzertifikat verwenden möchten, können Sie eine Zertifikatssignieranforderung (Certificate Signing Request, CSR) generieren, um ein neues Zertifikat anzufordern.

 1. Klicken Sie unter **Allgemeine Einstellungen** im Abschnitt **Sicherheit** unter **Messaging-Serverzertifikate** auf **CSR erstellen**.
 2. Geben Sie die Details zum Anfordern einer CSR für Ihren Server ein und klicken Sie auf **Generieren**. Die Zertifikatssignieranforderung wird in der Tabelle angezeigt.
 3. Laden Sie die Anforderung herunter und übergeben Sie sie zum Signieren an eine Zertifizierungsstelle.
 4. Nach dem Erhalt eines Zertifikats können Sie es anhand der im Abschnitt [Zertifikat aus Ihrer Organisation hochladen](#upload_cert) beschriebenen Schritte hochladen. Nachdem das Zertifikat hochgeladen wurde, wird die Zertifikatssignieranforderung in der Tabelle durch das hochgeladene Zertifikat ersetzt.
