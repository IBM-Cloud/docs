---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-14"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Creación de un panel de control de Grafana
{:#monitoring_grafana}

Cree un panel de control personalizado de Grafana para mostrar métricas correspondientes a todos los contenedores que se ejecutan en un espacio de su organización {{site.data.keyword.Bluemix}}.
{:shortdesc}

Siga los siguientes pasos para crear un panel de control de Grafana: 

1. Inicie Grafana desde un navegador web. Para obtener más información,
consulte [Cómo ir al panel de control de Grafana desde un navegador web](monitoring_analyzing_metrics_grafana.html#launch_grafana_from_browser).

2. Guarde el panel de control predeterminado. 

    1. En la barra de herramientas, pulse el icono Guardar. 
    2. Escriba un nombre para el panel de control.
    3. Junto al campo de nombre, pulse el icono Guardar.
   
3. Inhabilite la renovación de página automática cuando trabaje en el panel de control. 

    1. Pulse el selector de tiempo en la cabecera.
    2. Seleccione **Renovación automática**.
    3. Pulse **Desactivar**.
 
 5. Suprima las filas de ejemplo.
 
     1. Junto a la cabecera *Bienvenido a Grafana*, mueva el cursor por la barra graduadora del menú Fila y pulse el icono del menú Fila que gradúa. 
     2. Pulse **Suprimir fila** y luego pulse **Sí**.
     
     Repita estos pasos para eliminar las filas Enlaces de documentación y Primer gráfico.  
     
     En la cabecera de la página, ajuste el selector de tiempo para asegurarse de que se ven los datos. El valor predeterminado es entre 6 horas y hace pocos segundos. Seleccione **Últimos 30d**.
     
6. Añada una visualización. 

    * Para añadir una visualización de CPU desocupada, consulte [Adición de una visualización de CPU desocupada](monitoring_grafana.html#grafana_add_cpu).
    * Para añadir una visualización de memoria utilizada, consulte [Adición de una visualización de memoria utilizada](monitoring_grafana.html#grafana_add_mem).
        
7. Guarde el panel de control personalizado.

    1. En la barra de herramientas, pulse el icono Guardar. 
    2. Escriba un nombre para el panel de control.
    3. Junto al campo de nombre, pulse el icono Guardar.
    

## Adición de una visualización de CPU desocupada
{:#grafana_add_cpu}

Para añadir un gráfico de CPU desocupada que incluya datos de todos los contenedores del espacio, siga los pasos siguientes:

1. Pulse el botón **Añadir una fila**. Se visualiza el graduador del menú Fila en el lateral de la fila.

    
2. Mueva el cursor sobre el graduador del menú de fila y pulse el icono del menú Fila que gradúa. 

3. Pulse **Añadir panel**. Luego pulse **gráfico**. 

4. Pulse el título del gráfico para abrir el menú del panel y pulse **Editar**. 

    El resto del panel de control está oculto; sólo se visualiza el editor de este gráfico y una vista previa del gráfico. 
    
5. En el separador Métricas, construya una consulta para recopilar datos para el gráfico. 

    Por ejemplo, cuando trabaje con contenedores, el formato de consulta incluye el ID de espacio y un ID de contenedor, un único ID de instancia de contenedor en el siguiente formato: `space_ID.group_ID.instance_ID.metric`
        
    1. En la fila A, pulse **Seleccionar métrica**. Luego seleccione su ID de espacio. 
    2. Pulse **Seleccionar métrica** y seleccione el asterisco (\*).
    
    Cuando selecciona (\*), los datos incluyen métricas procedentes de cada grupo de contenedores del espacio. De forma opcional, puede manipular este formato con una expresión regular para incluir métricas procedentes únicamente de determinados contenedores.
Por ejemplo, si desea ver las métricas solamente de contenedores únicos y excluir grupos de contenedores, pulse **Seleccionar métrica** y seleccione **0000**.
        
    3. Pulse **Seleccionar métrica** y vuelva a seleccionar el asterisco (\*). Este formato incluye métricas de cada contenedor único del espacio. 
        
    4. Pulse **Seleccionar métrica** y **cpu-0**.
        
    5. Pulse **Seleccionar métrica** y **cpu-idle**. La vista previa de gráfico se actualiza para mostrar las métricas que coinciden con esta consulta.
    
6. Opcional: Personalice la visualización del gráfico.
    
    * Para asignar un nombre el gráfico, pulse el separador General, y, en el campo Título, escriba un nombre para el gráfico, por ejemplo: CPU desocupada
    * Para asignar una etiqueta al eje vertical, pulse el separador Ejes y cuadrícula y en la sección Eje Y izquierdo y en el campo Etiqueta, escriba CPU.
    * Para cambiar el color de fondo del gráfico, en la sección Umbrales de cuadrícula, para el nivel 2 pulse el icono selector de color de fondo y cambie el color de fondo por blanco o gris claro.
    
    En la cabecera, pulse **Volver al panel de control**.
    
7. Para guardar los cambios que ha realizado en este panel de control, en la cabecera pulse el icono Guardar y, a continuación, pulse el icono Guardar en el menú.


## Adición de una visualización de memoria utilizada
{:#grafana_add_mem}

Siga los siguientes pasos para añadir una visualización de la memoria utilizada: 

1. Pulse el botón Añadir una fila. Se visualiza el graduador del menú de filas junto
a la fila.
   
2. Mueva el cursor sobre el graduador del menú de fila y pulse el icono del menú Fila que gradúa. 

    1. Pulse Añadir panel > gráfico. 
    2. Pulse Editar. El resto del panel de control está oculto; sólo se visualiza el editor de este gráfico y una vista previa del gráfico. 
    
3. En el separador Métricas, construya una consulta para recopilar datos para el gráfico. 

    Por ejemplo, cuando trabaje con contenedores, el formato de consulta incluye el ID de espacio y un ID de contenedor, un único ID de instancia de contenedor en el siguiente formato: space_ID.group_ID.instance_ID.metric 
        
    1. En la fila A, pulse **Seleccionar métrica**. Luego seleccione su ID de espacio. 
    2. Pulse **Seleccionar métrica** y seleccione el asterisco (\*).
    
    Cuando selecciona (\*), los datos incluyen métricas procedentes de cada grupo de contenedores del espacio. De forma opcional, puede manipular este formato con una expresión regular para incluir métricas procedentes únicamente de determinados contenedores.
Por ejemplo, si desea ver las métricas solamente de contenedores únicos y excluir grupos de contenedores, pulse **Seleccionar métrica** y seleccione **0000**.
    
    3. Pulse **Seleccionar métrica** y vuelva a seleccionar el asterisco (\*). Este formato incluye métricas de cada contenedor único del espacio. 
        
    4. Pulse **Seleccionar métrica** y **memoria**.
        
    5. Pulse **Seleccionar métrica** y **memoria utilizada**. La vista previa de gráfico se actualiza para mostrar las métricas que coinciden con esta consulta.
    
6. Opcional: Personalice la visualización del gráfico.
    
    * Para asignar un nombre el gráfico, pulse el separador General, y, en el campo Título, escriba un nombre para el gráfico, por ejemplo: Memoria utilizada 
    *  Para cambiar el formato de los valores del eje vertical, pulse el separador Ejes y cuadrícula y en la sección Eje Y izquierdo, para el
Formato, seleccione bytes.
    * Para asignar una etiqueta al eje vertical, en el campo Etiqueta, escriba
Memoria.
    * Para cambiar el color de fondo del gráfico, en la sección Umbrales de cuadrícula, para el nivel 2 pulse el icono selector de color de fondo y cambie el color de fondo por blanco o gris claro.
    
    En la cabecera, pulse **Volver al panel de control**.

7. Para guardar los cambios que ha realizado en este panel de control, en la cabecera pulse el icono Guardar y, a continuación, pulse el icono Guardar en el menú.

