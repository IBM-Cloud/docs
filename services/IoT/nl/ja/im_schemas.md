---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-03"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# デバイス・タイプ・スキーマの作成
{: #iotrtinsights_task}

ルールやアクションなどの {{site.data.keyword.iot_short}} 機能を使用する場合は、デバイス・プロパティーを分かりやすいプロパティー名にマップするためのスキーマを作成し、プロパティーのデータ単位を設定し、スキーマで使用するメッセージ・タイプを指定する必要があります。
{: shortdesc}

**重要:** ルールやアクションを使用するにはスキーマが必要です。詳しくは、[クラウド分析](cloud_analytics.html#rules)を参照してください。

**重要:** 分析機能は、{{site.data.keyword.iotrtinsights_full}} サービスからマージされます。既存の {{site.data.keyword.iotrtinsights_short}} インスタンスのデータ・ソースとして {{site.data.keyword.iot_short_notm}} 組織を使用する場合は、既存の {{site.data.keyword.iotrtinsights_short}} インスタンスのマイグレーションが完了するまでクラウド分析とエッジ分析が有効になりません。マイグレーションが完了するまでは、引き続き {{site.data.keyword.iotrtinsights_short}} ダッシュボードを使用して分析要件に対応してください。詳しくは、IBM developerWorks にある [IBM Watson IoT Platform のブログ ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} や既存の {{site.data.keyword.iotrtinsights_short}} インスタンス・ダッシュボードをご覧ください。  

## デバイス・スキーマの追加
{: #add_schema}

スキーマを追加するには、以下のようにします。  
1. **「デバイス」>「スキーマの管理」**に移動し、**「スキーマの追加」**をクリックします。  
2. このメッセージ・スキーマに関連付けるデバイス・タイプを選択します。**重要:** 1 つのデバイス・タイプにつき 1 つのスキーマだけを定義できます。

3. 1 つ以上のプロパティーを追加します。
      
接続先のデバイスからプロパティーを選択することも、既存のプロパティーを変更したり組み合わせたりする仮想プロパティーを作成することも、プロパティーを手動で追加することもできます。  

    **ヒント:** 使用可能なプロパティーは、デバイスから送信されるメッセージのペイロードで定義されています。{{site.data.keyword.iot_short}} のペイロードの形式の詳細については、[メッセージ・ペイロード](reference/mqtt/index.html#message-payloadl "メッセージ・ペイロード")のトピックを参照してください。   
  <dl>
  <dt>プロパティーを手動で追加する場合</dt>
  <p><b>ヒント:</b> プロパティーのネスト構造を作成する場合は、まずデータ・タイプ Parent のプロパティーを追加します。プロパティー表で、![「子の追加」アイコン](images/add_child.png "子の追加")をクリックして、1 つ以上の子プロパティーを追加できます。</p>
  <dd>
  <ol>
    <li>**「手動」**タブを選択します。</li>
    <li>プロパティーの詳細を以下のように定義します。
    <ul>  
      <li>名前 - {{site.data.keyword.iot_short}} のダッシュボードやメニューやウィザードで使用するプロパティーの記述名。</li>
      <li>データ・タイプ - プロパティーのデータ・タイプ。  
   `String`、`Integer`、`Float`、`Parent` のいずれか。</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>プロパティー - プロパティー ID。以下に例を示します。  
 `temp` または `speed`  </br> デバイス・メッセージからプロパティーを識別する方法については、[デバイスのプロパティーの識別](#identify-datapoints "プロパティーの確認")を参照してください。</li>
  <li>データ単位 - オプション: プロパティーのデータ単位。以下に例を示します。  
     `C` または `Mph`  </li>
     <li> 小数点以下の桁数 - オプション、Float のみ: デバイス・データに組み込む小数点以下の桁数。</li>
    </ul>
    </li>
    <li>**「完了」**をクリックして、プロパティーを作成します。</li>
  </ol>
  </dd>
  <dt>仮想プロパティーを作成する場合</dt>
  <dd> 例えば、デバイス・プロパティー temp から返される華氏の温度の値を摂氏に変換する場合は、*temp_c=(temp-32)/1.8* という関数を組み込んだ仮想プロパティー *temp_c* を作成できます。その後、ルール条件で、リアルタイム・プロパティー *temp* の代わりに仮想プロパティー *temp_c* を使用できます。  
  仮想プロパティーを作成するには、以下のようにします。
  <ol>
    <li>**「仮想プロパティー」**タブを選択します。</li>  
    <li>プロパティーの詳細を以下のように定義します。
    <ul>
    <li>名前 - {{site.data.keyword.iot_short}} のダッシュボードやメニューやウィザードで使用するプロパティーの記述名。</li>
    <li>データ・タイプ - プロパティーのデータ・タイプ。  
 `Float` または `Integer`。</li>
 <li>プロパティー - 仮想プロパティーのプロパティー ID。以下に例を示します。  
`temp_virt`</li>
    <li>計算 - 有効な関数を定義するために 1 つ以上の構成要素を追加します。プロパティー、数値、演算子 (+、-、\*、/、(、) など) を使用できます。  
エッジ・デバイスの一連のデータ・ポイントで使用する数式セットの**「詳細」**をクリックしてください。高度な数式の詳細については、[エッジ仮想プロパティーの高度な計算](im_vir_calculations.html)を参照してください。  
    **重要:** 高度な数式に基づいて仮想プロパティーを比較するルール条件は使用できません。</li>
    <li>データ単位 - オプション: プロパティーのデータ単位。例えば、`C` または `Mph` です。</li>
    <li> 小数点以下の桁数 - オプション、Float のみ: デバイス・データに組み込む小数点以下の桁数。</li>
   </ul>
   </li>
   <li>**「完了」**をクリックして、プロパティーを作成します。</li>
  </ol>
  </dd>
  <dt>接続先のデバイスからプロパティーを選択する場合</dt>
  <dd>
  <ol>
    <li>**「接続先から」**タブを選択します。</li>  
    <li>スキーマに追加する 1 つ以上のプロパティーを選択します。これらのプロパティーをあとで編集して、名前やデータ単位などの属性を設定できます。  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>**「OK」**をクリックして、プロパティーを作成します。</li>
  </ol>
  </dd>
    <dd>選択したプロパティーが追加され、説明がプロパティーの名前に設定されます。リスト内のプロパティーをクリックすれば、そのプロパティーを編集して、センサー・タイプ、データ・タイプ、小数点以下の桁数などの属性をさらに追加できます。</dd>
  </dl>
8. **「完了」**をクリックして、メッセージ・スキーマを作成します。

## デバイスのプロパティーの識別
{: #identify-datapoints}
デバイスのプロパティーは、{{site.data.keyword.iot_short}} ダッシュボードで確認できます。

1. {{site.data.keyword.iot_short}} ダッシュボードで**「デバイス」**に移動します。
2. デバイスをクリックして、そのデバイスの詳細をまとめたページを開きます。
3. **「センサー情報」**セクションにスクロールダウンして、接続先のデバイスで使用できるプロパティーのリストを確認します。
