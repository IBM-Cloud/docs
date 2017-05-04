---



copyright:

  years: 2017

lastupdated: "2017-03-20"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI de {{site.data.keyword.registrylong_notm}}
{: #containerregcli}

La CLI de {{site.data.keyword.registrylong}} es un plugin que le permite gestionar los recursos de registro, como espacios de nombres e imágenes, de la organización.
{: shortdesc}

**Requisitos previos**
* Antes de ejecutar mandatos de registro, inicie una sesión en {{site.data.keyword.Bluemix_short}} con el mandato `bs login` para generar una señal de acceso de {{site.data.keyword.Bluemix_short}} y autenticar la sesión.

<table summary="Gestión del registro de contenedores">
<caption>Tabla 1. Mandatos para gestionar {{site.data.keyword.registryshort}} en {{site.data.keyword.Bluemix_short}}
</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar el registro</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
Devuelve los detalles sobre el punto final de la API de registro sobre el que se ejecutan los mandatos. 

```
bx cr api
```
{: codeblock}


## bx cr info
Muestra el nombre y la organización del registro en el que ha iniciado la sesión. 

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Ver detalles sobre una determinada imagen. 

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go. </dd>
<dt>IMAGE</dt>
<dd>La vía de acceso completa del registro de {{site.data.keyword.Bluemix_short}} a la imagen que desea examinar. Si no se especifica ninguna etiqueta en la vía de acceso de imagen, se examina la imagen etiquetada como `latest`. Puede examinar varias imágenes creando una lista de cada vía de acceso privada al registro de {{site.data.keyword.Bluemix_short}} en el mandato con un espacio entre cada vía de acceso.</dd>
</dl>


## bx cr image-list
Ver todas las imágenes de la organización de {{site.data.keyword.Bluemix_short}}. 

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) No truncar la salida.</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Muestra un identificador exclusivo de la imagen en el formato: 'repository:tag'.</dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Incluye en la salida las imágenes públicas proporcionadas por IBM. Sin esta opción, solo se muestran en la lista las imágenes privadas. </dd>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go. </dd>
</dl>


## bx cr image-rm
Suprimir del registro una imagen especificada. 

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parámetros**
<dl>
<dt>IMAGE</dt>
<dd>La vía de acceso completa del registro de {{site.data.keyword.Bluemix_short}} a la imagen que desea eliminar. Si no se especifica ninguna etiqueta en la vía de acceso de la imagen, de forma predeterminada se suprime la imagen etiquetada como `latest`. Puede suprimir varias imágenes creando una lista de cada vía de acceso privada al registro de {{site.data.keyword.Bluemix_short}} en el mandato con un espacio entre cada vía de acceso.</dd>
</dl>


## bx cr login
Si Docker está instalado, este mandato ejecuta el mandato `docker login` sobre el registro. Se necesita el mandato `docker login` para poder ejecutar los mandatos `docker push` o `docker pull` para el registro. Este mandato no es necesario para ejecutar otros mandatos `bx cr`. Si Docker no está instalado, este mandato devuelve un mensaje de error.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Añade un espacio de nombres a la organización de Bluemix.  

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea añadir. El espacio de nombres debe ser exclusivo entre todas las organizaciones de {{site.data.keyword.Bluemix_short}}. </dd>
</dl>


## bx cr namespace-list
Ver todos los espacios de nombres de su organización de {{site.data.keyword.Bluemix_short}}. 

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Elimina un espacio de nombres de la organización de {{site.data.keyword.Bluemix_short}}. Las imágenes de este espacio de nombres se suprimen cuando se elimina el espacio de nombres. 

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea eliminar. </dd>
</dl>
