---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Trabajo con archivos de gran tamaño {: #large-files}
*Última actualización: 19 de octubre de 2016*
{: .last-updated}

La carga de objetos está limitada a un tamaño máximo de 5 GB en una carga única. Sin embargo, puede seguir cargando objetos mayores de 5 GB si los segmenta en objetos más pequeños. Una vez que se hayan cargado los objetos segmentados, también será necesario un archivo de manifiesto para concatenar los segmentos en el objeto original. Hay dos formas de hacerlo: Dynamic Large Objects (DLO) y Static Large Objects (SLO).
{: shortdesc}

### Dynamic Large Objects: {: #dynamic}

Hay dos formas de manejar DLO:
  * Hacer que el cliente de Swift lo maneje todo automáticamente
  * Utilizar la API Swift para hacerlo usted mismo

#### Utilización del cliente de Swift para manejar Dynamic Large Objects

El cliente de Swift utiliza el parámetro `-segment-size` para descomponer el objeto en piezas más pequeñas. El cliente crea un contenedor nuevo con el nombre del contenedor en el que desea cargar los archivos y añade un sufijo con el número de segmento (`<nombre_contenedor>_segmentos`). Los segmentos se cargan en paralelo. Una vez que se hayan cargado todos los segmentos, se descargarán como un objeto concatenado en un archivo de manifiesto con el nombre de archivo original.

1. Una vez que se haya registrado en {{site.data.keyword.Bluemix_notm}} y esté listo para cargar, ejecute el mandato siguiente para segmentar el archivo.

    ```
    swift upload <nombre_contenedor> <nombre_archivo> --segment-size <tamaño_en_bytes>
    ```
    {: pre}

#### Utilización de la API de Swift para manejar Dynamic Large Objects

Usted mismo puede segmentar los objetos para que tengan 5 GB o menos y, a continuación, cargarlos mediante la API de Swift. Es importante, al cargar, que cargue primero todos los segmentos antes de cargar el manifiesto. Si el objeto se descarga antes de que se hayan terminado de descargar todos los segmentos, el objeto descargado será incoherente. Puede cargar archivos grandes completando los pasos siguientes.

1. Ordene los segmentos por nombre en el orden en el que deberían estar concatenados para formar el objeto original.
2. Cargue los segmentos en un contenedor independiente del contenedor que aloja el archivo de manifiesto. El regulador para descargas se inicia una vez que se haya cargado el décimo segmento, y aumenta el tiempo de carga considerablemente. Por este motivo, se recomienda que el tamaño del segmento no sea inferior al tamaño del archivo dividido por 10.

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}
    
3. Cargue un archivo de manifiesto vacío con la cabecera `X-Object-Manifest` establecida en el valor `<contenedor>/prefijo>` correspondiente.

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}
    
    **Nota**: El archivo de manifiesto debe estar vacío. Si no lo está, el contenido del archivo será tenido en cuenta como uno de los segmentos y entrará en el orden de concatenación dictado por los nombres ordenados.
4. Descargue el objeto. Recibirá el objeto completo como resultado. Puede añadir o eliminar segmentos sin tener que actualizar el archivo de manifiesto. Los segmentos con el prefijo correcto seguirán formando parte del objeto. La supresión del manifiesto no suprimirá los segmentos.

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


### Static Large Objects {: #static}

Los Static Large Objects utilizan los segmentos y un archivo de manifiesto, pero le dan un mayor control. Con SLO, los segmentos no tienen que estar en el mismo contenedor; cada segmento se puede almacenar en cualquier contenedor y se les puede dar cualquier nombre. Sin embargo, los segmentos deben tener al menos 1 MB. No es necesario que establezca una cabecera para el archivo de manifiesto, aunque la cabecera “X-Static-Large-Object” se añade automáticamente y se establece en true una vez que se haya cargado un manifiesto correcto.
{: shortdesc}

El archivo de manifiesto es un documento JSON que proporciona detalles de los segmentos y que se debe cargar una vez que se hayan cargado todos los segmentos. Los datos proporcionados para cada segmento del manifiesto se comparan con los metadatos de los segmentos reales. Si algo no coincide, el manifiesto no se cargará.

<table>
  <tr>
    <th> Atributo</th>
    <th> Descripción</th>
  </tr>
  <tr>
    <td> path </td>
    <td> La ubicación y el nombre del segmento. Se especifica como container_name/object_name. </td>
  </tr>
  <tr>
    <td> etag </td>
    <td> Proporcionado por la solicitud PUT cuando se carga el objeto. También puede encontrarlo haciendo un HEAD al objeto. </td>
  </tr>
  <tr>
    <td> size_bytes </td>
    <td> El tamaño del objeto en bytes. </td>
  </tr>
</table>

*Tabla 1: Atributos JSON en el archivo de manifiesto en el orden de concatenación*

Puede cargar archivos grandes completando los pasos siguientes:

1. Ejecute el siguiente mandato para cargar los segmentos. El regulador para descargas se inicia una vez que se haya cargado el décimo segmento, y aumenta el tiempo de carga considerablemente. Por este motivo, se recomienda que el tamaño del segmento no sea inferior al tamaño del archivo dividido por 10.

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}
    
2. Cree el manifiesto:

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}
    
3. Cargue el manifiesto. Para ello, debe añadir la consulta `multipart-manifest=put` al nombre del manifiesto ejecutando el mandato siguiente:

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}
    
4. Descargue el objeto. 

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}
    
A continuación se muestran algunos mandatos que puede necesitar al trabajar con Static Large Objects.

* Para descargar el contenido del archivo de manifiesto, debe añadir la consulta `multipart-manifest=get` al mandato. El contenido que reciba no será idéntico al contenido que ha cargado.

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}
    
* Para suprimir el manifiesto, ejecute el mandato siguiente:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}
    
* Para suprimir el manifiesto y todos los segmentos, añada la consulta `multipart-manifest=delete` tras el nombre del manifiesto:

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}

**Nota**: Para añadir segmentos al objeto o para eliminar segmentos de él, debe cargar un nuevo archivo de manifiesto con una lista nueva de segmentos. El nombre de manifiesto puede mantenerse igual.
