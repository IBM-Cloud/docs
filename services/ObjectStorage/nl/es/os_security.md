---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# Gestión de acceso

Las Listas de control de acceso se pueden utilizar para gestionar el acceso al servicio. Los [usuarios administrativos](/docs/services/ObjectStorage/os_access_types.html) pueden conceder acceso de lectura y de escritura, así como eliminar el acceso al gestionar la instancia de servicio.
{: shortdesc}


Las Listas de control de acceso se pueden gestionar mediante la CLI de Swift o la IU de Bluemix. Para gestionar el acceso, asegúrese de que haya configurado el servicio y que haya comenzado a almacenar objetos. Hay que tener en cuenta algunas cosas al gestionar el acceso.
  * Cuando un usuario cree un contenedor, se le otorgará automáticamente privilegios administrativos a dicho contenedor.
  * Las listas de control de acceso no están disponibles para la instancia de servicio, la cuenta de almacenamiento ni a nivel de proyecto. El acceso sólo se puede gestionar a nivel de contenedor.
  * Asegúrese de comprobar que el acceso a un contenedor se haya [eliminado](/docs/services/ObjectStorage/os_remove_access.html).
