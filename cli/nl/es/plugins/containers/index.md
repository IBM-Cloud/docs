---



copyright:

  years: 2015, 2017

lastupdated: "2017-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# CLI de IBM Containers
{: #containercli}

*Versión:* 1.0.0

CLI de IBM Containers es un plug-in de CLI de {{site.data.keyword.Bluemix_notm}} para gestionar contenedores y grupos de contenedores en Bluemix.
{: shortdesc}

**Nota:** *Requisitos previos* lista las acciones que son necesarias antes de utilizar el mandato. Los mandatos que no tienen acciones de requisito previo listan **Ninguno**. De lo contrario, los requisitos previos pueden incluir una o varias de las acciones siguientes:
<dl>
<dt>Punto final</dt>
<dd>Un punto final de API se debe establecer por medio de la <code>bluemix api</code> antes de utilizar el mandato.</dd>
<dt>Login</dt>
<dd>El inicio de sesión que utiliza el mandato <code>bluemix login</code> es necesario antes de utilizar este mandato. Si inicia sesión con un ID federado, utilice la opción '--sso' para autenticarse con un código de acceso de una sola vez.</dd>
<dt>Target</dt>
<dd>El mandato <code>bluemix target</code> debe utilizarse para establecer un punto de extensión org y un espacio antes de utilizar este mandato.</dd>
<dt>Docker</dt>
<dd>CLI de Docker (docker) es obligatorio para ejecutar mandatos en el plugin de la CLI de IBM Containers.</dd>
</dl>

<table summary="Mandatos bluemix que pueden utilizarse para gestionar contenedores en Bluemix.">
<caption>Tabla 1. Mandatos para gestionar contenedores en Bluemix</caption>
 <thead>
 <th colspan="5">Mandatos para gestionar contenedores en Bluemix</th>
 </thead>
 <tbody>
 <tr>
 <td>[bluemix ic attach](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_attach)</td>
 <td>[bluemix ic build](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_build)</td>
 <td>[bluemix ic cp](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cp)</td>
 <td>[bluemix ic cpi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_cpi)</td>
 <td>[bluemix ic exec](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_exec)</td>
 </tr>
 <tr>
 <td>[bluemix ic group-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_create)</td>
 <td>[bluemix ic group-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_inspect)</td>
 <td>[bluemix ic group-instances](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_instances)</td>
 <td>[bluemix ic group-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_remove)</td>
 <td>[bluemix ic group-update](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_group_update)</td>
 </tr>
 <tr>
  <td>[bluemix ic groups](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_groups)</td>
  <td>[bluemix ic info](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_info)</td>
  <td>[bluemix ic init](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_init)</td>
  <td>[bluemix ic images](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_images)</td>
  <td>[bluemix ic inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_inspect)</td>
 </tr>
 <tr>
 <td>[bluemix ic ip-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_bind)</td>
 <td>[bluemix ic ip-release](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_release)</td>
 <td>[bluemix ic ip-request](/docs/cli/reference/bluemix_cli/index.html#ip_request)</td>
 <td>[bluemix ic ip-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ip_unbind)</td>
 <td>[bluemix ic ips](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ips)</td>
 </tr>
 <tr>
 <td>[bluemix ic kill](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_kill)</td>
 <td>[bluemix ic logs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_logs)</td>
 <td>[bluemix ic namespace-get](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_get)</td>
 <td>[bluemix ic namespace-set](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_namespace_set)</td>
 <td>[bluemix ic pause](/docs/cli/reference/bluemix_cli/index.html#pause)</td>
 </tr>
 <tr>
 <td>[bluemix ic port](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_port)</td>
 <td>[bluemix ic ps](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_ps)</td>
 <td>[bluemix ic rename](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rename)</td>
 <td>[bluemix ic reprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_reprovision)</td>
 <td>[bluemix ic restart](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_restart)</td>
 </tr>
 <tr>
 <td>[bluemix ic rm](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rm)</td>
 <td>[bluemix ic rmi](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_rmi)</td>
 <td>[bluemix ic route-map](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_map)</td>
 <td>[bluemix ic route-unmap](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_route_unmap)</td>
 <td>[bluemix ic run](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_run)</td>
 </tr>
 <tr>
 <td>[bluemix ic service-bind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_bind)</td>
 <td>[bluemix ic service-unbind](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_service_unbind)</td>
 <td>[bluemix ic start](/docs/cli/reference/bluemix_cli/index.html#ic_start)</td>
 <td>[bluemix ic stats](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_stats)</td>
 <td>[bluemix ic stop](/docs/cli/reference/bluemix_cli/index.html#ic_stop)</td>
 </tr>
 <tr>
 <td>[bluemix ic top](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_top)</td>
 <td>[bluemix ic unpause](/docs/cli/reference/bluemix_cli/index.html#unpause)</td>
 <td>[bluemix ic unprovision](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_unprovision)</td>
 <td>[bluemix ic volume-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_inspect)</td>
 <td>[bluemix ic volume-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_create)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-fs](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs)</td>
 <td>[bluemix ic volume-fs-create](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_create)</td>
 <td>[bluemix ic volume-fs-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_remove)</td>
 <td>[bluemix ic volume-fs-inspect](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_inspect)</td>
 <td>[bluemix ic volume-fs-flavors](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_fs_flavors)</td>
 </tr>
 <tr>
 <td>[bluemix ic volume-remove](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volume_remove)</td>
 <td>[bluemix ic volumes](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_volumes)</td>
 <td>[bluemix ic wait](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait)</td>
 <td>[bluemix ic wait-status](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_wait_status)</td>
 <td>[bluemix ic version](/docs/cli/reference/bluemix_cli/index.html#bluemix_ic_version)</td>
 </tr>
  </tbody>
 </table>


## bluemix ic attach
{: #bluemix_ic_attach}

Controlar un contenedor en ejecución o ver su resultado. Utilice `CTRL+C` para salir y detener el contenedor. Este mandato llama a la CLI de Docker. Para obtener más información, consulte el mandato [attach ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/attach/){: new_window} en la ayuda de Docker.

```
bluemix ic attach [--no-stdin] [--sig-proxy] CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>--no-stdin (opcional)</dt>
   <dd>No se incluye la entrada estándar.</dd>
   <dt>--sig-proxy (opcional)</dt>
   <dd>Usar proxy de todas las señales recibidas para el proceso. El valor predeterminado es <i>true</i>.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
    </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para adjuntar al contenedor `my_container`:
```
bluemix ic attach my_container
```



## bluemix ic build
{: #bluemix_ic_build}

Llama al servicio de compilación de IBM Containers para compilar una imagen Docker en local o en su repositorio privado de {{site.data.keyword.Bluemix_notm}}. Este mandato llama a la CLI de Docker. Para obtener más información, consulte el mandato [build ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/build/){: new_window} en la ayuda de Docker.

```
bluemix ic build -t TAG|--tag TAG [--no-cache] [-p|--pull] [-q|--quiet] DOCKERFILE_LOCATION
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:
   <dl>
   <dt>-t <i>TAG</i>|--tag <i>TAG</i> (necesario)</dt>
   <dd>Nombre de repositorio que se debe aplicar a la imagen creada.</dd>
   <dt>--no-cache (opcional)</dt>
   <dd>No utilizar la memoria caché cuando se crea la imagen. El valor predeterminado es <i>false</i>.</dd>
   <dt>--pull (opcional)</dt>
   <dd>Intentar obtener la imagen básica del registro aunque se encuentre en la memoria caché.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Suprimir la salida detallada generada por los contenedores. El valor predeterminado es <i>false</i>.</dd>
   <dt><i>DOCKERFILE_LOCATION</i> (necesario)</dt>
   <dd>Vía de acceso a Dockerfile y contexto en el host local.</dd>
    </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para compilar una imagen llamada *myimage*. El Dockerfile y otros artefactos a utilizar en la compilación están en el mismo directorio que el mandato desde el que se ejecuta. Como el registro y el espacio de nombres se incluyen en el nombre de imagen, la imagen se construye en el repositorio {{site.data.keyword.Bluemix_notm}} privado de su organización.
```
bluemix ic build -t registry.ng.bluemix.net/mynamespace/myimage .
```


## bluemix ic cp
{: #bluemix_ic_cp}
Copiar archivos o carpetas entre un contenedor y el sistema de archivos. Este mandato llama a la CLI de Docker. Para obtener más información, consulte el mandato [cp ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/cp/){: new_window} en la ayuda de Docker.


## bluemix ic cpi
{: #bluemix_ic_cpi}

Acceder a una imagen Docker Hub o una imagen desde su registro local y copiar la imagen en su repositorio privado de {{site.data.keyword.Bluemix_notm}}.

```
bluemix ic cpi SOURCE_IMAGE DESTINATION_IMAGE
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
   <dl>
   <dt><i>SOURCE_IMAGE</i> (necesario)</dt>
   <dd>Repositorio de origen y el nombre de la imagen.</dd>
   <dt><i>DESTINATION_IMAGE</i> (necesario)</dt>
   <dd>URL de repositorio de {{site.data.keyword.Bluemix_notm}} privado, que incluye el espacio de nombres y el nombre de la imagen de destino. La etiqueta de la imagen es opcional.</dd>
   </dl>

<strong>Ejemplos</strong>:

Copiar una imagen del repositorio de origen a su repositorio privado y añadir una etiqueta a la imagen:

```
bluemix ic cpi source_repository/source_image_name private_registry_URL/destination_image_name:tag
```

Copiar la imagen `sinatra` desde el repositorio `training` a su repositorio privado `registry.ng.bluemix.net/mynamespace` y llamar a la imagen `mysinatra`. Añadir una etiqueta `v1` a la imagen `mysinatra`.

```
bluemix ic cpi training/sinatra registry.ng.bluemix.net/mynamespace/mysinatra:v1
```


## bluemix ic exec
{: #bluemix_ic_exec}

Ejecutar un mandato dentro de un contenedor. Para obtener más información, consulte el mandato [exec ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/exec/){: new_window} en la ayuda de Docker.

```
bluemix ic exec [-d|--detach] [-it] [-u USER|--user USER] CONTAINER [CMD]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-d|--detach (opcional)</dt>
   <dd>Ejecutar el mandato especificado en segundo plano.</dd>
   <dt>-it (opcional)</dt>
   <dd>Modo interactivo. Mantenga visualizada la entrada estándar. Escriba <i>exit</i> para salir.</dd>
   <dt>-u <i>USER</i>|--user <i>USER</i> (opcional)</dt>
   <dd>Nombre de usuario.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>Mandato a ejecutar dentro del contenedor o contenedores especificados.</dd>
   </dl>

<strong>Ejemplos</strong>:

Ejecute el mandato `bash` dentro del contenedor `my_container` en modalidad interactiva:

```
bluemix ic exec -it my_container bash
```

Ejecutar el mandato `date` dentro del contenedor `my_container`:

```
bluemix ic exec my_container date
```


## bluemix ic group-create
{: #bluemix_ic_group_create}

Crear un grupo de contenedores escalable.

```
bluemix ic group-create [--publish,-p PORT] --name GROUP_NAME [--memory,-m MEMORY_SIZE] [-n,--hostname HOSTNAME] [-d,--domain DOMAIN] [--env,-e ENV_KEY=ENV_VAL] [--env-file ENVIRO

NMENT_VARIABLE_FILE] [-P false|true] [--volume] [--min MIN_INSTANCE_COUNT] [--max MAX_INSTANCE_COUNT] [--desired DESIRED_INSTANCE_COUNT] [--anti false|true] [--auto false|true] IMAGE_NAME [CMD [CMD ...]]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
   <dl>
    <dt><i>IMAGE_NAME</i> (necesario)</dt>
   <dd>Imagen que se debe incluir en cada instancia de contenedor en el grupo de contenedores. Puede listar mandatos tras la imagen, pero no opciones. Todas las opciones deben ir antes de especificar una imagen. <br><br>Si utiliza una imagen en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización, especifique la imagen en el formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Si usa una imagen proporcionada por IBM Containers, no incluya el espacio de nombres de la organización. Especifique la imagen en el formato:
<i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt>--name <i>GROUP_NAME</i> (necesario)</dt>
   <dd>Asigne un nombre al grupo. <i>-n</i> está en desuso.<br>
   <strong>Sugerencia:</strong> el nombre de contenedor debe empezar por una letra. El nombre puede incluir letras en mayúsculas y minúscula, números, puntos (.), caracteres de subrayado (_) o guiones (-).</dd>
   <dt>-m <i>MEMORY_SIZE</i>|--memory <i>MEMORY_SIZE</i> (opcional)</dt>
   <dd>Asigna un límite de memoria al grupo en MB. Cuando crea un grupo de contenedores desde la CLI, el valor predeterminado para cada contenedor de instancia es <i>64</i> MB. Cuando crea un grupo de contenedores desde el Panel de control de {{site.data.keyword.Bluemix_notm}}, el valor predeterminado para cada instancia es <i>256</i> MB. Los valores que se aceptan son <i>64</i>, <i>256</i>, <i>512</i>, <i>1024</i> y <i>2048</i>. Una vez asignado el límite de memoria, el valor no se puede cambiar.</dd>
   <dt>-n <i>HOSTNAME</i>|--hostname <i>HOSTNAME</i> (opcional)</dt>
   <dd>Nombre de host, como, por ejemplo, <i>mycontainerhost</i>. El host y el dominio se combinan para formar el URL de direccionamiento público completo, como <i>http://mycontainerhost.mybluemix.net</i>. Cuando revise los detalles de un grupo de contenedores con el mandato <i>bluemix ic group-inspect</i>, el host y el dominio se listan juntos como la ruta.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>Normalmente, el dominio es <i>.mybluemix.net</i>. El host y el dominio se combinan para formar el URL de direccionamiento público completo, como <i>http://mycontainerhost.mybluemix.net</i>. Cuando revise los detalles de un grupo de contenedores con el mandato <i>bluemix ic group-inspect</i>, el host y el dominio se listan juntos como la ruta.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i>|--env <i>ENV_KEY=ENV_VAL</i> (opcional)</dt>
   <dd>Establezca la variable de entorno. Listar varias claves por separado. Si se incluyen comillas, inclúyalas para el nombre para el valor de la variable de entorno. Por ejemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.  En la tabla siguiente se muestran algunas variables de entorno usadas con frecuencia que puede especificar:</dd>
    </dl>


|  Variable de entorno                              |     Descripción                            |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nombre_app&gt;*       | Enlazar un servicio con un contenedor. Utilice la variable de entorno `CCS_BIND_APP` para enlazar una app con un contenedor. La app se enlaza al servicio de destino y actúa como un puente que permite a {{site.data.keyword.Bluemix_notm}} aportar la información de `VCAP_SERVICES` de la app del puente a la instancia de contenedor en ejecución. Para obtener más información sobre la creación de una app de puente, consulte [Enlazar un servicio a un contenedor](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nombre_instancia_servicio1&gt;*,*&lt;nombre_instancia_servicio2&gt;* | Para enlazar un servicio de Bluemix directamente a un contenedor sin utilizar una app puente, utilice CCS_BIND_SRV. Este enlace permite a Bluemix inyectar la información de VCAP_SERVICES en la instancia del contenedor de ejecución. Para proporcionar una lista de varios servicios de Bluemix, inclúyalos como parte de la misma variable de entorno. |
| LOG_LOCATIONS=*&lt;vía_al_archivo&gt;* | Añadir un archivo de registro para supervisar en el contenedor. Incluir la variable de entorno de `LOG_LOCATIONS` con una vía de acceso al archivo de registro. |
{: caption="Table 2. Commonly used environment variables" caption-side="top"}

 <dl>
   <dt>--env-file <i>ENVIRONMENT_VARIABLE_FILE</i> (opcional)</dt>
   <dd> Importar variables de entorno de un archivo, donde ENVFILE es la vía de acceso al archivo en el directorio local. Cada línea del archivo representa un par clave=valor. </dd>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Adjuntar un volumen a un contenedor especificando los detalles con el formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: El nombre o ID de volumen.</li>
   <li><i>CONTAINER_PATH</i>: La vía de acceso absoluta al volumen en el contenedor.</li>
   <li>ro: opcional. Si se especifica <i>ro</i>, el volumen será de solo lectura, en lugar de tomar el valor predeterminado (lectura/grabación).</li></ul>
   </dd>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i> (opcional)</dt>
   <dd>Exponer el puerto para el tráfico HTTP. Los contenedores de su grupo deben atender a su puerto HTTP. No se pueden hacer solicitudes HTTPS. Para grupos de contenedor, no puede incluir varios puertos. <br><br>Cuando especifique un puerto, haga que su app esté disponible para el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} o los contenedores que intentan establecer contacto con el host en el mismo espacio de {{site.data.keyword.Bluemix_notm}}. A continuación, los contenedores y el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} pueden utilizar el puerto para alcanzar el host y la app en el mismo espacio de {{site.data.keyword.Bluemix_notm}}. Si especifica un puerto en el archivo de Docker para la imagen que está utilizando, incluya dicho puerto. <br>
   <strong>Consejos</strong>: <ul>
   <li>Para la imagen Liberty Server certificada de IBM o una versión modificada, especifique el puerto 9080.</li>
   <li>Para la imagen Node.js certificada de IBM o una versión modificada de esta imagen, especifique el puerto 8000.</li>
   </ul>
   </dd>
   <dt>-P (opcional)</dt>
   <dd>Publicar todos los puertos</dd>
   <dt>--min <i>MIN_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>El número mínimo de instancias. El valor predeterminado es 1. Si establece un número mínimo de instancias, el valor no se puede cambiar una vez creado el grupo de contenedor.</dd>
   <dt>--max <i>MAX_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>El número máximo de instancias. El valor predeterminado es 2. Si establece un número máximo de instancias, el valor no se puede cambiar una vez creado el grupo de contenedor.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>El número de instancias que necesita. El valor predeterminado es 2.</dd>
   <dt>--auto (opcional)</dt>
   <dd>Cuando el grupo de contenedores se crea y se habilita la recuperación automática, IBM Containers comprueba el estado de cada instancia con una solicitud HTTP para el puerto que se asigna.<br>
   Si no se recibe respuesta desde una instancia de contenedor en 2 intervalos subsecuentes de 90 segundos, la instancia se elimina y se sustituye por una instancia nueva. Si el contenedor no responde, no debe llevarse a cabo ninguna acción. Este proceso se repite continuamente. En un espacio de tiempo de 30 minutos, si el número total de contenedores distintos que son miembros del grupo es igual a (o supera) 3 veces el tamaño máximo observado del grupo, la recuperación automática se inhabilita de forma permanente para el grupo de contenedores. Para habilitar de nuevo la recuperación automática, debe volver a crear el grupo de contenedores.</dd>
  <dt>--anti (opcional)</dt>
  <dd> Utilice anti-affinity para mejorar la alta disponibilidad del grupo de contenedores. La opción --anti obliga a que cada instancia de contenedor del grupo se coloque en un nodo de cálculo físico independiente, lo que reduce las posibilidades de que todos los contenedores de un grupo dejen de funcionar debido a un fallo de hardware. Es posible que no pueda utilizar esta opción con tamaños de grupo mayores debido a que cada región y organización de Bluemix tiene un conjunto limitado de nodos de cálculo disponibles para el despliegue. Si el despliegue no se realiza con éxito, reduzca el número de instancias de contenedor del grupo o elimine la opción --anti. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>Mandato y argumentos que se pasan al grupo de contenedores para su ejecución. Este mandato debe ser un mandato de larga ejecución. No utilice un mandato breve que no se ejecute durante mucho tiempo, como por ejemplo <i>/bin/date</i>, porque los mandatos de vida breve podrían hacer que el contenedor se bloqueara.  <br> <strong>Notas:</strong> <ul>
   <li>El mandato y sus argumentos deben finalizar en la línea de mandatos de <i>bluemix ic run</i>.</li>
   <li>Si los argumentos del mandato incluyen el guión, como en <i>-c</i> en el mandato del ejemplo anterior, el mandato debe sustituirse por dos guiones (--).</li>
   </ul></dd>
   </dl>


<strong>Ejemplos</strong>:

Cree un grupo de contenedores `my_container_group` usando la imagen `registry.ng.bluemix.net/ibmnode` que proporciona IBM Containers y luego use el mandato de larga ejecución `ping localhost` sobre dicho grupo de contenedores:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode ping localhost
```

Cree un grupo de contenedores `my_container_group` usando la imagen `registry.ng.bluemix.net/ibmnode` que proporciona IBM Containers y luego use el mandato de larga ejecución `tail -f /dev/null` sobre dicho grupo de contenedores:

```
bluemix ic group-create --name my_container_group registry.ng.bluemix.net/ibmnode -- tail -f /dev/null
```

Cree un grupo escalable `mygroup` con la recuperación automática habilitada usando la imagen
`registry.ng.bluemix.net/ibmliberty`. El puerto es `9080`, el nombre de host es `mycontainerhost`, el nombre de dominio es `mybluemix.net`.
```
bluemix ic group-create -p 9080 --auto -n mycontainerhost -d mybluemix.net --name mygroup registry.ng.bluemix.net/ibmliberty
```


## bluemix ic group-inspect
{: #bluemix_ic_group_inspect}

Ver información detallada, como variables de entorno, puertos o memoria, especificada para un grupo de contenedores cuando se crea.

```
bluemix ic group-inspect CONTAINER_GROUP
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para inspeccionar el grupo de contenedores `my_group`:
```
bluemix ic group-inspect my_group
```


## bluemix ic group-instances
{: #bluemix_ic_group_instances}

Listar instancias de un grupo de contenedores especificado.

```
bluemix ic group-instances CONTAINER_GROUP
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER_GROUP</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>

<strong>Ejemplos</strong>:

Listar todas las instancias del grupo de contenedores `my_group`:
```
bluemix ic group-instances my_group
```


## bluemix ic group-remove
{: #bluemix_ic_group_remove}

Elimine un grupo de contenedores de un espacio.

```
bluemix ic group-remove [-f|--force] GROUP_NAME [GROUP_NAME2 [...]]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Fuerza la eliminación de un contenedor erróneo o en ejecución.</dd>
   <dt><i>GROUP_NAME</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>


<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para eliminar un grupo de contenedores, donde `my_group` es el nombre del grupo.
```
bluemix ic group-remove my_group
```


## bluemix ic group-update
{: #bluemix_ic_group_update}

Actualizar un grupo de contenedores.


```
bluemix ic group-update [--anti] [--desired DESIRED_INSTANCE_COUNT] [-e ENV_KEY=ENV_VAL] GROUP_NAME
```

**Sugerencia:** para actualizar el nombre de host o dominio de un grupo de contenedores, utilice
`bluemix ic route-map [-n HOST][-d DOMAIN] CONTAINER_GROUP`.

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
 <dl>
   <dt>--anti (opcional)</dt>
   <dd>Utilice anti-affinity para mejorar la alta disponibilidad del grupo de contenedores. La opción --anti obliga a que cada instancia de contenedor del grupo se coloque en un nodo de cálculo físico independiente, lo que reduce las posibilidades de que todos los contenedores de un grupo dejen de funcionar debido a un fallo de hardware. Es posible que no pueda utilizar esta opción con tamaños de grupo mayores debido a que cada región y organización de Bluemix tiene un conjunto limitado de nodos de cálculo disponibles para el despliegue. Si el despliegue no se realiza con éxito, reduzca el número de instancias de contenedor del grupo o elimine la opción --anti.</dd>
   <dt>--desired <i>DESIRED_INSTANCE_COUNT</i> (opcional)</dt>
   <dd>El número de instancias que necesita. El valor predeterminado es <i>2</i>.</dd>
   <dt>-e <i>ENV_KEY=ENV_VAL</i> (opcional)</dt>
   <dd>Establezca la variable de entorno. Listar varias claves por separado. Si se incluyen comillas, inclúyalas para el nombre para el valor de la variable de entorno. Por ejemplo: `-e "key1=value1" -e "key2=value2" -e "key3=value3"`.</dd>
   <dt><i>GROUP_NAME</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para actualizar el grupo de contenedores `my_group`:
```
bluemix ic group-update --desired 5 my_group
```


## bluemix ic groups
{: #bluemix_ic_groups}

Listar grupos de contenedor en el repositorio privado de {{site.data.keyword.Bluemix_notm}} de la organización.

```
bluemix ic groups [-q]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:
	<dl>
	<dt>-q (opcional)</dt>
   	<dd>Mostrar solo ID de grupo</dd>
	</dl>


## bluemix ic images
{: #bluemix_ic_images}

Ver una lista de todas las imágenes disponibles en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización. Para obtener más información, consulte el mandato [images ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/images){: new_window} en la ayuda de Docker. La lista incluye el ID de imagen, la fecha de creación y el nombre de imagen.

```
bluemix ic images [-a|--all] [-f CONDITION] [--no-trunc] [-q|--quiet]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Incluye todas las capas de la imagen por cada imagen del repositorio de la organización,
no solo la más reciente.</dd>
   <dt>-f (opcional)</dt>
   <dd>Filtre la lista de imágenes por la condición proporcionada.</dd>
   <dt>--no-trunc (opcional)</dt>
   <dd>No trunca la salida.</dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Muestra solo los ID numéricos.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para recibir una lista de imágenes disponibles para la organización:
```
bluemix ic images
```


## bluemix ic info
{: #bluemix_ic_info}

Ver un conjunto de información que describe el estado de la instancia de servicio de nube del contenedor. La información incluye
el límite de contenedores, el uso de los contenedores, los contenedores en ejecución, el límite de memoria, el límite de
dirección IP flotante, el uso de dirección IP flotante, el URL de host CCS, el URL de host de registro y estado de la modalidad de
depuración.

```
bluemix ic info
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino


## bluemix ic init
{: #bluemix_ic_init}

Inicializar el entorno de contenedores en su máquina local para usar todas las posibilidades del servicio IBM Containers.

```
bluemix ic init
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

**Nota:** antes de la inicialización, asegúrese de que la CLI de Docker (docker) esté instalada y configurada en su variable de entorno PATH. Para cambiar a otra región, utilice el mandato `bluemix region-set`.

<strong>Ejemplos</strong>:

Cambiar a la región `us-south`:

```
bluemix region-set us-south
```


## bluemix ic inspect
{: #bluemix_ic_inspect}

Ver la información sobre un contenedor. Para obtener más información, consulte el mandato [inspect ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/inspect){: new_window} en la ayuda de Docker.

```
bluemix ic inspect [IMAGE|images|CONTAINER]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>IMAGE</i> (necesario)</dt>
   <dd>Muestra información detallada sobre una imagen específica indicando el nombre o ID de la imagen.</dd>
   <dt>images (necesario)</dt>
   <dd>Muestra información detallada sobre todas las imágenes del repositorio.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Muestra información detallada sobre un contenedor específico indicando el nombre o el ID del contenedor.</dd>
   </dl>

**Consejo:** solo se puede especificar un parámetro *IMAGE*, *images* o *CONTAINER* a la vez.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para inspeccionar un contenedor llamado `proxy`:
```
bluemix ic inspect proxy
```


## bluemix ic ip-bind
{: #bluemix_ic_ip_bind}

Enlazar una dirección IP flotante disponible a un contenedor.

```
bluemix ic ip-bind IP_ADDRESS CONTAINER
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (necesario)</dt>
   <dd>Dirección IP que se debe enlazar.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>ID o nombre del contenedor que se debe enlazar.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para enlazar la dirección IP `192.123.12.12 to` al contenedor `proxy`:
```
bluemix ic ip-bind 192.123.12.12 proxy
```


## bluemix ic ip-release
{: #bluemix_ic_ip_release}

Liberar una dirección IP flotante de la instancia de servicio de nube del contenedor.

```
bluemix ic ip-release IP_ADDRESS [IP_ADDRESS2 [...]]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (necesario)</dt>
   <dd>Dirección IP que se debe liberar.</dd>
   </dl>


## bluemix ic ip-request
{: #ip_request}
Solicitar una nueva dirección IP flotante.

```
bluemix ic ip-request [-q]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Mostrar una lista únicamente de las direcciones IP, sin los ID de los contenedores vinculados a estas direcciones IP.</dd>
   </dl>


## bluemix ic ip-unbind
{: #bluemix_ic_ip_unbind}

Desenlazar una dirección IP flotante de su contenedor.

Las direcciones IP públicas son un recurso limitado en IBM Containers. Por lo tanto, las direcciones IP públicas con permiso asignadas a un espacio y no enlazadas a un contenedor se reclamen de forma periódica desde usuarios de prueba gratuitos, aproximadamente de forma semanal. Las direcciones IP públicas no enlazadas nunca se reclaman a clientes de suscripción o en fórmulas de pago previo.

```
bluemix ic ip-unbind IP_ADDRESS CONTAINER
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>IP_ADDRESS</i> (necesario)</dt>
   <dd>Dirección IP que se debe desenlazar.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>ID o nombre del contenedor que se debe desenlazar.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para desenlazar la dirección IP `192.123.12.12` del contenedor `proxy`:
```
bluemix ic ip-unbind 192.123.12.12 proxy
```


## bluemix ic ips
{: #bluemix_ic_ips}

Mostrar una lista de las direcciones IP flotantes disponibles para el usuario que ha iniciado la sesión. La lista incluye direcciones IP y el ID de contenedor al que están enlazadas las direcciones IP. Si la dirección IP no se utiliza, no se mostrará ID de contenedor.

```
bluemix ic ips [-q]
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-q (opcional)</dt>
   <dd>Mostrar una lista únicamente de las direcciones IP, sin los ID de los contenedores vinculados a estas direcciones IP.</dd>
   </dl>


<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para recibir una lista de todas las direcciones IP de la organización.
```
bluemix ic ips -q
```


## bluemix ic kill
{: #bluemix_ic_kill}

Detener un proceso en ejecución en un contenedor sin detener el contenedor. Para obtener más información, consulte el mandato [kill ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/kill/){: new_window} en la ayuda de Docker.

```
bluemix ic kill [-s CMD|--signal CMD] CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-s <i>CMD</i>|--signal <i>CMD</i> (opcional)</dt>
   <dd>Envía un mandato al proceso que se está ejecutando en el contenedor.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>ID o nombre del contenedor.</dd>
   </dl>


<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para terminar el proceso en un contenedor llamado `proxy`:
```
bluemix ic kill proxy
```


## bluemix ic logs
{: #bluemix_ic_logs}

Mostrar los registros de salida o errores para un contenedor en ejecución. Para obtener más información, consulte el mandato [logs ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/logs/){: new_window} en la ayuda de Docker.
```
bluemix ic logs [OPTIONS] CONTAINER
```


## bluemix ic namespace-get
{: #bluemix_ic_namespace_get}

Ver el nombre del repositorio de imágenes {{site.data.keyword.Bluemix_notm}} privado para la organización en la que inicia sesión.

```
bluemix ic namespace-get
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino


## bluemix ic namespace-set
{: #bluemix_ic_namespace_set}

Establezca el nombre del repositorio de imágenes {{site.data.keyword.Bluemix_notm}} privado de la organización en la que ha iniciado sesión.

*Restricción*: no puede utilizar un guión `-` en el nombre del espacio de nombres del repositorio.

```
bluemix ic namespace-set NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>NAME</i> (necesario)</dt>
   <dd>Función de una sola vez, para establecer el espacio de nombres del repositorio para su organización, si aún no está establecido. Después de establecer el espacio de nombres, reinicialice IBM Containers con el mandato `bluemix ic init` antes de continuar.</dd>
   </dl>


## bluemix ic pause
{: #pause}

Colocar en pausa todos los procesos dentro de un contenedor en ejecución. Para obtener más información, consulte el mandato [pause ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/pause/){: new_window} en la ayuda de Docker. Para detener un contenedor, consulte el mandato [bluemix ic unpause](#unpause).

```
bluemix ic pause CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:
   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Respuestas</strong>:

- El contenedor se ha puesto en pausa correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para poner en pausa un contenedor llamado `proxy`:
```
bluemix ic pause proxy
```


## bluemix ic port
{: #bluemix_ic_port}

Listar correlación de puertos o una correlación específica para el contenedor. Este mandato envuelve el mandato `docker port`. Para obtener más información, consulte el mandato [port ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/port/){: new_window} en la ayuda de Docker.


## bluemix ic ps
{: #bluemix_ic_ps}
Ver una lista de los contenedores que se ejecutan en el espacio de nombres del usuario con la sesión iniciada. De forma predeterminada, este mandato muestra solo los contenedores en ejecución. Para obtener más información, consulte el mandato [ps ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/ps/){: new_window} en la ayuda de Docker.

```
bluemix ic ps [-a|--all] [--filter env=SEARCH_CRITERIA] [-s|--size] [-l NUM|--limit NUM] [-q|--quiet]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-a|--all (opcional)</dt>
   <dd>Muestra todos los contenedores, los que se ejecutan y los que están detenidos.</dd>
   <dt>--filter env=<i>SEARCH_CRITERIA</i> (opcional)</dt>
   <dd>Contenedores de búsqueda que tienen un valor de variable de entorno específico. Puede filtrar los contenedores por cualquier valor o clave de variable de entorno que se lista en la sección Env de la respuesta de la CLI al inspeccionar un contenedor. Sustituya SEARCH_CRITERIA por la clave o el valor que está buscando. Los criterios de búsqueda no tienen que ser una coincidencia exacta. </dd>
   <dt>-s|--size (opcional)</dt>
   <dd>Lista los tamaños de los contenedores.</dd>
   <dt>-l <i>NUM</i>|--limit <i>NUM</i> (opcional)</dt>
   <dd>Lista los contenedores más recientes, donde <i>NUM</i> es el número de contenedores recientes que desea devolver. <br><br> Por ejemplo, si ha creado los contenedores <i>nodo1</i> a <i>nodo5</i> de forma secuencial, el mandato <i>bluemix ic ps --limit 2</i> devuelve nodo4 y nodo5 porque son los dos últimos contenedores creados. </dd>
   <dt>-q|--quiet (opcional)</dt>
   <dd>Muestra solo los ID de contenedor.</dd>
   </dl>


<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para ver todos los contenedores en ejecución o detenidos:
```
bluemix ic ps -a
```


## bluemix ic rename
{: #bluemix_ic_rename}
Renombrar un contenedor. Para obtener más información, consulte el mandato [rename ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rename/){: new_window} en la ayuda de Docker.

```
bluemix ic rename OLD_NAME NEW_NAME
```
<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

<dl>
   <dt><i>OLD_NAME</i> (necesario)</dt>
   <dd>El nombre antiguo del contenedor.</dd>
   <dt><i>NEW_NAME</i> (necesario)</dt>
   <dd>El nuevo nombre del contenedor.</dd>
   </dl>


## bluemix ic reprovision
{: #bluemix_ic_reprovision}

Volver a crear el servicio IBM Containers en el espacio de Bluemix en el que ha iniciado la sesión. La cuota original del espacio se mantiene.

<strong>Importante</strong>: al ejecutar este mandato, no se migrará ninguno de los contenedores individuales y grupos de este espacio al espacio que se ha vuelto a aprovisionar y se eliminarán durante el proceso de migración.

```
bluemix ic reprovision [--force|-f] [ENVIRONMENT_NAME]
```
<strong>Opciones de mandato</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Fuerza que se cree nuevamente el servicio IBM Containers en el espacio de Bluemix.</dd>
   <dt><i>AVAILABILITY_ZONE</i> (opcional)</dt>
   <dd>El nombre de la zona de disponibilidad de IBM Containers donde están desplegados los contenedores. Si no se especifica ninguna zona de disponibilidad, se utilizará la zona de disponibilidad predeterminada establecida para la región.</dd>
   </dl>


## bluemix ic restart
{: #bluemix_ic_restart}

Reiniciar un contenedor. Para obtener más información, consulte el mandato [restart ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/restart/){: new_window} en la ayuda de Docker.

```
bluemix ic restart CONTAINER [-t SECS|--time SECS]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>Número de segundos que deben transcurrir antes de que el contenedor se reinicie.</dd>
   </dl>


<strong>Respuestas</strong>:

- El contenedor se ha reiniciado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para reiniciar un contenedor llamado `proxy`:
```
bluemix ic restart proxy
```


## bluemix ic rm
{: #bluemix_ic_rm}

Eliminar un contenedor. Para obtener más información, consulte el mandato [rm ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rm/){: new_window} en la ayuda de Docker.

```
bluemix ic rm [-f|--force] CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-f|--force (opcional)</dt>
   <dd>Fuerza la eliminación de un contenedor erróneo o en ejecución.</dd>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Respuestas</strong>:

- El contenedor se ha eliminado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para eliminar un contenedor llamado `proxy`:
```
bluemix ic rm proxy
```


## bluemix ic rmi
{: #bluemix_ic_rmi}

Eliminar una imagen del espacio de nombres del usuario con la sesión iniciada. Para obtener más información, consulte el mandato [rmi ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/rmi/){: new_window} en la ayuda de Docker.

```
bluemix ic rmi [-R REGISTRY|--registry REGISTRY] IMAGE
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-R <i>REGISTRY</i>|--registry <i>REGISTRY</i> (opcional)</dt>
   <dd>Cambia el host del registro. El valor predeterminado es usar el registro que especifique en el mandato <i>bluemix ic init</i>.</dd>
   <dt><i>IMAGE</i> (necesario)</dt>
   <dd>Nombre de la imagen que desea eliminar. Si no se especifica una etiqueta en el nombre de la imagen, la imagen etiquetada como <i>latest</i> se suprime de forma predeterminada.</dd>
   </dl>

<strong>Respuestas</strong>:

- Eliminado: `{IMAGE}`

 Donde `{IMAGE}` es el nombre de la imagen que se ha eliminado.

- Error. No se ha especificado host de registro.

- Error de eliminación de imagen: no se ha podido conectar al registro de nube de contenedor

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

<strong>Ejemplos</strong>:

El siguiente ejemplo muestra una solicitud para eliminar la imagen `mynamespace/myimage:latest`:
```
bluemix ic rmi registry.ng.bluemix.net/mynamespace/myimage:latest
```


## bluemix ic route-map
{: #bluemix_ic_route_map}

Establecer la ruta que utiliza el tráfico de Internet para acceder al grupo de contenedores. Puede utilizar este mandato para establecer una nueva ruta o actualizar una ruta existente.

```
bluemix ic route-map [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>Nombre de host para la ruta. El nombre de host es la primera parte del URL de ruta pública completa, como <i>mycontainerhost</i> en el URL <i>mycontainerhost.mybluemix.net</i>.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>Nombre de dominio para la ruta, que es la segunda parte del URL de ruta pública completa. En la mayoría de los casos, el nombre de dominio es <i>mybluemix.net</i>. También puede utilizar este parámetro para especificar un dominio privado.</dd>
   <dt><i>CONTAINER_GROUP</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para correlacionar la ruta para el grupo denominado `GROUP1`, donde `my_host` es el nombre de host y `mybluemix.net` es el dominio.
```
bluemix ic route-map -n my_host -d mybluemix.net GROUP1
```


## bluemix ic route-unmap
{: #bluemix_ic_route_unmap}

Establecer la ruta que utiliza el tráfico de Internet para acceder al grupo de contenedores. Puede utilizar este mandato para establecer una nueva ruta o actualizar una ruta existente.

```
bluemix ic route-unmap [-n HOST|--hostname HOST] [-d DOMAIN|--domain DOMAIN] CONTAINER_GROUP
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-n <i>HOST</i>|--hostname <i>HOST</i> (opcional)</dt>
   <dd>Nombre de host para la ruta.</dd>
   <dt>-d <i>DOMAIN</i>|--domain <i>DOMAIN</i> (opcional)</dt>
   <dd>Nombre de dominio para la ruta.</dd>
   <dt><i>CONTAINER_GROUP</i> (necesario)</dt>
   <dd>ID o nombre del grupo de contenedores.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para anular la correlación de la ruta para el grupo denominado `GROUP1`, donde `my_host` es el nombre de host y `organization.com` es el dominio.
```
bluemix ic route-unmap -n my_host -d organization.com GROUP1
```


## bluemix ic run
{: #bluemix_ic_run}

Iniciar un nuevo contenedor en el servicio de nube del contenedor desde un nombre de imagen. Para obtener más información, consulte el mandato [run ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/run/){: new_window} en la ayuda de Docker.


```
bluemix ic run [-p PORT|--publish PORT] [-P] [-m MEMORY|--memory MEMORY] [-e ENV|--env ENV] [--volume VOLUME:CONTAINER_PATH] -n NAME|--name NAME [--link NAME:ALIAS] [-it] IMAGE [CMD [CMD ...]]
```
**Nota:** asegúrese de que la herramienta de mandatos de Cloud Foundry esté instalada y de que tiene una señal de Cloud Foundry. El inicio de sesión correcto utilizando `bluemix login` y `bluemix ic init` genera la señal y los certificados necesarios.


<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt>-p <i>PORT</i>|--publish <i>PORT</i>  (opcional)</dt>
   <dd>Exponer el puerto para el tráfico HTTP. Incluir los puertos que se especifiquen en el archivo de Docker para la imagen que está utilizando. Puede incluir varios puertos con varias opciones <i>-p</i>. Al ofrecer un puerto se enlaza automáticamente una dirección IP al contenedor si hay disponible una dirección IP pública. <br><br>Si tiene una dirección IP existente en el espacio que quiere enlazar al contenedor, puede especificar la dirección IP en lugar de enlazarlo más adelante. La dirección IP se debe especificar en el formato: &lt;dirección-ip&gt;:&lt;puerto-contenedor&gt;:&lt;puerto-contenedor&gt; <br><br>Para obtener más información sobre la solicitud de direcciones IP para un espacio, consulte el mandato <a href="index.html#ip_request" target="_blank">bluemix ic ip-request</a>. <br><br>Cuando especifica un puerto, hace que la app esté disponible para el equilibrador de carga de {{site.data.keyword.Bluemix_notm}} o los contenedores que están en el mismo espacio de {{site.data.keyword.Bluemix_notm}} y que intentan acceder al host. Si especifica un puerto en el archivo de Docker para la imagen que está utilizando, incluya dicho puerto. <br><br><strong>Consejos:</strong><ul><li>Para la imagen Liberty Server certificada de IBM o una versión modificada, especifique el puerto 9080.</li><li>Para la imagen Node.js certificada de IBM o una versión modificada de esta imagen, especifique el puerto 8000.</li></ul></dd>
   <dt>-P (opcional)</dt>
   <dd>Ofrecer automáticamente los puertos especificados en el archivo de Docker de la imagen para el tráfico HTTP.</dd>
   <dt>-m <i>MEMORY</i>|--memory <i>MEMORY</i> (opcional)</dt>
   <dd>Asigna un límite de memoria al grupo en MB. Cuando crea un grupo de contenedores desde la CLI, el valor predeterminado para cada contenedor de instancia es 64 MB.  Cuando crea un grupo de contenedores desde el Panel de control de {{site.data.keyword.Bluemix_notm}}, el valor predeterminado para cada instancia es 256 MB. Los valores que se aceptan son 64, 256, 512, 1024 y 2048. Una vez asignado el límite de memoria, el valor no se puede cambiar.</dd>
   <dt>-e <i>ENV</i>|--env <i>ENV</i> (opcional)</dt>
   <dd>Definir la variable de entorno, donde <i>ENV</i> es un par de clave=valor. Listar varias claves por separado. Si se incluyen comillas, inclúyalas para el nombre para el valor de la variable de entorno. Por ejemplo: -e "key1=value1" -e "key2=value2" -e "key3=value3". En la tabla siguiente se muestran algunas variables de entorno usadas con frecuencia que puede especificar:</dd>
   </dl>


|      Variable de entorno                          |   Descripción                              |
| :----------------------------- | :------------------------------ |
| CCS_BIND_APP=*&lt;nombre_app&gt;*       | Enlazar un servicio con un contenedor. Utilice la variable de entorno `CCS_BIND_APP` para enlazar una app con un contenedor. La app se enlaza al servicio de destino y actúa como un puente que permite a {{site.data.keyword.Bluemix_notm}} aportar la información de `VCAP_SERVICES` de la app del puente a la instancia de contenedor en ejecución. Para obtener más información sobre la creación de una app de puente, consulte [Enlazar un servicio a un contenedor](../../../containers/container_integrations_binding.html){: new_window}. |
| CCS_BIND_SRV=*&lt;nombre_instancia_servicio1&gt;*,*&lt;nombre_instancia_servicio2&gt;* | Para enlazar un servicio de Bluemix directamente a un contenedor sin utilizar una app puente, utilice CCS_BIND_SRV. Este enlace permite a Bluemix inyectar la información de VCAP_SERVICES en la instancia del contenedor de ejecución. Para proporcionar una lista de varios servicios de Bluemix, inclúyalos como parte de la misma variable de entorno. |
| LOG_LOCATIONS=*&lt;vía_al_archivo&gt;* | Añadir un archivo de registro para supervisar en el contenedor. Incluir la variable de entorno de `LOG_LOCATIONS` con una vía de acceso al archivo de registro. |
{: caption="Table 3. Commonly used environment variables" caption-side="top"}


   <dl>
   <dt>--volume <i>VOLUME</i>:<i>CONTAINER_PATH</i>[:ro] (opcional)</dt>
   <dd>Adjuntar un volumen a un contenedor especificando los detalles con el formato <i>VolumeId:ContainerPath[:ro]</i>.
   <ul>
   <li><i>VOLUME</i>: El nombre o ID de volumen.</li>
   <li><i>CONTAINER_PATH</i>: La vía de acceso absoluta al volumen en el contenedor.</li>
   <li>ro: opcional. Si se especifica <i>ro</i>, el volumen será de solo lectura, en lugar de tomar el valor predeterminado (lectura/grabación).</li></ul>
   </dd>
   <dt>-n <i>NAME</i>|--name <i>NAME</i> (necesario)</dt>
   <dd>Asigne un nombre al contenedor. <br> <strong>Sugerencia:</strong> el nombre de contenedor debe empezar por una letra. El nombre puede incluir letras en mayúsculas y minúscula, números, puntos (.), caracteres de subrayado (_) o guiones (-).</dd>
   <dt>--link <i>NAME</i>:<i>ALIAS</i> (opcional)</dt>
   <dd>Siempre que quiera que un contenedor se comunique con otro contenedor que esté en ejecución, puede hacer referencia al mismo por medio de un alias para el nombre de host.</dd>
   <dt>-it (opcional)</dt>
   <dd>Ejecute el contenedor en modalidad interactiva. Una vez creado el contenedor, mantenga la entrada estándar visualizada. Escriba <i>exit</i> para salir.</dd>
   <dt><i>IMAGE</i> (necesario)</dt>
   <dd>Imagen que debe incluirse en el contenedor. Puede listar mandatos tras la imagen, pero no opciones. Todas las opciones deben ir antes de especificar una imagen. Todas las opciones deben ir antes de especificar una imagen. <br><br>Si utiliza una imagen en el repositorio {{site.data.keyword.Bluemix_notm}} privado de la organización, especifique la imagen en el formato: <i>registry.ng.bluemix.net/NAMESPACE/IMAGE</i>. <br><br>Si utiliza una imagen proporcionada por IBM Containers, especifíquela en el formato: <i>registry.ng.bluemix.net/IMAGE</i>. </dd>
   <dt><i>CMD</i> (opcional)</dt>
   <dd>Mandato y argumentos que se pasan al grupo de contenedores para su ejecución. Este mandato debe ser un mandato de larga ejecución. No utilice un mandato breve que no se ejecute durante mucho tiempo, como por ejemplo <i>/bin/date</i>, porque los mandatos de vida breve podrían hacer que el contenedor se bloqueara.</dd>
   </dl>


<strong>Ejemplos</strong>:

Ejecute el mandato de larga duración `sh -c "while true; do date; sleep 20; done"` en el contenedor `my_container` que se construye en la imagen `registry.ng.bluemix.net/ibmnode`.
```
bluemix ic run --name my_container registry.ng.bluemix.net/ibmnode -- sh -c "while true; do date; sleep 20; done"
```


Crear y luego iniciar un contenedor `proxy` con el límite de memoria `1024` MB usando la imagen `my_namespace/nginx`, en la que `my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n proxy -m 1024 registry.ng.bluemix.net/my_namespace/nginx
```

Crear y luego reiniciar un contenedor usando la imagen `my_namespace/blog`; pasar las credenciales como variables de entorno. `my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n my_container -e USER=johnsmith -e PASS=password registry.ng.bluemix.net/my_namespace/blog
```

Añadir un volumen a un contenedor usando la imagen `my_namespace/blog`, donde
`my_namespace` es el espacio de nombres asociado a los usuarios con sesión iniciada.
```
bluemix ic run -n my_container -v VolId1:/first/path -v VolId2:/second/path registry.ng.bluemix.net/my_namespace/blog
```


## bluemix ic service-bind
{: #bluemix_ic_service-bind}

Añadir un servicio a un grupo de contenedores en ejecución. Este mandato solo está disponible para grupos de contenedores. Los contenedores individuales deben enlazar un servicio como parte del mandato bluemix ic run.

```
bluemix ic service-bind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (necesario)</dt>
   <dd>El ID o nombre del grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (necesario)</dt>
   <dd>El nombre de la instancia de servicio a añadir al grupo de contenedores.</dd>
   </dl>


## bluemix ic service-unbind
{: #bluemix_ic_service-unbind}

Eliminar un servicio de un grupo de contenedores en ejecución. Este mandato solo está disponible para grupos de contenedores. Los contenedores individuales deben eliminar el contenedor y crear un nuevo contenedor sin el servicio.

```
bluemix ic service-unbind GROUP_NAME SERVICE_INSTANCE
```
<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>GROUP_NAME</i> (necesario)</dt>
   <dd>El ID o nombre del grupo.</dd>
   <dt><i>SERVICE_INSTANCE</i> (necesario)</dt>
   <dd>El nombre de la instancia de servicio a añadir al grupo de contenedores.</dd>
   </dl>


## bluemix ic start
{: #ic_start}
Iniciar un contenedor detenido. Para obtener más información, consulte el mandato [start ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/start/){: new_window} en la ayuda de Docker. Para detener un contenedor, consulte el mandato [bluemix ic stop](#ic_stop).

```
bluemix ic start CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>


<strong>Respuestas</strong>:

- El contenedor se ha iniciado correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para iniciar un contenedor llamado `proxy`.
```
bluemix ic start proxy
```


## bluemix ic stats
{: #bluemix_ic_stats}

Para uno o varios contenedores, vea las estadísticas de uso activo. Utilice `CTRL+C` para salir. Para obtener más información, consulte el mandato [stats ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stats/){: new_window} en la ayuda de Docker.

```
bluemix ic stats [--no-stream] CONTAINER [CONTAINER]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   <dt>--no-stream (opcional)</dt>
   <dd>Mostrar solo el resultado más reciente y no incluir información anterior.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para las estadísticas más recientes sobre un contenedor:
```
bluemix ic stats --no-stream my_container
```


## bluemix ic stop
{: #ic_stop}
Detener un contenedor en ejecución. Para obtener más información, consulte el mandato [stop ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/stop/){: new_window} en la ayuda de Docker. Para iniciar un contenedor, consulte el mandato [bluemix ic start](#ic_start).

```
bluemix ic stop CONTAINER [-t SECS|--time SECS]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   <dt>-t <i>SECS</i>|--time <i>SECS</i> (opcional)</dt>
   <dd>El número de segundos que se deben esperar antes de que el contenedor se elimine.</dd>
   </dl>

<strong>Respuestas</strong>:

- El contenedor se ha detenido correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para detener un contenedor llamado `proxy`.
```
bluemix ic stop proxy
```


## bluemix ic top
{: #bluemix_ic_top}

Mostrar los procesos que están en ejecución en el contenedor. Para obtener más información, consulte el mandato [top ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/top/){: new_window} en la ayuda de Docker.

```
bluemix ic top CONTAINER [CONTAINER]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente es una solicitud para mostrar los procesos del contenedor `my_container`.
```
bluemix ic top my_container
```


## bluemix ic unpause
{: #unpause}

Reanudar todos los procesos de un contenedor en ejecución. Para obtener más información, consulte el mandato [unpause ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/unpause/){: new_window} en la ayuda de Docker. Para poner en pausa un contenedor, consulte el mandato [bluemix ic pause](#pause).

```
bluemix ic unpause CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Respuestas</strong>:

- El contenedor se ha reactivado de la pausa correctamente.

- El mandato ha fallado con un servicio en la nube de contenedor.

 `{message}`

 Donde `{message}` es el error relacionado.

- El mandato ha fallado: no se ha podido conectar con el servicio en la nube del contenedor.

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para sacar de pausa un contenedor llamado `proxy`:
```
bluemix ic unpause proxy
```


## bluemix ic unprovision
{: #bluemix_ic_unprovision}

Suprimir el servicio IBM Containers del espacio de Bluemix en el que ha iniciado la sesión.

<strong>Atención</strong>: al ejecutar este mandato, se perderán todos los contenedores individuales y grupos de contenedores. El espacio seguirá estando disponible en Bluemix. Para volver a empezar a utilizar IBM Containers, debe ejecutar `bluemix ic reprovision` para volver a suministrar el servicio IBM Containers.

```
bluemix ic reprovision [--force|-f]
```
<strong>Opciones de mandato</strong>:

<dl>
   <dt>--force|-f (opcional)</dt>
   <dd>Fuerza la supresión del servicio del espacio de Bluemix.</dd>
 </dl>


## bluemix ic version
{: #bluemix_ic_version}

Mostrar la versión de Docker y la API de IBM Containers.

```
bluemix ic version
```

<strong>Requisitos previos</strong>: Docker

Para ver la versión de IBM Containers, ejecute `bluemix ic info`. Para obtener más información, consulte el mandato [version ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/version/){: new_window} en la ayuda de Docker.


## bluemix ic volume-create
{: #bluemix_ic_volume_create}

Crea un volumen.

```
bluemix ic volume-create VOLUME_NAME FS_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>FS_NAME</i> (opcional)</dt>
   <dd>El nombre de compartición de archivos. Si no hay disponible ninguna compartición de archivos o no se le pone nombre, el volumen se creará en la compartición de archivos predeterminada del espacio.</dd>
   <dt><i>VOLUME_NAME</i> (necesario)</dt>
   <dd>Nombre del volumen. El nombre puede contener letras en minúsculas, números, caracteres de subrayado
(_) y guiones (-).</dd>
   </dl>


<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para crear un volumen.
```
bluemix ic volume-create volume_name fileshare_name
```


## bluemix ic volume-fs
{: #bluemix_ic_volume_fs}

Listar comparticiones de archivos.

```
bluemix ic volume-fs
```


## bluemix ic volume-fs-create
{: #bluemix_ic_volume_fs_create}

Crear una compartición de archivos.

```
bluemix ic volume-fs-create FILE_SHARE_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (necesario)</dt>
   <dd>El nombre de compartición de archivos. El nombre puede contener letras en minúsculas, números, caracteres de subrayado
(_) y guiones (-).</dd>
   </dl>

<strong>Ejemplos</strong>:

El siguiente ejemplo muestra una solicitud para crear una compartición de archivos.
```
bluemix ic volume-fs-create my_file_share
```


## bluemix ic volume-fs-flavors
{: #bluemix_ic_volume_fs_flavors}

Listar todos los tipos de compartición de archivos.

```
bluemix ic volume-fs-flavors
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino


## bluemix ic volume-fs-inspect
{: #bluemix_ic_volume_fs_inspect}

Inspeccionar una compartición de archivos.

```
bluemix ic volume-fs-inspect FILE_SHARE_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

  <dl>
  <dt><i>FILE_SHARE_NAME</i> (necesario)</dt>
   <dd>El nombre de compartición de archivos.</dd>
   </dl>

<strong>Ejemplos</strong>:

El siguiente ejemplo es una solicitud para inspeccionar una compartición de archivos, donde `my_file_share` es el nombre de la compartición de archivos.
```
bluemix ic volume-fs-inspect my_file_share
```


## bluemix ic volume-fs-remove
{: #bluemix_ic_volume_fs_remove}

Eliminar una compartición de archivos.

```
bluemix ic volume-fs-remove FILE_SHARE_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>FILE_SHARE_NAME</i> (necesario)</dt>
   <dd>El nombre de compartición de archivos.</dd>
   </dl>

<strong>Ejemplos</strong>:

El siguiente ejemplo muestra una solicitud para eliminar una compartición de archivos, donde `my_file_share` es el nombre de la compartición de archivos.
```
bluemix ic volume-fs-remove my_file_share
```


## bluemix ic volume-inspect
{: #bluemix_ic_volume_inspect}

Inspeccionar un volumen.

```
bluemix ic volume-inspect VOLUME_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (necesario)</dt>
   <dd>Nombre del volumen.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente es una solicitud para inspeccionar un volumen, donde `volume_name` es el nombre del volumen.
```
bluemix ic volume-inspect volume_name
```


## bluemix ic volume-remove
{: #bluemix_ic_volume_remove}

Eliminar un volumen.

```
bluemix ic volume-remove VOLUME_NAME
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>VOLUME_NAME</i> (necesario)</dt>
   <dd>Nombre del volumen.</dd>
    </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para eliminar un volumen, donde `volume_name` es el nombre del volumen.
```
bluemix ic volume-remove volume_name
```


## bluemix ic volumes
{: #bluemix_ic_volumes}

Listar los volúmenes.

```
bluemix ic volumes
```

<strong>Requisitos previos</strong>:  Punto final, inicio de sesión, destino


## bluemix ic wait
{: #bluemix_ic_wait}

Salir de un contenedor y visualizar el código de salida como confirmación. Para obtener más información, consulte el mandato [wait ![icono de enlace externo](../../../icons/launch-glyph.svg)](https://docs.docker.com/engine/reference/commandline/wait/){: new_window} en la ayuda de Docker.

```
bluemix ic wait CONTAINER [CONTAINER]
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para salir del contenedor `my_container`:
```
bluemix ic wait my_container
```


## bluemix ic wait-status
{: #bluemix_ic_wait_status}

Esperar a que el contenedor individual o grupo de contenedores alcance un estado no transitorio. Durante este tiempo de espera, la línea de mandatos no devuelve nada y no podrá especificar mandatos. Tan pronto como el contenedor alcance un estado no transitorio, aparecerá un mensaje que indica que todo es correcto. Para contenedores individuales, los estados no transitorios incluyen En ejecución, Concluido, Bloqueado, En pausa o Suspendido. Para grupos de contenedores, los estados no transitorios incluyen CREATE_COMPLETE, UPDATE_COMPLETE o FAILED

```
bluemix ic wait-status CONTAINER
```

<strong>Requisitos previos</strong>:  Endpoint, Login, Target, Docker

<strong>Opciones de mandato</strong>:

   <dl>
   <dt><i>CONTAINER</i> (necesario)</dt>
   <dd>Nombre o ID del contenedor.</dd>
   </dl>

<strong>Ejemplos</strong>:

El ejemplo siguiente muestra una solicitud para salir del contenedor `my_container`:
```
bluemix ic wait my_container
```
