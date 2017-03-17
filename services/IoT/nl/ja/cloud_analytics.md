---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# クラウド分析
{: #cloud_analytics}

{{site.data.keyword.iot_short}} クラウド分析を使用することによって、リアルタイムのデバイス・データに基づいて、条件を満たした場合にアラートやオプションのアクションを起動するルール条件を指定できます。    
{: shortdesc}

例えば、1 つのルールを作成し、その中で、デバイスが除去された場合やデバイスの温度が急上昇した場合に、アラートをユーザーのデバイス上のダッシュボードに送信し、E メールを管理者に送信するように指定することもできます。

## 始めに
{: #byb}
ルールで条件として使用するデバイス・プロパティーがスキーマにマップされていることを確認します。詳しくは、[デバイスの接続](iotplatform_task.html)と[スキーマの作成](im_schemas.html)を参照してください。

また、[Using Rules and Actions with {{site.data.keyword.iot_short}} Cloud Analytics ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/using-rules-and-actions-with-ibm-watson-iot-platform-cloud-analytics/){: new_window} レシピを参照し、クラウド分析で使用するルールとアクションについて理解してください。

## ルールとアクションの管理  
{: #managing_rules}

組織用にルールとアクションを作成して管理するには、**「ルール」**ダッシュボードを使用します。

デバイス用にトリガーされたルールとアラートの概説を入手するには、以下のボードを使用します。

 |ボード名 | 説明 |  
 |:---|:---|  
  |ルール中心型の分析 | 組織のルールを表示します。追加のカードに、トリガーされたアラート、関連デバイス、デバイス・プロパティー、アラート情報がリスト表示されます。 |  
 |デバイス中心型の分析 | 組織に接続されているデバイスを表示します。追加のカードに、選択されたデバイスのアラート、選択されたデバイスの情報、デバイス・プロパティー、アラート情報がリスト表示されます。 |

 デフォルトの分析ボートについて詳しくは、[ボードとカードを使用したリアルタイム・データの視覚化](data_visualization.html#default_boards)を参照してください。


## ルールの作成
{: #rules}

ルールは、リアルタイム・デバイス・データを事前定義しきい値または他のプロパティー・データと突き合わせる条件に基づく決定点です。条件が満たされた場合に、アラートがトリガーされます。{{site.data.keyword.iot_short}} ダッシュボードに表示されるアラートに加えて、ルールがトリガーされた場合にビジネス・ロジックを実行する 1 つ以上のアクションを追加できます。

**重要:** デバイス・タイプのルールを作成するには、事前にデバイス・タイプのスキーマを作成しておく必要があります。詳しくは、[デバイス・タイプ・スキーマの作成](im_schemas.html)を参照してください。

ルールを作成するには、次のようにします。
1. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」**に移動します。
2. **「ルールの作成 (Create A Rule)」**をクリックし、ルールに名前を付け、説明を入力し、ルールを適用するデバイス・タイプを選択してから、**「次へ」**をクリックします。  
3. ルール・ロジックを設定するために、ルールのトリガーとして使用する 1 つ以上の IF 条件を追加します。
  
並列行に条件を追加して OR 条件として適用したり、順次列に条件を追加して AND 条件として適用したりすることもできます。
  
**重要:** 2 つのプロパティーを比較する条件をトリガーしたり、AND を使用して順次に結合された 2 つ以上のプロパティー条件をトリガーしたりする場合は、トリガーするデータ・ポイントを同じデバイス・メッセージに含める必要があります。複数のメッセージでデータを受け取った場合、条件または順次条件はトリガーしません。
  
**例:**  
パラメーター値が 1 つの指定値を上回った場合にアラートをトリガーする場合、ルールは単純です。
Condition = `temp_cpu>80`  
しきい値の組み合わせが満たされたときにトリガーする場合、ルールはもう少し複雑になります。
Condition = `temp_cpu>60 AND cpu_load>90`   

4. ルールに対して条件付きトリガー要件を構成します。
  
一定期間にわたってあるルールでトリガーされるアラートの数を制御する場合、ルールに対して条件付きトリガー要件を構成できます。  
**重要:**  条件付きトリガーは、ルール内のどの条件に対しても作用します。例えば、1 つのルールに OR を使用して設定された 5 つの異なる並列条件が含まれる場合、満たされる各条件は条件付きトリガー・カウントに加算されます。
ルールに対して条件付きトリガーを設定するには、次のようにします。
 1. ルール・エディターで、デフォルトの**「条件が満たされるたびにトリガーする (Trigger each time conditions are met)」**リンクをクリックし、「頻度要件の設定 (set frequency requirement)」ダイアログ・ボックスを開きます。
 2. ルールで使用する条件付きトリガーを選択して構成します。
 <ul>
 <li>条件が満たされるたびにトリガーします。</li>
 <li>条件が M *時間単位*内に N 回満たされたらトリガーします。</li>
 </ul>  
条件付きトリガーについて詳しくは、[条件付きルールのトリガー](#conditional "条件付きトリガーの概要")を参照してください。
5. ルールの条件が満たされた場合に発生する 1 つ以上のアクションを作成または選択します。
  
アクションについて詳しくは、[ルールでのアクションの使用](#shared "アクションの作成")を参照してください。
    
例として、E メールの送信や、Webhook への通知といったアクションが考えられます。
3. **オプション:** ルールのアラートの優先順位を選択します。
  
優先順位は、**「ルール・ベースの分析 (Rule-Based Analytics)」**ボードに表示されるアラートを分類するために使用されます。デフォルトの優先順位は「低 (Low)」です。
6. ルールが完成した後、アクティブ化せずに保存するには**「保存」**をクリックし、ルールを保存してアクティブにするには**「アクティブ化 (Activate)」**をクリックします。

これで、ルールが作成されました。ルールをアクティブにした場合にルールの条件が満たされると、アラートが**「ボード (Boards)」>「ルール・ベースの分析 (Rule-Based Analytics)」**ボードに追加され、該当するルール・アクションが実行されます。

## 条件付きルールのトリガー
{: #conditional}

一定期間にわたってあるルールでトリガーされるアラートの数を制御する場合、ルールに対して条件付きトリガー要件を構成できます。

メッセージの頻度やルール条件によっては、トリガー条件が満たされた場合にルールがトリガーする回数が非常に多くなることがあります。例えば、条件が `temp >= 90` であり、温度が上昇し、91 度で安定した場合、ルールは着信メッセージのたびにトリガーされます。ルールを実行するよう設定されているデバイス・メッセージの頻度やアクションによっては、このアラート数によって E メールの受信ボックスがすぐにいっぱいになったり、Twitter フィードがほとんど意味のないメッセージであふれてしまったりすることがあります。

**重要:** 条件付きトリガーは、ルール内のどの条件に対しても作用します。例えば、1 つのルールに OR を使用して設定された 5 つの異なる並列条件が含まれる場合、満たされる各条件は条件付きトリガー・カウントに加算されます。

条件 | 説明
------------- | -------------
条件が満たされるたびにトリガーします。 | ルール条件が満たされるたびにルールがトリガーされます。
条件が *M* *日/時間/分/カスタム*内に *N* 回満たされるとトリガーします | 選択した時間間隔内に条件が *N* 回満たされた場合にルールがトリガーされ、構成された期間が経過するまで再びトリガーされることはありません。</br>例: 条件付きトリガー要件 = `30 分以内に 4 回条件が満たされた場合に 1 回だけトリガーする`。デバイスは 5 分ごとに 1 つの新規メッセージを送信します。正午に、温度が初めて 90 度を超え、条件が満たされます。条件付きトリガーのカウンターが開始されますが、ルールはまだトリガーされません。15 分が経過し、`temp > 90` を示すさらに 3 つのメッセージを受け取ると、ルールはトリガーされます。温度にかかわらず、ルールはその後の 15 分間はトリガーされません。
条件が初めて適合した場合にのみトリガーし、条件が適合しなくなったらリセットします。 | 条件が満たされるとルールはトリガーされますが、条件を満たす連続メッセージに対してはトリガーされません。トリガー基準は、ルール条件を満たさない最初のメッセージによってリセットされます。

*M* *日/時間/分/カスタム*の条件が続くとトリガーします | 選択した時間間隔中に受信したすべてのデータ・ポイントが条件を満たしている場合や、追加のデータ・ポイントを受信していない場合は、その時間間隔の後に規則がトリガーされます。時間間隔は、条件が最初に満たされた時点で開始します。



## ルールでのアクションの使用
{: #shared}

{{site.data.keyword.iot_short}} は、アラート・ダッシュボードにアラートを表示するだけでなく、E メールの送信や Webhook への通知など、いくつかのタイプのルール・トリガーのアクションをサポートします。

ルール・エディターで直接アクションを作成するか「アクション」タブでアクションを作成し、ルールを作成するときにアクションを選択することができます。

「アクション」タブでアクションを作成するには、次のようにします。
1. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」**に移動します。
2. 「ルール」ダッシュボードで、**「アクション」**タブを選択します。
2. **「アクションの作成 (Create An Action)」**をクリックし、アクションに名前と説明を付け、アクション・タイプを選択し、**「次へ」**をクリックします。
3. 作成するアクションのタイプに必須パラメーターを指定します。
  
アクションのタイプ:  
 - [E メールの送信](#email "E メールの送信")
 - [IFTTT](#ifttt "IFTTT")
 - [Node-RED](#nodered "Node-RED")
 - [Webhook](#webhook "Webhook")
4. **「OK」**をクリックして、新規アクションを作成します。

アクションがルール・エディターで使用できるようになります。

**注:** 以下のサンプルはすべて、ルール条件 `temp_cpu >= 80` を使用して、デバイスの `temp_cpu` プロパティーによって表される温度が 80 度を超えたときにサービス・エンジニアに通知するアクションを示しています。

### E メールの送信  
{: #email}
E メールの送信アクションを使用して、ルールがトリガーされたときに 1 人以上の受信者に E メールを送信します。

例: [E メールを送信します](#emailex)。

以下のパラメーターは E メールの送信アクションを構成する場合に使用します。

パラメーター | 説明
---|---
名前 | アラート・ダッシュボードで使用されるアクションの名前。
説明 | アクションの簡単な説明。
件名 | E メールの件名行。デフォルトの件名行は、「IBM Watson IoT Alert: Mail action」です。
宛先 | これを選択して、自分自身または E メール・アドレスのコンマ区切りリストにアラートを送信します。自分に送信することを選択した場合、E メールは、ログインした {{site.data.keyword.iot_short}} の E メール・アドレスに送信されます。
Cc | なし、または E メール・アドレスのコンマ区切りリスト。
E メールの本文は、ルールがトリガーされた時点で、デバイスのメッセージから自動的に作成されます。  
**重要:** デフォルトで、機密情報が入っている可能性があるデバイス・データは E メールには含まれません。**「データを含める (Include Data)」**設定を変更して、デバイス・データを含めます。

#### 例: E メールの送信の使用
{: #emailex}

この例では、E メールの送信機能を使用して E メールをメインのサービス・エンジニアに送信し、バックアップ E メールをマネージャーにも送信するよう、アクションが構成されています。

E メール・アクションを作成するには次のようにします。
1. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」**に移動します。
2. **「アクションの作成 (Create An Action)」**をクリックします。
4. アクション名として `Send service request email` と入力します。
5. 説明として `Send an email to the service engineer and his manager` と入力します。
3. **「E メール」** タイプを選択します。
6. 「宛先」フィールドで、**「特定の人 (Specific people)」**を選択し、`service.engineer@company.com` と入力します。
7. 「CC」フィールドで、**「特定の人 (Specific people)」**を選択し、`service.manager@company.com` と入力します。
8. 件名行に `Service required` と入力します。
10. **「データを含める (Include Data)」**を選択して、E メールにデバイス・データを含めます。
11. **「完了」**をクリックして、アクションを保存します。  


### IFTTT  
{: #ifttt}

IFTTT アクションを使用して、ルールがトリガーされたときに IFTTT レシピをトリガーします。IFTTT レシピとしてアクションをトリガーする方法について詳しくは、IFTTT サイトの [Maker Channel ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://ifttt.com/maker){: new_window} を参照してください。

例: [IFTTT を使用して Trello カードを送付する](#iftttex)。

以下のパラメーターは IFTTT アクションを構成する場合に使用します。

パラメーター | 説明
---|---
名前 | アラート・ダッシュボードで使用されるアクションの名前。
説明 | アクションの簡単な説明。
キー  | イベントをトリガーするために使用する Maker Channel キー。
イベント | Maker Event のトリガーとして構成したイベント名。さまざまなトリガーを使用して複数のレシピを作成し、それぞれに異なるイベント名を付けることができます。
値 1-3 | これらのパラメーターの任意のコンテンツを渡すことができます。それらのコンテンツは IFTTT レシピのアクションに渡されます。**ヒント:** [変数置換](#variable_substitution)を使用して、追加データを動的にヘッダーに含めることができます。

#### 例: IFTTT を使用して Trello カードを送付する{: #iftttex}

この例では、IFTTT を使用して Trello のサービス要求リストにカードを送付するようにアクションが構成されます。

Trello アクションでカードを送付するには次のようにします。
1.	IFTTT で、Trello チャネルに接続します。
2.	IFTTT で、Maker チャネルに接続します。IFTTT キーをメモします。{{site.data.keyword.iot_short_notm}} から IFTTT に接続する際にこのキーが必要です。
5.	IFTTT で、次のようにレシピを作成します。
 1. **「THIS」**をクリックします。
 2. **「Maker」**チャネルを選択します。  
 2. **「Recieve a web request」**をクリックします。
 3. イベント名として `post-Trello-card` と入力します。
 4. **「THAT」**をクリックします。
 5. **「Trello」**チャネルを選択します。
 6. カードを作成する Trello ボードを選択します。
 7. カードを追加するリスト名を入力します。
 8. タイトルと説明を編集します。
 9. @service.engineer および @service.manager メンバーを割り当てます。
 8. **「Create Action」**をクリックします。   
3. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」>「アクション」**に進み、以下のパラメーターを持つ新規アクションを作成します。
<ul>
<li>タイプ - **IFTTT**</li>
<li>名前 - `Post service request card`</li>
<li>説明 - `IFTTT を使用して、Trello のサービス要求リストにカードを送付します。`</li>
<li>キー - IFTTT キー</li>
<li>イベント - `post-Trello-card`</li>
<li>オプションで、値 1 から 3 までの値を追加します。**ヒント:** [変数置換](#variable_substitution)を使用して、デバイス・データを動的に含めることができます。</li>
</ul>
4. **「OK」**をクリックしてアクションを保存します。


### Node-RED
{: #nodered}

Node-RED アクションを使用して、ルールがトリガーされたときに Node-RED アプリケーションに接続します。Node-RED の使用方法について詳しくは、[IoT スターター・アプリケーションによるアプリの作成](https://www.ng.bluemix.net/docs/starters/IoT/iot500.html)を参照してください。

例: [Node-RED を使用してテキスト・メッセージを送信します](#noderedex)。

以下のパラメーターは Node-RED アクションを構成する場合に使用します。

パラメーター | 説明
---|---
名前 | アラート・ダッシュボードで使用されるアクションの名前。
説明 | アクションの簡単な説明。
URL | ターゲット Node-RED HTTP 入力ノードの URL。
ユーザー名 | Node-RED サービスで必要とされる場合に含めます。
パスワード | Node-RED サービスで必要とされる場合に含めます。
**重要:** パスワードは平文で送信されます。
本文 | 本文フィールドはデフォルトで、[変数置換](#variable_substitution)にリストされているすべての変数で事前に定義されています。

#### 例: Node-RED を使用してテキスト・メッセージを送信する
{: #noderedex}

この例では、Twilio ノードを含む Node-RED を使用して、サービス・エンジニアにテキスト・メッセージを送信するようにアクションが構成されています。

テキスト・メッセージの送信アクションを作成するには次のようにします。
1. Twilio でメッセージング・サービスを見つけるか、または新規に作成して、テキスト・メッセージを Twilio アカウントから送信します。詳しくは、[Twilio の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://www.twilio.com/help){: new_window} を参照してください。
2. Bluemix で、Node-RED URL `http://mynodered.mybluemix.net/red/` を使用して Node-RED アカウントをセットアップしアクセスします。詳しくは、Bluemix 資料の [Node-RED Starter によるアプリの作成](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html)トピックを参照してください。
3. Node-RED で、簡単な 2 ノード・フロー ([RTI-alert]->[SMS] など) を作成します。
  
最初のノードが http ノードで、2 番目が twilio ノードです。
 1. 「http」入力ノードを追加し、以下の属性で構成します。
  <ul>
  <li>メソッド - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>名前 - RTI Action</li>
  </ul>
  2. 「http response」出力ノードを追加し、「http」入力ノードに接続します。この操作は、一方の出力ポートから他方の入力ポートにドラッグすることによって行います。
  3. 「twilio」出力ノードを追加し、以下の属性で構成します。
  <ul>
  <li>サービス - **External service**</li>
  <li>Twilio - twilio-api を新規追加</li>
  <li>SMS 宛先 - `サービス・エンジニアの電話番号`</li>
  <li>名前 - **SMS**</li>
  </ul>
  4. ノードをワイヤリングします。  
  HTTP ノードと Twilio ノードを接続します。接続するには、一方のノードの出力ポートを他方の入力ポートに差し込みます。
  5. **「Deploy」**ボタンをクリックしてフローをサーバーにデプロイします。
4. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」>「アクション」**に進み、以下のパラメーターを持つ新規アクションを作成します。
 - タイプ - **Node-RED**
 - 名前 - `Node-RED や Twilio を使用したテキストの送信`
 - 説明 - `テキスト・メッセージ・アラートをサービス・エンジニアに送信します。`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - BODY   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
5. **「完了」**をクリックして、アクションを保存します。



### Webhook
{: #webhook}

Webhook アクションを使用して、アラートがトリガーされたときに Webhook 対応の Web サービスに対して HTTP 要求を実行します。例えば、デバイスのセンサーによって異常な読み取りがレポートされた場合、Webhook を使用してアセットに対するサービス要求を開くことができます。

例: [Webhook を使用して Slack に通知する](#webhookex)。

以下のパラメーターは Webhook アクションを構成する場合に使用します。

パラメーター | 説明
---|---
名前 | アラート・ダッシュボードで使用されるアクションの名前。
説明 | アクションの簡単な説明。
URL | ターゲット Webhook 対応サーバーの URL。**ヒント:** [変数置換](#variable_substitution)を使用して、追加データを動的に URL に含めることができます。
メソッド | 実行する Webhook 呼び出しのタイプ。以下のいずれかのタイプを選択します: GET、HEAD、OPTIONS、PATCH、PUT、POST、または DELETE。
ユーザー名 | Web サービスで必要とされる場合に含めます。
パスワード | Web サービスで必要とされる場合に含めます。
**重要:** パスワードは平文で送信されます。
ヘッダー | ヘッダーはキーと値のペアで構成されます。**ヒント:** [変数置換](#variable_substitution)を使用して、追加データを動的にヘッダーに含めることができます。
コンテンツ・タイプ | 本文のコンテンツ・タイプ: JSON、XML、WWW フォーム URL エンコード、またはプレーン・テキスト。OPTIONS、PATCH、PUT、POST、DELETE メソッドで使用可能です。
本文 | Webhook 呼び出しの本文。OPTIONS、PATCH、PUT、POST、DELETE メソッドで使用可能です。本文フィールドはデフォルトで、[変数置換](#variable_substitution)にリストされているすべての変数で事前に定義されています。**重要:** Webhook サーバーでは特定のフィールドを本文に含めなければならない場合があります。例えば、Slack Webhook には "text" フィールドを含める必要があります。   

#### 例: Webhook を使用して Slack に通知する
{: #webhookex}

この例では、Webhook を使用して #service-requests Slack チャネルにメッセージを送付するようにアクションが構成されます。

Slack への通知アクションを作成するには次のようにします。
1. Slack で、チャネル #service-requests 用に Incoming Webhooks 統合をセットアップします。Webhooks URL をメモします。詳しくは、[Slack の資料 ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window} を参照してください。
2. {{site.data.keyword.iot_short}} ダッシュボードで、**「ルール」>「アクション」**に進み、以下のパラメーターを持つ新規アクションを作成します。
 - 名前 - `Post service request on Slack`
 - タイプ - **Webhook**
 - URL - `Slack Webhooks の URL`
 - メソッド - **POST**
 - コンテンツ・タイプ - `application/json`
 - 本文   
 ```json
 {"text":"*A device needs your attention*\n Time: {{timestamp}}\n {{site.data.keyword.iot_short}} instance: {{tenantId}}\n Device: {{deviceId}}\n Rule: {{ruleName}}\n Description: {{ruleDescription}}\n Condition: {{ruleCondition}}\n Raw device message: \n{{message}}"}
 ```  
  **重要:** Slack Webhook には少なくとも "text" フィールドを含める必要があります。詳しくは、Slack の資料の [Incoming Webhooks ![外部リンク・アイコン](../icons/launch-glyph.svg)](https://api.slack.com/incoming-webhooks){: new_window} を参照してください。
11. **「完了」**をクリックして、アクションを保存します。


### 変数置換  
{: #variable_substitution}

以下の変数置換を含めて、デバイス・データを動的に含めます。変数は二重中括弧で囲む必要があります。

変数 | 説明
---|---
**URL、ヘッド、本文** |
`{{timestamp}}` | メッセージのタイム・スタンプ。
`{{orgId}}` | {{site.data.keyword.iot_short_notm}} サービスの組織 ID。
`{{tenantId}}` | 非推奨: {{site.data.keyword.iotrtinsights_full}} サービスの ID。
`{{deviceId}}` | デバイスの ID。
`{{ruleName}}` | アクションを含むルールの名前。
`{{ruleID}}` | アクションを含むルールの ID。
**本文のみ** |
`{{ruleDescription}}`| アクションを含むルールの説明。
`{{ruleCondition}}` | アクションをトリガーしたルールの条件。
`{{message}}` | ルールをトリガーしたデータ・ポイント値を含むロー・デバイス・メッセージ。
## クラウド分析に関するレシピ

以下のレシピは、さまざまなユース・ケースでのクラウド分析機能の使用法を示しています。

- [Real Time Data Analysis Using IBM Watson™ IoT Platform Analytics ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/real-time-data-analysis-using-ibm-watson-iot-platform-analytics/){: new_window}

- [Predictive Analytics on IOT Sample Data ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/predictive-analytics-on-iot-sample-data/){: new_window}

- [Device List Card SIMPLIFIES Real Time Device Monitoring on WIoTP Dashboard ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/device-list-card-simplifies-real-time-device-monitoring-on-wiotp-dashboard/){: new_window}

- [Perform Actions in IBM Watson IoT Platform Cloud Analytics ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/perform-actions-in-ibm-watson-iot-platform-cloud-analytics/){: new_window}

- [Use IBM Data Science Experience to detect time series anomalies ![外部リンク・アイコン](../../icons/launch-glyph.svg)](https://developer.ibm.com/recipes/tutorials/use-ibm-data-science-experience-to-detect-time-series-anomalies/){: new_window}
