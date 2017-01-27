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


# Configuración del mantenimiento de versiones de objetos {: #setting-up-versioning}

Puede conservar versiones anteriores de los objetos automáticamente configurando el mantenimiento de versiones de objetos. Con el mantenimiento de versiones, puede ver un historial de cada objeto.
{: shortdesc}

Al cargar una versión nueva del archivo en el contenedor principal, la versión anterior se moverá automáticamente al contenedor de copia de seguridad. Si suprime el archivo del contenedor principal, la versión más reciente se moverá automáticamente del contenedor de copia de seguridad al contenedor principal para sustituir al archivo suprimido.

1. Cree un contenedor y póngale un nombre. Sustituya la variable *nombre_contenedor* por el nombre que desee dar al contenedor.

    ```
    swift post <nombre_contenedor>
    ```
    {: pre}

2. Cree un segundo contenedor que actúe como el almacenamiento de copia de seguridad y dele un nombre.

    ```
    swift post <nombre_contenedor_copia_de_seguridad>
    ```
    {: pre}

3. Configure el mantenimiento de versiones.

    Mandato Swift:

    ```
    swift post <container_name> -H "X-Versions-Location:<backup_container_name>"
    ```
    {: pre}

    Mandato cURL:

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:<backup_container_name>" https://<object-storage_url>/<container_name>
    ```
    {: pre}

4. Cargue un objeto en el contenedor principal por primera vez.

    ```
    swift upload <nombre_contenedor> <object>
    ```
    {: pre}

5. Realice un cambio en el objeto.

6. Cargue la versión nueva del objeto en el contenedor principal.

    ```
    swift upload <nombre_contenedor> <object>
    ```
    {: pre}

7.  Los objetos del contenedor de copia de seguridad se cambian de nombre automáticamente con el siguiente formato: `<Length><Object_name>/<Timestamp>`.
  <table>
  <caption> Tabla 1. Denominación de atributos descritos</caption>
    <tr>
      <th> Atributo </th>
      <th> Descripción </th>
    </tr>
    <tr>
      <td> <i>Length</i> </td>
      <td> La longitud del nombre del objeto. Es un número hexadecimal de 3 caracteres del teclado numeral. </td>
    </tr>
    <tr>
      <td> <i>Object_name</i> </td>
      <td> El nombre del objeto. </td>
    </tr>
    <tr>
      <td> <i>Timestamp</i> </td>
      <td> La indicación de fecha y hora de cuándo se cargó originalmente dicha versión del objeto. </td>
    </tr>
  </table>


6. Enumere los objetos del contenedor principal para ver la versión nueva del archivo.

    ```
    swift list --lh <nombre_contenedor>
    ```
    {: pre}

7. Enumere los objetos del contenedor de copia de seguridad. Verá la versión anterior del archivo que se almacenará en este contenedor. Observe que se ha añadido una indicación de fecha y hora al archivo.

    ```
    swift list --lh <nombre_contenedor_copia_de_seguridad>
    ```
    {: pre}

8. Suprima el objeto del contenedor principal. Cuando suprima el objeto, la versión más reciente del contenedor de copia de seguridad se volverá a mover automáticamente al contenedor principal.

    ```
    swift delete <nombre_contenedor> <object>
    ```
    {: pre}

9. Opcional: Inhabilitar el mantenimiento de versiones de objetos.

    Mandato Swift:

    ```
    swift post <container_name> -H "X-Remove-Versions-Location:"
    ```
    {: pre}

    Mandato cURL:

    ```
    cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/<container_name>
    ```
    {: pre}
