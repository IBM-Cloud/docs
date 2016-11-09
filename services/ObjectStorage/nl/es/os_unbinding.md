---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Desenlazar y desaprovisionar la instancia de {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

*Última actualización: 19 de octubre de 2016*
{: .last-updated}


### Desenlazar la instancia
Si ya no necesita {{site.data.keyword.objectstorageshort}} en la app de Cloud Foundry, pero desea mantener los datos guardados, puede desenlazar la instancia del servicio desde la app.

**Atención**: Si desenlaza una instancia de {{site.data.keyword.objectstorageshort}} desde una aplicación de {{site.data.keyword.Bluemix_notm}}, o si suprime la clave de servicio, se suprimirán todas las credenciales para dicha instancia y no se podrán restaurar.

1. Abra los detalles de la aplicación en la consola de {{site.data.keyword.Bluemix_notm}}.
2. Seleccione la instancia de {{site.data.keyword.objectstorageshort}} y pulse **Desenlazar servicio**.
3. Pulse **ELIMINAR**.
4. Pulse **VOLVER A TRANSFERIR**.



### Desaprovisionar la instancia

Si tiene una instancia desenlazada de {{site.data.keyword.objectstorageshort}} que ya no necesita, puede suprimir la instancia.

**Atención**: Cuando desaprovisione una instancia de {{site.data.keyword.objectstorageshort}}, se suprimirá el proyecto de Cloud. Todos los contenedores y objetos de la instancia desaprovisionada se suprimirán, y no se podrán restaurar.

1. Abra los detalles de la aplicación en la consola de {{site.data.keyword.Bluemix_notm}}.
2. Seleccione la instancia de {{site.data.keyword.objectstorageshort}} y pulse **Suprimir**.
3. Pulse **VOLVER A TRANSFERIR**.
