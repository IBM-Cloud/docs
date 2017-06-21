---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-13"

---

<!-- Attribute definitions -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.streaminganalyticsshort}} resolución de problemas 
{: #ts_StreamingAnalytics}

Puede encontrar respuestas a preguntas comunes sobre cómo utilizar {{site.data.keyword.streaminganalyticsshort}} en {{site.data.keyword.Bluemix_short}}.
{:shortdesc}

##Cuando inicio el servicio, me solicitan credenciales para iniciar sesión en la consola
{: #log_in_console}

Al iniciar {{site.data.keyword.streaminganalyticsshort}}, se le solicitarán las credenciales para iniciar sesión en la consola de servicio.
{:shortdesc}

Inicie un servicio {{site.data.keyword.streaminganalyticsshort}} que se ha creado previamente y, en lugar de acceder directamente a la consola de servicio, verá una página de inicio de sesión donde se le solicitarán las credenciales.
{: tsSymptoms}

La infraestructura de servicio se ha actualizado y la memoria caché del navegador está impidiendo que el servicio seleccione la actualización.
{: tsCauses}

Borre la memoria caché del navegador para asegurarse de obtener la versión más reciente de la consola de servicio.
{: tsResolve}

##Mi aplicación no funciona correctamente
{: #app_unhealthy}

No puede ejecutar la aplicación correctamente y su estado es `unhealthy`.
{:shortdesc}

Envía una aplicación a la instancia del servicio, la aplicación se inicia pero falla de inmediato y su estado es `unhealthy`. Aparece el siguiente error en el archivo de registro: `/lib64/libc.so.6: no se ha encontrado la versión GLIBC_2.14`.
{: tsSymptoms}

No ha compilado la aplicación con un sistema operativo RHEL 6.5 o una versión de CentOS equivalente.
{: tsCauses}

Debe volver a compilar la aplicación en un sistema operativo Red Hat Enterprise Linux (RHEL) 6.5 o una versión de CentOS equivalente utilizando procesadores Intel. Vuelva a enviar la aplicación a la instancia del servicio.
{: tsResolve}
