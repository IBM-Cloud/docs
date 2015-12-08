{:shortdesc: .shortdesc} 
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} とのサービスの統合
{: #v2api}
最終更新日: 2015 年 11 月 11 日

サービスを作成するには、およびそれらのサービスを {{site.data.keyword.Bluemix}} に統合するには、サービスを実装およびデプロイして、サービス用のサービス・ブローカーを実装し、その後、そのサービス・ブローカーを {{site.data.keyword.Bluemix_notm}} に登録する必要があります。 

サービス・ブローカーは、サービスを拡張し、サービスを {{site.data.keyword.Bluemix_notm}} に統合する RESTful Web サービスです。{{site.data.keyword.Bluemix_notm}} のサービス・ブローカーには、次の機能があります。
* {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースと **cf marketplace** コマンドの出力の両方に表示されるサービス・カタログにデータを設定する。
* プロビジョニング、バインディングなどの要求に応答することで、{{site.data.keyword.Bluemix_notm}} のアプリケーションがサービスを使用できるようにする。サービス・ブローカーを使用してサービスのインスタンスがアプリケーションにプロビジョンされ、バインドされた後、そのアプリケーションは、サービス・ブローカーなしでそのサービス・インスタンスと直接対話できます。

サービス・ブローカーは、{{site.data.keyword.Bluemix_notm}} に統合されるサービスを 2 種類サポートしています。1 つは {{site.data.keyword.Bluemix_notm}} 内に存在する通常の {{site.data.keyword.Bluemix_notm}} サービスで、もう 1 つは {{site.data.keyword.Bluemix_notm}} の外部でプロビジョンされるユーザー提供のサービスです。

サービス・ブローカーは、Cloud Foundry サービス・ブローカー API を使用して実装します。サービス・ブローカー API の動作の概要については、「Cloud Foundry Documentation」の[Service Broker API](http://docs.cloudfoundry.org/services/api.html)ページの**API Overview**セクションを参照してください。

**注:** {{site.data.keyword.Bluemix_notm}} 専用環境でサービスを使用可能にする場合、[Making services accessible from Dedicated](../MCCP/index.html)で詳細を確認してください。

## サービスの作成と統合の概要

独自のサービスを作成し、{{site.data.keyword.Bluemix_notm}} に統合できます。

サービスを作成し、{{site.data.keyword.Bluemix_notm}} に統合するプロセスは、次のタスクで構成されます。
1. サービスを実装します。サービスを作成し、それを {{site.data.keyword.Bluemix_notm}} に統合するには、最初にサービスの機能を実装する必要があります。{{site.data.keyword.Bluemix_notm}} のアプリケーションとしてサービスを作成し、デプロイできます。{{site.data.keyword.Bluemix_notm}} でのアプリケーションの作成について詳しくは、[Web アプリケーションの作成](https://www.stage1.eu-gb.bluemix.net/docs/starters/index.html) を参照してください。{{site.data.keyword.Bluemix_notm}} へのアプリケーションのデプロイについて詳しくは、[cf コマンドを使用してのアプリケーションのデプロイ](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps) を参照してください。
2. サービス・ブローカーを実装します。REST API 呼び出しを使用してサービス・ブローカーが {{site.data.keyword.Bluemix_notm}} と通信できるようにするには、Catalog、Provision、および Unprovision の API エンドポイントを実装する必要があります。これらのエンドポイントを通じて、サービスのリソース (ドキュメンテーション、アイコン・イメージ、クイック・スタート・ガイド、およびサービス・インスタンスのユーザー・インターフェースを提供する管理 I フレームの URL など) を提供する必要があります。 
   
   {{site.data.keyword.Bluemix_notm}} のアプリケーションにサービスをバインドできる場合、Bind エンドポイントおよび Unbind エンドポイントも実装する必要があります。
   
   詳しくは、[サービス・ブローカーの実装](./index.html#implementing-a-service-broker)を参照してください。
  
3. サービス・ブローカーを {{site.data.keyword.Bluemix_notm}} に登録します。**cloud-cli** コマンド・ライン・インターフェースを使用してサービス・ブローカーを登録します。詳しくは、[サービス・ブローカーの登録](./index.html#registering-the-service-broker)を参照してください。
   
サービスを {{site.data.keyword.Bluemix_notm}} に統合した後、**cf marketplace** コマンドの出力でそのサービスを見つけることができます。{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースのサービス・カタログでもそのサービスを見つけることができます。サービスは、サービス定義 JSON のタグ・フィールドで指定したサービス・カテゴリーの下にあります。


## 例: サービスの作成および統合

サービスの作成方法、および {{site.data.keyword.Bluemix_notm}} へのサービスの統合方法を確認するために、サンプル・サービスを試用できます。このサンプル・サービスのコードには、サービス・ブローカー API が既に実装されています。

サンプル・サービスをビルドし、{{site.data.keyword.Bluemix_notm}} に統合するには、次のステップを実行します。
1. [チュートリアルおよびサンプル](./index.html#tutorials-and-samples)にリストされているいずれかのサンプル・サービスをダウンロードします。 
2. サンプル・サービスを {{site.data.keyword.Bluemix_notm}} にデプロイします。{{site.data.keyword.Bluemix_notm}} へのアプリケーションのデプロイについて詳しくは、[cf コマンドを使用してのアプリケーションのデプロイ](https://www.stage1.eu-gb.bluemix.net/docs/manageapps/deployingapps.html#dep_apps) を参照してください。
3. サービス・ブローカー定義 JSON を作成します。詳しくは、[サービス・ブローカー定義](./index.html#service-broker-definition)を参照してください。
4. **cloud-cli create-service-broker** コマンドを使用して、サービス・ブローカー定義を {{site.data.keyword.Bluemix_notm}} に登録します。詳しくは、[サービス・ブローカーの登録](registering-the-service-broker)を参照してください。

サンプル・サービスを {{site.data.keyword.Bluemix_notm}} に統合した後、**cf marketplace** コマンドの出力、および {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースのサービス・カタログで、そのサンプル・サービスを見つけることができます。 


## サービス・ブローカーの実装
{: #v2impl}

{{site.data.keyword.Bluemix_notm}} でサービス・ブローカーを実装するには、Cloud Foundry サービス・ブローカー API を実装する必要があります。サービス・ブローカー API は、{{site.data.keyword.Bluemix_notm}} で使用される一連の REST エンドポイントです。
1. {{site.data.keyword.Bluemix_notm}} がサービス・ブローカーに送信する HTTP 要求のための認証を指定します。サービス・ブローカーで HTTP 基本認証を使用して {{site.data.keyword.Bluemix_notm}} の認証が行われます。このため、サービス・ブローカーを実装するときに認証方式を指定する必要があります。また、{{site.data.keyword.Bluemix_notm}} が送信する HTTP 要求の認証ヘッダー内のユーザー名およびパスワードをチェックする必要があります。ユーザー名およびパスワードが無効の場合、401 無許可メッセージを返す必要があります。
   
   **注:** サービス・ブローカーを登録するとき、サービス・ブローカーの定義 JSON で認証に使用するユーザー名とパスワードを指定する必要があります。定義 JSON について詳しくは、[サービス・ブローカー定義
](./index.html#service-broker-definition)を参照してください。

2. サービス・ブローカーの API エンドポイントを実装します。コードで、{{site.data.keyword.Bluemix_notm}} のサービス・ブローカーの API 仕様に従い、HTTP 要求を処理する必要、および Catalog、Provision、および Deprovision API エンドポイントの関連応答を指定する必要があります。API エンドポイントについて詳しくは、[REST API リファレンス](./index.html#rest-api-reference)を参照してください。 
   
   Java&trade、Node.js、および Ruby の API エンドポイントを実装するサンプル・サービスについては、『チュートリアルおよびサンプル』(./index.html#tutorials-and-samples) を参照してください。 
   
3. エラーが発生した場合に {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示される、サービス・ブローカーのエラー・メッセージを指定します。サービス・ブローカーのエンドポイントのエラー・メッセージを指定するには、description 項目を含む JSON オブジェクトを返す必要があります。以下に例を示します。```
   {
  "description" : "Service failed due to invalid authorization"
   }
   ```

   
## サービス・ブローカーの登録
{: #v2reg}

サービス・ブローカーを実装した後、それを {{site.data.keyword.Bluemix_notm}} に登録する必要があります。

サービス・ブローカーを {{site.data.keyword.Bluemix_notm}} に登録するには、次のタスクを実行する必要があります。 
1. JSON ファイルでサービス・ブローカー定義を作成します。詳しくは、[サービス・ブローカー定義](./index.html#service-broker-definition)を参照してください。
2. サービスの Catalog (GET) の結果を完全にするために、サービス・メタデータ、クイック・スタート・ガイド、サービス・アイコン・イメージ、およびドキュメンテーションを用意する必要があります。詳しくは、[REST API リファレンス](./index.html#rest-api-reference)を参照してください。
3. {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに組み込まれている I フレームを使用して、サービスのユーザー・インターフェースを準備します。詳しくは、[管理 I フレームのサポート](./index.html#administration-iframe-support)を参照してください。
4. 登録のために **cloud-cli** コマンド・ライン・インターフェースを使用します。
   1. 次の target コマンドを入力して、{{site.data.keyword.Bluemix_notm}} が実行されているホストおよびポートを指定します。```
	  cloud-cli target https://console.{{site.data.keyword.domainname}}
	  ```
   2. 登録済みのユーザー名およびパスワードを使用して {{site.data.keyword.Bluemix_notm}} にログインします。```
	  cloud-cli login -userID example@bluemix.net -pw password
	  ```
   3. **cloud-cli create-service-broker** コマンドを入力して、サービス・ブローカーを {{site.data.keyword.Bluemix_notm}} に登録します。```
	  cloud-cli create-service-broker sample_broker.json
	  ```
   4. **cf marketplace** コマンドを入力して、サービス・オファリングが存在するかどうかを確認します。```
      cf marketplace
          service       version   provider  plans    description 
          mongodb       2.2       core      100      MongoDB NoSQL database 
          mysql         5.5       core      100      MySQL database      
                        
          Sample        0.1       ace       100      A sample hello world service. Instructional use only, not for use in production.
          postgresql    9.1       core      100      PostgreSQL database (vFabric)                
          rabbitmq      2.8       core      100      RabbitMQ message queue	  
      ```		
      **注:** **cloud-cli** コマンドを入力するたびに {{site.data.keyword.Bluemix_notm}} ターゲットおよび資格情報を指定できますが、他の **cloud-cli** コマンドを実行する前に、{{site.data.keyword.Bluemix_notm}} ターゲットおよびログイン情報を指定する場合、それらのターゲットおよびログイン情報を保存できます。これにより、次回 **cloud-cli** コマンドを入力するときにこれらの情報を指定する必要はなくなります。
	  
	  これで {{site.data.keyword.Bluemix_notm}} 内でこのサービス・オファリングを使用でき、アプリケーションでこれをプロビジョンおよびバインドできます。
	  
	  help オプションを使用することで **cloud-cli** コマンドの使用方法にアクセスできます。```
	  cloud-cli help
	  ```
	  また cloud-cli コマンド・ライン・インターフェースでは、次のコマンドを指定することで、各コマンドの詳しいヘルプを表示できます。```
	  cloud-cli help `commandName`
	  ```
	  
**注:**

サービス登録には制限があります。誰でも自由に新しいサービスを登録できますが、そのサービスを表示できるユーザーについては制限があります。新しいサービスの登録時、そのサービスでワイルドカードは使用しないでください (*acls.wildcards** プロパティーのアスタリスク (***) など)。つまり、新しいサービスは、ユーザーの E メール・アドレスに基づいて明示的にリストされたユーザーに制限されます。サービスを幅広く使用できるようにする場合、`cloudoe-admin@us.ibm.com` メーリング・リストに E メールを送信して、サービスの ACL リストを変更するように要求してください。

ワイルドカードを使用してサービスを登録しようとすると、登録は拒否され、**無許可**エラー・メッセージが返されます。

幅広く使用できるようにするサービスは次の基準を満たしている**必要**があります。
* {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示できるアイコンを含める。
* {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示できる説明テキストを含める。
* **docURL** プロパティーで参照されるドキュメンテーションを含める。
* ユーザーがサービスについて質問できるようにするため、またはサービスで問題が発生したときのために、ドキュメンテーションの一部として連絡先情報を含める。


## cloud-cli コマンド・ライン・インターフェースでのサービス・ブローカーの更新
{: #v2update}

サービス・ブローカーを定義し、それを {{site.data.keyword.Bluemix_notm}} に登録した後、**cloud-cli** コマンド・ライン・インターフェースを使用してそのサービス・ブローカーを更新できます。例えば、サービス・ブローカーの定義 JSON ファイル内のフィールドを更新することや、GET /v2/catalog の JSON 応答内のフィールドを更新することができます。

サービス・ブローカーを更新するには、次のコマンドを使用します。```
cloud-cli update-service-broker serviceBrokerJsonFile
```

このコマンドで、serviceBrokerJsonFile はサービス・ブローカーの JSON ファイルです。

サービス・ブローカーの名前を変更する場合、originalName オプションを使用し、このオプションでサービス・ブローカーの元の名前を指定します。**cloud-cli** コマンドについて詳しくは、[cloud-cli commands](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html) を参照してください。


## 拡張機能の作成
{: #create_extension}

V2 サービスの JSON 定義のメタデータ・セクションに extension ブロックを追加することで、このサービスを拡張機能として宣言できます。

{{site.data.keyword.Bluemix}} ユーザー・インターフェースは、{{site.data.keyword.Bluemix_notm}} 拡張機能をサポートしています。拡張機能は、アプリケーションのコード内でビルディング・ブロックではなくサービスとしてモデル化され、スペース内のアプリケーションに対してサポートを提供します。{{site.data.keyword.Bluemix_notm}} 拡張機能の例には、Agile Planning、Auto-Scaling、APM、MQA などがあります。

**注:** {{site.data.keyword.Bluemix_notm}} は、V1 サービス・ブローカーからの拡張機能の作成をサポートしていません。```
{ "services" :
      [{
          // "bindable" applies to all services, but extensions in particular are more likely to set "bindable" to false
         "bindable" : true,
         "description" : "Extension Description",
         "id" : "a_unique_id1",
         "name" : "My Extension Name",
         // Including "bluemix_extensions" in "tags" is recommended
         "tags" : ["bluemix_extensions"], 
         "metadata" : { 
              // Presence of "extension" block tells the Bluemix user interface the service should be treated as an extension in the UI
              "extension" : {
              },
                ...
          },
        ...
       }
     ]}
```

拡張機能として宣言されたサービスは、通常のサービスとは異なる方法で扱われます。拡張機能のインスタンスはスペース内で 1 つのみ作成できます。これは、cf コマンド・ラインではなく、{{site.data.keyword.Bluemix_notm}}  ユーザー・インターフェースで強制されます。拡張機能をアプリケーションにバインドし、その拡張機能のインスタンスがアプリケーションのスペースで既に作成されている場合、拡張機能の既存のインスタンスが再使用されます。


## 翻訳済みメタデータの指定
{: #translation}

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示される翻訳可能テキストには、サービス、スターター、サポート・プラン、ランタイム・プランのテキスト・ストリングなどがあります。サービスやスターターのメタデータ内のテキスト・ストリングの翻訳後、metadata.i18n フィールドを使用することで、{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに、これらの翻訳済みテキスト・ストリングを表示できます。

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示されるテキスト・ストリングは、次の表にリストされている言語に翻訳できます。翻訳を提供する場合、メタデータで特定言語の言語コードを指定する必要があります。

*表 1. サポートされる言語*

言語 | 言語コード----- | -----
中国語 (簡体字) | zh-Hans
中国語 (繁体字) | zh-Hant
フランス語 | fr
ドイツ語 | de
イタリア語 | it
日本語 | ja
韓国語 | ko
ポルトガル語 (ブラジル) | pt-BR
スペイン語 | es{{site.data.keyword.Bluemix_notm}} で翻訳済みのテキスト・ストリングを表示するには、i18n フィールドを使用する必要があります。このフィールドには、サービスやスターターの定義の翻訳関連のメタデータ・フィールドが含まれます。 

metadata.i18n フィールドに翻訳済みのテキスト・ストリングを追加する場合、次のガイドラインを参照してください。

* metadata.i18n フィールドには、オブジェクト・ハッシュのキーとして言語コードを入力する必要があります。
* 各ロケールのメタデータの構造は、トップレベル・メタデータの構造と同じにする必要があります。これにより、トップレベル・メタデータに含まれる英語のストリングを翻訳済みストリングで上書きできます。これにより、翻訳済みストリングを {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示できます。
* 翻訳済みストリングには、各プランの ID を含める必要があります。これにより、トップレベルで指定されているプランの英語バージョンを翻訳済みプランで上書きできます。

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに翻訳済みのテキスト・ストリングを表示する場合、次のステップを使用します。

* サービス・プロバイダーの場合、サービス・メタデータで翻訳済みのテキスト・ストリングを提供できます。翻訳済みストリングを、サービス定義の GET /v2/catalog の結果の metadata.i18n フィールドで返す必要があります。
  
  metadata.i18n フィールドを含むサービス定義の例として、次の JSON ストリングを参照してください。```
  {
    "services": [
        {
            "id": "766fa866-a950-4b12-adff-c11fa4cf8fdc",
            "name": "cloudamqp",
            "description": "Managed HA RabbitMQ servers in the cloud",
            "metadata": {
                "displayName": "CloudAMQP",
                "longDescription": "Managed, highly available, RabbitMQ clusters in the cloud",
                "providerDisplayName": "84codes AB",
                "instructionsUrl": "/path/to/instructions.md",
                "i18n": {
                    "fr": {
                        "description": ...,
                        "metadata": {
                            "displayName": ...,
                            "longDescription": ...,
                            "providerDisplayName": ...
                            "instructionsUrl": "/path/to/fr/instructions.md"
                        },
                        "plans": [
                            "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                            "description": ...,
                            "metadata": {
                                "bullets": [
                                    "20 GB des messages",
                                    "..."
                                ],
                                "costs": [
                                     {
                                       "unitId": "INSTANCES_PER_MONTH",
                                       "unit": "MONTHLY",
                                       "partNumber": "D15UTLL"
                                      }
                                  ],             
                                "displayName": ...
                            }
                        ],
                        
                    },
                    "de": {
                        ...
                    },
                    ...
                }
            },
            "plans": [
                {
                    "id": "024f3452-67f8-40bc-a724-a20c4ea24b1c",
                    "name": "bunny",
                    "description": "A mid-sided plan",
                    "metadata": {
                        "bullets": [
                            "20 GB of messages",
                            "20 connections"
                        ],
                        "costs": [
                            {
                              "unitId": "INSTANCES_PER_MONTH",
                              "unit": "MONTHLY",
                              "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Big Bunny"
                    }
                }
            ],
            
        }
    ]
  }
  ```
  メタデータ内のテキスト・ストリングに加えて、クイック・スタート・ガイドの翻訳済みバージョンも提供できます。これは、マークダウン・フォーマットです。クイック・スタート・ガイドの英語バージョンの URL は、metadata.instructionsUrl フィールドで指定します。クイック・スタート・ガイドが翻訳されたすべてのロケールのメタデータの metadata.instructionsUrl フィールドで、翻訳済みガイドの URL を指定する必要があります。翻訳済みクイック・スタート・ガイドの URL により、トップレベル・メタデータにある metadata.instructionsUrl フィールドがオーバーライドされます。これにより、翻訳済みクイック・スタート・ガイドが {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示されます。 
  
* スターター・プロバイダーの場合、スターター・メタデータで翻訳済みのテキスト・ストリングを提供できます。この翻訳済みデータを、スターターの metadata.json ファイルの extra フィールドで返します。
   
  extra.i18n フィールドを含むスターター定義の例として、次の JSON ストリングを参照してください。```
  {
    "name": "Java DB Web Starter",
    "description": "This sample application demonstrates how to use Java JPA to connect to a SQL Database.",
    "instructions": "app/instructions.md",
    "extra": {
        "i18n": {
            "fr": {
                "name": ...,
                "description": ...,
                "instructions": "app/fr/instructions.md"
            }
        }
    }
  }
  ```
  
* ビジネス・サポート・システム (BSS) チームがサポート・プランおよびランタイム・プランの翻訳を担当します。サポート・プランおよびランタイム・プランの JSON メタデータは、BSS サーバーが返します。このメタデータの構造は、サービス・プラン・メタデータの構造と同じです。  
  
  {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースに表示されるサポート・プランおよびランタイム・プランについては、[価格設定シート]({{site.data.keyword.pricing_list}})を参照してください。 
  
  

## サービス・ブローカー・リファレンス
{: #service_broker_references}

### サービス・ブローカー定義

サービス・ブローカーを登録するには、サービス・ブローカーを定義する JSON ファイルを用意する必要があります。JSON ファイルのフォーマットを以下に示します。

**name**

サービス・ブローカーの名前。この名前は {{site.data.keyword.Bluemix_notm}} 内で固有でなければなりません。また、名前に対して入力した値は、メトリックおよび分析の生成時にサービスを識別するために使用されます。分析ツールは、この値をサービス・ラベルとして参照します。

**broker_url**

サービス・ブローカー実装の URL。 

**auth_username**

サービス・ブローカーに対する HTTP 基本認証要求に含めるユーザー名。 

**auth_password**

サービス・ブローカーに対する HTTP 基本認証要求に含めるパスワード。 

**owningOrganization**

サービス・ブローカーの更新または削除を許可するマネージャーが所属する組織の名前。

**serviceKeysSupported**

サービス・キー API をサポートするかどうかを示すブール値。Bluemix の外部でサービスを使用できるようにするために、サービス・キー API が使用されます。デフォルト値は	false です。

**visibilities**

サービス・ブローカーが提供するサービスを表示できる組織に関する情報。 
* **visibilities.organization_name**
    
	サービスを表示できる組織の名前。 
* **visibilities.plan_id**
	   
	組織に表示するプラン。プランが指定されていない場合、組織は、サービス・ブローカーが提供するすべてのサービスおよびプランを表示できます。

**use_bss_proxy**

(オプション) サービス・ブローカーに他の地域からアクセスできるようにするかどうかを示すブール値。値 **true** を指定すると、サービス・ブローカーに他の地域からアクセスできます。デフォルト値は **false** です。 	   


**region_broker_urls**

(オプション) 特定専用地域用のサービス・ブローカーの名前および URL を含むストリングの配列。サービスを専用サービスとして使用できるようにする場合に限り、このフィールドを指定します。

**partner**

(オプション) サービスにすべての公的地域からアクセスできるようにするかどうかを示すブール値。このフィールドは、サード・パーティー・サービス・プロバイダーのサービス・ブローカーで使用します。デフォルト値は false です。

以下は、サービス・ブローカー定義のコードの例です。```
{
    "name" : "MyServiceBroker",
    "broker_url" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net",
    "auth_username": "ServiceBrokerUser",
    "auth_password": "ServiceBrokerPassword",
    "visibilities" : [
        {"organization_name" : "myOrganization"}
    ],
    "use_bss_proxy": true,
    "region_broker_urls": [ 
        {"name": "citi:production:us-south", "region_broker_url": "https://serviceBrokerImpl.citi-ng.bluemix.net"}
    ]
}
```


### REST API リファレンス
{: #v2build}

Bluemix は Cloud Foundry V2 サービス・ブローカー API をサポートしています。Bluemix は、Enable エンドポイントおよび State エンドポイントを含む拡張 API も提供しています。 

Bluemix がサポートする次の API エンドポイント間で、Catalog、Provision、および Deprovision エンドポイントを実装する必要があります。Catalog エンドポイント実装時に bindable パラメーターを true に設定した場合、Bind エンドポイントと Unbind エンドポイントも実装する必要があります。 

[**Catalog (GET)**](./index.html/catalog-get-)

サービス・カタログにデータを設定するサービス・ブローカーに関する情報を取得します。このエンドポイントを実装する場合、Bluemix ユーザー・インターフェースおよび cf コマンド・ライン・インターフェースに表示するサービス情報を指定する必要があります。

[**Provision (PUT)**](./index.html/provision-put-)

サービス・インスタンスを作成します。

[**Deprovision (DELETE)**]()

サービス・インスタンスを削除します。

[**Bind (PUT)**]()

アプリケーションがインスタンスにアクセスするために必要な資格情報を作成して、サービス・インスタンスとアプリケーションを接続します。

[**Unbind (DELETE)**]()

アプリケーションからサービス・インスタンスを切断します。

[**Enable (PUT)**]()

サービス・インスタンスを有効にします。

[**State (GET)**]()

サービス・インスタンスの状態を取得します。



#### Catalog (GET)
Catalog は、サービス・ブローカーに対して実装する必要のある最初のエンドポイントです。`cloud-cli create-service-broker` または `cloud-cli update-service-broker` を発行すると、Bluemix はこのエンドポイントを呼び出します。

**URL of Catalog (GET)**

サービス・ブローカー実装内で呼び出される GET メソッドの URL パスは `/v2/catalog` です。

**Response of Catalog (GET)**

GET /v2/catalog の JSON 応答で、サービスおよびサービス・プランの定義 (Bluemix ユーザー・インターフェースに表示するサービス情報を含む) を提供する必要があります。

状況コード 200 は、Bluemix で処理される正常な値を示します。

GET /v2/catalog の JSON 応答は、サービス・フィールド内のサービス定義およびサービス・プラン定義の配列で構成されます。すべての必須フィールドが含まれる JSON サンプルについては、『Catalog (GET) 応答の JSON サンプル』を参照してください。

サービス定義のすべての JSON フィールドについて詳しくは、次のリストを参照してください。

* **name**
	
	コマンド・ライン・インターフェースに表示されるサービスの名前。この名前は Bluemix 内で固有でなければなりません。また、この名前では小文字を使用する必要があり、スペースを含めることはできません。サービスを Bluemix に登録した後、サービスの名前は変更できません。

* **id**
    
	サービスの ID。この ID は Bluemix 内で固有でなければならず、また GUID (グローバル固有 ID) でなければなりません。サービスを Bluemix に登録した後、サービスの ID は変更できません。

* **bindable**
    
	サービス・インスタンスをアプリケーションにバインドできるかどうかを示すブール値。

* **description**
    
	**cf marketplace** コマンドを使用したとき、または Bluemix ユーザー・インターフェースのカタログ内のサービス・アイコンにマウス・ポインターを合わせたときに表示されるサービスの説明。説明のための単一の文または句を追加できます。	
 
* **metadata**
    
	Bluemix ユーザー・インターフェースのサービス詳細ページに表示されるサービス・メタデータ。有効な JSON が必要です。 
    
	metadata フィールドに含まれる以下のフィールドを指定できます。
	
	* **displayName**
	     
		 サービスの Bluemix ユーザー・インターフェースに表示される名前。この名前はスペースを含めて 19 文字まで表示可能で、その文字数を超えると切り捨てられます。
  
    * **providerDisplayName**
	    
		サービス・プロバイダーの名前。
		
	* **longDescription**
	
	    サービスの詳細な説明。少なくとも 2 つの文章を使用して詳細説明を作成するよう検討してください。
		
	* **type**
	   
	    サービスのタイプ。このフィールドに使用できる値は以下のとおりです。
		
		* **referral**
		   
		    後述します...
			
		* **dedicated**
		
		    専用環境で使用可能なサービス。専用環境について詳しくは、[Bluemix Dedicated](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch) を参照してください。
		
		* **local**
		
		    ローカル環境で使用可能なサービス。ローカル環境について詳しくは、[Bluemix Local](https://www.stage1.eu-gb.bluemix.net/docs/overview/overview.html#ov_arch) を参照してください。
  
        * **partner**
		    
			IBM 以外の企業が提供するサード・パーティー・サービス。
			
    * **bullets**
	
	    各サービスに対して並べて表示される一連のストリング。bullets を使用して、詳細説明に加えて情報を提供できます。
bullets フィールドには、少なくとも 2 つのリスト項目エレメントが含まれていなければなりません。それぞれのリスト項目エレメントには以下のフィールドが含まれます。
		
		* **title**
		
		    リスト項目のタイトル。
			
		* **description**
		
		    リスト項目の説明。
			
	* **imageUrl**
	    
		大きな画像 (50 x 50 ピクセル) の URL。Bluemix ユーザー・インターフェースで使用されるサービス用イメージについて詳しくは、[サービス・アイコン・イメージ](./index.html#service-icon-images)を参照してください。
  
    * **smallImageUrl**
	
	    小さな画像 (24 x 24 ピクセル) の URL。
		
    * **mediumImageUrl**
	
	    中くらいの画像 (32 x 32 ピクセル) の URL。
		
    * **featuredImageUrl**
	    
		フィーチャー画像 (64 x 64 ピクセル) の URL。
		
	* **documentationUrl**
	
	    サービスに関する文書の URL。 
		
	* **instructionsUrl**
	
	    サービスの使用法に関するユーザー向けの説明を含むマークダウン・ファイルの URL。Bluemix ユーザー・インターフェースにサービスの説明を追加する方法について詳しくは、「クイック・スタート・ガイド」(./index.html#quick-start-guide) を参照してください。
  
    * **termsUrl**
  
        ご使用条件を含む PDF ファイルの URL。
		
    * **locationDisplayName**
	
	    サービスがホストされる地理的位置を指定するストリング。Bluemix 地域の 1 つでホストされるサービスに対し、その地域の Bluemix 表示名 (例えば、**米国南部**、**英国** など) を指定します。
    
	* **media**
	   
	    (オプション) Bluemix ユーザー・インターフェースにサービスを紹介するビデオおよび画面キャプチャーを表示するための一連のエレメント。media エレメントには以下のフィールドが含まれます。
		
		* **type**
		    
			media エレメントのタイプ。media のタイプとして次のオプションを指定できます。画面キャプチャーの場合は `image` オプションを使用し、ビデオの場合は youtube オプションおよび video オプションを使用します。
         
		    * **image**
			    
				画面キャプチャー。サービスのユーザー・インターフェースが I フレーム内にある場合、周囲の Bluemix ユーザー・インターフェースを画面キャプチャーに含めないでください。
				
				**注:** media タイプとして image を使用し、サービスの画面キャプチャーを提供する場合、次のガイドラインに従う必要があります。
				* 各サービスにつき 1 枚から 5 枚の画面キャプチャーを指定します。
				* 各画面キャプチャーにつき、1 枚のフルサイズ画像と 1 枚のサムネール画像を含めます。画面キャプチャーのサムネール画像のサイズは、フルサイズ画像より小さくなければなりません。
				* フルサイズ画像の幅は 640 ピクセル以上にしてください。
				* フルサイズ画像の最大サイズは 800 KB です。
				* サムネール画像の大きさは最小で 500x300 ピクセルです。サムネール画像の縦横比は 5:3 です。
				* サムネール画像の最大サイズは 300 KB です。
				* フルサイズ画像とサムネール画像の両方に対し、PNG ファイルを使用します。
  
            * **youtube**
			
			    YouTube により組み込まれたビデオ。このフィールドには、YouTube のビデオの**「組み込み (Embed)」**タブに記載された URL を指定します。 
				
				ビデオは、サービスのチュートリアルではなく、概要を提供します。YouTube のビデオは再使用可能で、インターネット接続に応じて画質を調節できます。
YouTube ビデオのサンプルについては、[「Exploring IBM Watson」](http://www.youtube.com/watch?v=6aKg_0t_zms)を参照してください。
				
			* **video**
			
			    YouTube 以外のサード・パーティー・サイトでホストされているビデオ。このフィールドでは、ビデオ用の MP4 ファイルと OGG ファイルの両方を指定します。 
			
            **注:** media タイプとして youtube または video を使用し、サービスのビデオを提供する場合、次のガイドラインに従う必要があります。	
                * ビデオ解像度は最低でも 720p にしてください。
				* ビデオの縦横比は 16:9 にしてください。
				* ビデオの大きさは最小で 640x360 ピクセルにしてください。
				* ビデオの長さは 1 分から 3 分にしてください。
				* ビデオのサムネール画像も提供してください。サムネール画像の最大サイズは 300k です。サムネール画像の大きさは最小で 500x300 ピクセル、サムネール画像の縦横比は 5:3 です。
				* ビデオの音声品質は最低でも 160 kbps にしてください。
				
	* **thumbnailUrl**
        
        media エレメント用のプレビュー画像の URL。

    * **url**
    
        画面キャプチャーまたは YouTube ビデオの URL。

    * **source**

        YouTube ではホストされていないビデオのソース。配列された source エレメントのそれぞれに、以下のフィールドが含まれます。

        * **type**

            ビデオのタイプ。例えば **video/mp4** や	**video/ogg** など、HTML5 でサポートされるビデオ・フォーマットでなければなりません。 	

        * **url**
        
            ビデオの URL。

    * **caption**

        media エレメントのキャプション。キャプションは、media エレメントの理解が困難なユーザーを補助するのに役立ちます。
 
        キャプションで media エレメントの内容について説明する必要があります。例えば、「このビデオでは、プッシュ・サービスとは何かについて説明します。また、プッシュ通知を使用して、適切なタイミングで適切な場所にいる適切なユーザーに、関連するコンテンツを送信する方法について説明します。」などと記述します。

        キャプションの最大長は 350 文字です。

    * **serviceKeysSupported**
  
        サービス・キー API をサポートするかどうかを示すブール値。Bluemix の外部でサービスを使用できるようにするために、サービス・キー API が使用されます。デフォルト値は	false です。

    * **plan_updateable**

        サービスでプランの変更をサポートするかどうかを示すブール値。デフォルト値は	false です。

    * **embeddableDashboard**

        (オプション) Bluemix ユーザー・インターフェースにサービス・ダッシュボードをどのように表示するか指定するフィールド。このフィールドを指定しない場合、ダッシュボードは組み込まれますが幅が最小 960px に制限され、またこのダッシュボードには iframe の周りに水平方向の埋め込みが追加されます。 

        このフィールドに使用できる値は以下のとおりです。

        * **true**
   
            最小幅なしの応答 I フレームを使用して、Bluemix ユーザー・インターフェースにサービス・ダッシュボードを埋め込むことを指定します。この値を	true に設定すると、embeddableDashboardFullWidth フィールドを指定できます。

        * **false**
  
            Bluemix ユーザー・インターフェースにサービス・ダッシュボードを埋め込まないことを指定します。その代わり、サービス・インスタンスのユーザー・インターフェースでボタンをクリックすると、別のブラウザー・タブでダッシュボードを開くことができます。

        * **drilldown**
  
            この値を指定すると、アプリケーションの概要ページからサービス・インスタンスのタイルをクリックしたとき、または Bluemix ダッシュボードでナビゲーション・ツリーからサービス・インスタンスをクリックしたときに、サービス・ダッシュボードが同じブラウザー・タブで開きます。 

        * **launch**

            この値を指定すると、アプリケーションの概要ページからサービス・インスタンスのタイルをクリックしたとき、または Bluemix ダッシュボードでナビゲーション・ツリーからサービス・インスタンスをクリックしたときに、サービス・ダッシュボードが新規ブラウザー・タブで開きます。

            **ヒント:** 新規ブラウザー・タブに**「戻る (Go Back)」**ボタンを表示するには、サービス・ダッシュボードの `ace_config` パラメーターで redirect を使用することで、リダイレクト URL を指定します。For more information about the `ace_config` parameter, see [Administration iframe support](./index.html#administration-iframe-support). 		
				
    * **embeddableDashboardFullWidth**

        (オプション) サービス・ダッシュボードがブラウザーのフル幅いっぱいになるどうかを指定するブール値。このフィールドを指定しない場合、この値は false に設定されます。値 false は、サービス・ダッシュボードでブラウザーの幅がいっぱいにならないことを意味しています。この値は、カタログのサービス詳細ページには影響しません。  
  
        **Important:** For the value of the embeddableDashboardFullWidth field that you specify to take effect, you must set the value of the embeddableDashboard field to **true**.
  
    * **notCreatable**
   
        (Optional) A Boolean value that indicates whether instances for the service can be created from the Bluemix user interface and from the cf command line interface. A value of true means that service instances cannot be created either from the Bluemix user interface or from the cf command line interface. デフォルト値は	false です。

    * **notCreatableMessage**	

        (Optional) A message that is displayed in the Bluemix user interface if service instances cannot be created. If you do not specify this field, the following default message will be displayed: `To be notified when it is available, confirm your e-mail address, or enter a different email address`.
  
    * **notCreatableRobotMessage**

        (Optional) A message that is displayed in the speech bubble of the service details page in the Bluemix user interface. このメッセージは、このサービスを使用できない原因となる問題やその他の理由が存在する可能性があることを示すために使用されます。
理由を説明するためのメッセージを指定できます。If you do not specify this field, the following default message will be displayed: `This service is currently unavailable`.

    * **apiReferenceUrl**

        (オプション) **「カタログ」**のサービス詳細ページにおける**「API 参照」**エリア内の iframe の URL。 
  
    * **sdkDownloadUrl **

        (オプション) **「SDK のダウンロード」**ボタンをクリックすると開く Web ページの URL。**「SDK のダウンロード」**ボタンは、**「ダッシュボード」**内のアプリケーション概要ページのサービス・タイルに配置されています。この Web ページは、新規ブラウザー・タブで開きます。  
 
    * **userDefinedService**

        ユーザー定義サービスのメタデータ。 
        * **parameters**
	
	        サービス・インスタンスの作成時にサービスによって定義される一連の鍵と値のペア。 
		
		    * **parameters.name**
		    
			    パラメーターの鍵。

            * **parameters.type**
		   
		        The type of input field that is displayed by the Bluemix user interface. この値はテキストにすることもパスワードにすることもできます。
			
		    * **parameters.value**
		
		        パラメーターのデフォルト値。
			
		    * **parameters.displayname**
		
		        表示されるパラメーターの名前。
			
		    * **parameters.invalidmessage**
		
		        テキスト・ボックスのコンテンツが無効の場合に表示されるメッセージ。
			
		    * **parameters.description**
		
		        パラメーターの値に関してユーザーを支援するために表示される、パラメーターの説明。
			
		    * **parameters.required**
		
		        A Boolean value that indicates whether the parameter must be entered in the Bluemix user interface.

            * **parameters.pattern**
		
		        値をチェックする際に照らし合わせる正規表現を指定します。 
			
		    * **parameters.placeholder**
		
		        期待される値について説明する短いヒントを指定します。
			
		    * **parameters.readonly**
		
		        パラメーターの値が表示のみ可能でユーザーによる変更が不可であるかどうかを示すブール値。デフォルト値は	false です。
			
		    * **parameters.hidden**
		
		        鍵と値のペアをユーザーに対して非表示にするかどうかを示すブール値。デフォルト値は	false です。
			
	    For sample metadata that includes user-defined parameters for a user-defined service, see the following JSON string:
		
	    ```
        {
           ...
           "metadata": {
"featuredDescription": "A user-provided service. Instructional use only, not for use in production.",
             "isFeatured": false,
             "docURL": "http://www.yourserver.com:7080/doc/Sample/RESTApi.html",
             "userDefinedService": {
                 "dashboard_url": "https://example.com/dashboard/", 
                 "parametersDescription": "A contextual description of the parameters, example would be: You must <a href=\"http://ibm.com\" target=\"_blank\">register</a> before you use the service.",
                 "parameters": [
                     {
                        "name": "host",
                        "type": "text",
                        "value": "example.com",
                        "readonly": true,
                        "hidden": true
                     },
                     {
                        "name": "userid",
                        "displayname": "User id",
                        "type": "text",
                        "description": "The user id that is used to access the service.",
                        "invalidmessage": "Not a valid email address",
                        "pattern": "^[_A-Za-z0-9-\\+]+(\\.[_A-Za-z0-9-]+)*@[A-Za-z0-9-]+(\\.[A-Za-z0-9]+)*(\\.[A-Za-z]{2,})$",
                        "placeholder": "email@example.com"
                     },
                     {
                        "name": "password",
                        "type": "password"
                     },
                     {
                        "name": "description",
                        "required": false
                     }
                 ]
             }
           }
        }
        ```

* **tags**

    Arrays of strings that indicate the categories, the providers, and the release readiness of services. 
	
	* The following tags determine the categories that services belong to. 
	  
	   Because a service can belong to only one category, you can select only one of the following category tags for each service. However, you can couple the category tag of a service with tags that specify the provider and the release readiness of the service, such as **ibm_created** and **ibm_beta**. 
	   
	   If a service does not have any of the following category tags, it will be displayed in the **web_and_app** category. 
	   
	    * **mobile**
	       
		   Mobile services.
		   
		* **web_and_app**
		
		   Web application services.
		   
		* **dev_ops**
		
		   DevOps Services.
		   
		* **integration**
		
		   Integration services.
		   
		* **data_management**
		
		    Data management services.
			
	    * **big_data**
		
		    Big data services.
			
		* **security**
		
		    Security services.
			
	    * **business_analytics**
		
		    Analytics services.
			
		* **watson**
		
		    Services for building cognitive applications.
			
	    * **internet_of_things**
		
		    Services for Internet of Things.
			
	    * **payments**
		
		    Services to collect and track payments.
			
		* **private**
		
		    Private services.
			
	* (Optional) The following tags indicate the providers of services. The default value is **ibm_community**.
	
	    * **ibm_created**
		
		    The service is provided by IBM. If a service already specified this value, the value is preserved. 
			
		* **ibm_third_party**
		
		    The service is provided by third-party partners. This value can be set only by an administrator. If a service already specified this value, the value is preserved. 
			
		* **ibm_community**
		
		    The service is provided by open source communities. This value can be set only by an administrator. If a service already specified this value, the value is preserved. 
			
		* **ibm_private**
		
		    The service is a private service that is visible only to certain users or organizations.
			
	* (Optional) The following tags indicate the release readiness of services. The default value is **ibm_release**.
	
	    * **ibm_experimental**
		
		    The service is experimental and is not ready for production. The service provider wants users to try the service, get feedback, and then decide whether they will continue to work on the service. The service provider does not provide support or guarantee for the experimental service. The service provider can remove the service from the catalog at any time.
			
			Services that have the ibm_experimental tag are labeled with **Experimental** in the Bluemix Labs Catalog. 
			
			The ibm_experimental tag takes precedence over other tags. For example, if a service has the ibm_created tag and the ibm_experimental tag at the same time, the service will be labeled with **Experimental** and displayed in the Bluemix Labs Catalog.
			
			**Note:** You can use only one of the tags that are used to indicate release readiness (ibm_experimental, ibm_beta, and ibm_release) at a time.
			
		* **ibm_beta**
		
		    The service is a beta release. Beta versions of services must include this tag.
			
		* **ibm_release**
		
		    The service is released. The default value if ibm_beta is not specified. 
			
* **plans**

    An array of service plan definitions. Each array entry of the plans field consists of the following fields: 
    
	* **name**

        The name of the service plan that is used in the cf command line interface. For example, the plan name is displayed in the output of the **cf marketplace** command. The plan name must be in lowercase letters and must not contain spaces, and it must be unique within the service.	
		
	* **description**
	
	    The description of the service plan. The description is displayed after you select a plan on the service details page in the Bluemix catalog.
		
	* **free**
	
	    A Boolean value that indicates whether the service plan is free. The default value is true. 
		
	* **id**
	
	    The ID of the service plan. The ID must be unique within Bluemix, and it must be a GUID. 
		
	* **metadata**
	 
	    The service plan metadata that is displayed in the Bluemix catalog and in the pricing sheet. The metadata field is an optional field. You can specify the following fields in the metadata field:
		
		* **displayName**
		
		    The name of the plan that is displayed in the Bluemix user interface. This name is displayed both on the service details page in the catalog and on the pricing sheet.
			
			**Notes:**
			
			* Capitalize only the first letter of the plan name; for example, **Small**, or **Month**.
            * Do not use **Default** as the default plan name. Use **Standard** instead.			
	   
	    * **type**
		
		    The type of the plan. このフィールドに使用できる値は以下のとおりです。
			
			* **subscription**
			
			    A subscription plan.
				
	    * **bullets**
		
		    A description of the resources that can be used with the plan. The description is displayed in the **Features** column on the service details page of the catalog and on the pricing sheet. The following example shows information that you might specify in the bullets field:
			
			```
			"bullets": ["1 free app with 3 free devices per Bluemix account."],
			```
			**Notes:**
			
			* For a service plan that is free, in the bullets field, you must specify the quantity of resources that are provided free of charge, and whether usage of the free resources is applied at the Bluemix account level or the service instance level.
			* Use sentence style capitalization for the text in each bullet. Capitalize only the initial letter of the first word in the text and other words that require capitalization, such as proper nouns (for example, the service name). Always capitalize the first word, and do not capitalize every word.
			* Sentence fragments (phrases) are acceptable. Avoid constructs such as "This is a free plan for..." when "Free plan for..." will do.
			* Insert a period at the end of each phrase or sentence in the text. 
			* Do not specify price details in the bullets field, such as **The first $5.00 of usage is free**.
			* Do not use the word "via". Instead, use one of the following synonyms: "across"," "along", "by","from", "on", or "through". 
			* Do not abbreviate "maximum" as "max".
			* If you use parentheses to contain a complete, separate sentence, insert a period inside the parentheses. If the parenthetical text is not a complete sentence, do not insert a period inside the parentheses.

        * **costs**
		
		    The cost information about the service that is displayed in the Price column on the service details page of the catalog and on the pricing sheet. Each array entry contains the following fields:
			
			* **unitId**
			    
				The ID of the unit. Use the plural form and capitalize all letters. For free plans, this field is optional.
				
				The value of this field is the same as the aggregation name that you specify in the definition of your service resource usage. For more information about the definition of resource usage for your services, see [Setting up Bluemix metering](https://www.stage1.eu-gb.bluemix.net/docs/services/reporting_resource_usage.html#metering).
				
				**Note:** For free plans, if your service does not send usage information, you do not need to specify the unitId field for this free plan.

            * **unit**
			
			    The metric that is used for calculating the charges of the service. The value of this field is used in the Bluemix user interface to represent the charge metric. For example, **$50.00 / GB**, where GB is the unit. For free plans, this field is optional.

				**Notes:**
     
	            * Capitalize only the first letter of the unit. Capitalize all letters of the unit only for abbreviations, such as GB, API, and so on.
				* For free plans, if your service does not send usage information, you do not need to specify the unit field for this free plan.
				
			* **partNumber**
 
                The part_number identifier that is used by the IBM Distributed Software (DSW) billing system. Check with your PLM about the value of this field. For free plans, this field is optional.
            
		* **paidOnly**

            (Optional) A Boolean value that indicates whether this service plan is available for Bluemix pay accounts only. A value of **true** means that the service plan is for pay accounts only and cannot be added to trial accounts. A value of **false** means that the service plan can be added to both pay accounts and trial accounts. The default value is **false**.	
        
        The following example shows how the JSON code in the plans field is mapped to the information that is displayed on the catalog details page and the pricing sheet: 
         
        ![Sample service plans](images/plan_metadata.png)		 

		
		
**Catalog (GET) 応答の JSON サンプル**

```
{
    "services": [
        {
            "bindable": true,
            "description": "Cool Service is a data warehousing and analytics solution.",
            "id": "cool-service-id",
            "name": "coolservice",
            "tags": [
                "business_analytics",
                "ibm_created"
            ],
            "metadata": {
                "displayName": "Cool Service",
                "providerDisplayName": "IBM",
                "longDescription": "Cool Service is a data warehousing and analytics solution. You can quickly move your data into a next-generation columnar in-memory database and start running complex analytical queries.",
                "bullets": [
                    {
                        "title": "Fast and Simple",
                        "description": "Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
                    },
                    {
                        "title": "Connectivity",
                        "description": "Cool Service is built to let you connect easily and to all of your services and applications. You can start analyzing your data right away with familiar tools."
                    }
                ],
                "featuredImageUrl": "http://path/to/icon_64x64.png",
                "imageUrl": "http://path/to/icon_50x50.png",
                "mediumImageUrl": "http://path/to/icon_32x32.png",
                "smallImageUrl": "http://path/to/icon_24x24.png",
                "documentationUrl": "http://path/to/documentation.html",
                "instructionsUrl": "http://path/to/servicesample.md",
                "termsUrl": "http://path/to/terms_of_agreement.pdf",
                "media": [{
			"type": "youtube",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/youtube/video",
			"caption": "Using Cool Service in 60 Seconds"
		},
		{
			"type": "image",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/image_file.png",
			"caption": "Cool Service connects applications"
		},
		{
			"type": "video",
			"thumbnailUrl": "http://path/to/thumb.png",
			"caption": "Cool Service works with tables",
			"source": [{
				"type": "video/mp4",
				"url": "http://path/to/video_file.mp4"
			},
			{
				"type": "video/ogg",
				"url": "http://path/to/video_file.ogg"
			}],
			
		},
		]
            },
            "plans": [
                {
                    "name": "smallplan",
                    "description": "Dedicated schema and tablespace per service instance on a shared server. 1GB and 10GB of compressed database storage can hold up to 5GB and 50GB of uncompressed data respectively based on typical compression ratios.",
                    "free": false,
                    "id": "cool-service-plan-id",
                    "metadata": {
                        "bullets": [
                            "1 GB Min per instance. 10 GB Max per instance."
                        ],
                        "costs": [
                            {
                                "unitId": "INSTANCES_PER_MONTH",
                                "unit": "MONTHLY",
                                "partNumber": "D15UTLL"
                            }
                        ],
                        "displayName": "Small"
                    }
                }
            ]
        }
    ]
}
```


The following example shows how the JSON response of GET /v2/catalog is mapped to the service details page in the Bluemix catalog:

![Sample service details page](images/metadata.png)


**Test for Catalog (GET)**

You can test your Catalog endpoint by using the following command:

```
curl -X GET -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e6dfc74d60e346c399bcfe04b1c2e760::a7a1bb74-5b5f-4356-ba70-eef0e36cf230"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/v2/catalog
```


#### Provision (PUT)

You can use the Provision REST API endpoint to create service instances.

**URL of Provision (PUT)**

  The URL path for the PUT method that is invoked within the service broker implementation is `/v2/service_instances/:instance_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance.

**Request of Provision (PUT)**

  The fields that are passed into PUT `/v2/service_instances/:instance_id` within the JSON body are as follows:

   * **organization_guid**
        
       The GUID of the organization for **cf create-service**. 		

   * **plan_id**
   
       The ID of the service plan that is chosen as part of **cf create-service**. This is one of the IDs of service plans from Get catalog. 

   * **service_id**
   
       The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog. 

   * **space_guid**
   
       The GUID of the space for **cf create-service**. 

**Sample JSON of the Provision (PUT) request**

```
{
  "organization_guid" : "a595cc4e-017a-437d-8a6f-7feb2fa0c88b",
  "plan_id"           : "Test V2 Service Broker Plan ID",
  "service_id"        : "Test V2 Service Broker ID",
  "space_guid"        : "af766c42-2f3f-41cf-8e4b-0c0761ef9d5c",
}
```

**Response of Provision (PUT)**

  A status code of 200 or 201 is the expected successful value that is handled by the Cloud Controller code. A status code of 409 signifies that the provisioning has already been done for this URL.
  
  The fields that are returned from PUT /v2/service_instances/:instance_id within the JSON result are as follows:
  
   * **dashboard_url**
   
       The URL for a dashboard or a user interface for this service instance. For information about the iframe support for this dashboard or user interface, see [Administration iframe support](./index.html#administration-iframe-support).
	   
**Sample JSON of the Provision (PUT) response**

```
{
  "dashboard_url" : "http://www.ibm.com"
}
```

**Test for Provision (PUT)**

You can test your Provision endpoint by using the following command:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:e81d9e214b9b4a13a843b1da12caa0f4::598af59e-b2b8-4ecd-bdea-b9cf20114509"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"organization_guid\":\"e6274fbc-e7d9-448f-a025-b2dbbe654edb\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c1e1e8-76a4-4137-a02e-fed2fc04ba64\",
\"space_guid\":\"b0e72e12-205e-4984-8835-991d51ba804a\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

#### Bind (PUT)
  
You can use the Bind REST API endpoint to create credentials to access the service instance by an application.

**URL of Bind (PUT)**

The URL path for the PUT that is invoked within the service broker implementation is `/v2/service_instances/:instance_id/service_bindings/:binding_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance, and `:binding_id` is the ID that is generated by the Cloud Controller for the service binding.	   
	   
**Request of Bind (PUT)**

The fields that are passed into PUT /v2/service_instances/:instance_id/service_bindings/:binding_id within the JSON body are as follows:

   * **app_guid**

       The GUID of the bound application. 
    
   * **plan_id**

        The ID of the plan that is chosen as part of **cf create-service**. This is one of the IDs of service plans from Get catalog. 

   * **service_id**		
   
       The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog. 
	   
**Sample JSON of the Bind (PUT) request**

```
{
  "app_guid" : "80e0caaa-4145-4f2a-9bf8-1ab00fff1766",
  "plan_id"           : "Test V2 Service Broker Plan ID",
  "service_id"        : "Test V2 Service Broker ID"
}
```

**Response of Bind (PUT)**

A status code of 200 or 201 is the expected successful value that is handled by the Cloud Controller code. A status code of 409 signifies the binding has already been done for this URL.

The fields that are returned from PUT /v2/service_instances/:instance_id/service_bindings/:binding_id within the JSON result are as follows:

  * **credentials**
  
      The hash value of credentials.
	  
**Sample JSON of the Bind (PUT) response**

```
{
  "credentials"   :
  {
    "url"      : "http://10.0.1.2:12345"
    "userid"   : "8401a824-1da7-4114-8664-2460db21661a",
    "password" : "b98e9690-c5e7-405f-9ef6-d6fa36afbaba"
  }
}
```

**Test for Bind (PUT)**

You can test your Bind endpoint by using the following command:
```
curl -X PUT -H "Accept:application/json" -H
"Content-Type:application/json" -H "X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:9449b70048434b3aa7106377cfb463e4::e9710444-5968-4895-9cf4-ae78d69bc168"
-u "TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"app_guid\":\"d3f16a48-8bd1-4aab-a7de-e2a22ad38292\",
\"plan_id\":\"9a4194b0-4314-4188-a862-eaa60355beae\",
\"service_id\":\"8c14e1e8-76a4-4137-a02e-fed2fc04ba64\"}"
http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210
```

#### Unbind (DELETE)

**URL of Unbind (DELETE)**

The URL path for the DELETE that is invoked within the service broker implementation is `/v2/service_instances/:instance_id/service_bindings/:binding_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance, and `:binding_id` is the ID that is generated by the Cloud Controller for the service binding.

**Request of Unbind (DELETE)**

The fields that are passed into `DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id` as query parameters are as follows:

   * **plan_id**
   
       The ID of the plan that is chosen as part of **cf create-service**. This is one of the service plan IDs from Get catalog. 

    * **service_id**
    
        The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog.	
		
		
**Response of Unbind (DELETE)**

A status code of 200 is the expected successful value that is handled by the Cloud Controller code. A status code of 410 signifies that the resource has already been deleted.

Currently no fields are returned from DELETE /v2/service_instances/:instance_id/service_bindings/:binding_id, but an empty hash is suggested for future expansion in either the 200 or the 410 case.

**Sample JSON of the Unbind (DELETE) response**

```
{
}
```

**Test for Unbind (DELETE)**

You can test your Unbind endpoint by using the following command:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:33021f6327374feb9b21fd66e1475aa7::fa04ffe3-0ee4-459c-8715-6c1779318955"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff/service_bindings/1eef45f2-6151-4394-a958-590a9be09210?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```

#### Deprovision (DELETE)

**URL of Deprovision (DELETE)**

The URL path for the DELETE invoked within the service broker implementation is `/v2/service_instances/:instance_id`, where `:instance_id` is the ID that is generated by the Cloud Controller for the service instance.

**Request of Deprovision (DELETE)**

The fields that are passed into DELETE /v2/service_instances/:instance_id as query parameters are as follows:

   * **plan_id**
	
	    The ID of the plan that is chosen as part of **cf create-service**. This is one of the service plans IDs from Get catalog. 
		
   * **service_id**
	
	    The ID of the service offering as part of **cf create-service**. This is one of the service IDs from Get catalog.
		
**Response of Deprovision (DELETE)**

A status code of 200 is the expected successful value that is handled by the Cloud Controller code. A status code of 410 signifies that the resource has already been deleted.

Currently no fields are returned from DELETE /v2/service_instances/:instance_id, but an empty hash is suggested for future expansion in either the 200 or the 410 case.

**Sample JSON of the Deprovision (DELETE) response**

```
{
}
```

**Test for Deprovision (DELETE)**

You can test your Unbind endpoint by using the following command:

```
curl -X DELETE -H "Accept:application/json" -H
"X-Broker-Api-Version:2.3" -H
"X-VCAP-Request-ID:eb8d14f15efc4832beb65220b2cb48a8::3e3e2108-d7e4-498a-9180-68588153208f"
-u "TestServiceBrokerUser:TestServiceBrokerPassword"
"http://localhost:3000/v2/service_instances/3d06cbfa-e3d3-438c-b8960f0e8f242ff?plan_id=9a4194b0-4314-4188-a862-eaa60355beae&service_id=8c14e1e8-76a4-4137-a02e-fed2fc04ba64"
```
	

#### Enable (PUT)

This is an endpoint of the extension API that is provided by Bluemix. This endpoint supports the enablement or disablement of a service instance.

**URL of Enable (PUT)**

The URL path for the PUT method for the service broker implementation is `/bluemix_v1/service_instances/:instance_id`, where `:instance_id` is the ID generated by the Cloud Controller for the service instance.
	
**Request of Enable (PUT)**

The fields that are passed into PUT /bluemix_v1/service_instances/:instance_id within the JSON body are as follows:

   * **enabled**
       
       A Boolean value that indicates whether the service instance needs to be enabled.

**Sample JSON of the Enable (PUT) request**

```
{
  "enabled" : true
}
```

**Response of Enable (PUT)**

A status code of 204 is the expected successful value.

**Test for Enable (PUT)**

You can test your Enable endpoint by using the following command:

```
curl -X PUT -H "Content-Type:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword" -d
"{\"enabled\":true}"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```


#### State (GET)

This is an endpoint of the extension API that is provided by Bluemix. This endpoint supports retrieving the current state of a service instance.

**URL of State (GET)**

The URL path for the GET method for the service broker implementation is `/bluemix_v1/service_instances/:instance_id`, where `:instance_id` is the ID generated by the Cloud Controller for the service instance.	   

**Response of State (GET)**

A status code of 200 is the expected successful value. The fields that are returned from GET /bluemix_v1/service_instances/:instance_id within the JSON result are as follows:

   * **enabled**
       
	   Whether the service instance is enabled or not.
	  
   * **state**
   
       The value is STARTING, STARTED, STOPPING, or STOPPED.
	   
   * **message**
   
       The string for details.
	   
**Sample JSON of the State (GET) response**

```
{
  "enabled" : true,
  "state" : "STARTED",
  "message" : "Service instance is enabled and started"
}
```

**Test for State (GET)**

You can test your State endpoint by using the following command:

```
curl -X GET -H "Accept:application/json" -u
"TestServiceBrokerUser:TestServiceBrokerPassword"
http://localhost:3000/bluemix_v1/service_instances/3d06cbfa-e3d3-438c-b894-60f0e8f242ff
```

### Quick Start guide
{: #v2next}

Service providers can display the Quick Start guide in the Bluemix user interface to provide instructions on using the service to users. The Quick Start guide can be specified during service registration, and will be displayed in the **View Quick Start** area on the **Overview** tab of the application details page when a service instance is created.

The content of the guide area is displayed in the following two formats:

* **Collapsed**

    Displays limited content of the guide, and can contain the following features: 
	
	* 40 character title
	* 45 character preview of the description

* **Expanded**

    Displays the full content of the guide, and can contain the following features: 
	
	* 40 character title
	* 説明
	* Bullets: Each bullet can be a maximum of 90 characters
	* Sample code or command line
	
The content of the guide is composed in Markdown format. In addition to Markdown format, the Bluemix user interface supports dynamic variables to generate portions of the content that is dynamically based on the instance. The following variables are replaced dynamically when specified in the format of `${variable_name}`:

* **api-url**

    API endpoint URL. You can use this variable for examples of target invocation of the cf command line.
	
* **username**

    User that is logged in.
	
* **service**

    Service offering name.
	
* **service-guid**

    Service offering GUID.
	
* **service-version**

    Service offering GUID.
	
* **service-plan**

    Service plan name.
	
* **service-instance**

    Service instance name.
	
* **doc-url**

    Base URL for the documentation for this instance of Bluemix.
	
* **ace-url** 

    Base URL for the Bluemix user interface; for example, `https://console.stage1.eu-gb.bluemix.net`.

To ensure consistency, the Markdown must use the following general Markdown pattern:
```
Getting started guide (40 char maximum)
----------------------------------------------

Description text displays up to 45 characters in preview but full
text is displayed when the guide is expanded.

1. Maximum of 90 characters (2 lines with 45 characters each)
2. Hyperlinks can also be specified [http://www.ibm.com](ibm.com)
3. Sample code can also be specified and displayed in a maximum
250px height window

    cf target ${api_url}
    cf login ${username}
    cf push ${app}
```

### Service icon images
{: #v2image}

As a service provider, you must provide the images that are used to display your service in the Bluemix user interface. You can provide image assets when you implement the service broker.

You must provide images in the following four image sizes. Different image sizes are used in different parts of the Bluemix user interface. All image files must be in PNG format on transparent bitmap backgrounds.

**Small 24 x 24**

A 24 x 24 pixel image is displayed in the following places on the Dashboard tab of the Bluemix user interface:

   * At the top of the user interface of the service after this service is provisioned.
   * On the tiles of the applications that the service is bound to.
   
**Medium 32 x 32**

A 32 x 32 pixel image is displayed on the tile of the service on the Dashboard tab of the Bluemix user interface.

**Large 50 x 50**

A 50 x 50 pixel image is displayed in the following places of the Bluemix user interface:

   * On the **Overview** page of the **Dashboard** tab for an application that the service is bound to.
   * In the service catalog on the **Catalog** tab 
   * On the service details page that opens after you click a service on the **Catalog** tab

**Featured 64 x 64**

A 64 x 64 pixel image is used to display the service when it is a featured service on the Bluemix **SOLUTIONS** page. This image size allows you to provide text that describes the service.

**Notes:**

   * If an image set is not provided by a service, Bluemix provides a default image set.
   * You must cache information for image assets to prevent images from reloading unnecessarily. You can cache image information by adding a unique version parameter to the image URL and by setting the cache expires headers to large values. When the image changes, the version number is updated. 例えば次のようにします。
   
   ```
   "imageUrl" : "http://serviceBrokerImpl.stage1.eu-gb.mybluemix.net/icons/serviceIcon?version=1" ,
   ```
   
**Tip:** To get approval from the Bluemix design team for your icons, go to [Master Icon List](https://releaseblueprints.ibm.com/display/CLOUDOE/Master+Icon+List).


### 管理 I フレームのサポート
{: #iframe}

The administration user interface of a service is displayed in the **Dashboard** tab of the Bluemix user interface within an iframe. The following information shows how the iframe is initialized and how the iframe code interacts with Bluemix. 

**Administration iframe initialization**

When the administration iframe is initialized, a parameter that is called ace_config is passed in the URL. It contains the following information:

```
{
  // id representing the current service; must be passed back to the Bluemix user interface in all messages
  id: "12345-12345",

  // if invoked from the dashboard in the Bluemix user interface:
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // if invoked from an app:
  appGuid: "12345-12345",
  orgGuid: "12345-12345",
  spaceGuid: "12345-12345",

  // pixel height for 'ideal' iframe size, wherein it fits completely in
  // viewport without scrollbars (width is handled by the Bluemix user interface)
  idealHeight: 300
  //Provides a full URL to go back to a location in the Bluemix UI. This is particularly useful for services who specify launch for embeddableDashboard and want to provide a "Go Back" button.
  redirect: "https://console.stage1.eu-gb.bluemix.net",
} 
```

To retrieve this object, you must take the following action: 

```
// string contents of the `ace_config` URL parameter are stored in `aceConfigString`
var aceConfig = JSON.parse(decodeURIComponent(aceConfigString)); 
```

**Responsive UI**

All service or extension administration code must be responsive -- that is, it must correctly display across a wide variety of widths, reflowing the UI components as necessary to fit within the given width. 

To enable your responsive UI in the iframe, you must set the value of the embeddableDashboard field in the service metadata to **true**. For more information about service metadata, see v2metadata.html#v2metadata. 

By default, the Bluemix user interface sets the iframe height to 1024 pixels. If the administration UI requires more or less area to minimize white space or to have vertical scroll bars, the administration code can send a message to the Bluemix user interface by using the window.postMessage API. 例えば次のようにします。 

```
function sendFrameSizeMessage() {
    var targetOrigin = '*';
    var payload = {
        type: '/ace/service/framesize',
        data: {
            id: '12345-12345',   // ace_config.id
            height: 300
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```
For more information about the window.postMessage API, see [Window.postMessage](https://developer.mozilla.org/en-US/docs/Web/API/Window/postMessage).

The following example shows how to enable an administration UI to resize when the iframe is first loaded and to resize dynamically when the browser window is resized. 

```
(function() {

    function addEventListener(el, type, listener, useCapture) {
        if (el.addEventListener) {
            el.addEventListener(type, listener, useCapture);
        } else if (el.attachEvent) {
            el.attachEvent('on' + type, listener);
        }
    }

    var savedBodyHeight = 0;

    function sendResizeMessage() {
        var height = document.body.offsetHeight;

        if (height !== savedBodyHeight) {
            savedBodyHeight = height;

            var targetOrigin = '*';
            var payload = {
                type: '/ace/service/framesize',
                data: {
                    id: '12345-12345',   // ace_config.id
                    height: height
                }
            };
            window.top.postMessage(payload, targetOrigin);
        }
    }

    addEventListener(window, 'load', sendResizeMessage);
    addEventListener(window, 'resize', sendResizeMessage);

})();
```

**Ideal height**

When the administration iframe is initialized, the Bluemix user interface will also calculate the ideal height for the iframe, given the size of the current viewport. This is the height at which the iframe can be displayed on the page without showing vertical scroll bars on the page. It is provided as part of the ace_config URL parameter.

If the service or extension administration UI can be dynamically sized, it can be set to display at this ideal height. The iframe code should then send the `/ace/service/framesize` message to the Bluemix user interface with this height. 


**Setting the dirty state**

If the service or extension administration UI allows for user input, then the code can set the dirty state of the page to prevent the user from accidentally closing or navigating away from the page. This can be done by sending the ``/ace/service/dirty`` message to the Bluemix user interface, with the dirty property set to true. Set the value to false to disable the dirty state. 以下に例を示します。```
function sendDirtyMessage() {
  var targetOrigin = '*';
  var payload = {
        type: '/ace/service/dirty',
        data: {
            id: '12345-12345',   // ace_config.id
            dirty: true          // or false
        }
    };
    window.top.postMessage(payload, targetOrigin);
}
```

## リソース使用量の報告 
{: #reporting_resource_usage}

To calculate the usage of service resources and report the usage to Bluemix™, you must use Bluemix Metering Service. 

### Setting up Bluemix metering
{: #metering}

Bluemix users are charged based on the amount of resources that they use. For example, Bluemix users that use database services might be charged based on the amount of storage that their applications use.

After you register your resource definition with the Bluemix metering service, you can use the API that the Bluemix metering service provides to report usage data of service resources that are consumed by Bluemix users.

To use the Bluemix metering service to report usage data, complete the following steps:

1. Create a resource definition in JSON format to list service resources that you want to measure. You must also specify metrics and aggregation models for these resources, which are used for measuring and also shown to Bluemix users in the Bluemix user interface. For details about the format and content for the resource definition, see [Resource definition](.index.html#resource-definition).

   Ensure that the resource definition follows ID and naming guidelines detailed in [Usage submission guidelines](./index.html#usage-submission-guidelines).

2. Register the resource definition with the Bluemix metering service by sending an email to [Bluemix metering administrator](mailto:Bluemix-MeteringService).

3. Implement the Bluemix metering service API to report usage data of your service. See [Bluemix metering service API for details](./index.html#bluemix-metering-service-api) for details.

   Ensure that you follow submission guidelines detailed in [Usage submission guidelines](./index.html#usage-submission-guidelines).


### Resource definition

The resource definition is used to list service resources that you want to measure and to specify metrics and aggregation models of these resources.

The resource definition must be in JSON format and must contain all of the required fields. You must follow all of the usage submission guidelines when you specify values for these fields. For details, see [Usage submission guidelines](./index.html#usage-submission-guidelines).

* **id**
    
	The ID of the service. This ID must be unique in Bluemix and must be a GUID. 
	
* **resources** 

    The names and units of the resources of the service.
	
	* **resources.name**
	
	    The name of the service resource. 
		
	* **resources.unit**
	
	    The unit name and quantity type for the usage of the service resource.
		
		* **resources.unit.name**
		
		    The unit name for the service resource. For example, you can specify **GIGABYTES** or **API_CALL** for this field.
			
		* **resources.unit.quantityType**
		
		    The quantity type for the service resource. For example, you can specify **CURRENT** or **DELTA** for this field.

* **aggregations**
	
    An array of strings that represent the aggregation models for the resources of the service. 

    * **aggregations.id**

        The identifier of the aggregation model for the service resource usage. Ensure that the value of the aggregations.id field is the same as the value of the cost.unitId field. The cost.unitId field is contained in the plans field of the service definition in the Get Catalog result. For more information about the plans field, see plans.

    * **aggregations.unit**

        The unit name of the aggregation model. 

    * **aggregations.aggregationGroup**

        The name of the aggregation group that the aggregation model belongs to.

    * **aggregations.formula**
  
        The formula of the aggregation model. You must include a function and a resource unit in the formula. Functions that you can use include **AVG**, **SUM**, and **MAX**. Resource units must be the units that are defined in the resources field. 

See the following definition of a resource usage as an example:

```
{
    "id": "MyService-8e9f8a35-dc03-4192-8bba-a77ae60222eb",
    "resources": [
        {
            "name": "Storage",
            "units": [
                {
                    "name": "GIGABYTE",
                    "quantityType": "CURRENT"
                }
            ]
        },
        {
            "name": "ApiCalls",
            "units": [
                {
                    "name": "API_CALL",
                    "quantityType": "DELTA"
                }
            ]
        }
    ],
    "aggregations": [
        {
            "id": "GB_PER_MONTH",
            "unit": "GIGABYTE",
            "aggregationGroup": {
                "name": "monthly"
            },
            "formula": "AVG({GIGABYTE})"
        },
        {
            "id": "API_CALLS_PER_MONTH",
            "unit": "API_CALL",
            "aggregationGroup": {
                "name": "monthly"
            },
            "formula": "SUM({API_CALL})"
        }
    ]
}
```

### Usage submission guidelines
{: #metering_guidelines}

You must follow specific guidelines when you use the Bluemix metering service.

**Submission guidelines**

  Refer to the following guidelines when you submit resource usage data by using the Bluemix metering service:
  
   * Submit the resource usage data to the metering service once every 2 - 24 hours. How often you submit your usage data depends on how often your usage metrics change.
   * Submit the resource usage data of a day by the end of the following day in Coordinated Universal Time (UTC).
   * A successful submission returns a response code of 201. If any other response code is returned, update and resend the data until you receive the 201 code.
   * For the Yellow Stage 1 environment, access the metering service by using the following URL: 
     ```
     https://MeteringInterface-Provider.stage1.ng.bluemix.net
     ```
   * For the Yellow Production environment, access the metering service by using the following URL: 
     ```
     https://meteringinterface-provider.ng.bluemix.net
     ```

**Service ID guidelines**

  You must follow these guidelines when you specify the service ID by using the id field in the resource definition:
  * Start the ID with an alphanumeric character.
  * Use characters A - Z, a - z, and 0 - 9. The only special characters that you can use are hyphens (-) and underscores (_).
  * Follow the camel case convention if the ID contains more than one word.
  * Ensure that the maximum length of the ID is 50 characters.
  
**Resource name guidelines**

  You must follow these guidelines when you specify the resource name by using the resources.name field in the resource definition:
  
  * Use only words that describe your resources. For example, **Storage** or **ApiCalls**. 
  * Follow the camel case convention if the name contains more than one word.
  * Capitalize the first character of the name.

**Resource unit name guidelines**

  You must follow these guidelines when you specify the resource unit name by using the resources.unit.name field in the resource definition:

  * Use one word for the unit name, and use an underscore (_), instead of a space, to separate words. For example, specify **API_CALL** instead of **API CALL**.  
  * Capitalize all letters of the name.
  
**Resource unit quality guidelines**

  You must follow these guidelines when you specify the resource quantity type by using the resources.unit.quantityType field in the resource definition:
  
  * Use one word for the quantity type.
  * Capitalize all letters of the quantity type.
  
**Aggregation ID guidelines**

  You must follow these guidelines when you specify the aggregation ID by using the aggregations.id field in the resource definition:

  * Capitalize all letters of the quantity type.
  * Use an underscore (_), instead of a space, to separate words.
  * Ensure that this ID starts with or matches with the value of aggregations.unit. For example, you can specify **API_CALLS_PER_MONTH** for aggregations.id and specify **API_CALLS** for aggregations.unit.

**Aggregation unit guidelines**

  You must follow these guidelines when you specify the aggregation unit by using the aggregations.unit field in the resource definition:
   
  * Use singular form for the unit name.
  * Capitalize all letters of the unit name.
  * Ensure that the unit name that you specify in the aggregations.unit field is an aggregate of the unit name that you specify in the resources.unit.name field.
  
**Aggregation group guidelines**

  You must use lowercase letters for the aggregations.aggregationGroup field in the resource definition.
  
**Aggregation formula guidelines**

  For the aggregations.formula field in the resource definition, if you want to use arithmetic operations in the formula, you must use the resource unit as one operand and use an infix arithmetic expression in the function of the formula. For example, you can use the following formula to convert Bytes to Megabytes:
  ```
  SUM({BYTE}/1048576)
  ```
  
### Bluemix metering service API
{: #metering_api}

You can use the API endpoints of the Bluemix metering service to report or retrieve the usage data of your service by providing a service ID or a service instance ID in the HTTP requests.

In the response header for every usage submission, the Location property contains the URL to retrieve the usage submission record. You can save this URL for future reference.

**Request**

 * **Route**
 
   ```
   POST /v1/metering/services/:service_id/usage?region=us-south
   ```
   **Note:** Posting usage data by using this API reduces the number of HTTP calls.
   
 * **Query parameters**
    
     * **地域 (region)** 
		
		  The ID of the region of usage data. You can use eu-gb for London, us-south for Dallas, and au-syd for Sydney.
		  
 * **パラメーター**
    
	 * **service_id**
	   
	     The ID of the service. This ID must be unique and must be a GUID.
		 
 * **Header**
 
     * **許可**
	 
	     Basic authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).
		 
 * **本文**
    
     * **service_instances**

         An array of strings that contain usage data of service instances that you want to post. These service instances use the same region as the query parameter.

         * **usage**

             An array of usage data that you want to post. This usage data has the same region as the query parameter.
    
             Within the usage data, the plan_id is the ID of the service plan that is specified as a parameter of cf create-service. The ID must be unique within Bluemix and must be a GUID. The value of this plan_id field is the same as the plan_id field that is in the Provision (PUT) request when the service instance is created. For more information about the plan_id field in the Provision (PUT) endpoint, see [Provision (PUT)].	
		 
         See the following JSON string as an example:
		```
         {
             "service_instances": [
                {
                     "service_instance_id": "myServiceInstance-guid",
                     "usage": [
                         {
                             "plan_id": "",
                             "start": 1396421450000,
                             "end": 1396421451000,
                             "organization_guid": "myOrganization-guid",
                             "space_guid": "mySpace-guid",
                             "consumer": {
                                 "type": "cloud-foundry-application",
                                 "value": "myApplication-guid"
                             },
                             "resources": [
                                 {
                                     "unit": "GIGABYTE",
                                     "quantity": 10
                                 },
                                 {
                                     "unit": "API_CALL",
                                     "quantity": 10
                                 }
                             ]
                         }
                     ]
                 }
             ]
         }	

        ```	 
		
**Response**

  * **Header**
 
      * **Location**
    
          The URL to get the usage record by using the HTTP GET method.


**Request**

  * **Route**
      
    ```
    GET /v1/metering/services/:service_id/usage/:usage_id?region=us-south
    ```
 * **Query parameters**
   
     * **地域 (region)**
	 
	     The ID of the region of usage data. You can use **eu-gb** for London and **us-south** for Dallas.
		 
 * **パラメーター**

     * **service_id**

         The ID of the service. This ID must be unique and must be a GUID.

     * **usage_id**

         The ID of the usage record that you want to retrieve.

 * **Header**
    
     * **許可**

         Basic Authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).

**Response**

  * **本文**

      * **usage**

          An array of strings that contain the usage records that are returned from this usage ID.


**Request**

  * **Route**

    ```
    GET /v1/metering/service_instances/:instance_id/usage/:usage_id?region=us-south
    ```	  

  * **Query parameters**

      * **地域 (region)**

          The ID of the region of usage data. You can use **eu-gb** for London and **us-south** for Dallas.	  
	
  * **パラメーター**

      * **instance_id**
   
          The ID of the service instance.
  
      * **usage_id**

          The ID of the usage record that you want to retrieve.

  * **Header**
 
      * **許可**
   
          Basic Authentication credentials. The username and password fields are the same as in the service broker definition. For more information about the format of the basic authentication scheme, see [RFC1945](http://tools.ietf.org/html/rfc1945#section-11.1).   
	  
**Response**

  * **本文**
  
      * **usage**
	    
		  An array of strings that contain the usage records that are returned from this usage ID.
		

		
## RELATED LINKS		
		
### チュートリアルおよびサンプル

[A sample service for Java](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/java-v2)

[A sample service for Node.js](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/node-v2)

[A sample service for Ruby](https://github.rtp.raleigh.ibm.com/bluemix/sample-services/tree/master/v2/ruby-v2)

### GENERAL

[Service Broker API of Cloud Foundry](http://docs.cloudfoundry.org/services/api.html)

[Catalog Metadata of Cloud Foundry](http://docs.cloudfoundry.org/services/catalog-metadata.html)

[Catalog Management of Pivotal](http://docs.run.pivotal.io/services/api.html#catalog-mgmt)

[Bluemix user interface](https://ace.stage1.ng.bluemix.net)

[Deploying your app with the Cloud Foundry command line interface](https://www.stage1.eu-gb.bluemix.net/docs/starters/install_cli.html)

[cloud-cli コマンド (cloud-cli commands)](https://www.stage1.eu-gb.bluemix.net/docs/cli/cloudcli.html)

[Markdown](http://daringfireball.net/projects/markdown/)

[V2 Provisioning API on Cloud Foundry](http://docs.cloudfoundry.org/services/api.html#provisioning)

[Service Broker API Enablement Extensions](http://rchgsa.ibm.com/~anhkhoa/public/projects/coe/docs/)


















