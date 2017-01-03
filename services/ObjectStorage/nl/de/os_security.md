---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Zugriff verwalten

Mit Zugriffssteuerungslisten kann der Zugriff auf den Service verwaltet werden. [Benutzer mit Administratorberechtigung](/docs/services/ObjectStorage/os_access_types.html) können im Rahmen der Serviceintanzverwaltung Lese- und Schreibzugriff gewähren sowie Zugriff entfernen.
{: shortdesc}


Zugriffssteuerungslisten können über die Swift-CLI oder die Bluemix-Benutzerschnittstelle verwaltet werden. Bevor Sie Zugriff verwalten, stellen Sie sicher, dass der Service konfiguriert wurde und bereits Objekte gespeichert wurden. Bei der Verwaltung des Zugriffs müssen einige Aspekte berücksichtigt werden.
  * Wenn ein Benutzer einen Container erstellt, erhält er automatisch Administratorberechtigungen für diesen Container.
  * Zugriffssteuerungslisten stehen nicht für die Serviceinstanz, das Speicherkonto und auf Projektebene zur Verfügung. Der Zugriff kann nur auf Containerebene verwaltet werden.
  * Stellen Sie sicher, dass der Zugriff auf einen Container [entfernt](/docs/services/ObjectStorage/os_remove_access.html) wurde.
