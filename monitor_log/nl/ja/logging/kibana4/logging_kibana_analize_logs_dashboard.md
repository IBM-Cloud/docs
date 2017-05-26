---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# ダッシュボードを使用した Kibana でのログの分析
{:#kibana_analize_logs_dashboard}

Kibana の「*Dashboard*」ページを使用して、ダッシュボードでグループ化された視覚化のコレクションを表示します。ダッシュボードを使用して、ログ・データの分析および結果の比較を行います。
{:shortdesc}

{{site.data.keyword.Bluemix}} では、さまざまなタイプのダッシュボードがあり、それらを定義およびカスタマイズしてデータを視覚化および分析できます。例えば、以下の表では、一般的なダッシュボード・タイプをいくつかリストします。

| ダッシュボードのタイプ | 説明 |
|-------------------|-------------|
| single-cf-app ダッシュボード | これは、単一の Cloud Foundry アプリケーションの情報を表示するダッシュボードです。 |
| 単一コンテナー・ダッシュボード  | これは、単一のコンテナーの情報を表示するダッシュボードです。  |
| コンテナー・グループ・ダッシュボード  | これは、特定のコンテナー・グループの情報を表示するダッシュボードです。  |
| multi-cf-app ダッシュボード | これは、同じ {{site.data.keyword.Bluemix_notm}} スペースにデプロイされているすべての Cloud Foundry アプリケーションの情報を表示するダッシュボードです。  | 
| 複数コンテナー・ダッシュボード | 同じ {{site.data.keyword.Bluemix_notm}} スペースにデプロイされているすべてのコンテナーの情報を表示するダッシュボードです。  |
| スペース・ダッシュボード | これは、{{site.data.keyword.Bluemix_notm}} スペースで使用可能なロギング・データを表示するダッシュボードです。  | 
{: caption="表 1. ダッシュボード・タイプのサンプル" caption-side="top"}

ダッシュボードでデータを視覚化するには、パネルを構成します。Kibana には、さまざまな視覚化 (表、トレンド、ヒストグラムなど) が組み込まれているので、情報を分析するためにそれらを利用できます。視覚化は、ダッシュボードにパネルとして追加されます。ダッシュボード内のパネルの追加、削除、並べ替えを行うことができます。各パネルの目標は異なります。一部のパネルは、1 つ以上の照会の結果を表す行に編成されています。その他のパネルは、文書またはカスタム情報を表示します。各パネルは、検索に基づきます。検索により、パネルに表示されるデータのサブセットを定義します。データを視覚化し、分析するために、例えば、棒グラフ、円グラフ、または表を構成することができます。  

以下の表では、「Dashboard」ページで実行できる各種タスクをリストします。

| タスク | 詳細情報 |
|------|------------------|
| [新規ダッシュボードの作成](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | 複数のダッシュボードを作成できます。各ダッシュボードは、異なる検索、視覚化、およびログ・データの異なるサブセットを含めるように設計できます。  |
| [ダッシュボードの保存](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | ダッシュボードを将来再使用するために保存できます。 |
| [ダッシュボードのロード](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | ダッシュボードをアップロードして、そのデータを更新するか、ダッシュボードを変更するか、データを分析できます。 |
| [ダッシュボードの削除](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | 必要ではないダッシュボードを削除します。 |
| [ダッシュボードのエクスポート](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | ダッシュボードを JSON ファイルとしてエクスポートできます。 |
| [ダッシュボードのインポート](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | ダッシュボードを JSON ファイルとしてインポートできます。 |
| [ダッシュボードの共有](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | HTML ソースまたは Kibana ダッシュボードでダッシュボードを共有できます。 |
| [視覚化の追加](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | 既存の視覚化または検索をダッシュボードに追加できます。|
{: caption="表 2. ダッシュボードを操作するタスク" caption-side="top"}

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。

## 新規検索または視覚化の追加
{: #k4_dashboard_add_visualization}

既存の視覚化または検索を追加するには、以下のステップを実行します。

1. 「Dashboard」ページのツールバーで、**「Add visualization」**ボタン ![視覚化の追加](images/k4_dash_add_visualization_icon.jpg "視覚化の追加") をクリックします。

    **注**: 視覚化および検索を追加できます。 

2. **「Visualizations」**タブを選択して視覚化を追加するか、**「Searches」**タブを選択して検索を追加します。

3. 追加する検索または視覚化をクリックします。

    その検索または視覚化のパネルがダッシュボードに追加されます。

## 新規 Kibana ダッシュボードの作成
{: #K4_dashboard_new}

新規ダッシュボードを作成するには、以下のステップを実行します。

1. 「Dashboard」ページのツールバーで、**「New dashboard」**ボタン![新規ダッシュボード](images/k4_dash_new_icon.jpg "新規ダッシュボード") をクリックします。

2. 1 つ以上の検索および視覚化を追加します。詳しくは、『[新規検索または視覚化の追加](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization)』を参照してください。

    検索または視覚化を追加すると、パネルがダッシュボードに追加されます。

3. パネルをドラッグし、ダッシュボード上の配置する部分にドロップします。
 
4. 将来再使用するためにダッシュボードを保存します。詳しくは、『[Kibana ダッシュボードの保存](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save)』を参照してください。

## Kibana ダッシュボードの削除
{: #k4_dashboard_delete}

視覚化を削除するには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Visualizations」**タブで、削除する視覚化を選択します。

3. **「削除」**をクリックします。

## Kibana ダッシュボードのエクスポート
{: #k4_dashboard_export}

ダッシュボードを JSON ファイルとしてエクスポートするには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Dashboard」**タブで、エクスポートするダッシュボードを選択します。

3. **「エクスポート」**をクリックします。

4. ファイルを保存します。

## Kibana ダッシュボードのインポート
{: #k4_dashboard_import}

ダッシュボードを JSON ファイルとしてインポートするには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Dashboard」**タブで**「Import」**を選択します。

3. ファイルを選択し、**「Open」**をクリックします。

ダッシュボードがダッシュボードのリストに追加されます。

## Kibana ダッシュボードのロード
{: #k4_dashboard_reload}

保存済みダッシュボードをロードするには、以下のステップを実行します。

1. 「Dashboard」ページのツールバーで**「Load Saved Dashboard」**ボタン ![保存済みダッシュボードのロード](images/k4_dash_load_icon.jpg "保存済みダッシュボードのロード") をクリックします。

2. ロードするダッシュボードを選択します。 

## Kibana ダッシュボードの保存
{: #k4_dashboard_save}

カスタマイズした Kibana ダッシュボードを保存するには、以下の手順を実行します。

1. ツールバーで、**「Save」**ボタン ![ダッシュボードの保存](images/k4_dash_save_icon.jpg "ダッシュボードの保存") をクリックします。

2. ダッシュボードの名前を入力します。

    **注:** スペースを含む名前でダッシュボードを保存しようとすると、保存されません。

3. 名前フィールドの横の**「保存」**アイコンをクリックします。

## Kibana ダッシュボードの共有
{: #k4_dashboard_share}

ダッシュボードを共有するには、以下のステップを実行します。

1. 「Dashboard」ページのツールバーで、**「Share dashboard」**ボタン ![ダッシュボードの共有](images/k4_dash_share_icon.jpg "ダッシュボードの共有") をクリックします。

2. 次のアクションのいずれかを選択してください。

    * **Embed this dashboard**: HTML ソースでダッシュボードを共有する場合は、このオプションを選択します。 
    
        コピー・ボタン ![クリップボードにコピー](images/k4_copy_to_clipboard.jpg "クリップボードにコピー") をクリックして、HTML ソースでダッシュボードを埋め込むために使用できる HTML コードをコピーします。 
        
        **注**: ダッシュボードを表示するには、ユーザーは Kibana にアクセスできなければなりません。
	
    * **Share a link**: Kibana のダッシュボードを他のユーザーと共有する場合は、このオプションを選択します。



