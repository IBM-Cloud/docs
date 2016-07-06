---

copyright:
  years: 2015, 2016

---
# Supervisión de apps con {{site.data.keyword.mobileanalytics_short}}
{: #monitoringapps}
*Última actualización: 6 de mayo de 2016*
{: .last-updated}

{{site.data.keyword.mobileanalytics_full}} proporciona funciones de supervisión y analíticas para sus aplicaciones móviles. Puede efectuar registros de cliente y supervisar datos con el SDK de cliente de {{site.data.keyword.mobileanalytics_short}}. Los desarrolladores pueden elegir cuándo desean enviar estos datos al servicio de {{site.data.keyword.mobileanalytics_short}}. Al entregar los datos a {{site.data.keyword.mobileanalytics_short}}, puede utilizar el panel de control de {{site.data.keyword.mobileanalytics_short}} para obtener información analítica sobre las aplicaciones móviles, los dispositivos y los registros de cliente.
{: shortdesc}

## Visualización de datos con gráficos personalizados
{: #custom-charts}

Puede visualizar los datos analíticos recopilados en el repositorio de analíticas. Esta visualización constituye una forma eficaz de inspeccionar datos para casos de uso específicos. Puede crear gráficos con datos que ya haya recopilado Operational Analytics, además de los datos personalizados que notifique.

### Creación de gráficos personalizados para registros de cliente
{: #custom-charts-client-logs}

Puede crear un gráfico personalizado para los registros de cliente que contienen información que se envía con la API del registrador para la plataforma. La información de registro también incluye información contextual sobre el dispositivo, el entorno incluido, el nombre y la versión de la app.

En este ejemplo se utilizan los datos de registro del cliente para crear un diagrama de flujo. En el gráfico final se muestra la distribución de los niveles de registro en una app específica. También dispone de los siguientes datos para visualizarlos en un gráfico:

* Datos específicos
  * Nivel de registro
* Datos de mensaje
  * Indicación de fecha y hora
* Datos contextuales del sistema operativo del dispositivo
  * Nombre de la aplicación
  * Versión de la aplicación
  * Sistema operativo del dispositivo
* Datos contextuales del dispositivo
  * ID del dispositivo
  * Modelo del dispositivo
  * Versión de sistema operativo del dispositivo


1. Asegúrese de que tiene una aplicación que recopila registros de dispositivo o analíticas.
2. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el separador **Gráficos personalizados** de la página **Panel de control**. Puede crear un gráfico a partir de los mensajes de analíticas enviados al servidor.
3. Pulse **Crear gráfico** para crear un gráfico personalizado nuevo e indique los siguientes valores:
  * Título del gráfico: aplicación y niveles de registro
  * Tipo de evento: registros de cliente
  * Tipo de gráfico: diagrama de flujo
5. Pulse el separador **Definición de gráfico** e indique los siguientes valores:
  * Origen: nombre de la aplicación
  * Destino: nivel de registro
  * Propiedad: nombre de la app
7. Pulse **Guardar**

### Exportación de datos personalizados
{: #export-custom-data}

Puede exportar los datos de cada gráfico personalizado al formato JSON, XML o CSV.

La estructura de los datos exportados depende del gráfico exportado. Para exportar los datos, pulse el icono de exportación que está en la zona superior derecha del gráfico personalizado.



### Exportación e importación de definiciones de gráficos personalizados
{: #export-import-custom}

Puede importar y exportar las definiciones del gráfico personalizado mediante programación o manualmente en el panel de control de {{site.data.keyword.mobileanalytics_short}}.

Asegúrese de que tiene al menos un gráfico personalizado en el panel de control de {{site.data.keyword.mobileanalytics_short}}.
En este ejemplo se exportan e importan las definiciones del gráfico personalizado de forma manual.

1. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el separador **Gráficos personalizados** de la página **Panel de control**.
2. Para exportar las definiciones del gráfico personalizado, pulse **Exportar gráficos**. Con esta acción se muestra un cuadro de diálogo para guardar un archivo `customChartsDefinition.json`.
3. Elija una ubicación para guardar el archivo.
4. Pulse el icono **Suprimir gráfico**, situado junto a cada gráfico personalizado, para suprimir todos los gráficos personalizados.
5. Para importar una definición del gráfico personalizado, pulse **Importar gráficos**. Con esta acción se muestra un cuadro de diálogo para elegir un archivo.
6. Elija el archivo `customChartsDefinition.json` que ha exportado antes para abrirlo.

También puede exportar e importar definiciones de un gráfico personalizado mediante programación utilizando el cliente HTTP que desee (por ejemplo, CURL o postman):
* El punto final GET de la exportación es `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* El punto final POST de la importación es `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Nota**: Si importa una definición de un gráfico personalizado que existe, acabará duplicando definiciones, lo que implica que en el panel de control de {{site.data.keyword.mobileanalytics_short}} se mostrarán gráficos personalizados duplicados.

## Configuración de alertas
{: #alerts}

Puede establecer umbrales en las definiciones de alerta en la consola de {{site.data.keyword.mobileanalytics_short}} para supervisar mejor las actividades.

Puede configurar umbrales que, si se superan, activan alertas para notificar al monitor de la consola de {{site.data.keyword.mobileanalytics_short}}. Las alertas activadas se pueden visualizar en la consola o bien se pueden gestionar con un webhook personalizado. Gracias a esta función, se pueden detectar de forma proactiva errores en los registros de cliente, errores en los registros de servidor, períodos de latencia de red ampliados y errores de autenticación. Gracias a los umbrales y las alertas reactivos, no hace falta que examine a conciencia los datos y puede establecer umbrales con un espectro de granularidad amplio.

### Creación de una definición de alerta para los registros de cliente
{: #alert-def-client-logs}

Puede crear una definición de alerta basada en registros de cliente.

En este ejemplo se utilizan los datos de registro del cliente para crear una definición de alerta. La alerta supervisa todos los registros de cliente recibidos en los últimos 5 minutos y sigue efectuando comprobaciones cada 5 minutos hasta que se inhabilita o se suprime la definición de alerta. Se activa una alerta para cada dispositivo que ha enviado 3 o más registros de error de cliente con el mismo nombre y la misma versión de la app.

1. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el icono de la campana para ir a la página **Registro de alertas**.
2. Vaya a la página **Gestión de alertas** y pulse **Crear alerta**.
3. Indique los siguientes valores:
	* Nombre de la alerta: alerta para registros de cliente
	* Mensaje: alerta de mensaje de error
	* Frecuencia de consulta: 5 minutos
	* Tipo de evento: registros de cliente
		* Propiedad: nivel de registro
			* Valor: error
			* Umbral
				* Tipo de umbral: total para instancia de aplicación

					**Nota**: Si elige la opción Promedio para aplicación, se calcula el promedio de los registros de cliente por el número de dispositivos. Por ejemplo, si tiene dos dispositivos y uno envía seis registros de cliente, mientras que el otro envía tres, la media será de 4,5 registros de cliente.
				* Operador: es igual o mayor que 3
	<!-- insert alert definition tab image? -->

4. Pulse **Siguiente** o el separador **Método de distribución** e indique el siguiente valor:
	* Método: solo consola de analíticas

		Nota: Elija la opción Consola de analíticas y POST de red si también desea enviar un mensaje POST con una carga útil JSON a su dirección URL personalizada. Si elige esta opción, estarán disponibles los siguientes campos:
		* URL POST de red
        * Cabeceras
        * Tipo de autenticación
5. Pulse **Guardar**.

Ha creado una definición de alerta para activar una alerta al término de cada intervalo de 5 minutos si los registros de cliente alcanzan el umbral de 3 o más registros de error.

### Creación de una definición de alerta para bloqueos de apps
{: #alert-def-app-crash}

Puede crear una definición de alerta basada en bloqueos de app.

En este ejemplo se utilizan los datos de bloqueo de app para crear una definición de alerta. La alerta supervisa todos los bloqueos de app de los últimos 2 minutos y sigue efectuando comprobaciones cada 2 minutos hasta que se inhabilita o se suprime la definición de alerta. Se activa una alerta para cada app bloqueada 5 o más veces. Para obtener más información sobre los bloqueos de apps, consulte [Bloqueos de app](app_crash/c_op_analytics_crashes.html).

1. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el icono **Alertas**. Esta acción le dirige a la página Registro de alertas.
2. Pulse el separador **Gestión de alertas** y pulse **Crear alerta**.
3. Indique los siguientes valores:
	* Nombre de la alerta: alerta para bloqueos de app
	* Mensaje: alerta de bloqueo de app
	* Frecuencia de consulta: bloqueos de aplicación
		* Nombre de la aplicación: cualquier aplicación
		* Versión de la aplicación: cualquier versión
    * Umbral
      * Tipo de umbral: recuento de bloqueos
      * Operador: es igual o mayor que 5
4. Pulse el separador **Método de distribución** e indique el siguiente valor:
  * Método: solo consola de analíticas

    **Nota**: Elija la opción **Consola de analíticas y POST de red** si también desea enviar un mensaje POST con una carga útil JSON a su dirección URL personalizada. Si elige esta opción, estarán disponibles los siguientes campos:
      * URL POST de red (obligatorio)
      * Cabeceras (opcional)
      * Tipo de autenticación (obligatorio)
5. Pulse **Guardar**.

### Gestión de definiciones de alerta
{: #managing-alert-definitions}

En este ejemplo se gestionan las definiciones de alerta desde la página Gestión de alertas.

1. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el icono **Alertas**. Esta acción abre la página Registro de alertas.
2. Pulse el separador **Gestión de alertas**.
3. Opcional: Marque o desmarque el recuadro de selección de la columna **Habilitado** para habilitar o inhabilitar una definición de alerta en concreto.
4. Opcional: Pulse el icono **Duplicar** si desea crear una copia de una definición de alerta y cambiar algunos valores.
5. Opcional: Pulse el icono **Lápiz** si desea editar una definición de alerta.
6. Opcional: Pulse el icono **Papelera** si desea suprimir una definición de alerta.

### Visualización de los detalles de alertas
{: #viewing-alert-details}

En este ejemplo se muestran los detalles de las alertas activadas desde la página Registro de alertas.

1. En la consola de {{site.data.keyword.mobileanalytics_short}}, pulse el icono **Alertas**. Esta acción le dirige a la página Registro de alertas.
2. Pulse el icono **+** de cualquiera de las alertas. Con esta acción se muestran las secciones **Definición de alerta** e **Instancias de alerta**.

    **Nota**: Si la definición de alerta correspondiente no se ha suprimido o modificado, puede editarla pulsando **Editar alerta**. De lo contrario, no podrá pulsar el botón **Editar alerta** y se mostrará el siguiente mensaje:

    `Esta definición de alerta se ha modificado o suprimido.`

3. Opcional: Seleccione una alerta y pulse el icono **Papelera** para suprimir la alerta.

## Bloqueos de apps
{: #monitor-app-crash}

Puede consultar la información de los bloqueos de app en la consola de {{site.data.keyword.mobileanalytics_short}} a fin de supervisar las apps y resolver los posibles problemas de forma más eficaz.

### Supervisión de bloqueos de apps
{: #app-crash}

Puede consultar rápidamente la información relacionada con los bloqueos de apps en la sección **Panel de control** de la consola de {{site.data.keyword.mobileanalytics_short}}.

En la página **Visión general** de la sección **Panel de control**, en el gráfico de barras **Bloqueos** se muestra un histograma de los bloqueos producidos con el tiempo.

Puede visualizar los datos de dos formas:

1. Visualizar frecuencia de bloqueos: frecuencia de bloqueos con el tiempo
2. Visualizar bloqueos totales: bloqueos totales con el tiempo


### Resolución de problemas de bloqueos de apps
{: #app-crash-troubleshooting}

Puede ver la página **Bloqueos** en la sección **Aplicaciones** de la consola de {{site.data.keyword.mobileanalytics_short}} para administrar sus apps de forma más eficaz.

En la tabla **Visión general de bloqueos** se muestran las siguientes columnas de datos:

* App: nombre de la app
* Bloqueos: número total de bloqueos de dicha app
* Usos totales: número total de veces que un usuario abre y cierra dicha app
* Frecuencia de bloqueo: porcentaje de bloqueos por uso

La tabla **Resumen de bloqueos** se puede ordenar e incluye las siguientes columnas de datos:

* Bloqueos
* Dispositivos
* Último bloqueo
* App
* Sistema operativo
* Mensaje

Puede pulsar el icono +, situado junto a cualquier entrada, para ver la tabla **Detalles de bloqueo**, que incluye las siguientes columnas:

* Tiempo de bloqueo
* Versión de aplicación
* Versión de sistema operativo
* Modelo del dispositivo
* ID del dispositivo
* Descargar: enlace para descargar los registros que han provocado el bloqueo

Puede expandir cualquier entrada de la tabla **Detalles de bloqueo** para obtener información más detallada (por ejemplo, un seguimiento de pila).

**Nota**: Los datos de la tabla **Resumen de bloqueos** se rellenan consultando los registros de cliente de nivel muy grave. Si su app no recopila dichos registros, no habrá datos disponibles.


