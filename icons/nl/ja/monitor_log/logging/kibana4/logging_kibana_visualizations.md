---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# 視覚化を使用した Kibana でのログの分析 
{:#logging_kibana_visualizations}

ログ・データの分析および結果の比較に使用できるグラフや表などの視覚化を作成するには、Kibana の「*Visualize*」ページを使用します。
{:shortdesc}

ログを分析するために個別に視覚化を使用できます。 

* 「*Discover*」ページで定義して保存した検索から、または「*Visualize*」ページで定義した新規照会から視覚化を作成できます。検索により、視覚化で表示されるデータのサブセットを定義します。

* 選択した視覚化のタイプにより、分析用にどのようにデータが表示されるのかが決定します。

以下の表では、各種視覚化タイプをリストします。

| 視覚化タイプ | 説明 |
|-----------------------|-------------|
| Area chart (面グラフ) | グラフィカルに数量データが表示されます。2 つ以上の集約データ・セットを比較する場合に使用します。 |
| Data table (データ表) | 構成された集約の生データが表形式で表示されます。 |
| Line chart (折れ線グラフ) | 時間ベースのデータが表示されます。2 つ以上の時間ベースの集約データ・セットを比較する場合に使用します。 |
| Markdown widget (マークダウン・ウィジェット) | テキスト情報を表示する場合に使用します。 |
| Metric (メトリック) | ヒット数、または数値フィールドの平均を表示する場合に使用します。 |
| Pie chart (円グラフ) | 1 つのフィールドの各値を表示する場合に使用します。 | 
| Vertical bar chart (垂直棒グラフ) | 時間ベースのデータおよび時間ベースでないデータが表示されます。データをグループ化する場合に使用します。 |

「Visualize」ページで、以下の任意のタスクを実行できます。

| タスク | 詳細情報 |
|------|------------------|
| [新規視覚化の作成](logging_kibana_visualizations.html#logging_k4_visualizations_create) | 「*Discover*」ページで定義して保存した検索から、または「*Visualize*」ページで定義した新規照会から視覚化を作成できます。 |
| [視覚化の保存](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | 視覚化を将来再使用するために保存できます。 |
| [視覚化のロード](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | 視覚化をアップロードして、そのデータを更新するか、視覚化を変更するか、データを分析できます。 |
| [視覚化の削除](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | 必要ではない視覚化を削除します。 |
| [視覚化のエクスポート](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | 視覚化を JSON ファイルとしてエクスポートできます。  |
| [視覚化のインポート](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | 視覚化を JSON ファイルとしてインポートできます。  |
| [視覚化の共有](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | HTML ソースまたは Kibana ダッシュボードで視覚化を共有できます。  |


## Kibana での照会からの視覚化の作成
{:#logging_k4_visualizations_create}

「Visualize」ページから視覚化を作成するには、以下のステップを実行します。

1. Kibana を起動してから、**「Visualize」**ページを選択します。

2. 新規視覚化を作成します。ツールバーでは、**「New Visualization」**ボタン ![新規視覚化](images/k4_visualization_new_icon.jpg "新規視覚化") をクリックします。

3. 視覚化を選択します。
    
4. 検索ソースを選択します。次のオプションのいずれかを選択してください。

    * **「From a new search」**をクリックします。
    * **「From a saved search」**をクリックします。 
  
5. 照会を構成します。

    * **「From a saved search」**を選択した場合、検索照会を選択します。照会は、視覚化に使用されるデータを取得するために使用されます。 

        検索を選択すると、視覚化ビルダーが開き、選択した照会のデータがロードされます。「*This visualization is linked to a saved search: your_search_name*」というメッセージが表示されます。 
	
	**注**: 保存済み検索に行った変更はすべて、視覚化で自動的に反映されます。この視覚化にリンクされた照会に行われる自動更新を無効にするには、「*This visualization is linked to a saved search: your_search_name*」というメッセージをダブルクリックします。 

    * **「From a new search」**を選択した場合、新規照会を定義します。照会は、視覚化で取得および使用されるデータのサブセットを定義するために使用されます。

        詳しくは、『[カスタム検索照会の定義によるログのフィルタリング](k4_filter_queries.html#k4_filter_queries)』を参照してください。

6. 視覚化ビルダーで、Y 軸のメトリック集約を選択します。

7. 視覚化ビルダーで、バケット・タイプを選択します。次に、1 つのバケット集約を選択します。
  
8. データを分解するためのサブバケットを追加します。

Kibana について詳しくは、「[Kibana User Guide ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}」を参照してください。
 
## 視覚化の保存
{:#logging_kibana_visualizations_save}

「Visualize」ページで視覚化を保存するには、以下のステップを実行します。

1. 「Visualize」ページのツールバーで、**「Save Visualization」**ボタン ![視覚化の保存](images/k4_visualization_save_icon.jpg "視覚化の保存") をクリックします。

2. 視覚化の名前を入力します。

3. 「保存」をクリックします。 

## 視覚化のロード
{:#logging_kibana_visualizations_reload}

保存済み視覚化をロードするには、以下のステップを実行します。

1. 「Visualize」ページのツールバーで**「Load Saved Visualization」**ボタン ![保存済み視覚化のロード](images/k4_visualization_open_icon.jpg "保存済み視覚化のロード") をクリックします。

2. ロードする視覚化を選択します。 



## 視覚化の削除
{:#logging_kibana_visualizations_delete}

視覚化を削除するには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Visualizations」**タブで、削除する視覚化を選択します。

3. **「削除」**をクリックします。


## 視覚化のエクスポート
{:#logging_kibana_visualizations_export}

視覚化を JSON ファイルとしてエクスポートするには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Visualizations」**タブで、エクスポートする視覚化を選択します。

3. **「エクスポート」**をクリックします。

4. ファイルを保存します。

## 視覚化のインポート
{:#logging_kibana_visualizations_import}

視覚化を JSON ファイルとしてインポートするには、「Settings」ページで以下のステップを実行します。

1. 「Settings」ページで**「Objects」**タブを選択します。

2. **「Visualizations」**タブで**「Import」**を選択します。

3. ファイルを選択し、**「Open」**をクリックします。

視覚化が視覚化のリストに追加されます。


## 視覚化の共有
{:#logging_kibana_visualizations_share}

「Visualize」ページで視覚化を共有するには、以下のステップを実行します。

1. 「Visualize」ページのツールバーで、**「Share Visualization」**ボタン ![視覚化の共有](images/k4_visualization_share_icon.jpg "視覚化の共有") をクリックします。

2. 次のアクションのいずれかを選択してください。

    * **Embed this visualization**: HTML ソースで視覚化を共有する場合は、このオプションを選択します。 
    
        コピー・ボタン ![クリップボードにコピー](images/k4_copy_to_clipboard.jpg "クリップボードにコピー") をクリックして、HTML ソースで視覚化を埋め込むために使用できる HTML コードをコピーします。 
	
	**注**: 視覚化を表示するには、ユーザーは Kibana にアクセスできなければなりません。
	
    * **Share a link**: Kibana の視覚化を他のユーザーと共有する場合は、このオプションを選択します。



