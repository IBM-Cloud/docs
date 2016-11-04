---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Trabajo con mantenimiento de versiones de objetos {: #work-with-object-versioning}

*Última actualización: 19 de octubre de 2016*
{: .last-updated}

Con el mantenimiento de versiones de objetos, puede conservar versiones independientes de los objetos sin cambiar el nombre de los archivos. Esto le permite ver un historial de cada objeto y realizar el seguimiento de cuándo se realizaron cambios.
{: shortdesc}


### Configuración del mantenimiento de versiones de objetos{: #setting-up-versioning}

Puede configurar versiones de cada objeto del contenedor mediante el parámetro `X-Versions-Location`. Para ello, cree un contenedor adicional para conservar versiones más antiguas de los objetos como se indica a continuación.

Puede configurar el mantenimiento de versiones de objetos mediante el cliente de Swift o utilizando mandatos cURL.
* Si está utilizando el cliente de Swift, ejecute el mandato siguiente:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}
    
* Si está utilizando cURL, puede configurarlo de la forma siguiente:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}
    
**Nota**: Los objetos del contenedor de copia de seguridad se cambiarán de nombre automáticamente con el siguiente formato: `<Length><Object_name>/<Timestamp>`.
<table>
  <tr>
    <th> Atributo</th>
    <th> Descripción</th>
  </tr>
  <tr>
    <td> `Length` </td>
    <td> La longitud del nombre del objeto. Es un número hexadecimal de 3 caracteres del teclado numeral. </td>
  </tr>
  <tr>
    <td> `Object_name` </td>
    <td> El nombre del objeto.</td>
  </tr>
  <tr>
    <td> `Timestamp` </td>
    <td> La indicación de fecha y hora de cuándo se cargó originalmente dicha versión del objeto.</td>
  </tr>
</table>

### Inhabilitación de versiones de objetos{: #disabling-versioning}

Puede inhabilitar el mantenimiento de versiones mediante el cliente de Swift o utilizando mandatos cURL.

* Para utilizar el cliente de Swift, ejecute el mandato siguiente:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}
    
* Ejecute el siguiente mandato cURL para inhabilitar el mantenimiento de versiones:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}


### Guía de aprendizaje de mantenimiento de versiones de objetos{: #versioning-tutorial}
<!--- SHAWNA: This needs more background information. What are they doing? Why are they doing it? What is the outcome? --->

Puede utilizar la siguiente guía de aprendizaje para entender el ciclo de vida completo del mantenimiento de versiones de objetos.

1. Cree un contenedor denominado `container_one`.

    ```
    swift post container_one
    ```
    {: pre}
    
3. Cree un segundo contenedor con el nombre `container_two`.

    ```
    swift post container_two
    ```
    {: pre}
    
2. Configure el mantenimiento de versiones.

    ```
    swift post container_one -H "X-Versions-Location:container_two"
    ```
    {: pre}
    
4. Cargue un objeto en el contenedor principal por primera vez.

    ```
    swift upload container_one object
    ```
    {: pre}
    
7. Cargue una versión nueva del objeto en container_one. Al cargar una versión nueva del archivo, la versión anterior se moverá automáticamente al contenedor de copia de seguridad que ha especificado al configurar el mantenimiento de versiones.

    ```
    swift upload container_one object
    ```
    {: pre}
    
8. Para ver la versión nueva del archivo en el contenedor, enumere los objetos en container_one.

    ```
    swift list container_one
    ```
    {: pre}
    
9. Liste objetos en container_two. Verá la versión anterior del archivo que se almacenará en este contenedor.

    ```
    swift list container_two
    ```
    {: pre}
    
10. Suprima el objeto en container_one. Cuando suprima el objeto, la versión anterior del contenedor de copia de seguridad se moverá automáticamente al contenedor principal.

    ```
    swift delete container_one object
    ```
    {: pre}
    
11. Liste ambos contenedores. Verá el archivo original en `container_one` y `container_two` estará vacío.

    ```
    swift list container_one
    swift list container_two
    ```
    {: pre}
