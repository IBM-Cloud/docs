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

# Almacenamiento de objetos

Puede cargar objetos para almacenarlos mediante la IU o la CLI. La carga de objetos está limitada a un tamaño máximo de 5 GB en una carga única. Sin embargo, puede cargar objetos más pequeños segmentándolos en objetos más pequeños.
{: shortdesc}


## Almacenamiento de objetos en contenedores mediante la IU{: #storing-ui}

**Nota**: Al cargar un archivo con el mismo nombre, {{site.data.keyword.objectstorageshort}} sustituirá el archivo almacenado por el nuevo archivo. Si descarga un archivo y realiza ediciones, asegúrese de dar otro nombre al archivo, o [configure el mantenimiento de versiones del objeto](/docs/services/ObjectStorage/os_versioning.html) antes de cargar para mantener las dos versiones del archivo.


1. Desde el panel de control de la instancia de servicio, añada un contenedor desde el menú desplegable **Acciones**.
2. Dé un nombre al contenedor y pulse **CREAR**.
3. Desde el menú desplegable **Acciones**, seleccione **Añadir archivos**. Se abrirá un recuadro de diálogo.
4. Seleccione el archivo o archivos que desee cargar y pulse **Abrir**.



## Almacenamiento de objetos en contenedores mediante la CLI {: #storing-cli}

1. Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Cree un contenedor de {{site.data.keyword.objectstorageshort}} ejecutando el siguiente mandato. Ahora establecerá la variable *nombre_contenedor*. 

  ```
  swift post <nombre_contenedor>
  ```
  {: pre}

**Nota**: Si recibe un mensaje de error, confirme que ha instalado [el software de requisito previo](/docs/services/ObjectStorage/os_configuring.html#install-swift-client).

3. Opcional: Para verificar que se haya creado el contenedor, ejecute el siguiente mandato para listar los contenedores.

  ```
  swift list
  ```
  {: pre}

4. Para evitar la destrucción de datos debido a sobrescrituras accidentales, [configure el mantenimiento de versiones de objetos](/docs/services/ObjectStorage/os_versioning.html). Si no desea el mantenimiento de versiones de objetos, genere una lista de los archivos existentes en el almacén y, si es necesario, renombre el directorio o los archivos antes de cargarlos.

5. Cargue un archivo en el contenedor ejecutando el siguiente mandato.

  ```
  swift upload <nombre_contenedor> <nombre_archivo>
  ```
  {: pre}

  **Nota**: Para cargar archivos mayores de 5 GB, [son necesarios pasos adicionales](/docs/services/ObjectStorage/os_large_files.html).

6. Opcional: Para verificar que la carga ha sido correcta, visualice el contenido del contenedor ejecutando el mandato siguiente.

  ```
  swift list <nombre_contenedor>
  ```
  {: pre}
