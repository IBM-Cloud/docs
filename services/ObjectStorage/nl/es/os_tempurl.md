---

copyright:
  years: 2014, 2016
lastupdated: "2016-11-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Creación de un URL temporal {: #create-temporary-url}


Un URL temporal es un URL largo y difícil de adivinar que se puede utilizar para un periodo específico para descargar objetos sin que requieran una mayor autenticación.
{: shortdesc}


1. Identifique la información de autenticación imprimiendo la información de la cuenta con el mandato siguiente:
```
swift stat
```
{: pre}

**Nota**: Localice el campo Account y anote toda la cadena de texto que aparece tras *Account*: incluido `AUTH_`.

2. Establezca una clave secreta. Esta clave puede ser cualquiera que seleccione, pero la práctica recomendada es que seleccione una serie larga, aleatoria y difícil de adivinar. Para establecer la clave, ejecute el mandato siguiente:

```
swift post -m "Temp-URL-Key:<key>"
```
{: pre}

3. Verifique que la `Temp-URL-Key` se haya establecido correctamente ejecutando el siguiente mandato.

```
swift stat
```
{: pre}

4. Cree un URL temporal ejecutando el siguiente mandato:

```
swift tempurl GET <segundos> <vía_acceso> <clave>
```
{: pre}

La tabla siguiente explica los argumentos de posición que toma el mandato `tempurl` de Swift.
<table>
  <tr>
    <th> Argumento </th>
    <th> Descripción </th>
  </tr>
  <tr>
    <td> [method] </td>
    <td> GET permitir la descarga. PUT para permitir la carga. </td>
  </tr>
  <tr>
    <td> [seconds] </td>
    <td> Tiempo durante el que el URL estará disponible, en segundos. </td>
  </tr>
  <tr>
    <td> [path] </td>
    <td> Vía de acceso completa del objeto expresada como <code>/v1/<i>cuenta_autorización</i>/<i>nombre_contenedor</i>/<i>nombre_objeto</i>. </code>Para obtener más información, consulte la <a href="https://console.bluemix.net/docs/services/ObjectStorage/os_api.html#access-points">Documentación de URL de {{site.data.keyword.objectstorageshort}}</a>.</td>
  </tr>
  <tr>
    <td> [key] </td>
    <td> Clave secreta establecida en el paso 2. </td>
  </tr>
</table>

Tabla 2: Argumentos de posición del URL temporal

5. (Opcional): Adjunte el URL devuelto al nombre de clúster para obtener un URL completo. A continuación, puede utilizar el URL completo para descargar objetos con cualquier cliente de HTTP compatible como por ejemplo cURL, wget o Firefox.
