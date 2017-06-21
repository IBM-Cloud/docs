---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI es un plugin que permite gestionar su registro y sus recursos de su cuenta.
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
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

Devuelve los detalles sobre el punto final de la API de registro sobre el que se ejecutan los mandatos.

```
bx cr api
```
{: codeblock}


## bx cr info
Visualiza el nombre y la cuenta del registro en el que ha iniciado una sesión. 

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
Visualiza detalles sobre una imagen específica. 

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**Parámetros**


<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go. 


</dd>
<dt>IMAGE</dt>
<dd>Vía de acceso completa de registro de {{site.data.keyword.Bluemix_short}} a la imagen que desea examinar, que se encuentra en formato `namespace/image:tag`. Si no se especifica ninguna etiqueta en la vía de acceso de imagen, se examina la imagen etiquetada como `latest`. Puede examinar varias imágenes creando una lista de cada vía de acceso privada al registro de {{site.data.keyword.Bluemix_short}} en el mandato con un espacio entre cada vía de acceso.</dd>
</dl>


## bx cr image-list (bx cr images)
Visualiza todas las imágenes de su cuenta de {{site.data.keyword.Bluemix_short}}. 

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**Parámetros**
<dl>
<dt>--no-trunc</dt>
<dd>(Opcional) No truncar los resúmenes de imagen.</dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Cada imagen se lista en el formato: `repository:tag`.</dd>
<dt>--include-ibm</dt>
<dd>(Opcional) Incluye en la salida las imágenes públicas proporcionadas por IBM. Sin esta opción, de forma predeterminada solo se muestran en la lista las imágenes privadas.</dd>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go. 


</dd>

</dl>


## bx cr image-rm
Suprime de su registro una o varias de las imágenes especificadas. 

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**Parámetros**
<dl>
<dt>IMAGE</dt>
<dd>Vía de acceso de registro de {{site.data.keyword.Bluemix_short}} a la imagen que desea eliminar, en el formato `namespace/image:tag`. Si no se especifica ninguna etiqueta en la vía de acceso de la imagen, de forma predeterminada se suprime la imagen etiquetada como `latest`. Puede suprimir varias imágenes creando una lista de cada vía de acceso privada al registro de {{site.data.keyword.Bluemix_short}} en el mandato con un espacio entre cada vía de acceso.</dd>
</dl>


## bx cr login
Este mandato ejecuta el mandato `docker login` sobre el registro. Se necesita el mandato `docker login` para poder ejecutar los mandatos `docker push` o `docker pull` para el registro. Este mandato no es necesario para ejecutar otros mandatos `bx cr`. Si Docker no está instalado, este mandato devuelve un mensaje de error.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Añade un espacio de nombres a su cuenta {{site.data.keyword.Bluemix_short}}. 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea añadir. El espacio de nombres debe ser exclusivo entre todas las cuentas de {{site.data.keyword.Bluemix_short}} en la misma región. </dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
Visualiza todos los espacios de nombres cuyo propietario es su cuenta de {{site.data.keyword.Bluemix_short}}. 

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
Elimina un espacio de nombres de su cuenta de {{site.data.keyword.Bluemix_short}}. Las imágenes en este espacio de nombres se suprimen cuando se elimina el espacio de nombres. 

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**Parámetros**
<dl>
<dt>NAMESPACE</dt>
<dd>El espacio de nombres que desea eliminar.</dd>
</dl>


## bx cr token-add
Añade una señal que sirve para controlar el acceso a un registro. 

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**Parámetros**
<dl>
<dt>--description VALUE</dt>
<dd>(Opcional) Especifica el valor como una descripción para la señal, que se visualiza al ejecutar `bx cr token-list`. Si IBM Bluemix Container Service ha creado su señal de forma automática, la descripción se establece en su nombre clúster Kubernetes. En este caso, la señal se elimina de forma automática al eliminar su clúster. </dd>
<dt>-q, --quiet</dt>
<dd>(Opcional) Visualiza únicamente la señal, sin ningún texto a su alrededor. </dd>
<dt>--non-expiring</dt>
<dd>(Opcional) Crea una señal con un acceso que no caduca. Si no se establece este parámetro, de forma predeterminada el acceso con la señal caduca después de 24 horas. </dd>
<dt>--readwrite</dt>
<dd>(Opcional) Crea una señal que otorga acceso de lectura y escritura. Sin esta opción, de forma predeterminada el acceso es de solo lectura. </dd>
</dl>


## bx cr token-get
Recupera la señal especificada desde el registro. 

```
bx cr token-get TOKEN
```

{: codeblock}

**Parámetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) Identificador exclusivo de la señal que desea recuperar. </dd>
</dl>


## bx cr token-list (bx cr tokens)
Visualiza todas las señales que existen para su cuenta de {{site.data.keyword.Bluemix_short}}. 

```
bx cr token-list --format FORMAT
```
{: codeblock}

**Parámetros**
<dl>
<dt>--format FORMAT</dt>
<dd>(Opcional) Formatear los elementos de salida mediante una plantilla de Go. 


</dd>
</dl>


## bx cr token-rm
Elimina una o varias de las señales especificadas. 

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**Parámetros**
<dl>
<dt>TOKEN</dt>
<dd>(Opcional) TOKEN puede ser la propia señal, o el identificador exclusivo de la señal, tal como se muestra en `bx cr token-list`. 
Es posible especificar varias señales separándolas con espacios en blanco. </dd>
</dl>


</dd>
</dl>


