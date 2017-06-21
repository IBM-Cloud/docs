---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Reutilización de recursos de Kibana para analizar registros de Bluemix
{:#k4_reuse_resource}

Para copiar una búsqueda, una visualización o un panel de control desde un espacio de {{site.data.keyword.Bluemix}} a uno distinto, utilice las funcionalidades de importación y exportación que están disponibles en Kibana. Puede copiar recursos individualmente o exportar todos los recursos en Kibana.
{:shortdesc}

| Tarea | Descripción |
|------|-------------|
| [Copiar una búsqueda](k4_reuse_resource.html#k4_reuse_search) | Copia una búsqueda entre espacios. |
| [Copiar una visualización](k4_reuse_resource.html#k4_reuse_visualization) | Copia una visualización entre espacios. |

Considere los siguientes escenarios en {{site.data.keyword.Bluemix_notm}} para la reutilización de búsquedas, visualizaciones o paneles de control: 

* Copiar un recurso entre espacios en la misma organización.

    Por ejemplo, es posible que desee copiar las visualizaciones desde su espacio de desarrollo en {{site.data.keyword.Bluemix_notm}} a su espacio de transferencia.
    
* Copiar un recurso entre espacios en diferentes organizaciones en la misma cuenta.

    Por ejemplo, es posible que desee copiar sus visualizaciones desde un espacio en su organización de desarrollo en {{site.data.keyword.Bluemix_notm}} a un espacio en su organización de transferencia.

* Copiar un recurso entre espacios en la misma organización pero ubicados en regiones públicas diferentes.

    Por ejemplo, podría desear copiar sus visualizaciones desde un espacio en la organización A en la instancia de {{site.data.keyword.Bluemix_notm}} ubicada en la región pública US South a un espacio en su organización A en la región pública United Kingdom.



## Copia de una búsqueda
{:#k4_reuse_search}

Complete los siguientes pasos para copiar una búsqueda entre espacios en {{site.data.keyword.Bluemix_notm}}:

1. Inicie Kibana donde la búsqueda que desea copiar esté disponible. 

    * Inicie Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}: El archivo de búsqueda JSON que puede exportar incluye los siguientes campos: *space ID* y *application ID* para aplicaciones Cloud Foundry (CF) o el campo *instance ID* para contenedores. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde el panel de control de {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Inicie Kibana desde un navegador: El archivo de búsqueda JSON que puede exportar incluye el campo *space ID*. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde un navegador](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).

2. En la página *Valores*, seleccione **Objetos** y el separador **Búsquedas**. A continuación seleccione una búsqueda y copie la siguiente información:

    <table>
      <tbody>
        <tr>
          <th align="center">Campo de búsqueda</th>
          <th align="center">Descripción</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> ID de espacio donde se aplica la búsqueda para filtrar datos.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nombre de la búsqueda.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Versión de la búsqueda.</td>
        </tr>
      </tbody>
    </table>
   
3. Exporte la búsqueda.

    1. En la página Valores, seleccione el separador **Objetos**.
    2. En el separador **Búsquedas**, seleccione las búsquedas que desea exportar.
    3. Pulse **Exportar**.
    4. Guarde el archivo JSON.

4. En la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, cambie al espacio donde desea copiar la búsqueda, y compruebe que el contenedor o la aplicación CF están disponibles y en ejecución.
    
5. Inicie Kibana para el espacio de {{site.data.keyword.Bluemix_notm}} donde desea importar la búsqueda y, a continuación, obtenga la siguiente información:

    Desde la [interfaz de usuario de Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix):
    
    <table>
      <tbody>
        <tr>
          <th align="center">Campo de búsqueda</th>
          <th align="center">Descripción</th>
        </tr>
        <tr>
          <td align="left">space ID</td>
          <td align="left"> <ol><li> En la página *Valores*, seleccione el separador *Índices*.</li> <br> <li>El espacio ID se incluye en el patrón de índice. El formato del patrón de índice es el siguiente: `[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` donde *SpaceID* es el ID del espacio. Copie el ID de espacio.</li></ol></td>
        </tr>
        <tr>
          <td align="left">application ID o instance ID</td>
          <td align="left"><ul><li>Cuando inicia Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, la página de *Descubrir* se abre de forma predeterminada. Obtenga el ID de aplicación o el ID de instancia desde la barra de búsqueda en la página *Descubrir*, por ejemplo, `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`.</li> <br> <li>Cuando inicie Kibana desde un navegador, seleccione el campo application_id o instance_id desde la lista de campos en la página Descubrir.</li></ul></td>
        </tr>
      </tbody>
    </table>

6. Modifique el archivo de búsqueda JSON que exportó en el paso anterior. Sustituya el valor del ID de aplicación. 

    A continuación se muestra un ejemplo de un archivo JSON de búsqueda. 
 
    <pre class="pre">
    [
  {
    "_id": "52edf6e6-5386-4235-8fb8-598de3b80f41_Dev",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "52edf6e6-5386-4235-8fb8-598de3b80f41",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:4ae73dcd-1fc4-48f0-9dc7-425839040436\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>
    
    En este archivo JSON de ejemplo, puede modificar las siguientes variables con la información del nuevo espacio: 
    
    * SPACEID: Sustituya esta variable con el espacio ID del nuevo espacio.
    * NAME: Sustituya esta variable si desea cambiar el nombre de la búsqueda en el nuevo espacio. Para mantener el mismo nombre, no cambie este valor.
    * APPID: Sustituya esta variable con el valor del application_id de la app CF en el nuevo espacio o el ID de instancia del contenedor en el nuevo espacio.
    
   <pre class="pre">
   [
  {
    "_id": "SPACEID_NAME",
    "_type": "search",
    "_source": {
      "columns": [
        "application_id",
        "source_id",
        "instance_id"
      ],
      "description": "",
      "group": "SPACEID",
      "hits": 0,
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:APPID\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"APPID\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"APPID\",\"type\":\"phrase\"}}}}]}"
      },
      "sort": [
        "@timestamp",
        "desc"
      ],
      "title": "Dev",
      "version": 1
    }
  }
]
    </pre>

6. Importe el archivo JSON de búsqueda en Kibana para el nuevo espacio.

    1. En la página Valores, seleccione el separador **Objetos**.
    2. En el separador **Búsquedas**, seleccione el archivo JSON de búsqueda que desea importar.
    3. Pulse **Importar**.

Utilice la búsqueda en Kibana para supervisar los datos disponibles para su aplicación en el nuevo espacio.


    
## Copia de una visualización
{:#k4_reuse_visualization}

Complete los siguientes pasos para copiar una visualización que utiliza para analizar datos de una aplicación de un espacio a otro espacio:

1. Inicie Kibana para el espacio en donde está disponible la visualización que desea copiar. 

    * Inicie Kibana desde la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}: El archivo de búsqueda JSON que puede exportar incluye los siguientes campos: *space ID* y *application ID* para aplicaciones Cloud Foundry (CF) o el campo *instance ID* para contenedores. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde el panel de control de {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Inicie Kibana desde un navegador: El archivo de búsqueda JSON que puede exportar incluye el campo *space ID*. Para obtener más información, consulte [Cómo ir al panel de control de Kibana desde un navegador](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
2. Copie la búsquela que está asociada con la visualización entre espacios. Para obtener más información, consulte [Copia de una búsqueda entre espacios de Bluemix](k4_reuse_resource.html#k4_reuse_search).

    Una visualización utiliza una búsqueda para filtrar los datos que muestra. Una visualización podría estar enlazada a una búsqueda de forma que todas las actualizaciones que realizase a la búsqueda se actualizarían de forma automática, o no estar enlazada a la búsqueda de forma que únicamente los datos que estuviesen disponibles para su análisis serían los datos visualizados en el momento de crear la visualización.

    Cuando se copia una visualización también debe copiar la búsqueda que está asociada a la misma, independientemente del estado de enlace a dicha búsqueda. **Nota:** Cuando importa una visualización en el nuevo espacio, la nueva visualización se enlaza a la búsqueda en el nuevo espacio.
    
3. En la página *Valores*, seleccione **Objetos** y el separador **Visualizaciones**. A continuación, seleccione una visualización y obtenga la siguiente información: 

    <table>
      <tbody>
        <tr>
          <th align="center">Campo de visualización</th>
          <th align="center">Descripción</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> Valor de ID de espacio donde la visualización se utiliza para analizar los datos.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nombre de la visualización.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Versión de la visualización.</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">ID de la búsqueda que se utiliza para filtrar los datos que se visualizan con la visualización. <br> El valor tiene el formato siguiente: `SpaceID_SearchTitle` donde SearchTitle es el valor del campo *title* de la búsqueda. </td>
        </tr>
      </tbody>
    </table>
   

4. Exporte la visualización.

    1. En la página Valores, seleccione el separador **Objetos**.
    2. En el separador **Visualizaciones**, seleccione la visualización que desea exportar.
    3. Pulse **Exportar**.
    4. Guarde el archivo JSON.
    
5. En la interfaz de usuario de {{site.data.keyword.Bluemix_notm}}, cambie al espacio donde desea copiar la visualización, y compruebe que el contenedor o la aplicación CF están disponibles y en ejecución.
    
6.  Modifique el archivo de visualización JSON que exportó en el paso anterior. Sustituya los valores del ID de espacio y el ID de búsqueda. 

    A continuación se muestra un ejemplo de un archivo JSON de visualización. 

    <pre class="pre">
    [
  {
    "_id": "3d8d2eae-f3f0-44f6-9717-126113a00b51_test",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "3d8d2eae-f3f0-44f6-9717-126113a00b51",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "3d8d2eae-f3f0-44f6-9717-126113a00b51_Default_9d222152-8834-4bab-8685-3036cd25931a",
      "title": "test",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>
    
    En este archivo JSON de ejemplo, puede modificar las siguientes variables: 
    
    * SPACEID: Sustituya esta variable con el espacio ID del nuevo espacio.
    * NAME: Sustituya esta variable si desea cambiar el nombre de la visualización en el nuevo espacio.
    * SEARCHID: Sustituya esta variable con el ID de búsqueda en el nuevo espacio. Este es el ID de la consulta que se utiliza para filtrar los datos que se visualizan con la visualización.
    
       <pre class="pre">
    [
  {
    "_id": "SPACEID_NAME",
    "_type": "visualization",
    "_source": {
      "description": "",
      "group": "SPACEID",
      "kibanaSavedObjectMeta": {
        "searchSourceJSON": "{\"filter\":[]}"
      },
      "savedSearchId": "SPACEID_SEARCHID",
      "title": "NAME",
      "version": 1,
      "visState": "{\"type\":\"line\",\"params\":{\"shareYAxis\":true,\"addTooltip\":true,\"addLegend\":true,\"showCircles\":true,\"smoothLines\":false,\"interpolate\":\"linear\",\"scale\":\"linear\",\"drawLinesBetweenPoints\":true,\"radiusRatio\":9,\"times\":[],\"addTimeMarker\":false,\"defaultYExtents\":false,\"setYExtents\":false,\"yAxis\":{}},\"aggs\":[{\"id\":\"1\",\"type\":\"count\",\"schema\":\"metric\",\"params\":{}}],\"listeners\":{}}"
    }
    }
    ]
    </pre>

8. Importe la visualización.

    1. En la página Valores, seleccione el separador **Objetos**.
    2. En el separador **Visualizaciones**, seleccione el archivo JSON de visualización que desea importar.
    3. Pulse **Importar**.


Utilice la visualización en Kibana para supervisar los datos disponibles para su aplicación en el nuevo espacio.
    
