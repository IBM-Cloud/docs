---

copyright:

years: 2015, 2017

lastupdated: "2017-03-16"


---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# ゲートウェイの接続
{: #IoT_connectGateway}

ゲートウェイに接続されているデバイスからデータを受信する操作を開始するには、その前にゲートウェイを {{site.data.keyword.iot_full}} に接続する必要があります。ゲートウェイを {{site.data.keyword.iot_short_notm}} に接続することには、ゲートウェイのデバイス・タイプを作成し、ゲートウェイを {{site.data.keyword.iot_short_notm}} に登録することが関係します。その後、登録情報を使用して、ゲートウェイを {{site.data.keyword.iot_short_notm}} に接続することができます。
{:shortdesc}

ゲートウェイは、{{site.data.keyword.iot_short_notm}} でのデバイスの特殊なクラスです。ゲートウェイは、他のデバイスの {{site.data.keyword.iot_short_notm}} へのアクセス・ポイントとして機能します。


## 始めに
{: #Prerequisites}

ゲートウェイ・デバイスには通常のデバイスより多くの許可があり、以下の機能を実行することができます。
- {{site.data.keyword.iot_short_notm}} への新規デバイスの登録
- 直接接続されているデバイスのような独自のセンサー・データの送受信
- 接続されたデバイスのデータの代行送受信
- 管理可能にするためのデバイス管理エージェントの実行。これによって、接続されたデバイスも管理可能にします。
  
ゲートウェイの開発者情報については、[ゲートウェイの MQTT 接続](mqtt.html)を参照してください。

ゲートウェイを使用して、ゲートウェイ・デバイスが送信しているデータに対してエッジ分析を実行することもできます。詳しくは、[エッジ分析](../edge_analytics.html)と[エッジ分析エージェントのインストール](#edge)を参照してください。

## ステップ 1: {{site.data.keyword.iot_short_notm}} へのゲートウェイの登録  
{: #register_gateway}

ゲートウェイの登録には、ゲートウェイ・タイプとしてデバイスを分類すること、ゲートウェイに名前を付けること、ゲートウェイ情報を提供することが含まれています。その後、接続トークンを指定するか、{{site.data.keyword.iot_short_notm}} によって生成されるトークンを受け入れます。


**ヒント:** {{site.data.keyword.iot_short_notm}} ダッシュボードから一度に 1 つずつゲートウェイを追加するか、[組織管理 API ![外部リンク・アイコン](../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/orgAdmin.html#!/Device_Bulk_Configuration/post_bulk_devices_add){: new_window} を使用して一度に 1 つ以上のゲートウェイを追加することができます。

{{site.data.keyword.iot_short_notm}} ダッシュボードからゲートウェイを追加するには、以下のようにします。

1. {{site.data.keyword.iot_short_notm}} ダッシュボードで、**「デバイス」**を選択します。
2. **「デバイスの追加」**をクリックします。
3. 追加するデバイスのデバイス・タイプを選択するか作成します。
  
{{site.data.keyword.iot_short_notm}} に接続する各デバイスには、デバイス・タイプを関連付ける必要があります。デバイス・タイプとは、共通の特性を共有するデバイス・グループのことです。  
 1. **「デバイス・タイプの作成」**、**「ゲートウェイ・タイプの作成」**の順にクリックします。
 2. デバイス・タイプ名 (`my_gateway_type` など) とそのゲートウェイ・タイプの説明を入力します。
   
 **重要:** デバイス・タイプ名は 36 文字以下でなければなりません。以下の文字だけを含めることができます。
 <ul>
  <li>英数字 (a-z、A-Z、0-9)</li>
  <li>ハイフン (-)</li>
  <li>下線 (&lowbar;)</li>
  <li>ピリオド (.)</li>
  </ul>3. オプション: ゲートウェイ・タイプの属性やメタデータを入力します。    
 **ヒント:** 属性とメタデータは、後で追加したり編集したりすることもできます。 4. **「作成」**をクリックして、新しいゲートウェイ・タイプを追加します。
10. **「次へ」**をクリックして、選択したゲートウェイ・タイプのゲートウェイ・デバイスを追加するプロセスを開始します。
11. `my_gateway_device` などのデバイス ID を入力します。
  
デバイス ID は、{{site.data.keyword.iot_short_notm}} ダッシュボードでゲートウェイ・デバイスを識別するために使用され、ゲートウェイ・デバイスを {{site.data.keyword.iot_short_notm}} に接続するための必須パラメーターでもあります。  
**重要:** デバイス ID は 36 文字以下でなければなりません。以下の文字だけを含めることができます。
 <ul>
 <li>英数字 (a-z、A-Z、0-9)</li>
 <li>ハイフン (-)</li>
 <li>下線 (&lowbar;)</li>
 <li>ピリオド (.)</li>  
 </ul>
 **ヒント:** ネットワークに接続されたデバイスの場合は、デバイス MAC アドレス (区切り文字のコロンは付けない) などをデバイス ID として入力できます。  
12. オプション: **「追加フィールド」**をクリックして、シリアル番号、製造元、型式などのゲートウェイ・デバイス情報を追加します。
   
 **ヒント:** この情報は、後で追加したり編集したりすることもできます。
12. オプション: デバイスの JSON メタデータを入力します。
   
 **ヒント:** デバイスのメタデータは、後で追加したり編集したりすることもできます。
13. **「次へ」**をクリックして、ゲートウェイ・デバイスの追加を完了します。
14. 要約情報が正しいことを確認してから、**「追加」**をクリックしてゲートウェイ・デバイスを追加します。
  
**ヒント:** 自動生成の認証トークンを受け入れることも、自分で認証トークンを指定することもできます。自分でトークンを作成する場合は、長さを 8 文字から 36 文字にして、小文字と大文字、数字、記号 (ハイフン、下線、ピリオドのいずれか) を組み合わせる必要があります。反復した文字シーケンスや、辞書に出てくる単語やユーザー名などの事前定義シーケンスをトークンに含めないでください。
15. デバイス情報のページで、以下のデバイス情報をコピーして保存します。  
 - 組織 ID (`tubo8x` など)
 - デバイス・タイプ (`my_gateway_type` など)
 - デバイス ID。**ヒント:** ネットワーク接続のデバイスの場合は、区切り文字のコロンを使用しない MAC アドレスなどになることもあります。
 - 認証方式 (`token` など)
 - 認証トークン (`PtBVriRqIg4uh)_-Kl` など)  
  **ヒント:** {{site.data.keyword.iot_short_notm}} へのデバイスの接続を構成するときに、組織 ID、認証トークン、デバイス・タイプ、デバイス ID が必要になります。  

これで、ゲートウェイ・デバイスを登録できました。次に、ゲートウェイ・デバイスから {{site.data.keyword.iot_short_notm}} に接続するための構成を行います。

ゲートウェイの登録に必要なフローが示されている、詳細な手順については、[How to Register Gateways in IBM Watson IoT Platform ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/how-to-register-gateways-in-ibm-watson-iot-platform/){:new_window} レシピを参照してください。

## 手順 2: ゲートウェイを {{site.data.keyword.iot_short_notm}} に接続する
{: #connect_gateway}

ゲートウェイを {{site.data.keyword.iot_short_notm}} に登録したら、登録情報を使用してゲートウェイを {{site.data.keyword.iot_short_notm}} に接続し、ゲートウェイに接続されているデバイスからのデータの受信を開始します。

{{site.data.keyword.iot_short_notm}} へのゲートウェイの接続について詳しくは、[ゲートウェイの MQTT 接続](mqtt.html)を参照してください。

**ヒント:** {{site.data.keyword.iot_short_notm}} へのデバイスの接続では、一連のレシピを使用できます。レシピのリストについては、IBM.com の[デバイス接続のレシピ ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/category/internet-of-things-iot/){:new_window} を参照してください。


## ステップ 3: ゲートウェイを介したデバイスの接続
{: #gateway_devices}

ゲートウェイに接続されているデバイスは、ゲートウェイがデバイスからメッセージを発行するときに自動的に追加される {{site.data.keyword.iot_short_notm}} です。デバイス・タイプとデバイス自体のどちらも、まだ存在していないデバイス・タイプとデバイス ID の組み合わせのメッセージをゲートウェイが発行するときに自動的に作成されます。

デバイスの自動登録、接続されたデバイスのデータの発行と受信については、[ゲートウェイの MQTT 接続](mqtt.html)を参照してください。


デバイスがゲートウェイに正常に接続されると、{{site.data.keyword.iot_short_notm}} 組織のダッシュボードに表示されます。

詳しいフローと説明については、レシピ [Connecting Raspberry Pi as a Gateway to Watson IoT ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/connecting-raspberry-pi-as-a-gateway-to-watson-iot-using-node-red/){:new_window} を参照してください。

**注:** {{site.data.keyword.iot_short_notm}} ダッシュボード、デバイス、ゲートウェイが {{site.data.keyword.iot_short_notm}} に直接接続されている場合、接続されていることを示す状況アイコンが表示されます。ゲートウェイに対するデバイス接続は認識されないため、ゲートウェイを介して間接的に接続されているデバイスは、切断されているものとしてダッシュボードに表示されます。


## エッジ分析エージェントのインストール
{: #edge}

エッジ分析エージェント (EAA) は、エッジ処理用に最適化されたストリーミング・エンジン上に構築されるソフトウェア・コンポーネントです。これを使用して、{{site.data.keyword.iot_short_notm}} ダッシュボードからエッジ分析ルールをアップロード/管理することにより、ゲートウェイに対してエッジ分析操作を実行します。エッジ分析について詳しくは、[エッジ分析](../edge_analytics.html)を参照してください。

### EAA のインストール
{: #eaa_install}

ゲートウェイに EAA をインストールするには、次のようにします。
1. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」**に移動します。
2. **「エッジ・エージェントのダウンロード」**をクリックして、[IBM エッジ分析のコミュニティー ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://www.ibm.com/developerworks/community/groups/service/html/communitystart?communityUuid=3df173af-0c21-4b9c-9fd1-e8e5561ef460&ftHelpTip=true){:new_window} に移動します。
3. **「ファイル」**セクションに移動し、ゲートウェイのタイプに該当する圧縮ディレクトリーをダウンロードします。  
エッジ分析ソリューションは、Java をサポートしているデバイスの場合は SDK、Cisco ゲートウェイ・デバイスの場合は DSLink として入手可能です。
4. EAA ソフトウェア・コンポーネントをゲートウェイにインストールして構成する方法については、以下の情報を参照してください。
 - SDK  
コミュニティーで使用可能な PDF ファイル、README ファイル、ビデオのリンクを参照してください。  
 [SDK でのエッジのレシピ - 概説 (SDK) ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/tutorials/getting-started-with-the-ibm-edge-analytics-sdk-in-watson-iot-platform/){:new_window} レシピ。
 - DSLink  
 [Watson IoT Platform でのエッジ分析の概説 ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](https://developer.ibm.com/recipes/?post_type=pnext_tutorial&p=19472){:new_window} レシピ。

### EAA 構成の設定
{: #eaa_configuration}

EAA config.properties ファイルを使用して、基本ソフトウェア構成パラメーターを設定することができます。

EAA 構成を更新するには、次のようにします。
1. EAA が実行されているゲートウェイ・システムで、EAA config.properties ファイルを見つけます。  
例えば、`../dglux-server/dslinks/ibm-watson-iot-edge-analytics-dslink-java-0.0.1/config.properties` です。
2. 設定の編集を開始する前に、ファイルのバックアップ・コピーを作成しておきます。
3. 編集のために config.properties ファイルを開きます。
4. 環境に合わせて構成パラメーターを編集します。
 <dl>
 <dt>DataDirectSendEnable</dt>
 <dd>BOOLEAN (true|false)</br>
 TRUE (デフォルト) - すべてのデータを {{site.data.keyword.iot_short_notm}} に送信します。</br>
 FALSE - ルールがエンジンで設定されている場合にのみ、データを {{site.data.keyword.iot_short_notm}} に送信します。</dd>
 <dt>MonitorInterval</dt>
 <dd>INTEGER (ミリ秒)</br>
 新しいモニター・メッセージが {{site.data.keyword.iot_short_notm}} に送信されるまでの時間 (ミリ秒)。</br>
 モニター・メトリックの報告の頻度を増やす場合は、小さな値を設定します。{{site.data.keyword.iot_short_notm}} に関して、より詳しいモニター情報が必要な場合は、大きい値を設定します。</br>
 デフォルト: 60000    </br>
 推奨範囲: [1000, 360000]</dd>
 <dt>MonitorLogDesample</dt>
 <dd>INTEGER  </br>
ローカル・ログに入るメッセージに対する、{{site.data.keyword.iot_short_notm}} に送信されるモニター・メッセージの数の間の De-sampling 率。例えば、`MonitorLogDesample` が 10 に設定されている場合、{{site.data.keyword.iot_short_notm}} に送信される 10 個のメッセージごとに 1 つのローカル・ログ項目だけが書き込まれます。</br>大きな数値を設定すると、ローカル・ログは小さく保たれます。小さな数値を設定すると、より詳細なローカル・ログが提供されます。</br>
 デフォルト: 10</br>
 推奨範囲: [1, 100]</dd>
 <dt>MemoryAlertThreshold</dt>
 <dd>INTEGER (M バイト)</br>
 メモリー警告ログ・メッセージが {{site.data.keyword.iot_short_notm}} 診断ログに送信されるときの空き JVM ヒープ・メモリーのしきい値。アラートは、モニタリングに基づいて出されます。</br>小さな値を指定すると、{{site.data.keyword.iot_short_notm}} に送信されるアラート・メッセージの数が減ります。大きな値を指定すると、EAA サーバーでメモリーの問題が発生したときに、より早く警告が出されます。</br>**ヒント:** [クラウド分析](../cloud_analytics.html)ルールを使用して、アラート・アクションを構成できます。例えば、E メール通知によって、メモリーの問題のアラートを出すことができます。ルールを作成するために使用できる使用可能なプロパティーについて詳しくは、[エッジ分析エージェントの診断メトリック](../edge_analytics.html#eaa_metrics)を参照してください。</br>
 デフォルト: 10</br>
 推奨範囲: [10 または合計メモリーの 5%, 200]</dd>
 </dl>
5. 編集したファイルを保存し、EAA を再始動します。

EAA config.properties のサンプル・ファイル
```
#######################################################################
# エンジンのパラメーター
#######################################################################
# DataDirectSendEnable
#                    - BOOLEAN(true|false)。すべてのデータを転送する場合
#                      は true に設定します。エンジンでルールが設定され
#                      ていないときに IOTP へのデータの直接送信を無効に
#                      する場合は false に設定します。
#                      デフォルト: true
#######################################################################
DataDirectSendEnable=true

#######################################################################
# モニター・パラメーター
#######################################################################
# MonitorInterval    - INTEGER。新しいモニター・メッセージが生成される
#                      までの時間間隔 (ミリ秒)。モニター・メトリックを
#                      より頻繁に報告する場合は、小さな値に設定します。
#                       IoTP で、より詳細なモニター情報を得るには、
#                      大きな値に設定します。
#                      デフォルト: 60000    推奨: [1000, 360000]
# MonitorLogDesample - INTEGER。ローカル・ログに入るメッセージに対する、
#                      IOTP に送信されるモニター・メッセージの数の
#                      de-sampling 率。つまり、EAA が N 個のメッセージ
#                      ごとに 1 個だけ情報ログに出力する場合の、
#                      モニター・メッセージ N の数値。ログのサイズを
#                      小さくするには、大きい値に設定します。小さくする
#                      と詳細なモニター情報がローカル・ログに入ります。
#                      デフォルト: 10       推奨: [1, 100]
# MemoryAlertThreshold
#                    - INTEGER。ログ・メッセージが生成されて IOTP 診断
#                      ログに送信する際の、空き JVM ヒープ・メモリー
#                      (M バイト)。アラートは、モニタリングに基づいて
#                      出されます。IoTP で不要なアラート・メッセージを
#                      除外する場合は、小さい値を設定します。システム
#                      でのクラッシュの可能性があるときに、早くアラート
#                      を受け取る場合は、大きい値を設定します。
#                      Min(Max(10MB, 合計メモリーの 5%), 200MB) への
#                      設定が推奨されています。
#                      デフォルト: 10       推奨: [10, 200]
#######################################################################

MonitorInterval=60000
MonitorLogDesample=10
MemoryAlertThreshold=10
```
