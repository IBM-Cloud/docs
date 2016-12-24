---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Objekte verwalten

Sie können die Swift-CLI, API oder die Bluemix-Benutzerschnittstelle für die Verwaltung von Objekten und Containern verwenden.
{: shortdesc}

Bevor Sie Objekte verwalten können, stellen Sie sicher, dass Sie die Serviceinstanz authentifiziert, Serviceberechtigungsnachweise generiert und die Swift-CLI konfiguriert haben. 

Bei der Arbeit mit dem Service können Sie Objekte speichern, herunterladen und löschen. Bei der Verwaltung der Objekte müssen einige Aspekte berücksichtigt werden.
  * Es gibt zwar keine Größenbegrenzung für das gespeicherte Datenvolumen, jeder Uploadvorgang darf jedoch nicht mehr als 5 GB umfassen. Zum Hochladen von Dateien von mehr als 5 G befolgen Sie die Schritte im Abschnitt zum [Speichern großer Objekte](/docs/services/ObjectStorage/os_large_files.html).
  * Swift hat keine eigentliche Verzeichnisstruktur, Sie können jedoch ein [vorhandenes Verzeichnis](/docs/services/ObjectStorage/os_directories.html) zu Ihren Befehlen hinzufügen.
  * Um unbeabsichtigte Überschreibungsaktionen zu vermeiden, [richten Sie die Objektversionierung ein](/docs/services/ObjectStorage/os_versioning.html). 
  * Sie können für das Löschen Ihrer Objekte [einen bestimmten Zeitpunkt festlegen](/docs/services/ObjectStorage/os_deletion.html).
