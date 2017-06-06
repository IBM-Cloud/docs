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

# Gestión de recursos en sus entornos
{: #managing}

{{site.data.keyword.bplong}} simplifica la gestión de sus entornos. Puede modificar los recursos desplegados y volver a desplegar repetidamente los cambios a petición.

{:shortdesc}

Los cambios en su entorno se pueden desplegar con un proceso ligero. Si desea cambiar los recursos asignados, codifique los cambios en su configuración en sintaxis declarativa, lo que significa que solo debe indicar el resultado deseado. Con {{site.data.keyword.bpshort}}, puede obtener una vista previa de los cambios antes del despliegue.


## Actualización de recursos con la interfaz gráfica de usuario
{: #gui}

Si previere una vista gráfica para gestionar los recursos de sus entornos, puede utilizar el panel de control de {{site.data.keyword.bpshort}}.
{:shortdesc}

Después de publicar en GitHub los cambios de código en su configuración, o modificar variables en la interfaz gráfica de usuario, realice los siguientes pasos para desplegar actualizaciones en su entorno:

1. En el panel de control de **{{site.data.keyword.bpshort}}**, seleccione **Entornos**.

2. Pulse la fila del entorno específico que desea actualizar.

3. Pulse **Plan** y revise el registro del plan en busca de errores. El entorno está bloqueado hasta que usted u otros colaboradores de su cuenta de {{site.data.keyword.Bluemix_notm}} apliquen el plan o lo cancelen. 

4. Pulse **Aplicar** para desplegar las actualizaciones. 


## Actualización de recursos con la CLI
{: #cli}

Puede actualizar los recursos en sus entornos mediante programación con la CLI de {{site.data.keyword.bpshort}}.
{:shortdesc}

Después de publicar en GitHub los cambios de código en su configuración, realice los siguientes pasos para desplegar actualizaciones en su entorno:

1. Ejecute el mandato `plan`. La CLI de {{site.data.keyword.bpshort}} toma la configuración del entorno actualizada de GitHub y genera una vista previa de las diferencias de sus recursos con el despliegue actual.

  ```
  bx schematics action plan --id ENVIRONMENT_ID
  ```
  {: codeblock}

2. Consulte la salida del plan en el registro de actividad.

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

3. Despliegue el plan ejecutando el mandato `apply`. 

  ```
  bx schematics action apply --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Actualización de recursos con la API
{: #api}

Puede gestionar los recursos en sus entornos mediante programación con la API de {{site.data.keyword.bpshort}}.
{:shortdesc}

Después de publicar en GitHub los cambios de código en su configuración, realice los siguientes pasos para desplegar actualizaciones en su entorno:

1. Ejecute la llamada `POST v1/environments/<environment_ID>/plan`. La API de {{site.data.keyword.bpshort}} toma la configuración del entorno actualizada de GitHub y la compara con el archivo de estado de Terraform para mostrar las diferencias de sus recursos con el despliegue actual.

  ```
  curl -X POST \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/plan \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

  Ejemplo de respuesta:
  ```
  {
    "activityid": "<activity_ID>"
  }
  ```
  {: screen}

2. Consulte la salida del plan en el registro de actividad.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Despliegue el plan ejecutando la llamada `PUT /v1/environments/<environment_ID>/apply`. 

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/apply \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json' \
  ```
  {: codeblock}


## Auditoría de cambios en sus entornos
{: #auditing}

Las configuraciones pueden auditarse en el historial de versiones de su repositorio de control de origen. Para supervisar despliegues en su entorno, o ver registros de despliegues anteriores, {{site.data.keyword.bpshort}} ofrece las siguientes opciones para visualizar los registros de auditoría. 

### Desde el panel de control de {{site.data.keyword.bpshort}} 
{: #auditing-gui}

1. Seleccione la fila del entorno para acceder a la página de detalles del entorno.

2. Supervise la sección **Actividades recientes**. También puede consultar los registros históricos de planes y despliegues anteriores.

### Con la CLI de {{site.data.keyword.bpshort}} 
{: #auditing-cli}

1. Recupere el ID del entorno. 

  ```
  bx schematics environment list
  ```
  {: codeblock}

2. Recupere los ID de actividad para su entorno. Los ID de actividad se asignan para planificar, aplicar, destruir y suprimir acciones. El mandato siguiente genera una lista de todas las actividades que se han ejecutado en su entorno. 

  ```
  bx schematics activity list --id ENVIRONMENT_ID
  ```
  {: codeblock}

3. Recupere los datos sobre una actividad específica, como quién ha realizado los cambios en un entorno y cuándo.

  ```
  bx schematics activity show --id ACTIVITY_ID
  ```
  {: codeblock}

4. Opcional: para consultar un registro detallado, como la salida de plan o apply, ejecute el mandato `log`. 

  ```
  bx schematics activity log --id ACTIVITY_ID
  ```
  {: codeblock}

### Con la API de {{site.data.keyword.bpshort}}
{: #auditing-api}

1. Recupere el ID del entorno. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
  
  El cuerpo de respuesta contiene todos los entornos de su cuenta de {{site.data.keyword.Bluemix_notm}}. Localice el valor de `id` del entorno específico que desea auditar. 

2. Recupere los ID de actividad para las acciones que se ejecutan en su entorno.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

3. Obtenga una actividad específica para un entorno. 

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID> \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}

4. Revise un informe detallado de la salida de Terraform.

  ```
  curl -X GET \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/activities/<activity_ID>/log \
    -H 'accept: text/html' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
