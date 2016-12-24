---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Gestión de objetos

Puede utilizar la CLI de Swift, la API, o la IU de Bluemix para gestionar los objetos y contenedores.
{: shortdesc}

Para poder gestionar los objetos, asegúrese de que haya autenticado la instancia de servicio, que haya generado las credenciales de servicio y que haya configurado la CLI de Swift.

Puede almacenar, descargar y suprimir objetos al trabajar con el servicio. Hay que tener en cuenta algunas cosas al gestionar los objetos.
  * Hay un límite en la cantidad de datos que puede almacenar, pero cada carga no puede tener más de 5 GB. Si necesita cargar archivos de más de 5 GB, siga los pasos que se encuentran en [almacenamiento de objetos grandes](/docs/services/ObjectStorage/os_large_files.html).
  * Swift no tiene una auténtica estructura de directorios, sino que puede añadir un [directorio existente](/docs/services/ObjectStorage/os_directories.html) a los mandatos.
  * Para impedir una sobrescritura accidental de un archivo, [configure el mantenimiento de versiones de objetos](/docs/services/ObjectStorage/os_versioning.html).
  * Puede [planificar una hora](/docs/services/ObjectStorage/os_deletion.html) para la supresión de los objetos.
