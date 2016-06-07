---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administración de {{site.data.keyword.iotdriverinsights_short}}
{: #1stanchor}
*Última actualización: 6 de mayo de 2016*


La administración de {{site.data.keyword.iotdriverinsights_full}} incluye visualizar la información de arrendatario y restablecer la contraseña del arrendatario, configurar los parámetros para el servicio y gestionar los datos almacenados en el servicio.
{:shortdesc}

Puede realizar las tareas de administración desde la {{site.data.keyword.iotdriverinsights_full}} Consola de administración. 

Para acceder a la Consola de administración: 

1. Vaya a la vista **Gestionar** de la instancia del servicio. 
2. Pulse **Iniciar**. Se abre la **Consola de administración** en una nueva ventana. 
3. Especifique el *nombre de usuario* y la *contraseña* como se muestra en la vista **Gestionar** y pulse **Iniciar sesión**.

## Visualización de la información de arrendatario
{: #viewtenantinfo}

Después de iniciar sesión en la **Consola de administración**, puede ver la vista **Información de arrendatario** y la información del arrendatario. 

## Restablecimiento de la contraseña de arrendatario
{: #resettenantpassword}

En la vista **Información de arrendatario**: 

1. Pulse **RESTABLECER**.
2. En el diálogo de confirmación, pulse **ACEPTAR**.
Se muestra la contraseña en la vista **Información de arrendatario**.

## Configuración de parámetros para el servicio
{: #configureparameters}

Pulse **Parámetros** en el panel de navegación. Se abre la vista **Parámetros** y se muestran los parámetros. 

Puede editar los parámetros para modificar los resultados del análisis. 

En la siguiente tabla se describen los parámetros de comportamiento: 

|Categoría|Nombre de parámetro|Descripción|Valor predeterminado|
|:-------:|:--------:|:--------|:-------:|
|Límite de velocidad (km/h)|\-|Límite de velocidad para cada tipo de carretera. Si la velocidad del vehículo es superior a este valor en la carretera de cada tipo, el servicio lo identifica como exceso de velocidad. |\-|
|Límite de velocidad (km/h)|Autopista|Límite de velocidad para la autopista|120|
|Límite de velocidad (km/h)|Autovía urbana|Límite de velocidad para las autovías urbanas|90|
|Límite de velocidad (km/h)|Vía urbana principal|Límite de velocidad para la vía urbana principal|60|
|Límite de velocidad (km/h)|Carretera urbana|Límite de velocidad para la carretera urbana|40|
|Límite de velocidad (km/h)|Otros|Límite de velocidad para otros|30|
|Límite de velocidad (km/h)|Desconocido |Límite de velocidad desconocido|120|
|Girar|Velocidad angular (Mín \- Máx, deg/s)|Valor de velocidad angular en las curvas. El valor mínimo se utiliza como umbral para identificar el segmento de giro. El valor máximo se utiliza para detectar un comportamiento de giro brusco. |10 \- 25|
|Girar|Velocidad media (km/h)|Velocidad normal durante el giro. Este valor se utiliza para identificar comportamientos en segmentos de giro junto con los valores de velocidad angular. |60|
|Fatiga de conducción|Tiempo de conducción continuada (s)|Si un vehículo se conduce durante un período superior al indicado por este valor, el servicio lo identifica como fatiga de conducción. |10800|

En la siguiente tabla se describen los parámetros de contexto: 

|Categoría|Nombre de parámetro|Descripción|Valor predeterminado|
|:-------:|:--------:|:--------|:-------:|
|Huso horario de análisis|\-|Huso horario aplicado para el análisis |+00:00|
|Intervalo de tiempo|\-|Este valor define el tipo de período de tiempo|\-|
|Intervalo de tiempo|Día|Intervalo de horas durante el día|1030 \- 1730|
|Intervalo de tiempo|Noche|Intervalo de horas durante la noche|2030 \- 0700|
|Intervalo de tiempo|Pico de la mañana|Intervalo de horas durante el pico del día|0700 \- 1030|
|Intervalo de tiempo|Pico de la tarde|Intervalo de horas durante el pico de la tarde|1730 \- 2030|
|Tipo de carretera|\-|Estos valores se utilizan para correlacionar el valor de tipo de carretera de usuario en los datos de entrada con las clasificaciones de tipo de carretera únicas de {{site.data.keyword.iotdriverinsights_short}}. Si no tiene un valor de tipo de carretera, puede recuperar el valor mediante la API REST `getLinkInformation` proporcionada por **{{site.data.keyword.iotmapinsights_short}}**. El tipo de carretera se almacena en **propiedades > tipo** en la respuesta. [Ejemplo JSON](#sampleJson) representa la posición de `type` en la respuesta. |\-|
|Tipo de carretera|Autopista|Valor de tipo de carretera correlacionado con autopista|1|
|Tipo de carretera|Autovía urbana|Valor de tipo de carretera correlacionado con autovía urbana|2|
|Tipo de carretera|Vía urbana principal|Valor de tipo de carretera correlacionado con vía urbana principal|3|
|Tipo de carretera|Carretera urbana|Valor de tipo de carretera correlacionado con carretera urbana|4|
|Tipo de carretera|Otros|Valor de tipo de carretera correlacionado con otros|5|
|Límite de velocidad (Bajo \- Alto, km/h)|\-|Este valor define el intervalo de velocidad media para cada tipo de carretera. |\-|
|Límite de velocidad (Bajo \- Alto, km/h)|Autopista|Intervalo de velocidad media para autopista|55 \- 85|
|Límite de velocidad (Bajo \- Alto, km/h)|Autovía urbana|Intervalo de velocidad media para autovía urbana|35 \- 65|
|Límite de velocidad (Bajo \- Alto, km/h)|Vía urbana principal|Intervalo de velocidad media para vía urbana principal|20 \- 40|
|Límite de velocidad (Bajo \- Alto, km/h)|Carretera urbana|Intervalo de velocidad media para carretera urbana|15 \- 35|
|Límite de velocidad (Bajo \- Alto, km/h)|Otros|Intervalo de velocidad media para otros|10 \- 20|
|Límite de velocidad (Bajo \- Alto, km/h)|Desconocido |Intervalo de velocidad media para desconocido|20 \- 60|


Para aplicar cambios a parámetros:

1. Pulse **GUARDAR**. 
2. En el diálogo de confirmación, pulse **ACEPTAR**. 

A continuación, se aplican los nuevos parámetros, que pasan a ser efectivos para el siguiente trabajo emitido. 

### Respuesta JSON de ejemplo de la API REST "getLinkInformation"
{: #sampleJson}

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


## Gestión de datos almacenados en el servicio
{: #managedata}

- Pulse **Gestión de datos** en el panel de navegación. Puede ver la vista **Gestión de datos** y los datos de los resultados del análisis de coches. 
- Para eliminar los datos, pulse **ELIMINAR** en un registro.
