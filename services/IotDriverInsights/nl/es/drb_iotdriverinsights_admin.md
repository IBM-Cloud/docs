---

copyright:
  año: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Administración de Driving Behavior Analysis
{: #1stanchor}
Última actualización: 19 de junio de 2016
{: .last-updated}

Administre la instancia de servicio {{site.data.keyword.iotdriverinsights_full}} utilizando la consola de administración en el panel de control de {{site.data.keyword.Bluemix_notm}}.
En la consola de administración se pueden configurar parámetros para {{site.data.keyword.iotdriverinsights_short}} y gestionar los datos almacenados en el servicio. También puede ver la información de arrendatario y restablecer la contraseña de arrendatario.

{:shortdesc}

## Inicio de la consola de administración
{: #start-admin-console}

Para acceder a la consola de administración para el servicio {{site.data.keyword.iotdriverinsights_short}}:

1. En el panel de control de {{site.data.keyword.Bluemix_notm}}, pulse el mosaico del servicio {{site.data.keyword.iotdriverinsights_short}}.
2. Seleccione la vista **Gestionar** de la instancia de servicio.
Anote las credenciales de *Nombre de usuario* y *Contraseña*. Para acceder a la consola de administración, es necesario el ID de IBM, que puede que no sea el mismo que sus credenciales de {{site.data.keyword.Bluemix_notm}}.
3. Pulse **Iniciar** y, cuando se le solicite, escriba las credenciales de ID de IBM. 
4. Pulse **INICIAR SESIÓN**. Se abre la **Consola de administración** en una nueva ventana. 

## Gestión de la información de arrendatario
{: #viewtenantinfo}

Para ver la información de arrendatario, pulse **Información de arrendatario**.

### Restablecimiento de la contraseña de arrendatario
{: #resettenantpassword}

Para restablecer la contraseña de arrendatario:

1. En la ventana **Información de arrendatario**, pulse **RESTABLECER**.
2. En el cuadro de diálogo de confirmación, pulse **Aceptar**.
Se genera una nueva contraseña y se visualiza en la vista **Información de arrendatario**.
**Importante:** Asegúrese de que actualiza la contraseña en todas las aplicaciones que acceden a la API de {{site.data.keyword.iotdriverinsights_short}}.

## Configuración de parámetros de servicio
{: #configureparameters}

Los parámetros de servicio controlan cómo se analizan los datos de trayectos. Para modificar los parámetros de servicio: 

1. Abra la vista **Parámetros** y ajuste los siguientes parámetros de servicio según sea necesario:

  - Pulse el separador **Comportamiento** y actualice los [parámetros de comportamiento de conducción](#behavior_parameters) de modo que satisfagan sus necesidades.

  - Pulse el separador **Contexto** y actualice los[parámetros de correlación de contexto](#context_parameters) de modo que satisfagan sus necesidades. 
2. Pulse **GUARDAR**.
3. Pulse **Aceptar**.

Los valores de parámetros actualizados se aplican al próximo trabajo que se someta.

### Parámetros de comportamiento de conducción
{: #behavior_parameters}

Las siguientes tablas describen los parámetros de comportamiento de conducción para las categorías que se pueden configurar en el separador **Comportamiento**.

#### Calores de límite de velocidad

Puede especificar el límite de velocidad el km/h para cada tipo de carretera. Si la velocidad excede el valor de límite de velocidad que se especifica para el tipo de carretera, se detecta un exceso de velocidad.


|Nombre de parámetro|Descripción|Valor predeterminado(km/h)|
|:--------|:--------|:-------|
|Autopista|Límite de velocidad para un tipo de carretera de autopista|120|
|Autovía urbana|Límite de velocidad para un tipo de carretera de autovía urbana|90|
|Vía urbana principal|Límite de velocidad para un tipo de carretera de vía urbana principal|60|
|Carretera urbana|Límite de velocidad para un tipo de carretera de carretera urbana|40|
|Otros|Límite de velocidad para un tipo de carretera clasificada como 'Otros'|30|
|Desconocido|Límite de velocidad para tipos de carretera desconocidos|120|

#### Valores de giro

|Nombre de parámetro|Descripción|Valor predeterminado|
|:--------|:--------|:-------|
|Velocidad angular (Mín \- Máx, deg/s)|Valor de velocidad angular normal de un giro. El valor mínimo se utiliza como umbral para identificar el segmento de giro. El valor máximo se utiliza para detectar un comportamiento de giro brusco. |10 \- 25|
|Velocidad media (km/h)|Velocidad normal durante un giro. Este valor se utiliza para identificar comportamientos en un segmento de giro que tenga valores de velocidad angular. |60|

#### Valores de fatiga de conducción

|Nombre de parámetro|Descripción|Valor predeterminado|
|:--------|:--------|:-------|
|Tiempo de conducción continuada (s)|La longitud máxima de conducción continuada permitida.|10800|


### Parámetros de correlación de contexto
{: #context_parameters}

Las siguientes tablas describen los parámetros de correlación de contexto para las categorías que se pueden configurar en el separador **Contexto**.

#### Valores de huso horario e intervalo de tiempo

Especifique el huso horario y las horas para cada periodo de tiempo.

|Nombre de parámetro|Descripción|Valor predeterminado|
|:--------|:--------|:-------|
|Huso horario de análisis|Huso horario aplicado para su análisis. |+00:00|
|Día|Intervalo de horas durante el día.|1030 \- 1730|
|Noche|Intervalo de horas durante la noche.|2030 \- 0700|
|Pico de la mañana|Intervalo de horas durante el pico del día.|0700 \- 1030|
|Pico de la tarde|Intervalo de horas durante el pico de la tarde.|1730 \- 2030|

#### Tipos de carretera

Los parámetros de tipos de carretera se utilizan para correlacionar los valores de tipo de carretera de los datos de entrada con las clasificaciones de tipos de carretera de {{site.data.keyword.iot4auto_short}}. Si no tiene un valor de tipo de carretera, puede recuperar el valor mediante la API REST "getLinkInformation" proporcionada por "{{site.data.keyword.iotmapinsights_short}}".

 El valor de tipo de carretera se almacena en "propiedades > tipo" en la respuesta. Para obtener un ejemplo que muestra la posición de "tipo" en la respuesta, consulte [Respuesta JSON de ejemplo para `getLinkInformation`](#sampleJson).

 |Nombre de parámetro|Descripción|Valor predeterminado|
 |:--------|:--------|:-------|
|Autopista|Valor de tipo de carretera que se correlaciona con autopista.|1|
|Autovía urbana|Valor de tipo de carretera que se correlaciona con autovía urbana.|2|
|Vía urbana principal|Valor de tipo de carretera que se correlaciona con vía urbana principal.|3|
|Carretera urbana|Valor de tipo de carretera que se correlaciona con carretera urbana.|4|
|Otros|Valor de tipo de carretera que se correlaciona con Otro.|5|

#### Límite de velocidad

Los parámetros de límite de velocidad definen el rango de velocidad medio para cada tipo de carretera en km/h. El rango de velocidad media es el rango entre los valores más bajo y más alto que se especifican. 

|Nombre de parámetro|Descripción|Valor predeterminado|
|:--------|:--------|:-------|
|Autopista|Intervalo de velocidad media para tipo de carretera de autopista.|55 \- 85|
|Autovía urbana|Intervalo de velocidad media para tipo de carretera de autovía urbana.|35 \- 65|
|Vía urbana principal|Intervalo de velocidad media para tipo de carretera de vía urbana principal.|20 \- 40|
|Carretera urbana|Intervalo de velocidad media para tipo de carretera de carretera urbana.|15 \- 35|
|Otros|Intervalo de velocidad media para tipo de carretera Otros.|10 \- 20|
|Desconocido|Intervalo de velocidad media para tipo de carretera Desconocido.|20 \- 60|

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

Los datos de sondeo de coche, los datos de contexto y los resultados de análisis se almacenan en el servicio hasta que se suprimen.

Para suprimir datos almacenados en el servicio:

1. Pulse **Gestión de datos** para ver los datos de sondeo de coche y resultados de análisis.
2. Seleccione un registro y, a continuación, en el registro pulse **SUPRIMIR**.
