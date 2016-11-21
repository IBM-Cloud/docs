---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Planificación de la supresión de objetos {: #schedule-object-deletion}
*Última actualización: 19 de octubre de 2016*
{: .last-updated}

Puede planificar la supresión de los objetos. Puede hacer esto haciendo uso de las cabeceras `X-Delete-At` o `X-Delete-After`.
{: shortdesc}

La cabecera `X-Delete-At` toma un número entero que representa el tiempo Epoch en el que se suprime el objeto. La cabecera `X-Delete_After` toma un número entero que representa el número de segundos tras los que se suprimirá el objeto. Para utilizar el cliente de Swift para planificar la supresión de objetos, ejecute el siguiente mandato que se ajuste mejor a sus necesidades.

* Para establecer el objeto que se suprimirá en una fecha y hora específicas, ejecute el mandato siguiente:
    
    ```
    swift post -H "X-Delete-At:<epoch_time>" <container_name> <object_name>
    ```
    {: pre}
    
    Ejemplo:
    
    Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", debe ejecutar el mandato siguiente:
    
    ```
    swift post -H "X-Delete-At:1459515600" <container_name> <object_name>
    ```
    {: screen}
* Para establecer el objeto que se suprimirá en una hora desde este momento, utilice el mandato siguiente:
    
    ```
    swift post -H "X-Delete-After:<number_of_seconds" <container_name> <object_name>
    ```
    {: pre}
    
    Ejemplo:
    
    Para establecer el objeto que se suprimirá en una hora desde este momento, debe ejecutar el mandato siguiente:
    
    ```
    swift post -H "X-Delete-After:3600" container object
    ```
    {: screen}
* Para eliminar la hora de caducidad del objeto, utilice el mandato siguiente:
    
    ```
    swift post -H "X-Remove-Delete-After:<number_of_seconds>" container object
    ```
    {: pre}

Para utilizar los mandatos de cURL para la supresión de objetos planificados, puede ejecutar el siguiente mandato que se ajuste mejor a sus necesidades. Los estándares para la hora son los mismos que el cliente de Swift.

* Para establecer el objeto que se suprimirá en "2016/04/01 08:00:00", utilice el mandato siguiente:
   
   ```
   cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:<epoch_time>" https://<object-storage_url>/<container_name/<object_name>
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

**Nota:** La supresión real de un objeto puede que no se produzca a la hora exacta indicada. Sin embargo, el objeto caducará de hecho a la hora especificada. Esto significa que no se podrá llegar más a él. La supresión real tendrá lugar la próxima vez que se ejecute el daemon swift-object-expirer configurado en el clúster Swift.
