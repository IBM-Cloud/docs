---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Réutilisation de ressources Kibana pour analyser des journaux Bluemix
{:#k4_reuse_resource}

Pour copier une recherche, une visualisation ou un tableau de bord depuis un espace {{site.data.keyword.Bluemix}} vers un autre espace, utilisez les fonctions d'exportation et d'importation disponible dans Kibana. Vous pouvez copier des ressources une par une ou exporter toutes les ressources dans Kibana.
{:shortdesc}

| Tâche | Description |
|------|-------------|
| [Copie d'une recherche](k4_reuse_resource.html#k4_reuse_search) | Copie d'une recherche d'un espace vers un autre.  |
| [Copie d'une visualisation](k4_reuse_resource.html#k4_reuse_visualization) | Copie d'une visualisation d'un espace vers un autre |

Prenez en compte les scénarios suivants dans {{site.data.keyword.Bluemix_notm}} pour réutiliser des recherches, des visualisations ou des tableaux de bord : 

* Copie d'une ressource depuis un espace vers un autre figurant dans une même organisation

    Par exemple, vous souhaiterez peut-être copier des visualisations depuis votre espace de développement dans {{site.data.keyword.Bluemix_notm}} vers votre espace de préproduction. 
    
* Copie d'une ressource depuis un espace vers un autre figurant dans différentes organisations d'un même compte

    Par exemple, vous souhaiterez peut-être copier vos visualisations depuis un espace de votre organisation de développement dans {{site.data.keyword.Bluemix_notm}} vers un espace de votre organisation de préproduction. 

* Copie d'une ressource depuis un espace vers un autre situés dans une même organisation mais figurant dans différentes régions publiques

    Par exemple, vous souhaiterez peut-être copier vos visualisations depuis un espace de l'organisation A dans {{site.data.keyword.Bluemix_notm}} qui est situé dans la région publique Sud des Etats-Unis vers un espace de votre organisation A qui est situé dans la région publique Royaume-Uni. 



## Copie d'une recherche
{:#k4_reuse_search}

Pour copier une recherche depuis un espace vers un autre dans {{site.data.keyword.Bluemix_notm}}, procédez comme suit :

1. Lancez Kibana pour l'espace sur lequel la recherche que vous souhaitez copier est disponible.  

    * Lancez Kibana à partir de l'interface utilisateur {{site.data.keyword.Bluemix_notm}} : le fichier de recherche JSON que vous pouvez exporter inclut les zones suivantes : *ID d'espace* et *ID d'application* pour les applications Cloud Foundry (CF) ou *ID d'instance* pour les conteneurs. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Lancez Kibana depuis un navigateur : le fichier de recherche JSON que vous pouvez exporter inclut la zone *ID d'espace*. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis un navigateur](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).

2. Sur la page *Paramètres*, sélectionnez **Objets**, puis l'onglet **Recherches**. Ensuite, sélectionnez une recherche et copiez les informations suivantes : 

    <table>
      <tbody>
        <tr>
          <th align="center">Zone de recherche</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> ID de l'espace où la recherche est appliquée à des données de filtre. </td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nom de la recherche. </td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Version de la recherche. </td>
        </tr>
      </tbody>
    </table>
   
3. Exportez la recherche. 

    1. Dans la page Settings (Paramètres), sélectionnez l'onglet **Objects** (Objets).
    2. Dans l'onglet **Searches** (Recherches), sélectionnez celle que vous désirez exporter.
    3. Cliquez sur **Export** (Exporter).
    4. Sauvegardez le fichier JSON. 

4. Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, passez dans l'espace où vous souhaitez copier la recherche, puis vérifiez que l'application ou le conteneur CF est disponible et en cours d'exécution. 
    
5. Lancez Kibana pour l'espace {{site.data.keyword.Bluemix_notm}} dans lequel vous souhaitez importer la recherche, puis procurez-vous les informations suivantes :

    Depuis l'[interface utilisateur Bluemix](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix) :
    
    <table>
      <tbody>
        <tr>
          <th align="center">Zone de recherche</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">ID d'espace</td>
          <td align="left"> <ol><li> Sur la page *Settings*, sélectionnez l'onglet*Indices* tab.</li> <br> <li>L'ID d'espace est imbriqué dans le modèle d'index. Le format du modèle d'index est le suivant : `[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` où *SpaceID* est l'ID d'espace. Copiez l'ID d'espace. </li></ol></td>
        </tr>
        <tr>
          <td align="left">ID d'application ou ID d'instance</td>
          <td align="left"><ul><li>Lorsque vous lancez Kibana depuis l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, la page *Discover* s'ouvre par défaut. Récupérez l'ID d'application ou l'ID d'instance dans la barre de recherche de la page *Discover*, par exemple, `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`.</li> <br> <li>Lorsque vous lancez kibana depuis un navigateur, sélectionnez l'élément application_id ou instance_id dans la liste de zones de la page Discover. </li></ul></td>
        </tr>
      </tbody>
    </table>

6. Modifiez le fichier de recherche JSON que vous avez exporté lors d'une étape précédente. Remplacez la valeur de l'ID d'application.  

    L'objet JSON suivant est un exemple de fichier JSON de recherche : 
 
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
    
    Dans cet exemple de fichier JSON, vous pouvez modifier les variables suivantes avec les informations du nouvel espace : 
    
    * SPACEID : Remplacez cette variable par l'ID d'espace du nouvel espace. 
    * NAME : Remplacez cette variable si vous souhaitez modifier le nom de la recherche dans le nouvel espace. Pour conserver le même nom, ne modifiez pas cette valeur. 
    * APPID : Remplacez cette variable par la valeur application_id de l'application CF dans le nouvel espace ou l'ID d'instance du conteneur dans le nouvel espace. 
    
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

6. Importez le fichier JSON de recherche dans Kibana pour le nouvel espace. 

    1. Sur la page Settings, sélectionnez l'onglet **Objects**. 
    2. Sur l'onglet **Searches**, sélectionnez le fichier JSON de recherche que vous souhaitez importer. 
    3. Cliquez sur **Import**.

Vous pouvez utiliser la recherche dans Kibana pour surveiller les données disponibles pour votre application dans le nouvel espace. 


    
## Copie d'une visualisation
{:#k4_reuse_visualization}

Procédez comme suit pour copier vers un autre espace une visualisation à utiliser en vue d'analyser les données d'une application d'un espace :

1. Lancez Kibana pour l'espace sur lequel la visualisation que vous souhaitez copier est disponible.  

    * Lancez Kibana à partir de l'interface utilisateur {{site.data.keyword.Bluemix_notm}} : le fichier de recherche JSON que vous pouvez exporter inclut les zones suivantes : *ID d'espace* et *ID d'application* pour les applications Cloud Foundry (CF) ou *ID d'instance* pour les conteneurs. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis le tableau de bord {{site.data.keyword.Bluemix_notm}}](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Lancez Kibana depuis un navigateur : le fichier de recherche JSON que vous pouvez exporter inclut la zone *ID d'espace*. Pour plus d'informations, voir [Accès au tableau de bord Kibana depuis un navigateur](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser).
    
2. Copiez la recherche qui est associée à la visualisation d'un espace vers un autre. Pour plus d'informations, voir [Copie d'une recherche d'un espace Bluemix vers un autre](k4_reuse_resource.html#k4_reuse_search).

    Une visualisation utilise une recherche pour filtrer les données qui s'affichent. Il se peut qu'une visualisation soit liée à une recherche, dans ce cas, toutes les mises à jour que vous apportez à cette recherche sont mises à jour automatiquement, ou qu'elle ne soit pas liée à une recherche, dans ce cas, les seules données disponibles pour analyse sont celles qui sont affichées au moment où la visualisation est créée. 

    Lorsque vous copiez une visualisation, quel que soit son statut de liaison à une recherche, vous devez aussi copier la recherche qui lui est associée. **Remarque :** lorsque vous importez une visualisation dans le nouvel espace, la nouvelle visualisation est liée à la recherche dans le nouvel espace. 
    
3. Sur la page *Settings*, sélectionnez **Objects**, puis l'onglet **Visualizations**. Puis, sélectionnez une visualisation et procurez-vous les informations suivantes :  

    <table>
      <tbody>
        <tr>
          <th align="center">Zone de visualisation</th>
          <th align="center">Description</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> ID de l'espace sur lequel la visualisation est utilisée pour analyser des données. </td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Nom de la visualisation. </td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Version de la visualisation.</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">ID de la recherche qui est utilisée pour filtrer les données affichées via la visualisation. <br> Le format de la valeur est le suivant :`SpaceID_SearchTitle` où SearchTitle est la valeur de la zone *title* de la recherche. </td>
        </tr>
      </tbody>
    </table>
   

4. Exportez la visualisation. 

    1. Sur la page Settings, sélectionnez l'onglet **Objects**. 
    2. Dans l'onglet **Visualizations**, sélectionnez la visualisation que vous désirez exporter.
    3. Cliquez sur **Export**. 
    4. Sauvegardez le fichier JSON. 
    
5. Dans l'interface utilisateur {{site.data.keyword.Bluemix_notm}}, passez dans l'espace où vous souhaitez copier la visualisation, puis vérifiez que l'application ou le conteneur CF est disponible et en cours d'exécution. 
    
6.  Modifiez le fichier de visualisation JSON que vous avez exporté lors d'une étape précédente. Remplacez les valeurs de l'ID d'espace et de l'ID de recherche.  

    L'objet JSON suivant est un exemple de fichier JSON de visualisation : 

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
    
    Dans cet exemple de fichier JSON, vous pouvez modifier les variables suivantes : 
    
    * SPACEID : Remplacez cette variable par l'ID d'espace du nouvel espace. 
    * NAME : Remplacez cette variable si vous souhaitez modifier le nom de la visualisation dans le nouvel espace. 
    * SEARCHID : Remplacez cette variable par l'ID de recherche du nouvel espace. ID de la requête qui est utilisée pour filtrer les données affichées via la visualisation. 
    
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

8. Importez la visualisation. 

    1. Sur la page Settings, sélectionnez l'onglet **Objects**. 
    2. Sur l'onglet **Visualizations**, sélectionnez le fichier JSON de visualisation que vous souhaitez importer.
    3. Cliquez sur **Import**.


Vous pouvez utiliser la visualisation dans Kibana pour surveiller les données disponibles pour votre application dans le nouvel espace. 
    
