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

# Destrucción de recursos en entornos temporales
{: #destroying}

Puede utilizar {{site.data.keyword.bplong}} para destruir recursos. Cuando destruye recursos, está destrozando su entorno y todos los recursos asociados.  
{:shortdesc}

**Aviso**: la acción de destruir recursos no se puede revertir. No se recomienda destruir recursos en entornos de producción, pero puede resultar útil para entornos temporales, como pruebas o control de calidad. 

Antes de destruir recursos, tenga en cuenta las siguientes directrices: 
* Asegúrese de que el tráfico no se dirige a los recursos.
* Asegúrese de que cualquier dato que pudiera necesitar tenga copia de seguridad. 


## Destrucción de recursos con la interfaz gráfica de usuario
{: #gui}

Puede utilizar el panel de control de {{site.data.keyword.bpshort}} para usar y destrozar entornos temporales.
{:shortdesc}

1. En el panel de control de **{{site.data.keyword.bpshort}}**, seleccione el separador **Entornos**.

2. Pulse la fila del entorno específico que desea eliminar. 

3. En el menú de opciones, seleccione **Destruir recursos** o **Suprimir entorno**. Las acciones de suprimir y destruir son irreversibles. Para determinar qué opción seleccionar, considere si dispone de recursos activos.
  * Seleccione **Destruir recursos** si desea detener y eliminar los recursos activos. Se recomienda ejecutar un plan antes de la destrucción para confirmar si los recursos que están asociados con el entorno se pueden eliminar.
  * Seleccione **Suprimir entorno** si desea eliminar la configuración del entorno del servicio de {{site.data.keyword.bpshort}}. Esta opción se utiliza normalmente si el entorno no está desplegado y no tiene recursos activos. Si selecciona esta opción con los recursos activos, ya no podrá utilizar el servicio de {{site.data.keyword.bpshort}} para realizar un seguimiento o desplegar modificaciones en su entorno. Los recursos activos tienen que gestionarse de forma individual, desde sus paneles de control de servicio.
  
  Siga las indicaciones en pantalla para confirmar su selección. 


## Destrucción de recursos con la CLI
{: #cli}

Puede utilizar la CLI de {{site.data.keyword.bpshort}} para usar y destrozar entornos temporales.
{:shortdesc}

1. Ejecute el mandato `destroy` para destruir su entorno y recursos.

  ```
  bx schematics action destroy --id ENVIRONMENT_ID
  ```
  {: codeblock}
  
2. Opcional: Ejecute el mandato `delete` si desea eliminar su configuración del servicio.

  ```
  bx schematics environment delete --id ENVIRONMENT_ID
  ```
  {: codeblock}


## Destrucción de recursos con la API
{: #api}

Puede utilizar la API de {{site.data.keyword.bpshort}} para usar y destrozar entornos temporales.
{:shortdesc}

1. Ejecute la llamada `PUT v1/environments/<environment_ID>/destroy` para destruir los recursos.

  ```
  curl -X PUT \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID>/destroy \
    -H 'accept: application/json' \
    -H 'authorization: bearer <IAM_token>' \
    -H 'content-type: application/json'
  ```
  {: codeblock}

2. Opcional: Ejecute la llamada `DELETE v1/environments/<environment_ID>` si desea eliminar la configuración del servicio {{site.data.keyword.bpshort}}. 

  ```
  curl -X DELETE \
    https://us-south.schematics.bluemix.net/v1/environments/<environment_ID> \
    -H 'accept: text/plain' \
    -H 'authorization: bearer <IAM_token>'
  ```
  {: codeblock}
