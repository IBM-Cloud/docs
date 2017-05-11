---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Kibana-Ressourcen zur Analyse von Bluemix-Protokoll wiederverwenden
{:#k4_reuse_resource}

Zum Kopieren einer Suche, einer Visualisierung oder eines Dashboards aus einem {{site.data.keyword.Bluemix}}-Bereich in einen anderen verwenden Sie die in Kibana verfügbaren Export- und Importfunktionen. Sie können Ressourcen einzeln kopieren oder alle Ressourcen in Kibana exportieren.
{:shortdesc}

| Task | Beschreibung |
|------|-------------|
| [Suche kopieren](k4_reuse_resource.html#k4_reuse_search) | Sie können eine Suche zwischen Bereichen kopieren. |
| [Visualisierung kopieren](k4_reuse_resource.html#k4_reuse_visualization) | Sie können eine Visualisierung zwischen Bereichen kopieren. |

Betrachten Sie die folgenden Szenarios in {{site.data.keyword.Bluemix_notm}} für die Wiederverwendung von Suchen, Visualisierungen und Dashboards:  

* Sie können eine Ressource zwischen Bereichen derselben Organisation kopieren. 

    Beispiel: Sie möchten vielleicht Ihre Visualisierungen aus Ihrem Entwicklungsbereich in {{site.data.keyword.Bluemix_notm}} in Ihren Staging-Bereich kopieren. 
    
* Sie können eine Ressource zwischen verschiedenen Organisationen im selben Konto kopieren. 

    Beispiel: Sie möchten vielleicht Ihre Visualisierungen aus einem Bereich in Ihrer Entwicklungsorganisation in {{site.data.keyword.Bluemix_notm}} in einen Bereich Ihrer Staging-Organisation kopieren. 

* Sie können eine Ressource zwischen Bereichen kopieren, die sich zwar in derselben Organisation, aber in verschiedenen öffentlichen Regionen befinden. 

    Beispiel: Sie möchten vielleicht Ihre Visualisierungen aus einem Bereich in Organisation A in {{site.data.keyword.Bluemix_notm}}, die sich in der öffentlichen Region 'Vereinigte Staaten (Süden)' befindet, in einen Bereich Ihrer Organisation A in der öffentlichen Region 'Vereintes Königreich' kopieren. 



## Suche kopieren
{:#k4_reuse_search}

Führen Sie die folgenden Schritte aus, um eine Suche zwischen Bereichen in {{site.data.keyword.Bluemix_notm}} zu kopieren: 

1. Starten Sie Kibana von einer Position aus, an der die Suche, die Sie kopieren wollen, verfügbar ist.  

    * Kibana über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle (UI) starten: Die JSON-Suchdatei, die Sie exportieren können, enthält die folgenden Felder: *Bereichs-ID* und *Anwendungs-ID* für Cloud Foundry-Anwendungen (CF-Anwendungen) oder *Instanz-ID* für Container. Weitere Informationen finden Sie unter [Kibana-Dashboard über das {{site.data.keyword.Bluemix_notm}}-Dashboard aufrufen](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Kibana über einen Browser starten: Die JSON-Suchdatei, die Sie exportieren können, enthält das Feld *Bereichs-ID*. Weitere Informationen finden Sie unter [Kibana-Dashboard im Browser aufrufen](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser). 

2. Wählen Sie auf der Seite *Settings* die Registerkarte **Objects** und die Registerkarte **Searches** aus. Wählen Sie anschließend eine Suche aus und kopieren Sie die folgenden Informationen: 

    <table>
      <tbody>
        <tr>
          <th align="center">Suchfeld</th>
          <th align="center">Beschreibung</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> Die Bereichs-ID (Space ID) für den Bereich, in dem die Suche zum Filtern von Daten angewendet wird. </td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Der Name der Suche. </td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Die Version der Suche. </td>
        </tr>
      </tbody>
    </table>
   
3. Exportieren Sie die Suche. 

    1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus.
    2. Wählen Sie auf der Registerkarte **Searches** die Suche aus, die Sie exportieren wollen.
    3. Klicken Sie auf **Export**.
    4. Speichern Sie die JSON-Datei. 

4. Wechseln Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zu dem Bereich, in dem Sie die Suche kopieren wollen, und prüfen Sie, ob die CF-Anwendung bzw. der Container verfügbar und aktiv ist. 
    
5. Starten Sie Kibana für den {{site.data.keyword.Bluemix_notm}}-Bereich, in den Sie die Suche importieren wollen, und ermitteln Sie die folgenden Informationen: 

    Aus der [Bluemix-Benutzerschnittstelle](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix): 
    
    <table>
      <tbody>
        <tr>
          <th align="center">Suchfeld</th>
          <th align="center">Beschreibung</th>
        </tr>
        <tr>
          <td align="left">Bereichs-ID</td>
          <td align="left"> <ol><li> Wählen Sie auf der Seite *Settings* die Registerkarte *Indices* aus. </li> <br> <li>Die Bereichs-ID (SpaceID) ist in das Indexmuster eingebettet. Das Format des Indexmusters sieht wie folgt aus: `[logstash-3d8d2eae-SpaceID-]JJJJ.MM.TT`. Dabei ist *SpaceID* die ID des Bereichs. Kopieren Sie die Bereichs-ID. </li></ol></td>
        </tr>
        <tr>
          <td align="left">Anwendungs-ID oder Instanz-ID</td>
          <td align="left"><ul><li>Wenn Sie Kibana von der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle aus starten, wird standardmäßig die Seite *Discover* geöffnet. Ermitteln Sie die Anwendungs-ID oder die Instanz-ID in der Suchleiste auf der Seite *Discover*, zum Beispiel: `application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133`. </li> <br> <li>Wenn Sie Kibana in einem Browser starten, wählen Sie das Feld 'application_id' bzw. 'instance_id' in der Liste 'Fields' auf der Seite 'Discover' aus. </li></ul></td>
        </tr>
      </tbody>
    </table>

6. Ändern Sie die JSON-Suchdatei, die Sie in einem vorherigen Schritt exportiert haben. Ersetzen Sie den Wert für die Anwendungs-ID (application_id).  

    Beispiel: Der folgende JSON-Code ist ein Beispiel für eine JSON-Suchdatei.  
 
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
        "searchSourceJSON": "{\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]JJJJ.MM.TT\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:4ae73dcd-1fc4-48f0-9dc7-425839040436\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-52edf6e6-5386-4235-8fb8-598de3b80f41-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"4ae73dcd-1fc4-48f0-9dc7-425839040436\",\"type\":\"phrase\"}}}}]}"
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
    
    In diesem Beispiel für eine JSON-Datei können Sie die folgenden Variablen mit den Informationen des neuen Bereichs ändern:  
    
    * SPACEID: Ersetzen Sie diese Variable durch die Bereichs-ID des neuen Bereichs. 
    * NAME: Ersetzen Sie diese Variable, wenn Sie den Namen der Suche im neuen Bereich ändern wollen. Soll der gleiche Name beibehalten werden, ändern Sie diesen Wert nicht. 
    * APPID: Ersetzen Sie diese Variable durch den Wert für 'application_id' der CF-App im neuen Bereich bzw. durch die Instanz-ID des Containers im neuen Bereich. 
    
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
        "searchSourceJSON": "{\"index\":\"[logstash-SPACEID-]JJJJ.MM.TT\",\"query\":{\"query_string\":{\"analyze_wildcard\":true,\"query\":\"application_id:APPID\"}},\"highlight\":{\"pre_tags\":[\"@kibana-highlighted-field@\"],\"post_tags\":[\"@/kibana-highlighted-field@\"],\"fields\":{\"*\":{}},\"fragment_size\":2147483647},\"filter\":[{\"meta\":{\"negate\":false,\"index\":\"[logstash-SPACEID-]YYYY.MM.DD\",\"key\":\"application_id\",\"value\":\"APPID\",\"disabled\":false},\"query\":{\"match\":{\"application_id\":{\"query\":\"APPID\",\"type\":\"phrase\"}}}}]}"
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

6. Importieren Sie die JSON-Suchdatei in Kibana für den neuen Bereich. 

    1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus.
    2. Wählen sie auf der Registerkarte **Searches** die JSON-Suchdatei aus, die Sie importieren wollen. 
    3. Klicken Sie auf **Import**. 

Sie können die Suche nun in Kibana zur Überwachung der Daten verwenden, die für Ihre Anwendung in dem neuen Bereich verfügbar sind. 


    
## Visualisierung kopieren
{:#k4_reuse_visualization}

Führen Sie die folgenden Schritte aus, um eine Visualisierung, die Sie zur Analyse von Daten einer Anwendung in einem Bereich verwenden, in einen anderen Bereich zu kopieren: 

1. Starten Sie Kibana für den Bereich, in dem die zu kopierende Visualisierung verfügbar ist.  

    * Kibana über die {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle (UI) starten: Die JSON-Suchdatei, die Sie exportieren können, enthält die folgenden Felder: *Bereichs-ID* und *Anwendungs-ID* für Cloud Foundry-Anwendungen (CF-Anwendungen) oder *Instanz-ID* für Container. Weitere Informationen finden Sie unter [Kibana-Dashboard über das {{site.data.keyword.Bluemix_notm}}-Dashboard aufrufen](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix).
    
    * Kibana über einen Browser starten: Die JSON-Suchdatei, die Sie exportieren können, enthält das Feld *Bereichs-ID*. Weitere Informationen finden Sie unter [Kibana-Dashboard im Browser aufrufen](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser). 
    
2. Kopieren Sie die Suche, die der Visualisierung zugeordnet ist, zwischen Bereichen. Weitere Informationen finden Sie unter [Suche zwischen Bluemix-Bereichen kopieren](k4_reuse_resource.html#k4_reuse_search). 

    Eine Visualisierung verwendet eine Suche zum Filtern der Daten, die sie anzeigt. Eine Visualisierung kann zudem mit einer Suche verknüpft sein, sodass alle Aktualisierungen, die an der Suche vorgenommen werden, automatisch aktualisiert werden. Sie kann auch nicht mit einer Suche verknüpft sein, sodass die Daten, die für die Analyse verfügbar sind, nur die Daten sind, die zu dem Zeitpunkt angezeigt wurden, zu dem Sie die Visualisierung erstellt haben. 

    Wenn Sie eine Visualisierung kopieren, müssen Sie unabhängig vom Verknüpfungsstatus mit einer Suche auch die Suche kopieren, die ihr zugeordnet ist. **Hinweis:** Wenn Sie eine Visualisierung in den neuen Bereich importieren, wird die neue Visualisierung mit der Suche im neuen Bereich verknüpft. 
    
3. Wählen Sie auf der Seite *Settings* die Registerkarte **Objects** und die Registerkarte **Visualizations** aus. Wählen Sie anschließend eine Visualisierung aus und ermitteln Sie die folgenden Informationen:  

    <table>
      <tbody>
        <tr>
          <th align="center">Visualisierungsfeld</th>
          <th align="center">Beschreibung</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> Der ID-Wert für den Bereich, in dem die Visualisierung zur Analyse von Daten verwendet wird. </td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">Der Name der Visualisierung. </td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">Die Version der Visualisierung. </td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">Die ID der Suche, die zum Filtern der Daten verwendet wird, die durch die Visualisierung angezeigt werden. <br> Der Wert hat das folgende Format: `SpaceID_SearchTitle`. Dabei ist 'SearchTitle' der Wert des Felds *title* der Suche. </td>
        </tr>
      </tbody>
    </table>
   

4. Exportieren Sie die Visualisierung. 

    1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus.
    2. Wählen Sie auf der Registerkarte **Visualizations** die Visualisierung aus, die Sie exportieren wollen.
    3. Klicken Sie auf **Export**.
    4. Speichern Sie die JSON-Datei. 
    
5. Wechseln Sie in der {{site.data.keyword.Bluemix_notm}}-Benutzerschnittstelle zu dem Bereich, in dem Sie die Visualisierung kopieren wollen, und prüfen Sie, ob die CF-Anwendung bzw. der Container verfügbar und aktiv ist. 
    
6.  Ändern Sie die JSON-Visualisierungsdatei, die Sie in einem vorherigen Schritt exportiert haben. Ersetzen Sie die Werte für die Bereichs-ID und die Such-ID.  

    Beispiel: Der folgende JSON-Code ist ein Beispiel für eine JSON-Visualisierungsdatei.  

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
    
    In diesem Beispiel für eine JSON-Datei können Sie die folgenden Variablen ändern:  
    
    * SPACEID: Ersetzen Sie diese Variable durch die Bereichs-ID des neuen Bereichs. 
    * NAME: Ersetzen Sie diese Variable, wenn Sie den Namen der Visualisierung im neuen Bereich ändern wollen. 
    * SEARCHID: Ersetzen Sie diese Variable durch die Such-ID (SEARCHID) im neuen Bereich. Dies ist die ID der Abfrage, die zum Filtern der Daten verwendet wird, die durch die Visualisierung angezeigt werden. 
    
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

8. Importieren Sie die Visualisierung. 

    1. Wählen Sie auf der Seite 'Settings' die Registerkarte **Objects** aus.
    2. Wählen sie auf der Registerkarte **Visualizations** die JSON-Visualisierungsdatei aus, die Sie importieren wollen. 
    3. Klicken Sie auf **Import**. 


Sie können die Visualisierung nun in Kibana zur Überwachung der Daten verwenden, die für Ihre Anwendung in dem neuen Bereich verfügbar sind. 
    
