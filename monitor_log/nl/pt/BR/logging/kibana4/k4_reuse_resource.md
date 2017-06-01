---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Reutilizando recursos do Kibana para analisar logs do Bluemix
{:#k4_reuse_resource}

Para copiar uma procura, uma visualização ou um painel de um espaço do {{site.data.keyword.Bluemix}} para um diferente, use os recursos de exportação e importação que estão disponíveis no Kibana. É possível copiar recursos individualmente ou exportar todos os recursos no Kibana.
{:shortdesc}

| Atividade | Descrição |
|------|-------------|
| [Copiar uma procura](k4_reuse_resource.html#k4_reuse_search) | Copie uma procura entre espaços. |
| [Copiar uma visualização](k4_reuse_resource.html#k4_reuse_visualization) | Copiar uma visualização entre espaços |

Considere os cenários a seguir no {{site.data.keyword.Bluemix_notm}} para reutilizar procuras, visualizações ou painéis: 

* Copie um recurso entre espaços na mesma organização.

    Por exemplo, você pode desejar copiar suas visualizações de seu espaço de desenvolvimento no {{site.data.keyword.Bluemix_notm}} para seu espaço de estágio.
    
* Copie um recurso entre espaços em organizações diferentes na mesma conta.

    Por exemplo, você pode desejar copiar suas visualizações de um espaço em sua organização de desenvolvimento no {{site.data.keyword.Bluemix_notm}} para um espaço em sua organização de preparação.

* Copie um recurso entre espaços que estão na mesma organização, mas localizados em regiões públicas diferentes.

    Por exemplo, você pode desejar copiar suas visualizações de um espaço na organização A no {{site.data.keyword.Bluemix_notm}} que está localizado na região pública Sul dos EUA para um espaço em sua organização A na região pública Reino Unido.



## Copiando uma procura
{:#k4_reuse_search}

Conclua as etapas a seguir para copiar uma procura entre espaços no {{site.data.keyword.Bluemix_notm}}:

1. Ative o Kibana no qual a procura que você deseja copiar está disponível. 

    * Ative o Kibana por meio da UI do {{site.data.keyword.Bluemix_notm}}: o arquivo de procura JSON que é possível exportar inclui os campos a seguir: *ID do espaço* e *ID do aplicativo* para aplicativos Cloud Foundry (CF) ou *ID da instância* para contêineres. Para obter mais informações, veja [Acessando o painel do Kibana por meio do painel do {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Ative o Kibana por meio de um navegador: o arquivo de procura JSON que é possível exportar inclui o campo *ID do espaço*. Para obter mais informações, veja [Acessando o painel do Kibana por meio de um navegador](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).

2. Na página *Configurações*, selecione **Objetos** e a guia **Procuras**. Em seguida, selecione uma procura e copie as informações a seguir:

    <table>
      <tbody>
        <tr>
          <th align="center">Campo de pesquisa</th>
          <th align="center">Descrição</th>
        </tr>
        <tr>
          <td align="left">agrupar</td>
          <td align="left"> ID do espaço no qual a procura é aplicada a dados de filtro.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nome da procura.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Versão da procura.</td>
        </tr>
      </tbody>
    </table>
   
3. Exporte a procura.

    1. Na página Configurações, selecione a guia **Objetos**.
    2. Na guia **Procuras**, selecione a procura que deseja exportar.
    3. Clique em **Exportar**.
    4. Salve o arquivo JSON.

4. Na UI do {{site.data.keyword.Bluemix_notm}}, mude para o espaço no qual você deseja copiar a procura e verifique se o aplicativo CF ou contêiner está disponível e em execução.
    
5. Ative o Kibana para o espaço do {{site.data.keyword.Bluemix_notm}} no qual você deseja importar a procura e, em seguida, obtenha as informações a seguir:

    Na [UI do Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix):
    
    <table>
      <tbody>
        <tr>
          <th align="center">Campo de pesquisa</th>
          <th align="center">Descrição</th>
        </tr>
        <tr>
          <td align="left">ID do espaço</td>
          <td align="left"> <ol><li> Na página *Configurações*, selecione a guia *Índices*.</li> <br> <li>O ID do espaço é integrado ao padrão de índice. O formato do padrão de índice é o seguinte: `[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` em que *SpaceID* é o ID do espaço. Copie o ID do espaço.</li></ol></td>
        </tr>
        <tr>
          <td align="left">ID do aplicativo ou ID da instância</td>
          <td align="left"><ul><li>Quando você ativa o Kibana por meio da UI do {{site.data.keyword.Bluemix_notm}}, a página *Descobrir* é aberta por padrão. Obtenha o ID do aplicativo ou o ID da instância na barra de procura na página *Descobrir*, por exemplo, `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`.</li> <br> <li>Ao ativar o Kibana por meio de um navegador, selecione o campo application_id ou instance_id na Lista de campos na página Descobrir.</li></ul></td>
        </tr>
      </tbody>
    </table>

6. Modifique o arquivo de procura JSON de procura que você exportou em uma etapa anterior. Substitua o valor do ID do aplicativo. 

    Por exemplo, o JSON a seguir é um exemplo de um arquivo JSON de procura. 
 
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
    
    Nesse arquivo JSON de amostra, é possível modificar as variáveis a seguir com as informações do novo espaço: 
    
    * SPACEID: substitua essa variável pelo ID do espaço do novo espaço.
    * NAME: substitua essa variável se você desejar mudar o nome da procura no novo espaço. Para manter o mesmo nome, não mude esse valor.
    * APPID: substitua essa variável pelo valor application_id do app CF no novo espaço ou pelo ID da instância do contêiner no novo espaço.
    
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

6. Importe o arquivo JSON de procura para o Kibana para o novo espaço.

    1. Na página Configurações, selecione a guia **Objetos**.
    2. Na guia **Procuras**, selecione o arquivo JSON de procura que você deseja importar.
    3. Clique em **Importar**.

É possível usar a procura no Kibana para monitorar os dados que estão disponíveis para seu aplicativo no novo espaço.


    
## Copiando uma visualização
{:#k4_reuse_visualization}

Conclua as etapas a seguir para copiar uma visualização que você usa para analisar dados de um aplicativo em um espaço para um espaço diferente:

1. Ative o Kibana para o espaço no qual a visualização que você deseja copiar está disponível. 

    * Ative o Kibana por meio da UI do {{site.data.keyword.Bluemix_notm}}: o arquivo de procura JSON que é possível exportar inclui os campos a seguir: *ID do espaço* e *ID do aplicativo* para aplicativos Cloud Foundry (CF) ou *ID da instância* para contêineres. Para obter mais informações, veja [Acessando o painel do Kibana por meio do painel do {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Ative o Kibana por meio de um navegador: o arquivo de procura JSON que é possível exportar inclui o campo *ID do espaço*. Para obter mais informações, veja [Acessando o painel do Kibana por meio de um navegador](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
2. Copie a procura que está associada à visualização entre espaços. Para obter mais informações, veja [Copiando uma procura entre espaços do Bluemix](k4_reuse_resource.html#k4_reuse_search).

    Uma visualização usa uma procura para filtrar os dados que ela exibe. Uma visualização pode ser vinculada a uma procura, assim todas as atualizações que você faz na procura são atualizadas automaticamente ou não são vinculadas a uma procura, assim os únicos dados disponíveis para análise são os dados exibidos no momento em que a visualização foi criada.

    Quando você copia uma visualização, independentemente de seu status vinculado a uma procura, também deve-se copiar a procura que está associada a ela. **Nota:** quando você importa uma visualização para o novo espaço, a nova visualização é vinculada à procura no novo espaço.
    
3. Na página *Configurações*, selecione **Objetos** e a guia **Visualizações**. Em seguida, selecione uma visualização e obtenha as informações a seguir: 

    <table>
      <tbody>
        <tr>
          <th align="center">Campo de visualização</th>
          <th align="center">Descrição</th>
        </tr>
        <tr>
          <td align="left">agrupar</td>
          <td align="left"> O valor do ID do espaço no qual a visualização é usada para analisar dados.</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nome da visualização.</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Versão da visualização.</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">ID da procura que é usada para filtrar os dados que são exibidos por meio da visualização. <br> O valor tem o formato a seguir: `SpaceID_SearchTitle`, em que SearchTitle é o valor do campo *title* da procura. </td>
        </tr>
      </tbody>
    </table>
   

4. Exporte a visualização.

    1. Na página Configurações, selecione a guia **Objetos**.
    2. Na guia **Visualizações**, selecione a visualização que deseja exportar.
    3. Clique em **Exportar**.
    4. Salve o arquivo JSON.
    
5. Na UI do {{site.data.keyword.Bluemix_notm}}, mude para o espaço no qual você deseja copiar a visualização e verifique se o aplicativo CF ou contêiner está disponível e em execução.
    
6.  Modifique o arquivo de visualização JSON de procura que você exportou em uma etapa anterior. Substitua os valores de ID do espaço e ID da procura. 

    Por exemplo, o JSON a seguir é um exemplo de um arquivo JSON de visualização. 

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
    
    Nesse arquivo JSON de amostra, é possível modificar as variáveis a seguir: 
    
    * SPACEID: substitua essa variável pelo ID do espaço do novo espaço.
    * NAME: substitua essa variável se você desejar mudar o nome da visualização no novo espaço.
    * SEARCHID: substitua essa variável pelo ID da procura no novo espaço. Esse é o ID da consulta que é usada para filtrar os dados que são exibidos por meio da visualização.
    
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

8. Importe a visualização.

    1. Na página Configurações, selecione a guia **Objetos**.
    2. Na guia **Visualizações**, selecione o arquivo JSON de visualização que você deseja importar.
    3. Clique em **Importar**.


É possível usar a visualização no Kibana para monitorar os dados que estão disponíveis para seu aplicativo no novo espaço.
    
