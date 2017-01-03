---

 

copyright:

  years: 2015，2016
lastupdated: "2016-11-02"  
 

---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.autoscaling}} サービス入門
{: #autoscaling}
最終更新日：2016 年 11 月 2 日
{: .last-updated}

{{site.data.keyword.Bluemix_notm}} では、アプリケーション能力を自動的に管理できます。 {{site.data.keyword.autoscaling}} サービスを使用すると、
アプリケーションの計算容量を自動的に増減できます。アプリケーション・インスタンスの数は、定義する
{{site.data.keyword.autoscaling}} ポリシーに基づき、動的に調整されます。
{:shortdesc} 

## 目次
  * [{{site.data.keyword.Bluemix_notm}} での {{site.data.keyword.autoscaling}} サービスの使用](#as-service)
  * [{{site.data.keyword.autoscaling}} サービスでの Node.js アプリの構成](#node-asagent)
  * [RESTful API を使用した {{site.data.keyword.autoscaling}}サービスの管理](#RESTAPI)
  * [{{site.data.keyword.autoscaling}} CLI を使用した {{site.data.keyword.autoscaling}} サービスの管理](#CLI)
  * [{{site.data.keyword.autoscaling}} サービスのポリシー・フィールド](#policy_fields)
  * [エラー・メッセージ](#err_msg)

## {{site.data.keyword.Bluemix_notm}} での {{site.data.keyword.autoscaling}} サービスの使用
{: #as-service}

{{site.data.keyword.autoscaling}} サービスを利用するには、次のステップを実行します。

1. {{site.data.keyword.Bluemix_notm}} ダッシュボードで*「サービスまたは API の追加」*をクリックし、次にサービス・カタログの DevOps セクションから {{site.data.keyword.autoscaling}} サービスを選択します。新しいウィンドウが表示され、 {{site.data.keyword.autoscaling}} サービスの概要が提示されます。
2. {{site.data.keyword.autoscaling}} サービスをバインドするアプリケーションを選択し、*「作成」*をクリックします。<br/>*重要:* 1 つのアプリケーションにバインドできる {{site.data.keyword.autoscaling}} サービスは 1 つのみです。 アプリケーションが既に他の {{site.data.keyword.autoscaling}} サービスにバインド済みの場合は、このステップではアプリケーションを選択しないでください。そうしないと CWSCV2004E エラーが発生します。<br/>「アプリケーションの再ステージ」ウィンドウが表示されます。
3. 追加した新しい {{site.data.keyword.autoscaling}} サービスを使用する前に、「アプリケーションの再ステージ」ウィンドウで*「再ステージ」*をクリックして、アプリケーションを再ステージします。<br/><ul><li>Liberty アプリケーションの場合は、{{site.data.keyword.autoscaling}} はアプリケーションの再ステージング後に自動構成され、すぐに使用できる状態になります。 </li> <li>Node.js アプリケーションの場合は、アプリケーションを {{site.data.keyword.Bluemix_notm}} にプッシュする前に、アプリケーション・コードを更新して {{site.data.keyword.autoscaling}} サービスを使用可能にする必要があります。詳しくは、[{{site.data.keyword.autoscaling}} サービスでの Node.js アプリの構成](index.html#node_asagent)を参照してください。</ul><br/>
アプリケーションの再ステージングが完了した後、アプリケーションに合わせた {{site.data.keyword.autoscaling}} サービスの構成が開始できます。
4. {{site.data.keyword.autoscaling}} をアプリケーションに合わせて構成するには、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースで、{{site.data.keyword.autoscaling}} サービスがバインドされているアプリケーションをクリックします。
5. ダッシュボードのサービス・セクションで、*「Auto-Scaling」*アイコンをクリックします。
6. アプリケーションの {{site.data.keyword.autoscaling}} ポリシーをまだ定義していない場合は、*「{{site.data.keyword.autoscaling}} ポリシーの作成 (Create Auto-Scaling Policy)」*をクリックして定義します。

これで、{{site.data.keyword.autoscaling}} ポリシーの構成、メトリック統計の表示、およびアプリケーションのスケーリング履歴の表示ができるようになりました。
<dl>
<dt>ポリシーの構成</dt>
<dd>このセクションを使用して、特定のスケーリング・アクティビティーをトリガーすべき条件を指定するスケーリング・ルールを作成または編集します。<ul>
<li> Liberty for Java? アプリケーションの場合は、ヒープ、メモリー、応答時間、およびスループットのスケーリング・ルールを定義することができます。   
<li> Node.js アプリケーションの場合は、ヒープ、メモリー、およびスループットのスケーリング・ルールを定義することができます。
<li> 
Ruby アプリケーションの場合は、メモリーのスケーリング・ルールを定義することができます。</ul>
*注:* スケーリング・ルールは、複数のメトリック・タイプに対して複数定義することができます。ただし、{{site.data.keyword.autoscaling}} サービスはスケーリング・ポリシー間の競合を検出しません。スケーリング・ポリシーを定義する際は、必ず、複数のスケーリング・ルールがお互いに競合しないようにする必要があります。さもないと、アプリケーションがスケールインしたかと思うと、次の瞬間スケールアウトするため、総インスタンス数が変動する場合があります。<br/><br/>アプリケーションのワークロードがピーク時と空き時間で大幅に変動する場合は、期間が変わればスケーリング要件を変えて対処するようにスケーリング・スケジュールを作成することができます。動的スケーリング・ルールはスケールイン・アクションとスケールアウト・アクションをトリガーするためにスケジュールに適用したまま、そのスケジュールに指定されている Minimum Instance Count パラメーターを使用して、アプリケーション・インスタンス数のベースラインを定義してください。</dd>
<dt>メトリック統計</dt>
<dd>アプリケーションのインスタンスについてメトリック統計を表示します。
平均統計を表示して特定のインスタンスを選択すると、その統計を表示することができます。
</dd>
<dt>スケーリングの履歴</dt>
<dd>ご使用のアプリケーションのスケーリング履歴を表示します。<ul>
<li> 過去の週 :
この 1 週間のスケーリング履歴を表示します。<li> 過去の月 :
この 1 カ月のスケーリング履歴を表示します。<li> カスタム範囲:
期間を設定することができます。</ul>
*注:* 履歴レコードは、「スケーリング状況 (Scaling Status)」または「スケールイン/スケールアウト (Scaling In/Out)」を選択することで、フィルタリングできます。</dd>
</dl>


## {{site.data.keyword.autoscaling}} サービスでの Node.js アプリの構成
{: #node-asagent}

Node.js アプリで {{site.data.keyword.autoscaling}} サービスを使用可能にするには、サービス・プロビジョンおよびステップのバインドの他に、{{site.data.keyword.Bluemix_notm}} にアプリをプッシュする前に以下のステップも完了する必要があります。

1. 以下のステップにより package.json ファイルを更新します。<ol><li>`blumix-autoscaling-agent` の依存関係エントリーを作成します。例えば、`"bluemix-autoscaling-agent": "*"` などです。<br/><li>(オプション) アプリに割り振ったメモリーに基づいて、`scripts` セクション内でヒープ限度を設定します。例えば次のようにします。`"start": "node --max-old-space-size=600 app.js"`<br/>*注: *ヒープ使用状況に基づいてスケーリングをトリガーする場合は、`max-old-space-size` に値を設定します。アプリケーションの始動時にこの値が設定されていない場合、ご使用のアプリに割り振られたメモリー量にかかわらず、デフォルトの Node.js ヒープ限度 1.4GB が使用されます。これにより、不適切な自動スケーリングの決定がなされる場合があります。<br/>

```
{
	"name": "NodejsStarterApp",
	"version": "0.0.1",
	"description": "A sample nodejs app for Bluemix",
	"scripts": {
		"start": "node --max-old-space-size=600 app.js"
	},
	"dependencies": {
		"bluemix-autoscaling-agent": "*"
	},
	"repository": {},
	"engines": {
		"node": "0.12.x"
	} 
}
```
</ol>
2. メインファイルを更新して、エージェント宣言 `var as_agent = require('bluemix-autoscaling-agent');` を追加します。以下のコード・スニペットは、自動スケーリングのエージェント宣言を含む完全なエントリー js ファイルを示しています。<br/>
```
var agent = require('bluemix-autoscaling-agent');
var http = require('http');
var server = http.createServer(function handler(req, res) {
	console.log("Hello!");
	
	}).listen(process.env.PORT || 3000);
console.log('App is listening on port 3000');
```

## RESTful API を使用した {{site.data.keyword.autoscaling}} サービスの管理 
{: #RESTAPI}

{{site.data.keyword.autoscaling}} RESTful API は、Bluemix UI の他に、{{site.data.keyword.autoscaling}} サービスを管理するための代替方法を提供します。また、スケーリング・データの検索と分析もサポートします。この API は、ポリシーの作成やスケーリング履歴の取得など、API を使用した {{site.data.keyword.Bluemix_notm}} UI と類似の機能を提供します。

{{site.data.keyword.autoscaling}} RESTful API を使用して {{site.data.keyword.autoscaling}} サービスを管理するには、次の前提条件を満たす必要があります。前のセクションで指定されたように、ご使用のアプリケーションと {{site.data.keyword.autoscaling}} サービスをバインドすること。`AccessToken`、{{site.data.keyword.autoscaling}} API サーバーの URL、およびスケールインまたはスケールアウトするアプリケーションの `app_id` を取得すること。

1. セキュリティーの目的のために、{{site.data.keyword.autoscaling}} RESTful API の各要求ヘッダーで、CloudFoundry UAA プロシージャーにより取得された適切な `AccessToken` を `Authorization` ヘッダーに指定して、要求の必要な検証を示します。この `AccessToken` を順守しないと、401 無許可応答が発生します。Cloud Foundry コマンド・ライン・ツールをインストールし、{{site.data.keyword.Bluemix_notm}} にログインした後にこの `AccessToken` を取得するには、以下の 2 つの方法があります。<ul><li>`cf oauth-token` コマンドを使用してこのトークンを取得できます。
   
   ```
   > cf oauth-token
   Getting OAuth token...
   OK

     bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk
   ```
返される長ストリングは“bearer”で始まり、これは {{site.data.keyword.autoscaling}} RESTful API の要求で使用できる AccessToken です。“Command not found”などのエラーが発生した場合は、Cloud Foundry コマンド・ライン・ツールを新しいバージョンに更新することができます。</li><li>この AccessToken は、ホーム・ディレクトリーでも検索できます。
コマンド・ライン・インターフェースから {{site.data.keyword.Bluemix_notm}} にログインした後、ホーム・フォルダー内に `.cf` フォルダーが作成されます。このフォルダー内には、組織、スペース、認証エンドポイントおよびバージョンなど、ユーザーの現行ロギングの環境情報リストを含む JSON ファイル名 `config.json` があります。ファイル内のエントリー `AccessToken` は以下のように見つけることができます。
    ```
   >cat ~/.cf/config.json
 {
  "ConfigVersion": 3,
  "Target": "https://api.ng.bluemix.net",
  "ApiVersion": "2.40.0",
  "AuthorizationEndpoint": "https://login.ng.bluemix.net/UAALoginServerWAR",
  "LoggregatorEndPoint": "wss://loggregator.ng.bluemix.net:443",
  "DopplerEndPoint": "wss://doppler.ng.bluemix.net:443",
  "UaaEndpoint": "https://uaa.ng.bluemix.net",
  "RoutingApiEndpoint": "https://api.ng.bluemix.net/routing",
  "AccessToken": "bearer eyJhbGciOiJIUzI1NiJ9.eyJqdGkiOiJhNjIzMGE1YS1mNzE3LTQ0YjItOWM3Yi1kNGJkYThhZGU0NjkiLCJzdWIiOiI4OGViNjM2My1hMjkzLTRlZTItYWQ1MS0yOGVkMTZmZjMwNzQiLCJzY29wZSI6WyJjbG91ZF9jb250cm9sbGVyLnJlYWQiLCJwYXNzd29yZC53cml0ZSIsImNsb3VkX2NvbnRyb2xsZXIud3JpdGUiLCJvcGVuaWQiXSwiY2xpZW50X2lkIjoiY2YiLCJjaWQiOiJjZiIsImF6cCI6ImNmIiwiZ3JhbnRfdHlwZSI6InBhc3N3b3JkIiwidXNlcl9pZCI6Ijg4ZWI2MzYzLWEyOTMtNGVlMi1hZDUxLTI4ZWQxNmZmMzA3NCIsIm9yaWdpbiI6InVhYSIsInVzZXJfbmFtZSI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJlbWFpbCI6Imtqa29uZ2tqQGNuLmlibS5jb20iLCJyZXZfc2lnIjoiZDhlNGY0MDIiLCJpYXQiOjE0NTU2MDc1NDUsImV4cCI6MTQ1NTY1MDc0NSwiaXNzIjoiaHR0cHM6Ly91YWEuc3RhZ2UxLm5nLmJsdWVtaXgubmV0L29hdXRoL3Rva2VuIiwiemlkIjoidWFhIiwiYXVkIjpbImNsb3VkX2NvbnRyb2xsZXIiLCJwYXNzd29yZCIsImNmIiwib3BlbmlkIl19.nrzsEAZmGXNOWjX8r5Xf7U8Hj5-CE1rtHg8_C-jZKSk",
  "SSHOAuthClient": "ssh-proxy",
 .....
 }
   ```
`config.json` 内の `AccessToken` は、一定の期間のみ有効です。REST API 要求に対する 401 無許可応答が発生した場合は、コマンド・ライン・インターフェースから再度ログインし直してファイルを最新表示し、新しい `AcessToken` を取得する必要がある可能性があります。</li></ul>
 
2.  {{site.data.keyword.autoscaling}} API サーバーの URL は、アプリケーションを {{site.data.keyword.autoscaling}} サービスとバインドした後、`VCAP_SERVICE` 環境変数をチェックすることで取得できます。`VCAP_SERVICE` では、{{site.data.keyword.autoscaling}} サービスのセクションを確認できます。`api_url` は、ご使用のアプリケーションがバインドされている API サーバーの URL です。この API サーバーの URL は、 {{site.data.keyword.autoscaling}} RESTful API サービスに接続する際に必要です。
   
   ```
    {
      "Auto-Scaling": [
      {
         "name": "Auto-Scaling-iw",
         "label": "Auto-Scaling",
         "plan": "free",
         "credentials": {
            "agentUsername": "agent",
            "api_url": "https://ScalingAPI.ng.bluemix.net",
            "service_id": "3f42b7ff-d939-4ff2-9a55-cb09cef9ab9e",
            "app_id": "2287f442-a7f3-4799-8919-d3908c386fa3",
            "url": "https://Scaling3.ng.bluemix.net",
            "agentPassword": "0cddf80b-37e1-4cfd-b648-83a6c8wee69f"
         }
      }
     ]
   }
   ``` 
この URL は `cf env APPNAME` コマンドを使用しても確認できることに注意してください。
   ```
   > cf env Hello
   Getting env variables for app Hello in org OE_Runtimes_SVT / space RT_SVT as Alice...
   OK

   System-Provided:
   {"VCAP_SERVICES": {
     "Auto-Scaling": [
     {
      "credentials": {
       "agentPassword": "b626b064-7d26-417a-b954-41c6d3cb5200",
       "agentUsername": "agent",
       "api_url": "https://ScalingAPI.ng.bluemix.net",
       "app_id": "aa8d19b6-eceb-4b6e-b034-926a87e98a51",
       "service_id": "8f482f78-58d8-493c-829b-635e4cbfd817",
       "url": "https://Scaling.ng.bluemix.net"
      },
      "label": "Auto-Scaling",
      "name": "ScalingService",
      "plan": "free",
      "tags": [
       "bluemix_extensions",
       "ibm_created",
       "dev_ops"
      ]
     }
   ...
   ```  
3.  `VCAP_SERVICES` 環境変数から `app_id` を取得することも、単純に `cf app APPNAME --guid` コマンドを実行することもできます。

   ```
   > cf app Hello --guid
   aa8d19b6-eceb-4b6e-b034-926a87e98a51
   > 
   ```

上記の前提条件がすべて揃ったら、ブラウザーで RestClient アドオンを使用して、もしくは `curl` のようなツールを使用して、REST API 要求を作成できます。 

REST クライアント・アドオンでは、Firefox や Chrome のアドオンの場合と同様に、{{site.data.keyword.autoscaling}} API サーバーに対する REST 要求をトリガーして、コマンドを実行することができます。REST API の URL と、この REST API が必要とするメソッドとヘッダーをこれらのアドオンに指定し、本文パートにパラメーターを指定するだけです。各 API の詳細については、[IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} の Rest API (Rest API of IBM auto-scaling for Bluemix)](https://new-console.ng.bluemix.net/apidocs/48){:new_window} を参照してください。

`curl` のようなツールを使用する場合、以下のようにスクリプト内で {{site.data.keyword.autoscaling}} サービスを管理できます。    
```
cf login -a http://api.ng.bluemix.net -u Alice -p pa55w0rd --skip-ssl-validation
    accessToken=$(cf oauth-token | grep bearer | sed -e s/bearer/Bearer/g)
    API_url=$(cf env Hello | grep "api_url" | awk '{print $2}' | cut -d "," -f1 | cut -d "\"" -f2 )
    policyJson="./policy.json"
    appId=$(cf app Hello --guid)echo  -e "\nCreate scaling policy using API :"
    createPolicyUrl="${API_url}/v1/autoscaler/apps/${appId}/policy"
    curl_cmd="curl $createPolicyUrl -X 'PUT' -H 'Content-Type:application/json'  -H 'Accept:application/json' -H 'Authorization:$accessToken' --data-binary @${policyJson} -s -o response.txt -w '%{http_code}\n'"
    eval status_code=$($curl_cmd)
    if [[ $status_code -eq 201 ]]; then
         echo "looks good"
    else
         echo "error happens"
         exit 255
    fi
  ```

## {{site.data.keyword.autoscaling}} CLI を使用した {{site.data.keyword.autoscaling}} サービスの管理 
{: #CLI}

{{site.data.keyword.autoscaling}} CLI は {{site.data.keyword.autoscaling}} RESTful API と類似の機能を提供しますが、より親しみやすい方法で {{site.data.keyword.autoscaling}} サービスを構成できます。{{site.data.keyword.autoscaling}} CLI では、`AccessToken` や API サーバーの URL など、{{site.data.keyword.autoscaling}} RESTful API の詳細について気に掛ける必要がありません。ただ CLI により順を追って提示される指示に従うだけです。{{site.data.keyword.autoscaling}} CLI のインストール方法および使用方法について詳しくは、[{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window} を参照してください。



## {{site.data.keyword.autoscaling}} サービスのポリシー・フィールド
{: #policy_fields}

| フィールド名  | 説明 |
|-------------|----------------------|
|*「許容最大インスタンス数 (Allowable maixmum instance count)」* |	開始できるアプリケーション・インスタンスの最大数。現在のアプリケーション・インスタンス数がこの値に等しい場合、 {{site.data.keyword.autoscaling}} サービスは、そのアプリケーションをそれ以上スケールアウトしません。「デフォルト最小インスタンス数」	開始できるアプリケーション・インスタンスの最小数。インスタンス数がこの値に等しい場合、 {{site.data.keyword.autoscaling}} サービスは、そのアプリケーションをそれ以上スケールインしません。 |
| *「メトリック・タイプ」*	| 	モニター可能なサポートされるメトリック・タイプ。詳細については、表 2 を参照してください。 |
| *「スケールアウト」* | 	スケールアウト・アクションがトリガーされるしきい値、およびスケールアウト・アクションがトリガーされた時に増加されるインスタンスの数を指定します。 |
| *「スケールイン」* |	スケールイン・アクションがトリガーされるしきい値、およびスケールイン・アクションがトリガーされた時に削減するインスタンスの数を指定します。 |
| *「統計ウィンドウ」* |	受け取ったメトリック値が有効と認識される、過去の期間の長さ。メトリック値は、タイム・スタンプがこの期間内に含まれている場合のみ有効です。Statistic Window パラメーターの単位は秒です。 |
| *「違反期間」*	| スケーリング・アクションがトリガーされる可能性がある、過去の期間の長さ。スケーリング・アクションは、収集されたメトリック値が、指定した時間より長い間、しきい値の上限を上回るかしきい値の下限を下回る場合にトリガーされます。Breach Duration パラメーターの単位は秒です。 |
| *「スケールインのクールダウン期間」* | スケールイン・アクションの発生後、Cooldown period for scaling in パラメーターで指定した期間中は、他のスケーリング要求は無視されます。このパラメーターの単位は秒です。 |
| *「スケールアウトのクールダウン期間」*	| スケールアウト・アクションの発生後、Cooldown period for scaling out パラメーターで指定した期間中は、他のスケーリング要求は無視されます。このパラメーターの単位は秒です。 |
| *「タイム・ゾーン (Time Zone)」*	| スケジュールが適用されるタイム・ゾーン。 |
| *「開始時刻 (Start Time)」*  |	反復スケジュールの開始時刻。 |
| *「終了時刻 (End Time)」*    |	反復スケジュールの終了時刻。	|
| *「反復曜日 (Repeat On)」*	|	反復スケジュールが適用される曜日。 |
| *「最小インスタンス数 (Minimum Instance Count)」* |	スケジュールで指定された期間に開始できる最小アプリケーション・インスタンス数。 |
| *「開始日時 (Start Date & Time)* |	特定日にセットアップされているスケジュールの開始日時。 |
| *「終了日時 (End Date & Time)」* |	特定日にセットアップされているスケジュールの終了日時。	|

表 1. スケーリング・ポリシーのポリシー・フィールド

| メトリック名 | 説明 | サポートされるアプリケーション・タイプ |
|-------------|----------------------| ------------------- |
| *「ヒープ」* |	ヒープ・メモリーの使用率。	| Liberty for Java, Node.js SDK |
| *「メモリー」*   |	メモリーの使用率。	|  すべて   |
| *「スループット」* | 1 秒当たりに処理される要求の数。| Liberty for Java, Node.js SDK |
| *「応答時間」* |	処理された要求の応答時間。	| Liberty for Java |

表 2. サポートされるメトリック名

*注:* Auto-Scaling のメトリック・データを収集するには、Liberty Web コンテナー経由で処理される HTTP/HTTPS 要求を測定するように、ご使用のアプリケーションを Liberty Web アプリとしてデプロイしてください。
例えば、「Main-Classs」アプリとして Spring Boot アプリケーションを実行する場合、Liberty ビルドパックは Java 環境のみを提供します。そして、アプリは実際には Tomcat コンテナーが埋め込まれた Spring 内で実行されます。したがって、Auto-Scaling サービスによって収集されるメトリック・データはありません。 Auto-Scaling サービスを使用して作業するためにはご使用のアプリをLiberty WAR として実行する必要があります。

## エラー・メッセージ
{: #err_msg}
このセクションでは {{site.data.keyword.autoscaling}} サービスで出される警告とエラー・メッセージをリストします。
 
### CWSCV2004E 他の {{site.data.keyword.autoscaling}} サービスが既にアプリケーションにバインド済みです。
**1 つのアプリケーションにバインドできる {{site.data.keyword.autoscaling}} サービスは 1 つのみです。このエラーは、既に {{site.data.keyword.autoscaling}} サービスにバインドされているアプリケーションに、別の {{site.data.keyword.autoscaling}} サービスをバインドしようとした時に発生します。**

どの {{site.data.keyword.autoscaling}} サービスにもバインドされていない他のアプリケーションを選択して、ターゲットの
{{site.data.keyword.autoscaling}} サービスをそのアプリケーションにバインドします。その他のすべての状況でこのエラーが発生する場合は、IBM サポートにお問い合わせください。

### CWSCV6001E API サーバーは API の入力 JSON ストリングを解析できません: {0}。
**入力 JSON ストリングを解析している時に問題が発生しました。**

API の資料で入力 JSON を調べ、エラーを修正してください。

### CWSCV6002E API サーバーは API の出力 JSON ストリングを解析できません: {0}。
**入力 JSON ストリングを解析している時に問題が発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6003E 入力 JSON ストリング・フォーマットのエラー: API の入力 JSON 内の {0}: {1}。
**入力 JSON ストリングを解析している時にフォーマット・エラーが検出されました。**

API の資料で入力 JSON を調べ、エラーを修正してください。

### CWSCV6004E 出力 JSON ストリング・フォーマットのエラー: API の出力 JSON 内の {0}: {1}。
**出力 JSON ストリングを解析している時にフォーマット・エラーが検出されました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6005E {0} 中、内部サーバー・エラーが発生しました。
**要求を処理している時に内部サーバー・エラーが発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6006E CloudFoundry API の呼び出しが失敗しました: {0}
**CloudFoundry API を呼び出している時にエラーが発生しました。**

詳細情報について、クラウド管理者にお問い合わせください。

### CWSCV6007E アプリケーションが見つかりません: {0}
**アプリケーションが見つかりません。**

詳細情報について、アプリケーション情報を調べてください。

### CWSCV6008E アプリケーション {0} の情報を取得している時に次のエラーが発生しました: {1} 
**何らかのエラーによりアプリケーション情報の取得に失敗しました。**

詳細情報について、アプリケーション情報を調べてください。

### CWSCV6009E サービス: アプリ {1} の {0} が見つかりません。
**このアプリケーションのサービスが見つかりません。**

詳細情報について、このアプリケーションのサービス・バインディングを調べてください。

### CWSCV6010E アプリ {0} のポリシーが見つかりません
**このアプリケーションのポリシーが見つかりません。**

詳細情報について、アプリケーション構成を調べてください。

### CWSCV6011E {0} 中、内部認証に失敗しました
**内部認証に失敗しました。**

詳細情報について、クラウド管理者にお問い合わせください。


# 関連リンク
{: #rellinks}

## サンプル
{: #samples}

* [チュートリアル: Make your application elastic on {{site.data.keyword.Bluemix_notm}}](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window}
* [Cloud Foundry アーキテクチャー・ラボ](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
{: #sdk}

* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} の Rest API (Rest API of IBM auto-scaling for Bluemix)](https://new-console.{DomainName}/apidocs/48){:new_window}

## 一般
{: #general}

* [コンテナーのスケーリング](https://www.{DomainName}/docs/containers/container_creating_ov.html#container_group_ov){:new_window}
* [仮想サーバーのスケーリング](https://www.{DomainName}/docs/virtualmachines/vm_index.html#vm_manage_instances){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}
* [Node.js の {{site.data.keyword.autoscaling}} エージェント](https://www.npmjs.com/package/bluemix-autoscaling-agent){:new_window}

