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

# Despliegue de recursos en entornos
{: #deploying}

Con {{site.data.keyword.bplong}}, puede desplegar las últimas modificaciones de código directamente desde su código fuente. Al desplegar su entorno, está desplegando los recursos que definen los archivos de configuración. A continuación, puede gestionar el suministro, las orquestaciones y el ciclo de vida del entorno desde dentro de {{site.data.keyword.bpshort}}.
{:shortdesc}

## Despliegue en sus entornos con la interfaz gráfica de usuario
{: #gui}

Si previere una vista gráfica para desplegar el entorno, puede utilizar el panel de control de {{site.data.keyword.bpshort}}.
{:shortdesc}


### Requisito previo
{: #gui-prereq}

* Almacene una configuración de Terraform en el control de origen. Las configuraciones se pueden escribir en sintaxis de HashiCorp Configuration Language (HCL) o de JSON. Consulte los <a href="https://www.terraform.io/docs/configuration/index.html">documentos de configuración de Terraform <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> para obtener la sintaxis de HCL y directrices sobre cómo escribir configuraciones. Consulte los recursos disponibles con el proveedor de <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} Cloud<img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a>.

Después de almacenar la configuración:

1. En el panel de control de **{{site.data.keyword.bpshort}}**, seleccione **Entornos**.

2. Pulse **Crear entorno** para añadir un entorno, o bien seleccione la fila de un entorno existente que desee desplegar.

3. Pulse **Plan** para previsualizar los recursos suministrados cuando despliega el entorno. Al ejecutar el plan, {{site.data.keyword.bpshort}} extrae las variables de los detalles de su entorno y la última versión de su configuración desde el control de origen. La salida del plan muestra cómo la configuración lo compara con lo que está desplegado de acuerdo con el archivo de estado de Terraform. Su entorno se bloquea a más cambios hasta que el plan se aplique al entorno o se cancele. 

4. Consulte el registro en la sección **Actividad reciente** para inspeccionar la salida del plan. La salida del plan muestra si existen errores y qué recursos el servicio planea crear, cambiar o destruir.

5. Cuando esté listo para iniciar el plan, pulse **Aplicar**. Puede supervisar el registro de actividad para asegurarse de que el plan se ha aplicado correctamente en la última ejecución. 


## Despliegue en sus entornos con la CLI
{: #cli}

Puede utilizar el plugin de {{site.data.keyword.bpshort}} para que la CLI de {{site.data.keyword.Bluemix_notm}} despliegue las actualizaciones en su entorno.
{:shortdesc}

### Requisitos previos
{: #cli-prereq}

* Almacene una configuración de Terraform en el control de origen.
* Su aún no tiene, instale la CLI de {{site.data.keyword.Bluemix_notm}} para su sistema operativo desde el repositorio de la CLI de [{{site.data.keyword.Bluemix_notm}}](http://clis.ng.bluemix.net/ui/home.html).

Después de iniciar sesión en la CLI de {{site.data.keyword.Bluemix_notm}}:

1. Instale el plugin de CLI de {{site.data.keyword.bpshort}} ejecutando el siguiente mandato.
  
  ```
  bx plugin install schematics -r Bluemix
  ```
  {: codeblock}

  El plugin de {{site.data.keyword.bpshort}} aparece bajo `bx plugin list`, si la instalación es correcta. 

2. Cree un entorno desde su configuración. Al crear su entorno, el servicio está apuntando al control de origen, de manera que pueda extraer el código más reciente.  
  
  ```
  bx schematics environment create --file FILE_NAME
  ```
  {: codeblock}
  
  <table summary="Descripción del mandato environment create.">
  <caption>Tabla 1. Descripción del mandato environment create.
  </caption>
  <thead>
  <th colspan="1">Mandato</th>
  <th colspan="1">Qué está haciendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--file FILE_NAME</td>
  <td>El archivo JSON donde se almacena información detallada sobre su entorno.<p>
  <p>JSON de ejemplo:
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
  }</pre>
  </td>
  </tr>
  </tbody></table>
  
  Tenga en cuenta el valor de `ID` que se devuelve. El `ID` es un identificador exclusivo que se asigna a su entorno y se utiliza en los mandatos posteriores. 
  
3. Ejecute el mandato `plan` para previsualizar cómo cambiaría su entorno. El mandato plan muestra qué recursos cambiarían y en qué cantidad, en comparación con lo que está desplegado, pero los cambios no surten efecto hasta que ejecuta el mandato `apply`.
  
  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Descripción del mandato plan.">
  <caption>Tabla 2. Descripción del mandato plan.
  </caption>
  <thead>
  <th colspan="1">Mandato</th>
  <th colspan="1">Qué está haciendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>El entorno específico para el cual desea aplicar un plan de ejecución. Puede ejecutar <code>bx schematics list</code> si necesita recuperar el valor para el ID de entorno. </td>
  </tbody></table>
  
  Se asigna un `activity_id` al plan y se registra en el registro de actividad. 

4. Recupere el registro de actividad para ver la salida del plan de Terraform.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  <table summary="Descripción del mandato log.">
  <caption>Tabla 3. Descripción del mandato log.
  </caption>
  <thead>
  <th colspan="1">Mandato</th>
  <th colspan="1">Qué está haciendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ACTIVITY_ID</td>
  <td>La actividad específica para la cual desea consultar el registro. Puede ejecutar <code>bx schematics activity list --id ENVIRONMENT_ID</code> si necesita recuperar el valor para el ID de actividad.</td>
  </tbody></table>
  
5. Ejecute el mandato `apply` para desplegar recursos en su entorno. 
  
  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
  <table summary="Descripción del mandato apply.">
  <caption>Tabla 4. Descripción del mandato apply.
  </caption>
  <thead>
  <th colspan="1">Mandato</th>
  <th colspan="1">Qué está haciendo</th>
  </thead>
  <tbody>
  <tr>
  <td>--id ENVIRONMENT_ID</td>
  <td>El entorno específico en el cual desea desplegar actualizaciones. Puede ejecutar <code>bx schematics list</code> si necesita recuperar el valor para el ID de entorno. </td>
  </tbody></table>
  
6. Supervise la salida de apply para asegurarse de que el despliegue se ha realizado correctamente. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

  Un despliegue correcto devuelve la siguiente línea hacia el final de la salida.
  
  ```
  ¡Aplicación completa! Recursos: N añadidos, N cambiados, N destruidos.
```
  {: screen}
  
## Despliegue en sus entornos con la API
{: #api}

Puede desplegar su entorno mediante programación con la API de {{site.data.keyword.bpshort}}.
{:shortdesc}

Las llamadas a la API de <a href="https://us-south.schematics.bluemix.net/swagger-api/">{{site.data.keyword.bpshort}} <img src="../../icons/launch-glyph.svg" alt="Icono de enlace externo"></a> apuntan al siguiente punto final de base:

```
https://us-south.schematics.bluemix.net
```
{: codeblock}

### Requisito previo
{: #api-prereq}

* Almacene una configuración de Terraform en el control de origen. 

Realice los pasos siguientes para desplegar recursos en su entorno:

1. Genere una señal de IAM OAuth para utilizarla en la cabecera de autenticación. El mandato genera una señal de UAA y una señal de IAM.
  
  ```
  bx iam oauth-tokens
  ```
  {: codeblock}
  
  Ejemplo de salida:
  ```
  Señal de IAM:  Portador eyJraWQ...
  ```
  {: screen}
    
  La salida de `Bearer eyJraWQ...` es un ejemplo truncado de la señal de IAM. Incluya la señal completa en la cabecera de sus llamadas de API. 
  
2. Cree un entorno ejecutando una llamada `POST v1/environments`.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
    -d '{
    "description": "(Opcional) Descripción del entorno",
    "frozen": false,
    "name": "Nombre del entorno",
    "sourceurl": "El URL de GitHub que apunta a la configuración de Terraform",
    "tags": [
      "(Opcional) metadata_tag_1",
      "(Opcional) metadata_tag_2"
    ],
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
  }'
  ```
  {: codeblock}
    
  Una respuesta correcta devuelve la siguiente salida.
  ```
  {
    "id": "ID del entorno",
    "name": "Nombre del entorno",
    "description": "Descripción del entorno",
    "account": "GUID de cuenta de {{site.data.keyword.Bluemix_notm}}",
    "owner": "El IBMid del usuario que ha creado el entorno",
    "creationtime": "YYYY-MM-DDTHH:MM:SSZ",
    "status": "CREATED",
    "frozen": false,
    "sourceurl": "El URL de GitHub que apunta a la configuración",
    "statefile": "La referencia al archivo de estado de Terraform",
    "terraformversion": "0.9",
    "tags": [
      "metadata_tag_1",
      "metadata_tag_2"
    ],
    "variablestore": [
      {
        "name": "(Opcional) variable_1",
        "value": "Valor visible"
      }
    ]
  }
  ```
  {: screen}
    
  Tenga en cuenta el valor de `id` que se devuelve. El `id` es un identificador exclusivo que se asigna a su entorno y se utiliza en las llamadas posteriores. 
  
3. Ejecute la llamada `POST v1/environments/<environment_ID>/plan` para previsualizar los recursos que se desplegarán en su entorno al aplicar la configuración. Los planes extraen las configuraciones de entorno en la rama maestra de su repositorio.
  
  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
  Una respuesta correcta devuelve un `activityid`. El valor del ID de actividad es necesario para ver los registros, como la salida de plan y apply.
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

4. Ejecute la llamada `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` para ver la salida del plan.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

5. Despliegue el entorno ejecutando la llamada `PUT v1/environments/<environment_ID>/apply/`.
  
  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}
  
6. Supervise el despliegue ejecutando la llamada `GET v1/environments/<environment_ID>/activities/<activity_ID>/log` para ver la salida de apply.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

  Un despliegue correcto devuelve la siguiente línea hacia el final de la salida.
  
  ```
  ¡Aplicación completa! Recursos: N añadidos, N cambiados, N destruidos.
```
  {: screen}
