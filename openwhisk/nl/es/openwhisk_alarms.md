---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Uso del paquete Alarm
{: #openwhisk_catalog_alarm}

El paquete `/whisk.system/alarms` se puede utilizar para activar un desencadenante con una frecuencia especificada. Esto es útil
para configurar trabajos o tareas recurrentes, como la invocación de una acción de copia de seguridad del sistema cada hora.

El paquete incluye la información de entrada siguiente.

| Entidad | Tipo | Parámetros | Descripción |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | paquete | - | Utilidad de alarmas y periodicidad |
| `/whisk.system/alarms/alarm` | canal de información | cron, trigger_payload, maxTriggers | Activar suceso desencadenante de forma periódica |


## Activación periódica de un suceso desencadenante
{: #openwhisk_catalog_alarm_fire}

La información de entrada `/whisk.system/alarms/alarm` configura un servicio de alarma para activar un suceso desencadenante
con una frecuencia especificada. Los parámetros son según se indica a continuación:

- `cron`: una serie, basada en la sintaxis crontab de UNIX, que indica cuándo activar el desencadenante en Hora Universal Coordinada (UTC). La serie es una secuencia de cinco campos separados por espacios: `X X X X X`.
Para obtener más detalles sobre cómo utilizar sintaxis cron, consulte: http://crontab.org. A continuación se muestran algunos ejemplos de la frecuencia indicada por la serie:

  - `* * * * *`: cada minuto en punto.
  - `0 * * * *`: a cada hora en punto.
  - `0 */2 * * *`: cada 2 horas (p. ej. 02:00:00, 04:00:00, ...)
  - `0 9 8 * *`: a las 9:00:00AM (UTC) en el octavo día de cada mes

- `trigger_payload`: el valor de este parámetro pasa a ser el contenido del desencadenante cada vez que se activa
el desencadenante.

- `maxTriggers`: dejar de activar desencadenantes cuando se alcanza este límite. El valor predeterminado es 1.000.000. Puede establecerlo en infinite (-1).

A continuación se muestra un ejemplo de la creación de un desencadenante que se activará una vez cada 2 minutos con los valores `name` y `place` en el suceso desencadenante.

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

Cada suceso generado incluirá como parámetros las propiedades especificadas en el valor `trigger_payload`. En este caso,
cada suceso desencadenante tendrá los parámetros `name=Odin` y `place=Asgard`.

**Nota**: el parámetro `cron` también da soporte a una sintaxis personalizada de seis campos, donde el primer campo representa segundos. 
Para obtener más detalles sobre cómo utilizar esta sintaxis cron personalizada, consulte: https://github.com/ncb000gt/node-cron. 
A continuación se muestra un ejemplo que utiliza la notación de seis campos:
  - `*/30 * * * * *`: cada treinta segundos.

