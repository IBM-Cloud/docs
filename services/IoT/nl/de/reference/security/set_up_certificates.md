---

copyright:
  years: 2015,2016

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Zertifikate einrichten
{: #set_up_certificates.md}
Letzte Aktualisierung: 15. November 2016
{: .last-updated}

Im Rahmen des Add-ons für das Risiko- und Sicherheitsmanagement werden Zertifikate für die Geräteauthentifizierung oder zum Ersetzen des Standardzertifikats des IBM Watson IoT Platform-Standardservers für das MQTT-Messaging verwendet. Geräten, die über keine gültigen und signierten Zertifikate verfügen, wird der Zugriff verweigert und eine Kommunikation mit dem Server ist nicht möglich.

Um Clientzertifikate und den Serverzugriff für Geräte zu konfigurieren, registriert der Systembediener die zugehörigen Zertifikate der Zertifizierungsstelle und optional die Zertifikate des Messaging-Servers in der Watson IoT Platform-Instanz. 

## Zertifikatsanforderungen

Für das von Ihnen registrierte Zertifikat muss die Geräte-ID entweder als allgemeiner Name (CN, Common Name) oder 'SubjectAltName' im Zertifikat eingegeben werden. Für das Feld *CN* lautet das Format 'CN=d:devtype:devid'. Für das Feld 'SubjectAltName' ist das Format 'SubjectAltName=d:devtype:devid', wobei 'devtype' der Gerätetyp und 'devid' die Client-ID des Geräts ist.

Die Verwendung einer Zertifikatsperrliste, die angibt, welche Geräte keine Verbindung mehr herstellen können, wird im Beta-Release nicht unterstützt.

Wenn Sie ein Zertifikat einer Zertifizierungsstelle hinzufügen oder das Zertifikat des Messaging-Servers ersetzen, müssen alle Geräte mithilfe eines MQTT-Clients eine Verbindung herstellen, der SNI (Server Name Indication) unterstützt. Bei der Multi-Tenant-Architektur teilt SNI dem MQTT-Server mit, welche Zertifikate für die einzelnen Organisation/Tenant-Verbindungen verwendet werden sollten.

##Zertifikate der Zertifizierungsstelle für die Geräteauthentifizierung registrieren

1. Melden Sie sich bei Watson IoT Platform an und navigieren Sie zu **Allgemeine Einstellungen**.
2. Klicken Sie im Abschnitt **Risikomanagement** unter **CA-Zertifikate** auf **Zertifikat hinzufügen**.
3. Navigieren Sie zu der Zertifikatsdatei, die hochgeladen werden soll, oder legen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab. In der Datei darf nur ein Zertifikat enthalten sein, welches gültige Datumsangaben aufweisen muss. Zulässig sind Dateien mit den Erweiterungen .pem, .cer, .cert oder .crt. Sie können eine Vorschau der Zertifikatsinformationen in der ausgewählten Datei anzeigen.
4. Geben Sie eine Beschreibung für die Zertifikatsdatei ein.
5. Stellen Sie sicher, dass die richtige Datei ausgewählt ist, und klicken Sie auf **Speichern**. Das ausgewählte Zertifikat wird in die Tabelle aufgenommen und ist standardmäßig aktiviert.

## Zertifikate des Messaging-Servers registrieren

Im Rahmen der Plattform werden Standardserverzertifikate bereitgestellt. Sie können eines dieser Standardzertifikate verwenden oder eines von Ihrer Organisation hochladen. Wenn Sie noch kein Zertifikat haben, können Sie eine Anforderung für ein neues Zertifikat erstellen. Nach dem Erhalt des neuen Zertifikats muss es signiert werden und anschließend zurück auf die Plattform hochgeladen werden.

Um eines der Standardzertifikate oder ein anderes Zertifikat zu verwenden, das bereits hochgeladen wurde, wählen Sie das gewünschte Zertifikat aus der Dropdown-Liste mit den Standardzertifikaten des Messaging-Servers in der Tabelle unter **Messaging-Serverzertifikate** aus.

### <a name="upload"> </a>Zertifikat aus Ihrer Organisation hochladen

1. Klicken Sie unter **Allgemeine Einstellungen** im Abschnitt **Risikomangement** unter **Messaging-Serverzertifikate** auf **Zertifikat hinzufügen**.
2. Navigieren Sie zu der Zertifikatsdatei, die hochgeladen werden soll, oder legen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab. 
3. Navigieren Sie zu der Datei mit privatem Schlüssel, die hochgeladen werden soll, oder fügen Sie eine Datei mithilfe der Drag-und-Drop-Funktion im Fenster **Zertifikat hinzufügen** ab.   
4. Geben Sie die Kennphrase des privaten Schlüssels ein, wenn der private Schlüssel mit einer Kennphrase verschlüsselt wurde.
5. Stellen Sie sicher, dass die richtige Datei ausgewählt ist, und klicken Sie auf **Speichern**. 
6. Wählen Sie das soeben hochgeladene Zertifikat aus der Dropdown-Liste mit den Standardzertifikaten des Messaging-Servers aus. Das ausgewählte Zertifikat wird in der Tabelle als das aktive Zertifikat angezeigt.


### Neues Zertifikat anfordern

 Wenn Sie ein neues Messaging-Serverzertifikat verwenden möchten, können Sie eine Zertifikatssignieranforderung (CSR, Certificate Signing Request) generieren, um ein neues Zertifikat anzufordern.

 1. Klicken Sie unter **Allgemeine Einstellungen** im Abschnitt **Risikomanagement** unter **Messaging-Serverzertifikate** auf **CSR erstellen**.
 2. Geben Sie die entsprechenden Details zum Anfordern einer Zertifikatssignieranforderung für den Server ein und klicken Sie auf **Generieren**. Die Zertifikatssignieranforderung wird in der Tabelle angezeigt.
 3. Laden Sie die Anforderung herunter und übergeben Sie sie zum Signieren an eine Zertifizierungsstelle.
 4. Nach dem Erhalt eines Zertifikats können Sie es anhand der im Abschnitt 'Zertifikat aus Ihrer Organisation hochladen' beschriebenen Schritte hochladen. Nachdem das Zertifikat hochgeladen wurde, wird die Zertifikatssignieranforderung in der Tabelle durch das hochgeladene Zertifikat ersetzt.
