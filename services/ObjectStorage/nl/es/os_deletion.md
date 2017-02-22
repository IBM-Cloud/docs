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


# Supresión de objetos

Una vez que no los necesite, puede suprimir objetos y contenedores de la instancia de almacenamiento. Puede realizar la supresión manualmente, o puede [planificar una hora](/docs/services/ObjectStorage/os_deletion.html#schedule-object-deletion) para la caducidad de los objetos.
{: shortdesc}

**Nota**: Si suprime el contenedor, se suprimirán todos los objetos almacenados dentro de dicho contenedor.


## Supresión de objetos y contenedores mediante la IU {: #deleting-ui}

1. En el panel de control de instancia de servicio, seleccione el contenedor con el archivo que ya no necesite.
2. Seleccione **Suprimir archivo** desde el menú desplegable **Acciones**.
3. Si ya no necesita el contenedor, seleccione **Suprimir contenedor** desde el menú desplegable **Acciones**.



## Supresión de objetos y contenedores mediante la CLI {: #deleting-cli}

1.  Si no ha iniciado la sesión en {{site.data.keyword.Bluemix_notm}}, inicie la sesión en la organización y espacio que contiene su instancia de {{site.data.keyword.objectstorageshort}}.
  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Opcional: Confirme que tiene una copia de seguridad de los objetos antes de suprimir los archivos y contenedores.

3. Ejecute el siguiente mandato para suprimir un archivo:
  ```
  swift delete <nombre_contenedor> <nombre_archivo>
  ```
  {: pre}

4. Para suprimir el contenedor, ejecute el mandato siguiente:
  ```
  swift delete <nombre_contenedor>
  ```
  {: pre}



## Planificación de la supresión de objetos {: #schedule-object-deletion}


Puede planificar la supresión de los objetos mediante las cabeceras `X-Delete-At` o `X-Delete-After`.
{: shortdesc}

La cabecera `X-Delete-At` toma un número entero que representa el tiempo Epoch en el que se suprime el objeto. La cabecera `X-Delete_After` toma un número entero que representa el número de segundos tras los que se suprime el objeto. 

**Nota:** La supresión real de un objeto puede que no se produzca a la hora exacta indicada. Sin embargo, el objeto caducará de hecho a la hora especificada. En ese momento, ya no se puede acceder al objeto. La supresión real tendrá lugar la próxima vez que se ejecute el daemon swift-object-expirer configurado en el clúster Swift.

#### Para utilizar mandatos de Swift:

* Para establecer el objeto que se suprimirá en una fecha y hora específicas, ejecute el mandato siguiente:

    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}

    Ejemplo:
    Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", debe ejecutar el mandato siguiente:

    ```
    swift post -H "X-Delete-At:1459515600" container1 file7
    ```
    {: screen}

* Para establecer el objeto que se suprimirá tras un intervalo de tiempo específico, utilice el mandato siguiente:

    ```
    swift post -H "X-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}

    Ejemplo:
    Para establecer el objeto que se suprimirá en una hora desde este momento, debe ejecutar el mandato siguiente:

    ```
    swift post -H "X-Delete-After:3600" container1 file7
    ```
    {: screen}

* Para eliminar la hora de caducidad del objeto, utilice el mandato siguiente:

    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" <container_name> <object_name>
    ```
    {: pre}



#### Para utilizar mandatos de cURL:

* Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", utilice el mandato siguiente:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Para establecer el objeto que se suprimirá en una hora desde este momento, utilice el mandato siguiente:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:<number_of_seconds>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Para comprobar si el objeto tiene la cabecera, utilice el mandato siguiente:

    ```
    cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}

* Para eliminar la hora de caducidad, utilice el mandato siguiente:

    ```
    cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name>/<object_name>
    ```
    {: pre}
