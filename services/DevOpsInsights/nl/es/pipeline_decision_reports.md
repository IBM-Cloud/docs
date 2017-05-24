---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Visualización de paneles de control e informes
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} proporciona una gran cantidad de información accionable sobre sus proyectos.
{:shortdesc}

## Paneles de control de {{site.data.keyword.DRA_short}}    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} proporciona paneles de control que muestran información sobre el rendimiento de toda su organización de Bluemix. Para verlos, tras abrir {{site.data.keyword.DRA_short}}, pulse **Verificación de compilación** o **Verificación de despliegue**.

Los paneles de control se rellenan automáticamente con la información más reciente de los trabajos de prueba de {{site.data.keyword.DRA_short}} de sus conductos. Pulse los elementos dentro de los paneles de control para obtener más información sobre ellos.

### Indicadores clave de rendimiento en compilaciones    
{: #DI_key_performance_indicators}

La página **Verificación de compilación** contiene tres gráficos con información sobre el estado de salud de la rama de desarrollo seleccionada:

<table>
<thead>
<tr>
<th>Gráfico</th>
<th>Descripción</th>
</tr>
</thead>

<tbody>
<tr>
<td>Últimas compilaciones</td>
<td>El número de compilaciones recientes que se han completado comparado con el número total de compilaciones recientes.</td>
</tr>
<tr>
<td>Pruebas</td>
<td>El número de pruebas que han pasado correctamente comparado con el número total de pruebas.</td>
</tr>
<tr>
<td>Cobertura de código</td>
<td>Los porcentajes de las sentencias y funciones de su código a las que llaman las pruebas.</td>
</tr>
</tbody></table>

## Visualización de informes de decisión    
{: #DI_decision_reports}

Tras ejecutarse un conducto, {{site.data.keyword.DRA_short}} empieza a recopilar y analizar los resultados de las pruebas para establecer una línea base. Los datos de cada ejecución posterior se recopila y se compara con los resultados anteriores. Las puertas de decisión utilizan estos datos para determinar cuándo se debe detener un despliegue. 

Para ver el informe de decisión de una puerta del conducto, siga estos pasos:

   1. En la etapa que contiene la puerta que se debe comprobar, pulse **Ver registros e historial**.

   2. En la ventana de trabajos de la etapa, pulse el nombre de la puerta.

   3. En la vista de registro, localice el mensaje 'Check {{site.data.keyword.DRA_short}} report here' y pulse el enlace proporcionado para abrir el informe.
