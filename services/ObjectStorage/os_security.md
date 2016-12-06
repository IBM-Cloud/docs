---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Managing access

Access Control Lists can be used to manage access to the service. [Admin users](/docs/services/ObjectStorage/os_access_types.html) can grant read and write access, as well as remove access when managing your service instance.
{: shortdesc}


Access Control Lists can be managed by using the Swift CLI or the Bluemix UI. Before managing access, ensure that you have configured the service and begun storing objects. There are a few things to keep in mind when managing access.
  * When a user creates a container, they are automatically granted admin privileges to that container.
  * Access control lists are not available for the service instance, storage account, or at the project level. Access can only be managed at the container level.
  * Be sure to verify that access to a container has been [removed](/docs/services/ObjectStorage/os_remove_access.html).
