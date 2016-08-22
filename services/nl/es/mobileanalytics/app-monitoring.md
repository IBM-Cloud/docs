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

<!--

## Visualizing data with custom charts
{: #custom-charts}

You can visualize the collected analytics data in your analytics repository. This visualization is a powerful way to inspect data for specific use cases. You can create charts with data that is already collected by Operational Analytics, in addition to custom data that you report.


### Creating custom charts for client logs
{: #custom-charts-client-logs}

You can create a custom chart for client logs that contain log information that is sent with the Logger API for the platform. The log information also includes contextual information about the device, including environment, app name, and app version.

In this example, you use client log data to create a flow chart. The final graph shows the distribution of log levels in a specific app. You also have the following data available to show in a chart:

* Specific data
  * Log level
* Message data
  * Timestamp
* Device OS contextual data
  * Application name
  * Application version
  * Device OS
* Device contextual data
  * Device ID
  * Device model
  * Device OS version


1. Make sure that you have an application that is collecting device logs or gathering analytics.
2. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab on the **Dashboard** page. You can create a chart that is based on the analytics messages that were sent to the server.
3. Click **Create Chart** to create a new custom chart and provide the following values:
  * Chart Title: Application and Log Levels
  * Event Type: Client Logs
  * Chart Type: Flow Chart
5. Click the **Chart Definition** tab and provide the following values:
  * Source: Application Name
  * Destination: Log Level
  * Property: your app name
7. Click **Save**

### Exporting custom data
{: #export-custom-data}

You can export the data from each custom chart into JSON, XML, or CSV format.

The structure of the exported data depends on the chart that is being exported. To export data, click the export icon at the upper right of the custom chart.



### Exporting and importing custom chart definitions
{: #export-import-custom}

You can import and export custom chart definitions programmatically or manually in the {{site.data.keyword.mobileanalytics_short}} Dashboard.

Ensure that you have at least one custom chart in the {{site.data.keyword.mobileanalytics_short}} Dashboard.
In this example, you manually export and import custom chart definitions.

1. In the {{site.data.keyword.mobileanalytics_short}} console, click the **Custom Charts** tab in the **Dashboard** page.
2. To export the custom chart definitions, click **Export Charts**. This action displays a dialog to save a `customChartsDefinition.json` file.
3. Choose a location to save the file.
4. Click the **Delete Chart** icon next to each custom chart to delete all custom charts.
5. To import a custom chart definition, click **Import Charts**. This action displays a dialog to choose a file.
6. Choose the `customChartsDefinition.json` file that you previously exported to open.

You can also export and import custom chart definitions programmatically by using your HTTP client of choice (for example, CURL or postman):
* The GET endpoint for export is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/`.
* The POST endpoint for import is `http://mobile-analytics-dashboard.ng.bluemix.net/analytics-service/rest/data/customCharts/import`.

**Note**: If you import a custom chart definition that exists, you end up with duplicate definitions, which also means that the {{site.data.keyword.mobileanalytics_short}} Dashboard shows duplicate custom charts.

-->

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


