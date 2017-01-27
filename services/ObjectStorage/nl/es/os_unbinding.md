---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Desenlazar y desaprovisionar la instancia de {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

Si el servicio {{site.data.keyword.objectstorageshort}} se ha enlazado con la app Cloud Foundry pero ya no necesita almacenamiento, puede desenlazar y desaprovisionar la instancia.
{: shortdesc}


## Desenlazar la instancia

Puede mantener los datos guardados y desenlazar el servicio de la app Cloud Foundry. La cuenta de {{site.data.keyword.objectstorageshort}} no se suprime hasta que se deja de suministrar el servicio. 

**Atención**: Si desenlaza una instancia de {{site.data.keyword.objectstorageshort}} desde una aplicación de {{site.data.keyword.Bluemix_notm}}, o si suprime la clave de servicio, se suprimirán todas las credenciales para dicha instancia y no se podrán restaurar. Puede generar credenciales de nube nuevas volviendo a enlazar o creando una nueva clave de servicio.

1. Para ver los servicios enlazados a su app, pulse el separador de conexiones en la aplicación de Cloud Foundry.
2. Localice el servicio que desea desenlazar y pulse el botón de menú del mosaico del servicio.
3. Seleccione **Desenlazar servicio**.
4. Deseleccione el recuadro **Suprimir instancia de servicio** y pulse **Aceptar**.
5. Pulse **Volver a transferir** para que el cambio entre en vigor.



## Desaprovisionar la instancia

Si tiene una instancia de {{site.data.keyword.objectstorageshort}} que ya no necesita, puede suprimir la instancia.

**Atención**: Cuando desaprovisione una instancia de {{site.data.keyword.objectstorageshort}}, se suprimirán el proyecto de nube y la cuenta de Swift. Todos los contenedores y objetos de la instancia desaprovisionada se suprimirán, y no se podrán restaurar.

1. Para ver los servicios enlazados a su app, pulse el separador de conexiones en la aplicación de Cloud Foundry.
2. Localice el servicio que desea desaprovisionar y pulse el botón de menú del mosaico del servicio.
3. Seleccione **Suprimir servicio**.
4. Pulse **Suprimir** para confirmar.
5. Pulse **Volver a transferir** para que el cambio entre en vigor.
