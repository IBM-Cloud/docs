---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-04"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Desenlazar y desaprovisionar la instancia de {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}



### Desenlazar la instancia
Si ya no necesita {{site.data.keyword.objectstorageshort}} en la app de Cloud Foundry, pero desea mantener los datos guardados, puede desenlazar la instancia del servicio desde la app.

**Atención**: Si desenlaza una instancia de {{site.data.keyword.objectstorageshort}} desde una aplicación de {{site.data.keyword.Bluemix_notm}}, o si suprime la clave de servicio, se suprimirán todas las credenciales para dicha instancia y no se podrán restaurar. La cuenta de {{site.data.keyword.objectstorageshort}} no se suprime hasta que desaprovisiona la instancia de {{site.data.keyword.objectstorageshort}}. Puede generar credenciales de nube nuevas volviendo a enlazar o creando una nueva clave de servicio.

1. Para ver los servicios enlazados a su app, pulse el separador de conexiones en la aplicación de Cloud Foundry.
2. Localice el servicio que desea desenlazar y pulse el botón de menú del mosaico del servicio.
3. Seleccione **Desenlazar servicio**.
4. Desmarque **Suprimir instancia de servicio** y pulse **Aceptar**.
5. Pulse **Volver a transferir** para que el cambio entre en vigor.



### Desaprovisionar la instancia

Si tiene una instancia desenlazada de {{site.data.keyword.objectstorageshort}} que ya no necesita, puede suprimir la instancia.

**Atención**: Cuando desaprovisione una instancia de {{site.data.keyword.objectstorageshort}}, se suprimirán el proyecto de nube y la cuenta de Swift. Todos los contenedores y objetos de la instancia desaprovisionada se suprimirán, y no se podrán restaurar.

1. Para ver los servicios enlazados a su app, pulse el separador de conexiones en la aplicación de Cloud Foundry.
2. Localice el servicio que desea desenlazar y pulse el botón de menú del mosaico del servicio.
3. Seleccione **Suprimir servicio**.
4. Pulse **Suprimir** para confirmar.
5. Pulse **Volver a transferir** para que el cambio entre en vigor.
