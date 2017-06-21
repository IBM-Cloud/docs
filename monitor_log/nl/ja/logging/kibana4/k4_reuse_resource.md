---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Bluemix ログを分析するための Kibana リソースの再使用
{:#k4_reuse_resource}

ある {{site.data.keyword.Bluemix}} スペースから別のスペースに検索、視覚化、またはダッシュボードをコピーするには、Kibana に用意されているエクスポートおよびインポート機能を使用します。Kibana では、個々のリソースをコピーすることも、すべてのリソースをエクスポートすることもできます。
{:shortdesc}

| タスク | 説明 |
|------|-------------|
| [検索のコピー](k4_reuse_resource.html#k4_reuse_search) | スペース間で検索をコピーします。 |
| [視覚化のコピー](k4_reuse_resource.html#k4_reuse_visualization) | スペース間で視覚化をコピーします。 |

検索、視覚化、またはダッシュボードを再使用するには、{{site.data.keyword.Bluemix_notm}} での以下のシナリオを検討してください。 

* 同じ組織内のスペース間でリソースをコピーする。

    例えば、{{site.data.keyword.Bluemix_notm}} で開発スペースからステージ・スペースに視覚化をコピーしたい場合があります。
    
* 同じアカウント内の異なる組織内のスペース間でリソースをコピーする。

    例えば、{{site.data.keyword.Bluemix_notm}} で開発組織の特定のスペースからステージング組織内の特定のスペースに視覚化をコピーしたい場合があります。

* 同じ組織内であるが、異なるパブリック地域にあるスペース間でリソースをコピーする。

    例えば、パブリック地域の米国南部にある、{{site.data.keyword.Bluemix_notm}} での組織 A の特定のスペースから、パブリック地域の英国の組織 A の特定のスペースに視覚化をコピーしたい場合があります。



## 検索のコピー
{:#k4_reuse_search}

{{site.data.keyword.Bluemix_notm}} でスペース間で検索をコピーするには、以下のステップを実行します。

1. コピーしたい検索を使用できる Kibana を起動します。 

    * {{site.data.keyword.Bluemix_notm}} UI からの Kibana の起動: エクスポートできる JSON 検索ファイルには、*space ID*、および Cloud Foundry (CF) アプリケーションの *application ID* またはコンテナーの *instance ID* フィールドが含まれています。詳しくは、『[{{site.data.keyword.Bluemix_notm}} ダッシュボードから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)』を参照してください。
    
    * ブラウザーからの Kibana の起動: エクスポートできる JSON 検索ファイルには、フィールド *space ID* が含まれています。詳しくは、『[Web ブラウザーから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)』を参照してください。

2. *「Settings」*ページで、**「Objects」**、**「Searches」**タブを選択します。次に、検索を選択して以下の情報をコピーします。

    <table>
      <tbody>
        <tr>
          <th align="center">検索フィールド</th>
          <th align="center">説明</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> データをフィルター操作するために検索が適用されるスペース ID。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">検索の名前。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">スペースのバージョン。</td>
        </tr>
      </tbody>
    </table>
   
3. 検索をエクスポートします。

    1. 「Settings」ページで**「Objects」**タブを選択します。
    2. **「Searches」**タブで、エクスポートする検索を選択します。
    3. **「エクスポート」**をクリックします。
    4. JSON ファイルを保存します。

4. {{site.data.keyword.Bluemix_notm}} UI で、検索のコピー元のスペースに移動し、CF アプリケーションまたはコンテナーが使用でき、実行されているか確認します。
    
5. 検索のインポート先の {{site.data.keyword.Bluemix_notm}} スペースで Kibana を起動し、以下の情報を取得します。

    [Bluemix UI](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix) から:
    
    <table>
      <tbody>
        <tr>
          <th align="center">検索フィールド</th>
          <th align="center">説明</th>
        </tr>
        <tr>
          <td align="left">space ID</td>
          <td align="left"> <ol><li> *「Settings」*ページで、*「Indices」*タブを選択します。</li> <br> <li>スペース ID が索引パターンに埋め込まれています。索引パターンのフォーマットは、`[logstash-3d8d2eae-SpaceID-]YYYY.MM.DD` です。ここで、*SpaceID* はスペースの ID です。スペース ID をコピーします。</li></ol></td>
        </tr>
        <tr>
          <td align="left">application ID または instance ID</td>
          <td align="left"><ul><li>{{site.data.keyword.Bluemix_notm}} UI から Kibana を起動すると、*「Discover」*ページがデフォルトで開きます。*「Discover」*ページの検索バーからアプリケーション ID またはインスタンス ID を取得します。例えば、`application_id:d88d1f16-e9d9-4623-bce7-0348c88f5133` などです。</li> <br> <li>ブラウザーから Kibana を起動した場合は、「Discover」ページの「Fields List」から application_id または instance_id を選択します。</li></ul></td>
        </tr>
      </tbody>
    </table>

6. 以前のステップでエクスポートした検索 JSON 検索ファイルを変更します。アプリケーション ID の値を置換します。 

    例えば、以下の JSON は、検索 JSON ファイルの例です。 
 
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
    
    このサンプル JSON ファイルで、新規スペースの情報で以下の変数を変更できます。 
    
    * SPACEID: この変数を新規スペースのスペース ID に置換します。
    * NAME: 新規スペースで検索の名前を変更したい場合は、この変数を置換します。同じ名前を維持したい場合は、この値を変更しないでください。
    * APPID: この変数を、新規スペース内の CF アプリの application_id 値に置換するか、新規スペース内のコンテナーのインスタンス ID に置換します。
    
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

6. 検索 JSON ファイルを新規スペースの Kibana にインポートします。

    1. 「Settings」ページで**「Objects」**タブを選択します。
    2. **「Searches」**タブで、インポートする検索 JSON ファイルを選択します。
    3. **「インポート」**をクリックします。

Kibana で検索を使用して、新規スペースのアプリケーションで使用できるデータをモニターできます。


    
## 視覚化のコピー
{:#k4_reuse_visualization}

あるスペースでアプリケーションのデータを分析するために使用した視覚化を別のスペースにコピーするには、以下のステップを実行します。

1. コピーする視覚化が使用できるスペースで Kibana を起動します。 

    * {{site.data.keyword.Bluemix_notm}} UI からの Kibana の起動: エクスポートできる JSON 検索ファイルには、*space ID*、および Cloud Foundry (CF) アプリケーションの *application ID* またはコンテナーの *instance ID* フィールドが含まれています。詳しくは、『[{{site.data.keyword.Bluemix_notm}} ダッシュボードから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_bluemix)』を参照してください。
    
    * ブラウザーからの Kibana の起動: エクスポートできる JSON 検索ファイルには、フィールド *space ID* が含まれています。詳しくは、『[Web ブラウザーから Kibana ダッシュボードへの移動](logging_analyzing_logs_Kibana.html#launch_Kibana_from_browser)』を参照してください。
    
2. スペース間で視覚化に関連付けられた検索をコピーします。詳しくは、『[Bluemix スペース間での検索のコピー (Copying a search between Bluemix spaces)](k4_reuse_resource.html#k4_reuse_search)』を参照してください。

    視覚化は、検索を使用して、表示するデータをフィルター操作します。視覚化は、検索に対して行うすべての更新が自動的に更新されるように検索にリンクさせることも、分析に使用可能なデータのみが視覚化を作成したときに表示されるデータとなるように、検索にリンクさせないことも可能です。

    視覚化をコピーする場合、検索にリンクされた状況にかかわらず、それに関連付けられた検索もコピーする必要があります。**注:** 視覚化を新規スペースにインポートすると、新規スペースで新規視覚化が検索にリンクされます。
    
3. *「Settings」*ページで、**「Objects」**および**「Visualizations」**タブを選択します。次に、視覚化を選択し、以下の情報を取得します。 

    <table>
      <tbody>
        <tr>
          <th align="center">視覚化フィールド</th>
          <th align="center">説明</th>
        </tr>
        <tr>
          <td align="left">group</td>
          <td align="left"> データの分析に視覚化が使用されるスペース ID の値。</td>
        </tr>
        <tr>
          <td align="left">title</td>
          <td align="left">視覚化の名前。</td>
        </tr>
        <tr>
          <td align="left">version</td>
          <td align="left">視覚化のバージョン。</td>
        </tr>
        <tr>
          <td align="left">savedSearchID</td>
          <td align="left">視覚化を通じて表示されるデータのフィルター操作に使用される検索の ID。<br> 値のフォーマットは `SpaceID_SearchTitle` です。ここで、SearchTitle は、検索の *title* フィールドの値です。</td>
        </tr>
      </tbody>
    </table>
   

4. 視覚化をエクスポートします。

    1. 「Settings」ページで**「Objects」**タブを選択します。
    2. **「Visualizations」**タブで、エクスポートする視覚化を選択します。
    3. **「エクスポート」**をクリックします。
    4. JSON ファイルを保存します。
    
5. {{site.data.keyword.Bluemix_notm}} UI で、視覚化のコピー元のスペースに移動し、CF アプリケーションまたはコンテナーが使用でき、実行されているか確認します。
    
6.  以前のステップでエクスポートした検索 JSON 視覚化ファイルを変更します。スペース ID および検索 ID の値を置換します。 

    例えば、以下の JSON は、視覚化 JSON ファイルの例です。 

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
    
    このサンプル JSON ファイルで、以下の変数を変更できます。 
    
    * SPACEID: この変数を新規スペースのスペース ID に置換します。
    * NAME: 新規スペースでの視覚化の名前を変更したい場合は、この変数を置換します。
    * SEARCHID: この変数を新規スペースのスペース ID に置換します。これは、視覚化を通じて表示されるデータのフィルター操作に使用される照会の ID です。
    
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

8. 視覚化をインポートします。

    1. 「Settings」ページで**「Objects」**タブを選択します。
    2. **「Visualizations」**タブで、インポートする視覚化 JSON ファイルを選択します。
    3. **「インポート」**をクリックします。


Kibana で視覚化を使用して、新規スペースのアプリケーションで使用できるデータをモニターできます。
    
