---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestión de acceso

Las Listas de control de acceso se pueden utilizar para gestionar el acceso al servicio. Los [usuarios administrativos](/docs/services/ObjectStorage/os_access_types.html) pueden conceder acceso de lectura y de escritura, así como eliminar el acceso.
{: shortdesc}

Para gestionar el acceso mediante la IU o la CLI de Swift, asegúrese de haber configurado el servicio y empezado a almacenar objetos.

Cuando trabaje con listas de control de acceso, tenga en cuenta los siguientes puntos:
  * Cuando un usuario cree un contenedor, se le otorgará automáticamente privilegios administrativos a dicho contenedor.
  * Las listas de control de acceso no están disponibles para la instancia de servicio, la cuenta de almacenamiento ni a nivel de proyecto. El acceso solo se puede gestionar a nivel de contenedor o de objeto.
  * Asegúrese de comprobar que el acceso a un contenedor se haya [eliminado](/docs/services/ObjectStorage/os_remove_access.html).
