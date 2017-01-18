---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Managing access

Access Control Lists can be used to manage access to the service. [Admin users](/docs/services/ObjectStorage/os_access_types.html) can grant read and write access, as well as remove access.
{: shortdesc}

Before managing access by using the UI or the Swift CLI, ensure that you have configured the service and begun storing objects.

When you are working with access control lists, keep the following points in mind:
  * When a user creates a container, they are automatically granted admin privileges to that container.
  * Access control lists are not available for the service instance, storage account, or at the project level. Access can be managed at the container or object level only.
  * Be sure to verify that access to a container was [removed](/docs/services/ObjectStorage/os_remove_access.html).
