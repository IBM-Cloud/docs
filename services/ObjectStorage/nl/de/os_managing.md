---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Objekte verwalten

Sie können die Swift-CLI, API oder die Bluemix-Benutzerschnittstelle für die Verwaltung von Objekten und Containern verwenden.
{: shortdesc}

Bevor Sie Objekte verwalten können, stellen Sie sicher, dass Sie die Serviceinstanz [authentifiziert](/docs/services/ObjectStorage/os_authenticate.html), Serviceberechtigungsnachweise [generiert](/docs/services/ObjectStorage/os_credentials.html) und die Swift-Befehlszeilenschnittstelle [konfiguriert](/docs/services/ObjectStorage/os_configuring.html) haben.

Beachten Sie bei der Verwaltung von Objekten die folgenden Aspekte:
  * Es gibt zwar keine Größenbegrenzung für das gespeicherte Datenvolumen, jeder Uploadvorgang darf jedoch nicht mehr als 5 GB umfassen. Zum Hochladen von Dateien von mehr als 5 GB befolgen Sie die Schritte im Abschnitt zum [Speichern großer Objekte](/docs/services/ObjectStorage/os_large_files.html).
  * Swift hat keine eigentliche Verzeichnisstruktur, Sie können jedoch ein [vorhandenes Verzeichnis](/docs/services/ObjectStorage/os_directories.html) zu Ihren Befehlen hinzufügen.
  * Um unbeabsichtigte Überschreibungsaktionen zu vermeiden, [richten Sie die Objektversionierung ein](/docs/services/ObjectStorage/os_versioning.html).
  * Sie können für das Löschen Ihrer Objekte [einen bestimmten Zeitpunkt festlegen](/docs/services/ObjectStorage/os_deletion.html).
