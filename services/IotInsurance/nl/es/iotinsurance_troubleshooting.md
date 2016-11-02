---

copyright:
  years: 2016
lastupdated: "2016-10-06"

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# Resolución de problemas
{: #troubleshooting}

A continuación se muestran las respuestas a las preguntas más habituales sobre resolución de problemas acerca del uso de {{site.data.keyword.iotinsurance_full}} en {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

## Problema al desplegar las apps
{: #deployingapps}

Es posible que no pueda desplegar las apps para {{site.data.keyword.iotinsurance_short}} si no tiene suficiente memoria libre en su organización de {{site.data.keyword.Bluemix_notm}}. Puede reducir la memoria que utilizan sus apps o aumentar la cuota de memoria de su cuenta.

### ¿Qué está pasando?

Cuando abre el servicio {{site.data.keyword.iotinsurance_short}}, la función Desplegar no está habilitada y no puede desplegar ninguna app.

### ¿Por qué está pasando?

Debe haber al menos 2 GB de memoria libre en su organización para habilitar la función Desplegar. Las cuentas de prueba tienen una cuota de memoria máxima de 2 GB. Si ha creado servicios o apps que no son de {{site.data.keyword.iotinsurance_short}}, su organización no tiene suficiente memoria para desplegar las apps de {{site.data.keyword.iotinsurance_short}}.

### ¿Cómo arreglarlo?

Puede aumentar la cuota de memoria de su cuenta o reducir la memoria que utilizan sus servicios y aplicaciones.

  - Para aumentar la cuota de memoria de su cuenta, puede [convertir su cuenta de prueba en una cuenta de pago](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts).

  - Para reducir la memoria en uso rápidamente, elimine todos los servicios y apps que no sean de {{site.data.keyword.iotinsurance_short}}. Reinicie el servicio {{site.data.keyword.iotinsurance_short}} para que los cambios entren en vigor.

  - Para las cuentas de pago que tienen más de 2 GB de memoria total, es posible que pueda evitar tener que eliminar otros servicios o apps ajustando la cantidad de memoria que utilizan. Para obtener información, consulte [El límite memoria de la organización se ha excedido](https://console.ng.bluemix.net/docs/troubleshoot/ts_apps.html#ts_outofmemory).
