---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Descarga de objetos

Puede descargar los objetos almacenados para su revisión o edición mediante la IU o la CLI.
{: shortdesc}


## Descarga de objetos desde la IU {: #downloading-ui}

1. Para evitar la destrucción de datos debido a sobrescrituras accidentales, [configure el mantenimiento de versiones de objetos](/docs/services/ObjectStorage/os_versioning.html). Si no desea el mantenimiento de versiones de objetos, cambie el nombre del directorio o de los archivos antes de descargar, si es necesario.
2. En el panel de control de instancia de servicio, seleccione el contenedor con el archivo que desee descargar.
3. Seleccione el archivo.
4. En el menú desplegable **Acciones**, seleccione **Descargar archivo**.


## Descarga de objetos con la CLI de Swift {: #downloading-cli}

1.  Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.

```
cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
```
{: pre}

2. Para evitar la destrucción de datos debido a sobrescrituras accidentales, [configure el mantenimiento de versiones de objetos](/docs/services/ObjectStorage/os_versioning.html). Si no desea el mantenimiento de versiones de objetos, genere una lista de los archivos existentes en el almacén y, si es necesario, renombre el directorio o los archivos antes de descargarlos.

3. Descargue un archivo ejecutando el siguiente mandato:

```
swift download <nombre_contenedor> <nombre_contenedor>
```
{: pre}
