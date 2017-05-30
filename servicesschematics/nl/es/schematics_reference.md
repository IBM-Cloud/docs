---

copyright:

  years: 2017

lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# plugin de {{site.data.keyword.bpshort}} CLI para la CLI de {{site.data.keyword.Bluemix_notm}}
{: #cli}

Consulte los mandatos de {{site.data.keyword.bpshort}} sobre cómo la CLI de {{site.data.keyword.Bluemix}} gestiona sus entornos y realiza otras operaciones en {{site.data.keyword.Bluemix_notm}}.
{: shortdesc}

Antes de utilizar los mandatos de CLI:

* Inicie sesión en {{site.data.keyword.Bluemix_notm}} con `bx login [--sso]` para autenticar su sesión. Los usuarios con un ID federado tienen que utilizar el distintivo `--sso` para generar un código de acceso puntual.

Para ver una lista de los mandatos, ejecute `bx schematics help`.

<table id="manage_environments" summary="Gestione sus entornos con los mandatos bx schematics environment.">
<caption>Tabla 1. Mandatos disponibles para gestionar su entorno. Los mandatos siguen la sintaxis <code>bx schematics environment</code>.
</caption>
 <thead>
 <th colspan="5">Gestión del entorno</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx schematics environment create](#environment-create)</td>
 <td>[bx schematics environment delete](#environment-delete)</td>
 <td>[bx schematics environment list](#environment-list)</td>
 <td>[bx schematics environment show](#environment-show)</td>
 <td>[bx schematics environment update](#environment-update)</td>
 </tr>
</tbody></table>
 
 <table id="update_resources" summary="Actualice los recursos suministrados por su entorno con los mandatos bx schematics action.">
 <caption>Tabla 2. Mandatos disponibles para actualizar recursos en su entorno. Los mandatos siguen la sintaxis <code>bx schematics action</code>.
 </caption>
  <thead>
  <th colspan="5">Actualización de los recursos</th>
  </thead>
  <tbody>
  <td>[bx schematics action apply](#action-apply)</td>
  <td>[bx schematics action destroy](#action-destroy)</td>
  <td>[bx schematics action plan](#action-plan)</td>
  </tr></tbody></table>
  
  <table id="audit_environment" summary="Actividades de auditoría que se han ejecutado en su entorno con los mandatos bx schematics activity.">
  <caption>Tabla 3. Mandatos disponibles para auditar las actividades que se han ejecutado en su entorno. Los mandatos siguen la sintaxis <code>bx schematics activity</code>.
  </caption>
   <thead>
   <th colspan="5">Auditoría del entorno</th>
   </thead>
   <tbody>
   <td>[bx schematics activity list](#activity-list)</td>
   <td>[bx schematics activity log](#activity-log)</td>
   <td>[bx schematics activity planfile](#activity-planfile)</td>
   <td>[bx schematics activity show](#activity-show)</td>
   </tr></tbody></table>

## bx schematics environment create
{: #environment-create notoc}

Cree un entorno en {{site.data.keyword.Bluemix_notm}} desde la configuración.

```
bx schematics environment create --file FILE_NAME [--json]
```
{: codeblock}

### Parámetros 

<dl>
<dt>--file FILE_NAME</dt>
<dd>El archivo JSON que se utiliza para pasar los detalles sobre el entorno.
<p>
<p>JSON de ejemplo con todos los valores disponibles:
<pre>{
      "description": "(Opcional) Descripción del entorno",
      "frozen": false,
      "name": "Nombre del entorno",
      "sourceurl": "El URL de GitHub que apunta a la configuración de Terraform",
    "tags": ["(Optional) metadata_tag_1", "(Optional) metadata_tag_2"],
      "terraformversion": "0.9",
      "variablestore": [{
          "name": "(Opcional) variable_1",
          "secure": false,
          "value": "Valor visible"
    },
    {
          "name": "(Opcional) variable_2_secret",
          "secure": true,
          "value": "Valor protegido"
    }]
}</pre></dd>
<dt>--json</dt>
<dd>Imprima la salida en formato JSON.</dd>
</dl>

## bx schematics environment delete
{: #environment-delete notoc}

Elimine la configuración de su entorno de {{site.data.keyword.Bluemix_notm}}. Este mandato solo se recomienda para entornos sin recursos en ejecución. Si suprime un entorno con recursos en ejecución, tendrá que gestionar cada recurso en los paneles de control de servicio individuales.

```
bx schematics environment delete --id ENVIRONMENT_ID [--force]
```
{: codeblock}

### Parámetros 

<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Fuerce el avance del mandato con una confirmación de sí/no.</dd>
</dl>

## bx schematics environment list
{: #environment-list notoc}

Recupere una lista de todos los entornos existentes en su cuenta de {{site.data.keyword.Bluemix_notm}}.

```
bx schematics environment list [--count VALUE] [--offset VALUE] [--json] 
```
{: codeblock}

### Parámetros 
<dl>
<dt>--count VALUE</dt>
<dd>El número de entornos para limitar en su retorno. </dd>
<dt>--offset VALUE</dt>
<dd>El desplazamiento en la lista de entornos.</dd>
<dt>--json</dt>
<dd>Imprima la salida en formato JSON.</dd>
</dl>

## bx schematics environment show
{: #environment-show notoc}

Recupere información detallada sobre un entorno existente.

```
bx schematics environment show --id ENVIRONMENT_ID [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--json</dt>
<dd>Imprima la salida en formato JSON.</dd>
</dl>
  
## bx schematics environment update
{: #environment-update notoc}

Actualice los detalles sobre un entorno existente, como el nombre del entorno o el URL de GitHub. Para actualizar el número de recursos asignados en el entorno, consulte [bx schematics action plan](#action-plan).

```
bx schematics environment update --id ENVIRONMENT_ID --file FILE_NAME [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>El archivo JSON que se utiliza para pasar los detalles sobre el entorno.
Consulte [bx schematics environment create](#environment-create) para obtener un ejemplo de fragmento de código de JSON con los valores permitidos.</dd>
<dt>--json</dt>
<dd>Imprima la salida en formato JSON.</dd>
</dl>

## bx schematics action apply
{: #action-apply notoc}

Despliegue la configuración del entorno. El mandato `apply` explora y ejecuta las configuraciones que se almacenan en el repositorio de GitHub.

```
bx schematics action apply --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Fuerce el avance del mandato con una confirmación de sí/no.</dd>
<dt>--json</dt>
<dd>Imprima la salida de apply en formato JSON.</dd>
</dl>

## bx schematics action destroy
{: #action-destroy notoc}

Destruya su entorno y recursos. El mandato `destroy` destruye su entorno, incluyendo los recursos en ejecución. Esta acción solo se suele utilizar para entornos temporales, como un entorno de control de calidad, con la intención de mantener el entorno por un tiempo limitado. No se recomienda destruir entornos de producción. La acción `destroy` no se puede revertir y debe utilizarse con precaución.

```
bx schematics action destroy --id ENVIRONMENT_ID [--force] [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--force</dt>
<dd>Fuerce el avance del mandato con una confirmación de sí/no.</dd>
<dt>--json</dt>
<dd>Imprima la salida de destroy en formato JSON.</dd>
</dl>
</dl>

## bx schematics action plan
{: #action-plan notoc}

Compare la configuración de su entorno con la configuración desplegada. El mandato `plan` explora la configuración de su repositorio de GitHub y ejecuta un diff en el archivo de estado asociado a su entorno de despliegue. La salida del plan muestra qué recursos deberían añadirse o eliminarse si desplegara la configuración del entorno con el mandato `apply`. 

```
bx schematics action plan --id ENVIRONMENT_ID [--file FILE_NAME] [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--file FILE_NAME</dt>
<dd>El archivo JSON opcional que se utiliza para pasar parámetros para la acción del plan. Puede pasar el parámetro <code>sourcesha</code> para hacer referencia a una rama de Git específica para la configuración de Terraform del entorno. La rama de Git debe especificarse como referencia de cabecera, como por ejemplo <code>refs/heads/BRANCH_NAME</code>. Si no se especifica el parámetro, el valor predeterminado es la cabecera de la rama maestra, esto es <code>refs/heads/master</code>.
<p>
<p>Ejemplo de fragmento de código de JSON con valor:
<pre>{
  "sourcesha": "refs/heads/BRANCH_NAME"
}</pre></dd>
<dt>--json</dt>
<dd>Imprima la salida del plan en formato JSON.</dd>
</dl>

## bx schematics activity list
{: #activity-list notoc}

Genera una lista de los datos de actividades de Terraform que se han ejecutado en un entorno. 

```
bx schematics activity list --id ENVIRONMENT_ID [--count VALUE] [--offset VALUE] [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ENVIRONMENT_ID</dt>
<dd>El identificador exclusivo del entorno. Puede recuperar este valor ejecutando <code>bx schematics environment list</code>.</dd>
<dt>--count VALUE</dt>
<dd>El número de actividades que se devolverán.</dd>
<dt>--offset VALUE</dt>
<dd>El desplazamiento en la lista.</dd>
<dt>--json</dt>
<dd>Imprima la salida del plan en formato JSON.</dd>
</dl>

## bx schematics activity log
{: #activity-log notoc}

Consulte registros de actividad detallados para las acciones que se ejecutan en un entorno.

```
bx schematics activity log --id ACTIVITY_ID
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>El distintivo para devolver detalles sobre una actividad específica. Puede recuperar una lista de los ID de actividad por entorno con el mandato <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity planfile
{: #activity-planfile notoc}

Consulte los archivos de plan para un entorno.

```
bx schematics activity planfile --id ACTIVITY_ID
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>El distintivo para devolver detalles sobre una actividad específica. Puede recuperar una lista de los ID de actividad por entorno con el mandato <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
</dl>

## bx schematics activity show
{: #activity-show notoc}

Recupere información detallada sobre una actividad específica que se ha ejecutado en un entorno. 

```
bx schematics activity show --id ACTIVITY_ID [--json]
```
{: codeblock}

### Parámetros 
<dl>
<dt>--id ACTIVITY_ID</dt>
<dd>El distintivo para devolver detalles sobre una actividad específica. Puede recuperar una lista de los ID de actividad por entorno con el mandato <code>bx schematics activity list --id ENVIRONMENT_ID</code>.</dd>
<dt>--json</dt>
<dd>Imprima la salida del plan en formato JSON.</dd>
</dl>
