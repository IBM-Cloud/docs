---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-13"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Filtrado de los registros correspondientes a un valor de campo específico
{:#k4_filter_logs_spec_field}

Puede buscar entradas que incluyan un determinado valor de campo.
{:shortdesc}

Siga estos pasos para buscar entradas que incluyan un determinado valor de campo:


1. Examine la página Descubrir de Kibana para ver el subconjunto de datos que muestra. Para obtener más información, consulte [Identificación de los datos que se muestran en la página Descubrir de Kibana](logging_kibana_analize_logs_interactively.html#k4_identify_data). 

2. En la *Lista de campos*, identifique el campo para la que desee definir un filtro y pulse sobre el mismo.

    En el campo se muestra un máximo de 5 valores. Cada valor tiene dos botones de lupa.  
    
    Si no puede ver el valor, consulte [Adición de un filtro para un valor que no aparece en la lista de campos](k4_add_filter_out_value.html#k4_add_filter_out_value).

3. Para añadir un filtro que busque entradas con un valor de campo, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_include_field_icon.jpg "Botón de lupa en modalidad de inclusión") para dicho valor.

    ![Filtro que incluye el valor de campo](images/k4_add_filter_for_field.jpg "Filtro que incluye el valor de campo")

    Para añadir un filtro que busque entradas que no incluyan este valor de campo, seleccione el botón de lupa ![Botón de lupa en modalidad de inclusión](images/k4_exclude_field_icon.jpg "Botón de lupa en modalidad de inclusión") para el valor.

    ![Filtro que excluye el valor de campo](images/k4_add_filter_to_exclude_field.jpg "Filtro que excluye el valor de campo")

4. Elija una de las siguientes opciones para trabajar con filtros en Kibana:

    <table>
      <tbody>
        <tr>
          <th align="center">Opción</th>
          <th align="center">Descripción</th>
          <th align="center">Otra info</th>
        </tr>
        <tr>
          <td align="left">Habilitar</td>
          <td align="left">Seleccione esta opción para habilitar un filtro.</td>
          <td align="left">Cuando añade un filtro, se habilita automáticamente. <br> Si un filtro está inhabilitado, pulse sobre el mismo para habilitarlo.</td>
        </tr>
        <tr>
          <td align="left">Inhabilitar</td>
          <td align="left">Seleccione esta opción para inhabilitar un filtro.</td>
          <td align="left">Después de añadir un filtro, si desea ocultar las entradas correspondientes a un valor de campo, pulse **inhabilitar**.</td>
        </tr>
        <tr>
          <td align="left">Fijar</td>
          <td align="left">Seleccione esta opción para que el filtro se aplique en todas las páginas de Kibana. </td>
          <td align="left">Puede fijar un filtro en la página *Descubrir*, en la página *Visualizar* o en la página *Panel de control*. </td>
        </tr>
        <tr>
          <td align="left">Conmutar</td>
          <td align="left">Seleccione esta opción para conmutar un filtro.</td>
          <td align="left">De forma predeterminada, se muestran las entradas que coinciden con un filtro. Para visualizar las entradas que no coinciden, conmute el filtro.</td>
        </tr>
        <tr>
          <td align="left">Eliminar</td>
          <td align="left">Seleccione esta opción para eliminar un filtro.</td>
          <td align="left"></td>
        </tr>
      </tbody>
    </table>

 

 
 

