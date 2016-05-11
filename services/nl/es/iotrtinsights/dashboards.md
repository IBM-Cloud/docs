---

copyright:
  años: 2015,2016

---

{:shortdesc: .shortdesc}

# Gestión de plantillas y paneles de control {: #managing-dashboards}

Los datos en tiempo real de los dispositivos IoT se muestran en los paneles de instrumentos personalizables. Puede crear manualmente los paneles de instrumentos que muestran métricas en tiempo real, que muestran gráficos y otra información para uno o varios dispositivos. Los paneles de instrumentos también pueden contener listas filtradas de dispositivos y enlaces a otros paneles de instrumentos.
{: shortdesc}

Además de crear manualmente los paneles de instrumentos, {{site.data.keyword.iotrtinsights_short}} viene con un panel de instrumentos de alertas de dispositivos predefinido en **Paneles de control > Visión general** y crea de forma dinámica paneles de instrumentos de dispositivos basados en los esquemas de mensajes que haya creado.

## Paneles de control {: #dashboards}

Los administradores pueden crear nuevos paneles de instrumentos y modificar los existentes para visualizar los datos de dispositivo de interés.  
Para crear un panel de control:
1.	Vaya a **Paneles de control > Examinar paneles de control**.
2.	Pulse **Añadir nuevo panel de control**.
3.	Ponga un nombre al panel de control y seleccione atributos, como por ejemplo icono y fondo. Seleccione también si desea convertir en editable este panel de control para usuarios de operador de {{site.data.keyword.iotrtinsights_short}}.
4.	Pulse ![Crear icono.](images/create.png "Crear icono").
5.	Pulse el nuevo mosaico del panel de control para abrir el panel de control vacío.
6.	Para añadir widgets al panel de control:  
 1.	Pulse **Añadir componente nuevo** para añadir un widget de panel de control inicial.
 2.	Seleccione un componente para añadir y, a continuación, seleccione más atributos de componentes y, si es necesario, seleccione propiedades de visualización.
 Por ejemplo, para visualizar el valor numérico de un determinado punto de datos para un dispositivo, seleccione `Dispositivo` y, a continuación, seleccione el dispositivo para añadir. En el editor del panel de control, bajo Visualización, seleccione un punto de datos para visualizar. A continuación, coloque el widget recién añadido en la cuadrícula del panel de control.
 3.	Pulse ![Crear icono.](images/create.png "Crear icono") para añadir el widget al panel de control.
7.	El panel de control se actualiza con los widgets recién añadidos, y muestra los datos en tiempo real definidos por el punto de datos seleccionado.

>**Consejo:** Para crear un panel de control que lista todos los dispositivos, haga lo siguiente:  
1. Vaya a **Paneles de control > Examinar paneles de control** y pulse **Añadir nuevo panel de control**.
2. Otorgue al panel de control un nombre descriptivo, como por ejemplo `Todos los dispositivos`, y pulse ![Crear icono.](images/create.png "Crear icono").
3. En el panel del panel de control, pulse el panel de control y, a continuación, pulse **Añadir componente nuevo**.
4. Seleccione el componente **Contenedor** y seleccione **Dispositivos filtrados** para crear una lista de todos los dispositivos.
5. Pulse ![Crear icono.](images/create.png "Crear icono").  

>Los dispositivos se listan en el nuevo panel de control. Pulse un icono de dispositivo para abrir el panel de control del dispositivo y para ver los datos en tiempo real para el dispositivo.
### Widgets de panel de control {: #dashboard-widgets}
Los paneles de control están compuestos de widgets que muestran datos en tiempo real de uno o varios dispositivos. El comportamiento del widget depende de su tipo, del punto de datos que se visualiza, y del modo en que el punto de datos está configurado en el esquema.  
Por ejemplo, si añade un widget de dispositivo para un punto de datos 'en bruto', el widget mostrará los datos en bruto como una única serie.

Si, sin embargo, configura el punto de datos con un valor mínimo y máximo, tiene la opción de visualizar un widget en forma de medidor.

También puede asignar un Tipo de sensor para el punto de datos para habilitar un tipo especial de widget de visualización para ilustrar mejor el tipo de datos de sensor que se visualizan. Por ejemplo, puede seleccionar el tipo de sensor `Luz encendida/apagada` para habilitar un widget de visualización `Indicador de luz simple (encendido/apagado)`.

También tiene la opción de incluir varios widgets para el mismo punto de datos en el mismo panel de control para mostrar el valor numérico en bruto y la humedad una al lado de la otra. ![Varios widgets para el mismo punto de datos.](images/widgets.svg "Varios widgets para el mismo icono de punto de datos")  
*Tres opciones de visualización para el mismo punto de datos.*


Widget | Tipo y visualización
------------- | -------------
Dispositivo | Datos - Valor el tiempo real de puntos de datos para el dispositivo. Si el punto de datos está configurado para incluir un valor mínimo y máximo, las opciones de visualización incluyen la muestra del punto de datos en forma de medidor. Además, si el punto de datos está configurado con un tipo de sensor, habrá disponibles opciones de visualización adicionales.
Gráfico | Gráfico - Represente los valores en tiempo real de puntos de datos para uno o varios dispositivos.
Panel de control | Enlace a un panel de control o una plantilla.
Texto | Recuadro de texto - Texto formateado.
Contenedor | Tipos de widgets de contenedor:<ul><li>Todos los paneles de control – Una lista enlazada de todos los paneles de control.</li><li>Dispositivos filtrados – Una lista de todos los dispositivos, o filtrados por nombre o ubicación.</li><li>Dispositivos filtrados con alertas – Una lista de todos los dispositivos con alertas, o filtrados por nombre o ubicación.</li><li>Alertas para dispositivo – Una lista de alertas para un dispositivo seleccionado en dispositivos filtrados con contenedor de alertas.</li></ul>
Especial | Tipos de widgets especiales:<ul><li>Correlacionar – Una correlación que localiza el dispositivo seleccionado.</li><li>Información de dispositivo adicional – Más información sobre el dispositivo seleccionado.</li></ul>

En la tabla siguiente se resumen las opciones de visualización que están disponibles para los widgets de dispositivos si el punto de datos seleccionado está configurado con un atributo de tipo de sensor en el esquema de mensajes.

Tipo de sensor de punto de datos | Opciones de visualización | Detalles | Tipo de datos soportado
------------- | ------------- | -------------
Sin selección | Valor simple | - | Cadena/Entero/Flotar
Luz encendida/apagada | Indicador de luz simple (encendida/apagada) | 0=apagada | Entero
Conmutar encendido/apagado | Indicador de conmutación simple (encendido/apagado) | 0=apagado | Entero
Sensor de temperatura | Medidor de temperatura genérico | N/D | Entero/Flotante
Control de temperatura | Medidor de temperatura genérico | N/D | Entero/Flotante
Sensor de presión | Medidor de presión simple | N/D | Entero/Flotante
Niveles de batería | Widget de batería simple (baja/alta) | 0=correcto | Entero
Claridad | Indicador de claridad (oscuro/claro) | 0=oscuro | Entero
Ventana abierta/cerrada | Estado de la ventana simple (abierta/cerrada) | 0=cerrada | Entero
Puerta abierta/cerrada | Estado de la puerta simple (abierta/cerrada) | 0=cerrada | Entero
Sensor de humedad | Estado de humedad (seco/mojado) | 0=seco | Entero
Consumo de energía | Medidor de alimentación simple | N/D | Entero/Flotante
Medidor de energía | Valor simple | N/D | Entero/Flotante
Porcentaje | Porcentaje simple (0-100) | N/D | Entero/Flotante
Voltaje | Medidor de voltaje simple | N/D | Entero/Flotante
Actual | Medidor actual simple | N/D | Entero/Flotante
Longitud | Ubicación del dispositivo en Especial > Widget de correlación (widget de latitud también necesario) | **Importante:** El punto de datos utilizado para el valor longitud debe tener asignada la Longitud del tipo de sensor en el esquema de mensajes. | Flotante
Latitud | Ubicación del dispositivo en Especial > Widget de correlación (widget de longitud también necesario) | **Importante:** El punto de datos utilizado para el valor latitud debe tener asignada la Latitud del tipo de sensor en el esquema de mensajes. | Flotante  


## Diseños de paneles de control predeterminados
{{site.data.keyword.iotrtinsights_short}} se suministra con paneles de control predefinidos: un panel de control de alertas y paneles de control de dispositivos.

Las tablas siguientes describen los widgets y el diseño de los paneles de control predefinidos.
### Panel de control de alertas (Paneles de control > Visión general)
Este panel de control se incluye con el producto y proporciona una lista de dispositivos que tienen alertas abiertas. Puede seleccionar un dispositivo para ver detalles sobre las alertas, y puede hacer clic en el icono del dispositivo para abrir un panel de control de dispositivos para mostrar los datos en tiempo real para el dispositivo.

<table>
<thead>
<tr>
<th colspan="3">Panel de control de alertas</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contenedor: Dispositivos con alertas</td>
<td style="width:30%">Contenedor: Alertas para el dispositivo</td>
<td style="width:30%">Especial: Información de dispositivo adicional</td>
</tr>
<tr>
<td style="width:30%"></td>
<td style="width:30%"></td>
<td style="width:30%">Especial: Correlacionar</td>
</tr>
</tbody>
</table>

*Diseño de Panel de control de alertas*

### Paneles de control del dispositivo
Al pulsar en un icono de dispositivo en una lista de dispositivos se abrirá un panel de control de dispositivos para el dispositivo. Cuando se añade un punto de datos al esquema de mensajes, también se añadirá como un widget en la plantilla de dispositivos, que crea de forma dinámica el panel de control del dispositivo. Los administradores pueden añadir o eliminar widgets de forma manual.

<table>
<thead>
<tr>
<th colspan="3">Panel de control del dispositivo</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Dispositivo: Punto de datos 1</td>
<td style="width:30%">Dispositivo: Punto de datos 2</td>
<td style="width:30%">Dispositivo: Punto de datos 3</td>
</tr>
<tr>
<td style="width:30%">Dispositivo: Punto de datos N</td>
<td style="width:30%"></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Diseño del panel de control de dispositivos predefinidos*

### Ejemplo del panel de control: Lista de todos los dispositivos
El siguiente panel de control incluye una lista de todos los dispositivos y proporciona información de dispositivos al seleccionar un dispositivo de la lista.

<table>
<thead>
<tr>
<th colspan="3">Panel de control Lista de todos los dispositivos</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Contenedor: Dispositivos filtrados (conjunto de parámetros sin filtro)</td>
<td style="width:30%">Especial: Información de dispositivo adicional</td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Diseño del panel de control Lista de todos los dispositivos*

## Plantillas {: #templates}
Las plantillas controlan el diseño de los paneles de control predefinidos para un tipo de dispositivo específico. Los administradores pueden modificar estas plantillas predefinidas para que se ajusten a sus necesidades. Por ejemplo, una plantilla predefinida solo incluye los puntos de datos genéricos. Puede añadir gráficos y otros componentes según sea necesario.

Por ejemplo, un usuario puede acceder al panel de control de dispositivos predefinido para ver datos de dispositivo básicos y, a continuación, seguir un enlace a una plantilla creada manualmente que podría contener un conjunto completo de gráficos en tiempo real. Cree una plantilla de un modo muy similar a como crea un panel de control.  

Para modificar una plantilla predefinida:
1.	Vaya a **Paneles de control > Gestionar plantillas**.
2.	En el panel Gestionar plantillas, busque el mosaico de plantilla y pulse ![Configurar icono.](images/gear.png "Configurar icono")** > Cambiar diseño** para abrir la plantilla para su edición.  
3.	Añada widgets a la plantilla.
 1.	Pulse **Añadir nuevo componente de plantilla** para añadir un widget de plantilla inicial.
 2.	Seleccione un componente para añadir y, a continuación, seleccione más atributos de componentes y, si es necesario, seleccione propiedades de visualización.  
 3.	Pulse ![Crear icono.](images/create.png "Crear icono") para añadir el widget a la plantilla.
4.	Editar widgets existentes.
 1.	Pase el ratón por encima de un widget de plantilla y pulse ![Configurar icono.](images/gear.png "Configurar icono").
 2.	Modifique el componente y sus atributos, y vuelva a situar el widget según sea necesario.
 3.	Pulse ![Crear icono.](images/create.png "Crear icono") para actualizar el widget.  

La plantilla se actualizará con sus cambios.

<!-- Administrators can also manually add templates for specific device types. These templates can then be linked to from the predefined templates.  -->

<!-- To create a template:
1.	Go to **Dashboards > Manage templates**.
2.	Click **Add new template**.
3.	Give the template a name, select a device type and attributes such as icon and background.
4.	Click ![Create icon.](images/create.png "Create icon").
5.	The empty template opens.
6.	Add widgets to the template.  
For a list of widgets, see below.
 1.	Click **Add new component** to add an initial template widget.
 2.	Select a component to add, then select further component attributes and, if needed, select display properties.
 For example, ... Then position the newly added widget in the dashboard grid.
 3.	Click ![Create icon.](images/create.png "Create icon") to add the widget to the template.
7.	The template updates with the newly added widgets.

### Template widgets
Widget | Type and visualization
------------- | -------------
Device | Data - Real-time value of data points for the device. For a description of the available widget options, see [Dashboard widgets](#dashboard-widgets "Dashboard widgets") above.
Chart | Graph - Plot real-time values of data points for one or more devices.
Dashboard | Link to a dashboard or a template.
Text | Text box - Formatted text
Container | Types of containers:<ul><li>All dashboards – A linked list of all dashboards</li><li>Filtered devices – A list of all devices, or filtered by name or location</li><li>Filtered devices with alerts – A list of all devices with alerts, or filtered by name or location</li><li>Alerts for device – A list of alerts for a device that is selected in a Filtered devices with alerts container</li></ul>
Special | Types of special:<ul><li>Map – A map that locates the selected device</li><li>Additional device information – More information about the selected device</li></ul>

### Template example: Selected set of graphs
One way of using device templates is to expand on the predefined device template by creating specialized templates for a device type, and then linking these from the predefined template by using a Dashboard widget.

<table>
<thead>
<tr>
<th colspan="3">Descriptive graphs template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: ID</td>
<td style="width:30%">Graph: One data point</td>
<td style="width:30%">Graph: Another data point</td>
</tr>
<tr>
<td style="width:30%">Special: Additional device information</td>
<td style="width:30%">Text: Short description of how to <br>interpret the device data in the graphs.</td>
<td></td>
</tr>
</tbody>
</table>

*Descriptive graphs template*

Link to this template from a predefined device template:

<table>
<thead>
<tr>
<th colspan="3">Predefined device dashboard layout with link to template</th>
</tr>
</thead>
<tbody>
<tr>
<td style="width:30%">Device: Datapoint 1</td>
<td style="width:30%">Device: Datapoint 2</td>
<td style="width:30%">Device: Datapoint 3</td>
</tr>
<tr>
<td style="width:30%">Device: Datapoint N</td>
<td style="width:30%"><b>Dashboard: Descriptive graphs template</b></td>
<td style="width:30%"></td>
</tr>
</tbody>
</table>

*Predefined device dashboard layout with link to template* -->


## Restablecimiento de plantillas y paneles de control predefinidos {: #resetting-dashboards}
Si modifica una plantilla predefinida, la plantilla ya no se actualizará de forma dinámica desde las actualizaciones del esquema de mensajes, y debe restablecer el panel de control o la plantilla para restaurar el diseño original y los widgets.
Para restablecer los paneles de control predefinidos y las plantillas:
1.	Vaya a **Paneles de control > Gestionar plantillas** o a **Paneles de control > Examinar paneles de control**.
2.	Busque la plantilla predefinida o el mosaico del panel de control y pulse **![Configurar icono.](images/gear.png "Configurar icono") > Restablecer diseño** para suprimir y volver a crear la plantilla.  

La plantilla o el panel de control se volverá a crear con el conjunto de widgets predeterminados.
