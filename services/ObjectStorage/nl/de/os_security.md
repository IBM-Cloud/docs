---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Zugriff verwalten

Mit Zugriffssteuerungslisten kann der Zugriff auf den Service verwaltet werden. [Benutzer mit Administratorberechtigung](/docs/services/ObjectStorage/os_access_types.html) können Lese- und Schreibzugriff gewähren sowie Zugriffsberechtigungen entfernen.{: shortdesc}

Bevor Sie Zugriffsberechtigungen mithilfe der Benutzerschnittstelle oder der Swift-Befehlszeilenschnittstelle verwalten, stellen Sie sicher, dass der Service konfiguriert wurde und bereits Objekte gespeichert wurden.

Beachten Sie bei der Arbeit mit Zugriffssteuerungslisten die folgenden Aspekte:
  * Wenn ein Benutzer einen Container erstellt, erhält er automatisch Administratorberechtigungen für diesen Container.
  * Zugriffssteuerungslisten stehen nicht für die Serviceinstanz, das Speicherkonto und auf Projektebene zur Verfügung. Der Zugriff kann nur auf Container- oder Objektebene verwaltet werden. 
  * Stellen Sie sicher, dass der Zugriff auf einen Container [entfernt](/docs/services/ObjectStorage/os_remove_access.html) wurde.
