---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# アクションの例

E メール送信、IFTTT、Node-RED、および Webhook の各アクション・タイプにより、幅広いタスク実行用オプションを利用できるようになり、受ける制約は、自らの想像力と他のツールで使用されているコネクターによる制限のみです。例えば、Slack にデバイス状況メッセージを投稿したり、テキスト・メッセージをサービス担当者に送信したり、デバイス・サービス要求を作成したりするアクションなどが可能です。
{: shortdesc}

以下の例はすべて、ルール条件 `temp >= 100` を使用して、デバイスの temp データ・ポイントで表される温度が 100 度を超えたときにサービス・エンジニアに通知するアクションを表しています。

ルール条件が満たされたときに、以下の 1 つ以上のアクション・タイプをトリガーできます。  
 - [E メール送信](#emailex "E メール送信")
 - [Webhook](#webhookex "Webhook")
 - [Node-RED](#noderedex "Node-RED")
 - [IFTTT](#iftttex "IFTTT")

## E メール送信の使用{: #emailex}
この例では、Real-Time Insights の E メール送信機能を使用して、E メールをメインサービス・エンジニアに送信するとともに、バックアップ E メールをそのエンジニアのマネージャーにも送信するアクションを構成します。

E メール・アクションを作成するには、以下のようにします。
1. Real-Time Insights で、**「分析 (Analytics)」>「アクション」**に移動します。
2. **「新規アクションの追加 (Add new action)」**をクリックします。
3. **「E メール送信 (Send Email)」**タイプを選択します。
4. アクション名として`「サービス要求 E メールの送信」`と入力します。
5. 説明として`「サービス・エンジニアとそのマネージャーに E メールを送信」`と入力します。
6. To フィールドに`「service.engineer@company.com」`と入力します。
7. CC フィールドに`「service.manager@company.com」`と入力します。
8. 件名行に`「サービスが必要」`と入力します。
9. 「{{site.data.keyword.iotrtinsights_short}} アラート」を前に付加するように選択して、E メールの送信元を明確化します。
10. デバイス・データを E メールに含めるために、**「デバイス・データを E メール・メッセージに含めない (Do not include device data in the email message)」**チェック・ボックスをクリアします。
11. **「OK」**をクリックしてアクションを保存します。  




## Webhook を使用した Slack への投稿{: #webhookex}

この例では、Webhook を使用してメッセージを #service-requests Slack チャネルに投稿するアクションを構成します。

Slack への投稿アクションを作成するには、以下のようにします。
1. Slack で、チャネル #service-requests の「Incoming Webhooks」統合をセットアップします。Webhook の URL をメモします。詳しくは、[Slack の資料](https://api.slack.com/incoming-webhooks)を参照してください。
2. Real-Time Insights で、**「分析 (Analytics)」>「アクション」**に移動し、以下のパラメーターが含まれている新規アクションを作成します。
 - タイプ - **Webhook**
 - 名前 - `Slack へのサービス要求の投稿`
 - URL - `Slack Webhook URL`
 - メソッド (Method) - **POST**
 - コンテンツ・タイプ (Content type) - application/json
 - **「カスタマイズしたメッセージ本文の使用 (Use customized message body)」**を選択
 - 本文
```{"text":"*要確認デバイスが発生*\n 時刻: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} インスタンス: {{tenantId}}\n デバイス: {{deviceId}}\n ルール: {{ruleName}}\n 説明: {{ruleDescription}}\n 条件: {{ruleCondition}}\n ロー・デバイス・メッセージ: \n{{message}}"}```
 {: codeblock}  
 **重要:** Slack Webhook には少なくとも「text」フィールドを含める必要があります。詳しくは、Slack の資料の『[Incoming Webhooks](https://api.slack.com/incoming-webhooks "Slack の資料")』を参照してください。
11. **「OK」**をクリックしてアクションを保存します。

## Node-RED を使用したテキスト・メッセージの送信{: #noderedex}

この例では、Twilio ノードで Node-RED を使用して、テキスト・メッセージをサービス・エンジニアに送信するアクションを構成します。

テキスト・メッセージの送信アクションを作成するには、以下のようにします。
1. Twilio で、Twilio アカウントからテキスト・メッセージを送信するために使用するメッセージング・サービスを見つけるか、そのような新規メッセージング・サービスを作成します。詳しくは、[Twilio の資料](https://www.twilio.com/help)を参照してください。
1. Bluemix で、Node-RED アカウントをセットアップし、Node-RED URL `http://mynodered.mybluemix.net/red/` を使用してそのアカウントにアクセスします。詳しくは、Bluemix 資料のトピック『[Creating apps with Node-RED Starter](https://www.ng.bluemix.net/docs/starters/Node-RED/nodered.html)』を参照してください。
2. Node-RED で、シンプルな 2 つのノードのフロー ([RTI-alert]->[SMS] など) を作成します。
ここで、最初のノードは HTTP ノードで、2 番目のノードは Twilio ノードです。
 1. 「HTTP」入力ノードを追加し、以下の属性を使用してそのノードを構成します。
  <ul>
  <li>メソッド (Method) - POST</li>
  <li>URL - `RTI-alert`</li>
  <li>名前 - RTI アクション</li>
  </ul>
  2. 「HTTP 応答」出力ノードを追加し、そのノードと「HTTP」入力ノードを接続します。接続するには、一方のノードの出力ポートを他方の入力ポートにドラッグします。
  3. 「Twilio」出力ノードを追加し、以下の属性を使用してそのノードを構成します。
  <ul>
  <li>サービス - **外部サービス (External service)**</li>
  <li>Twilio - 新規 twilio-api の追加 (Add new twilio-api)</li>
  <li>SMS 送信先 (SMS to) - `サービス・エンジニアの電話番号`</li>
  <li>名前 - **SMS**</li>
  </ul>
  4. ノードをワイヤリングします。HTTP ノードと Twilio ノードを接続します。接続するには、一方のノードの出力ポートを他方の入力ポートにドラッグします。
  5. **「デプロイ (Deploy)」**ボタンをクリックして、フローをサーバーにデプロイします。
3. {{site.data.keyword.iotrtinsights_short}} で、**「分析 (Analytics)」>「アクション」**に移動し、以下のパラメーターが含まれているアクションを作成します。
 - タイプ - **Node-RED**
 - 名前 - `Node-RED および Twilio を使用したテキストの送信`
 - 説明 - `テキスト・メッセージ・アラートをサービス・エンジニアに送信。`
 - URL - `http://mynodered.mybluemix.net/RTI-alert`
 - 本文 (BODY)
 ```{"text":"*要確認デバイスが発生*\n 時刻: {{timestamp}}\n {{site.data.keyword.iotrtinsights_short}} インスタンス: {{tenantId}}\n デバイス: {{deviceId}}\n ルール: {{ruleName}}\n 説明: {{ruleDescription}}\n 条件: {{ruleCondition}}\n ロー・デバイス・メッセージ: \n{{message}}"}```
 {: codeblock}
4. **「OK」**をクリックしてアクションを保存します。

## IFTTT を使用した Trello カードの投稿{: #iftttex}

この例では、IFTTT を使用して Trello 上のサービス要求リストにカードを投稿するアクションを構成します。

Trello にカードを投稿するアクションを作成するには、以下のようにします。
1.	IFTTT で、Trello チャネルに接続します。
2.	IFTTT で、Maker チャネルに接続します。IFTTT キーをメモします。これは、Real-Time Insights から IFTTT に接続する際に必要になります。
5.	IFTTT で、以下のようにレシピを作成します。
 1. **「THIS」**をクリックします。
 2. **「Maker」**チャネルを選択します。  
 2. **「Recieve a web request」**をクリックします。
 3. イベント名として`「post-Trello-card」`と入力します。
 4. **「THAT」**をクリックします。
 5. **「Trello」**チャネルを選択します。
 6. カードを作成する Trello ボードを選択します。
 7. カードを追加するリスト名を入力します。
 8. タイトルと説明を編集します。
 9. @service.engineer メンバーおよび @service.manager メンバーを割り当てます。
 8. **「Create Action」**をクリックします。   
3. {{site.data.keyword.iotrtinsights_short}} で、**「分析 (Analytics)」>「アクション」**に移動し、以下のパラメーターが含まれているアクションを作成します。
<ul>
<li>タイプ - **IFTTT**</li>
<li>名前 - `サービス要求カードの投稿`</li>
<li>説明 - `IFTTT を使用して Trello 内のサービス要求リストにカードを投稿。`</li>
<li>キー (Key) - IFTTT キー</li>
<li>イベント - `post-Trello-card`</li>
<li>オプションとして、「値 1 (Value 1)」から「値 3 (Value 3)」の値を追加。**ヒント:** [変数置換](actions.html#variable_substitution)を使用して、デバイス・データを動的に組み込むことができます。</li>
</ul>
4. **「OK」**をクリックしてアクションを保存します。
