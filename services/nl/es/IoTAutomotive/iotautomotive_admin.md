---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administración de {{site.data.keyword.iot4auto_short}}
{: #1stanchor}
Última actualización: 29 de julio de 2016
{: .last-updated}

Administre la instancia de servicio de {{site.data.keyword.iot4auto_full}} mediante la consola de administración del panel de control de {{site.data.keyword.Bluemix_notm}}. Desde la consola de administración, puede configurar los parámetros de {{site.data.keyword.iot4auto_short}} y gestionar los datos que se almacenan en el servicio. Además, puede visualizar la información de arrendatario, así como restablecer su contraseña. 

{:shortdesc}

## Inicio de la consola de administración
{: #start_admin_console}

Para acceder a la consola de administración del servicio {{site.data.keyword.iot4auto_short}}:

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico del servicio {{site.data.keyword.iot4auto_short}}. 
2. Seleccione la vista **Gestionar** de la instancia de servicio.
Anote las credenciales de nombre de usuario y contraseña ya que las necesitará más adelante. Para acceder a la consola de administración, necesita el ID de IBM, que puede no ser el mismo que las credenciales de {{site.data.keyword.Bluemix_notm}}. 
3. Pulse **Iniciar** y, cuando se solicite, indique las credenciales de IBM. 
4. Haga clic en **INICIAR SESIÓN**. Se abrirá la ventana **Consola de administración**.

## Gestión de la información de arrendatario
{: #view_tenant_info}

Para ver la información de arrendatario, haga clic en **Información de arrendatario**.

### Restablecimiento de la contraseña de arrendatario
{: #reset_tenant_password}

Para restablecer la contraseña del arrendatario:

1. En la ventana **Información de arrendatario**, pulse **RESTABLECER**.
2. En el recuadro de diálogo, haga clic en **Aceptar**.
Se generará una contraseña nueva, que se mostrará en la vista **Información de arrendatario**.
**Importante:** asegúrese de actualizar la contraseña en todas las aplicaciones que acceden a la API de {{site.data.keyword.iot4auto_short}}.

## Configuración de los parámetros de servicio
{: #configure_parameters}

Los parámetros de servicio controlan cómo se analizan los datos de viaje. Para modificarlo:

1. Abra la vista **Parámetros** y ajuste los parámetros de servicio siguientes:
  - Haga clic en el separador **Comportamiento** y actualice los [parámetros de comportamiento de conducción](#behavior_parameters) para que cumplan sus requisitos.
  - Haga clic en el separador **Contexto** y actualice los [parámetros de correlación de contexto](#context_parameters) para que cumplan sus requisitos.
2. Pulse **GUARDAR**.
3. Pulse **Aceptar**.

Los valores de los parámetros actualizados se aplicarán en el siguiente trabajo que se envíe.

### Parámetros de comportamiento de conducción
{: #behavior_parameters}


En las tablas siguientes, se describen los parámetros de comportamiento de conducción para las categorías que puede configurar en el separador **Comportamiento**.

#### Valores de límite de velocidad

Puede especificar el límite de velocidad en km/h para cada tipo de carretera. Si la velocidad supera el valor de límite que especifique para ese tipo de carretera, se detectará el exceso de velocidad. 

|Nombre de parámetro|Descripción|Valor predeterminado (km/h)|
|:--------|:--------|:-------|
|Autopista|Límite de velocidad para el tipo de carretera Autopista|120|
|Autovía urbana|Límite de velocidad para el tipo de carretera Autovía urbana|90|
|Vía urbana principal|Límite de velocidad para el tipo de carretera Vía urbana principal|60|
|Carretera urbana|Límite de velocidad para el tipo de carretera Carretera urbana|40|
|Otros|Límite de velocidad para el tipo de carretera clasificado como Otros|30|
|Desconocido|Límite de velocidad para el tipo de carretera Desconocido|120|
*Tabla 1. Parámetros de configuración del límite de velocidad*

#### Valores de giro

|Nombre de parámetro|Descripción|Valor Predeterminado|
|:--------|:--------|:-------|
|Velocidad angular (Mín \- Máx, deg/s)|Valor de velocidad angular en una curva. El valor mínimo se utiliza como umbral para identificar el segmento de giro. El valor máximo se utiliza para detectar un comportamiento de giro brusco.|10 \- 25|
|Velocidad media (km/h)|Velocidad normal durante un giro. Este valor se utiliza para identificar comportamientos en segmentos de con los valores de velocidad angular. |60|
*Tabla 2. Parámetros de configuración de giro de vehículo*

#### Valores de fatiga de conducción

|Nombre de parámetro|Descripción|Valor Predeterminado|
|:--------|:--------|:-------|
|Tiempo de conducción continuada (s)|La longitud máxima de conducción continuada que se permite.|10800|
*Tabla 3. Parámetros de configuración para la detección de la fatiga de conducción*

### Parámetros de correlación de contexto
{: #context_parameters}

En las tablas siguientes, se describen los parámetros de correlación de contexto para las categorías que puede configurar en el separador **Contexto**.

#### Parámetros de intervalo de tiempo y huso horario

Especifique el huso horario y las horas para cada periodo de tiempo.

|Nombre de parámetro|Descripción|Valor Predeterminado|
|:--------|:--------|:-------|
|Huso horario de análisis|Huso horario aplicado para análisis. |+00:00|
|Día|Intervalo de horas durante el día.|1030 \- 1730|
|Noche|Intervalo de horas durante la noche.|2030 \- 0700|
|Pico del día|Intervalo de horas durante el pico del día.|0700 \- 1030|
|Pico de la noche|Intervalo de horas durante el pico de la noche.|1730 \- 2030|
*Tabla 4. Parámetros de configuración del intervalo de tiempo y del huso horario*

#### Tipos de carretera

Los parámetros de tipos de carretera se utilizan para correlacionar los valore de tipo de carretera con los datos introducidos en las clasificaciones de tipo de carretera de {{site.data.keyword.iot4auto_short}}. Si no dispone de un valor de tipo de carretera, puede recuperarlo con el mandato de la API REST `getLinkInformation` que proporciona el servicio {{site.data.keyword.iotmapinsights_short}}.

El valor de tipo de carretera se devuelve y almacena en la sección de propiedades de la respuesta JSON de `getLinkInformation` JSON y se define como `type`, tal y como se describe en [Ejemplo de respuesta JSON para `getLinkInformation`](#sampleJson).


|Nombre de parámetro|Descripción|Valor Predeterminado|
|:--------|:--------|:-------|
|Autopista|Valor de tipo de carretera que se correlaciona con Autopista.|1|
|Autovía urbana|Valor de tipo de carretera que se correlaciona con Autovía urbana.|2|
|Vía urbana principal|Valor de tipo de carretera que se correlaciona con Vía urbana principal.|3|
|Carretera urbana|Valor de tipo de carretera que se correlaciona con Carretera urbana.|4|
|Otros|Valor de tipo de carretera que se correlaciona con Otros.|5|
*Tabla 5. Parámetros de configuración de tipo de carretera*

#### Umbral de velocidad

Los parámetros de umbral de velocidad definen el intervalo de velocidad media para el tipo de carretera en km/h. El intervalo de velocidad media es el intervalo entre los valores más altos y más bajos que se especifican. 

|Nombre de parámetro|Descripción|Valor Predeterminado|
|:--------|:--------|:-------|
|Autopista|El intervalo de velocidad media para el tipo de carretera Autopista.|55 \- 85|
|Autovía urbana|El intervalo de velocidad media para el tipo de carretera Autovía urbana.|35 \- 65|
|Vía urbana principal|El intervalo de velocidad media para el tipo de carretera Vía urbana principal.|20 \- 40|
|Carretera urbana|El intervalo de velocidad media para el tipo de carretera Carretera urbana.|15 \- 35|
|Otros|El intervalo de velocidad media para el tipo de carretera Otros.|10 \- 20|
|Desconocido|El intervalo de velocidad media para el tipo de carretera Desconocido.|20 \- 60|
*Tabla 6. Parámetros de configuración del umbral de velocidad*


### Ejemplo de respuesta JSON para `getLinkInformation`
{: #sampleJson}

El código siguiente es un ejemplo de respuesta JSON del mandato de API REST `getLinkInformation`:

```
{
	"links": [{
		"internal_link_id": "32088220365736308",
		"external_link_id": "3846419005",
		...
		"properties": {
			"type": "5",
			...
		},
		...
	}]
}
```
{: screen}

## Supresión de datos almacenados en el servicio
{: #managedata}

Los datos de sondeo de coche, los datos de contexto y los resultados de análisis se almacenan en el servicio hasta que se supriman.

Para suprimir los datos almacenados en el servicio:

1. Para visualizar los datos de sondeo de coche y los resultados de análisis, haga clic en **Gestión de datos**.
2. Seleccione un registre y pulse **SUPRIMIR**.
