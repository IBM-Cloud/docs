---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-22"
---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}



<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->

# Copia de seguridad de datos
Puede realizar la copia de seguridad de los datos de {{site.data.keyword.iotinsurance_full}} replicando la base de datos de {{site.data.keyword.cloudantfull}}.
{:shortdesc}

En la tabla siguiente se muestran las bases de datos de {{site.data.keyword.iotinsurance_short}} que se almacenan en {{site.data.keyword.iotinsurance_full}}.

*Tabla 1: Bases de datos de {{site.data.keyword.iotinsurance_short}}*

Nombres de base de datos| Frecuencia de cambio| Razón del cambio | Requiere copia de seguridad | Comentarios
------------- | -------------| -------------| -------------| -------------
favorites|Administración|Nueva acción de administrador|YES|-
Devices|Administración|Nuevos dispositivos o usuarios añadidos o eliminados|YES| El transformador genera una tabla de forma dinámica en la memoria y la rellena con datos del proveedor del dispositivo. Para pasarelas conectadas directamente, esta tabla almacena los dispositivos.
hazardevents|Aleatoria|Detectado nuevo suceso de cobertura|YES|-
Jscode|Administración|Desplegado nuevo código JS para coberturas|YES*| De forma opcional, el administrador puede omitir la copia de seguridad y desplegar una versión nueva del código JS.
Promotions|Administración|Nueva promoción añadida|YES|-
shieldassociations|Administración|Nuevo usuario o cobertura añadidos|YES|-
Shields|Administración|Nueva cobertura añadida|YES|-
Users|Administración|Nuevo usuario añadido|YES|-
aggregation|-|-|NO|Se puede volver a crear.
aggregationschedule|-|-| NO|Se puede volver a crear.

Para realizar la copia de seguridad de los datos de {{site.data.keyword.iotinsurance_short}}, lleve a cabo los siguientes pasos:

## Creación de una instancia de {{site.data.keyword.cloudant_short_notm}} de réplica
{: #createinstance}
Cree una instancia de {{site.data.keyword.cloudant}} de réplica utilizando las instrucciones de réplica de [{{site.data.keyword.cloudant}} ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://docs.cloudant.com/replication.html). Para fines de recuperación tras desastre, cree la réplica en una ubicación distinta del servicio de {{site.data.keyword.iotinsurance_short}} original. Por ejemplo, si la instancia original está en Dallas, la réplica podría estar en Londres.

## Localización de credenciales y URL
{: #locate_credentials}
Localice las credenciales y los URL para la instancia de {{site.data.keyword.cloudant}} original y la instancia replicada.
1. Abra el servicio {{site.data.keyword.cloudant}}.
2. Pulse el separador **Credenciales de servicio**, situado bajo el nombre del servicio.
3. Pulse **Ver credenciales**.
4. Tome nota del nombre de usuario, contraseña y URL.

## Creación de nuevas tareas de réplica
{: #create_replication}
Cree una tarea de réplica para cada base de datos que debe tener copia de seguridad. Las bases de datos que requieren copia de seguridad se listan en la Tabla 1 de la sección anterior.

1. Abra la consola de {{site.data.keyword.Bluemix_notm}}.

2. Abra el servicio {{site.data.keyword.cloudant}} original.

3. Pulse **Iniciar** para abrir el panel de control de {{site.data.keyword.cloudant}}.

4. En el menú, seleccione **Réplica**.

5. Especifique el URL de la base de datos original en la sección Base de datos de origen. Cada URL de base de datos está en el formato https://<CloudantbaseURL>/<nombre_basedatos>.  Por ejemplo, el URL de la base de datos hazardevents sería https://<CloudantbaseURL>/hazardevents.

6. Especifique el URL de la nueva base de datos en la Sección Base de datos de destino.

7. **Importante:** No seleccione **Convertir esta réplica en continua**.  La réplica continua afecta gravemente al rendimiento.

8. Pulse **Replicar datos**.  

9. (opcional) Como las tareas de réplica posteriores sobrescriben los datos anteriores, considere la opción de exportar los datos a un archivo CSV.  Para obtener instrucciones, consulte [Exportar Cloudant JSON como CSV, RSS o iCal ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://developer.ibm.com/clouddataservices/2015/09/22/export-cloudant-json-as-csv-rss-or-ical/){: new_window}.

10. Repita estos pasos para cada base de datos.

## Ejecución de una copia de seguridad
{: #run_backup}
Después de crear las tareas de réplica, puede volver a ejecutar copias de seguridad en cualquier momento.
1. Abra la consola de {{site.data.keyword.Bluemix_notm}}.
2. Abra el servicio {{site.data.keyword.cloudant}} original.
3. Pulse **Iniciar** para abrir el panel de control de {{site.data.keyword.cloudant}}.
4. En el menú, pulse **Réplica** y, a continuación, seleccione **Todas las réplicas**.
5. Seleccione todas las bases de datos y vuelva a ejecutar cada réplica. Puede comprobar el estado de los trabajos en curso pulsando **Réplicas activas**.
6. Una vez completadas todas las réplicas, puede exportar los datos a un archivo plano CSV.

## Restauración de los datos
{: #restore_data}
Puede restaurar los datos de una base de datos replicada o cargando un archivo CSV guardado.
1. Abra la consola de {{site.data.keyword.Bluemix_notm}}.
2. Detenga el servicio {{site.data.keyword.iotinsurance_short}}.
3. Restaure los datos de una de estas formas:
  - Cargue los datos desde un archivo de copia de seguridad CSV directamente a la instancia de Cloudant primaria
  - Cree una tarea de réplica que tenga la base de datos replicada como el origen y la base de datos original como el destino. Esta tarea transfiere los datos replicados a la base de datos original.
4. Ejecute los siguientes scripts para volver a crear documentos de diseño y restaurar la integridad referencial.  Los scripts están ubicados en el [{{site.data.keyword.iotinsurance_short}} sitio de GitHub de ejemplos de API ![Icono de enlace externo](../../icons/launch-glyph.svg)](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/){: new_window}.
  - iot4i-api/wearable-framework/auto-create/create.sh - Este script vuelve a crear los documentos de diseño en {{site.data.keyword.cloudant}}.
  - iot4i-api/wearable-framework/health/check-relations - Este script restablece la integridad referencial. Por ejemplo, el script corrige un caso en el que se suprime la cobertura pero aún existe la asociación a un usuario.
