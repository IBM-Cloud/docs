---

 

copyright:

  years: 2016
lastupdated: "2016-10-27"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} および SoftLayer 請求アカウントのアップグレードおよび一元化
{: #softlayerlink}

{{site.data.keyword.Bluemix_notm}} トライアル・アカウントを使用していて、「インフラストラクチャー」ダッシュボードにアクセスする場合、{{site.data.keyword.Bluemix_notm}} 従量課金 (PAYG) アカウントにアップグレードする必要があります。

既存の {{site.data.keyword.Bluemix_notm}} 請求アカウントと SoftLayer 請求アカウントをリンクして一元化できます。アカウントをリンクすると、{{site.data.keyword.Bluemix_notm}} と SoftLayer の両方のリソースについて {{site.data.keyword.Bluemix_notm}} から請求されるようになります。
{:shortdesc}

## {{site.data.keyword.Bluemix_notm}} 従量課金 (PAYG) アカウントへのアップグレード
{: #upgradetopayg}

トライアル・アカウントを使用して {{site.data.keyword.Bluemix_notm}} にログインした場合、{{site.data.keyword.Bluemix_notm}} の「インフラストラクチャー」ダッシュボードにアクセスできません。アプリでインフラストラクチャー・リソースを使用する場合、従量課金 (PAYG) アカウントにアップグレードする必要があります。

トライアル・アカウントを {{site.data.keyword.Bluemix_notm}} 従量課金 (PAYG) アカウントにアップグレードするには、以下のステップを実行します。

 1. **「アカウント」**&gt;**「請求処理」**をクリックします。
 2. 次に、**「クレジット・カードの追加」**をクリックします。
 3. 必要な請求処理詳細を入力します。 
 4. 従量課金 (PAYG) アカウントのご使用条件を読んで受け入れます。 
 5. 完了したら、**「アップグレード」**をクリックします。 
 
従量課金 (PAYG) アカウントにアップグレードした後には、**「インフラストラクチャー」**オプションが、{{site.data.keyword.Bluemix_notm}} **カタログ**にリストされます。使用量が無料枠を超えると、月次の {{site.data.keyword.Bluemix_notm}} 請求書を受け取ることになります。請求書は米国ドル (USD) 単位であり、リソースの課金について詳しく示されます。 

## {{site.data.keyword.Bluemix_notm}} アカウントと SoftLayer アカウントの一元化
{: #unifyingaccounts}

{{site.data.keyword.Bluemix_notm}} アカウントと SoftLayer アカウントを一元化して、組み合わせたリソースを使用できます。{{site.data.keyword.Bluemix_notm}} アカウントと Softlayer アカウントをリンクすると、単一の {{site.data.keyword.Bluemix_notm}} 請求書を受け取ることになります。既存の {{site.data.keyword.Bluemix_notm}} アカウントがある場合、SoftLayer リソースについての {{site.data.keyword.Bluemix_notm}} を介した請求は、アカウントのリンク後に開始する新しい請求処理サイクルから有効になります。

**重要:** {{site.data.keyword.Bluemix_notm}} でリンクされるアカウントはすべて、従量課金 (PAYG) アカウントでなければなりません。新規従量課金 (PAYG) アカウントを作成するか、既存の従量課金 (PAYG) アカウントをリンクできます。あるいは、既存のトライアル・アカウントをリンクすることもできますが、そのアカウントは従量課金 (PAYG) アカウントにアップグレードされます。サブスクリプション {{site.data.keyword.Bluemix_notm}} アカウントは、リンクできません。  

アカウントがリンクされると、以下のようになります。

* SoftLayer と {{site.data.keyword.Bluemix_notm}} アカウントの両方にアクセスするために、IBM ID 資格情報を使用する必要があります。
* 既存の SoftLayer 割引は、{{site.data.keyword.Bluemix_notm}} の料金全体に適用されます。 
* 米国ドル (USD) 単位の 1 つの請求書を受け取ります。
* {{site.data.keyword.BluSoftlayer}} ユーザー・インターフェースで {{site.data.keyword.Bluemix_notm}} リソースの使用量をモニターできます。 

**注意:** リンクされたアカウントをリンク解除することはできません。 

SoftLayer アカウントがあり、SoftLayer アカウントと {{site.data.keyword.Bluemix_notm}} アカウントをリンクする場合は、以下のステップを実行します。

 1. {{site.data.keyword.slportal}} で、**「{{site.data.keyword.Bluemix_notm}} アカウントをリンク (Link a {{site.data.keyword.Bluemix_notm}} Account)」**をクリックします。
 2. SoftLayer アカウントと {{site.data.keyword.Bluemix_notm}} アカウントをリンクする場合のご利用条件を読み、同意します。
 3. 要求されたら、{{site.data.keyword.Bluemix_notm}} アカウントに関連付けられている E メール・アドレスを指定します。{{site.data.keyword.Bluemix_notm}} アカウントがない場合は、使用する E メール・アドレスを指定し、{{site.data.keyword.Bluemix_notm}} への招待を受けてアカウントを作成するための手順に従います。

アカウントをリンクするには、SoftLayer アカウントのマスター・ユーザーでなければなりません。

アカウントをリンクすると、SoftLayer グローバル・ヘッダーで**「{{site.data.keyword.Bluemix_notm}} に進む」**リンクが使用可能になります。このリンクをクリックすると、{{site.data.keyword.Bluemix_notm}} ログイン・ページに移動します。また、{{site.data.keyword.Bluemix_notm}} ヘッダーで**「SoftLayer」**リンクが使用可能になっています。このリンクをクリックすると、新規ウィンドウで {{site.data.keyword.slportal}} のホーム・ページに移動します。

## アカウントがリンクされている場合の {{site.data.keyword.Bluemix_notm}} 使用量に対するクレジット
{: #slcredit}

SoftLayer アカウントから {{site.data.keyword.Bluemix_notm}} アカウントをリンクした場合、{{site.data.keyword.Bluemix_notm}} 内でのみ使用可能な $200.00 のクレジットを受け取ります。このクレジットは、アカウントをリンクしてから 30 日以内に使用する必要があります。

クレジットおよび有効期限の表示方法については、『[クレジットの表示](https://console.ng.bluemix.net/docs/pricing/index.html#credits)』を参照してください。

## {{site.data.keyword.Bluemix_notm}} への SoftLayer チーム・メンバーの招待
{: #invite_users}

{{site.data.keyword.Bluemix_notm}} アカウントと SoftLayer アカウントをリンクするときに、{{site.data.keyword.Bluemix_notm}} に参加するように SoftLayer チーム・メンバーを招待できます。あるいは、後で {{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから SoftLayer チーム・メンバーを招待することもできます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースから、SoftLayer アカウントのすべてのメンバーを招待することを選択します。また、個別にメンバーを選択することもできます。チーム・メンバーを招待する際には、被招待者の {{site.data.keyword.Bluemix_notm}} アカウントの役割を設定する必要があります。{{site.data.keyword.Bluemix_notm}} の各種役割について詳しくは、[ユーザー役割](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo)を参照してください。

チーム・メンバーを {{site.data.keyword.Bluemix_notm}} アカウントに招待するには、SoftLayer アカウントのマスター・ユーザーでなければなりません。

{{site.data.keyword.Bluemix_notm}} でチーム・メンバーを招待するには、以下のステップを実行します。

 1. **「アカウント」**&gt;**「チーム・メンバーの招待」**をクリックします。
 2. **「追加」**をクリックし、SoftLayer アカウントへの認証操作を行い、{{site.data.keyword.BluSoftlayer}} アカウントからチーム・メンバーのリストを表示します。
 3. 招待するチーム・メンバーを選択し、**「送信」**をクリックします。
 
チーム・メンバーは、**「組織に参加してください (Join the organization)」**リンクが含まれた E メールを受け取ります。チーム・メンバーは、IBM ID を所有していない場合、登録ページにリダイレクトされます。次に、チーム・メンバーは、いくつかの基本情報を入力し、{{site.data.keyword.Bluemix_notm}} アカウントを作成できます。

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェースを使用したチーム・メンバーの招待について詳しくは、『[チーム・メンバーの招待](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers)』を参照してください。

## IBM ID への切り替え
{: #ibmid_switch}

SoftLayer での認証では、
{{site.data.keyword.Bluemix_notm}} 用の単一のログインを提供するために、IBM ID を使用するようになりました。既存の SoftLayer アカウントがある場合、IBM ID に切り替えることができます。マイグレーション・ウィザードを使用して、この切り替えの処理を行います。
{:shortdesc}

IBM ID への切り替えを開始しても、プロセスを完了しない限り、キャンセルできます。ただし、その場合でも、次回ログイン時に IBM ID に切り替えるように求めるプロンプトが出されます。

IBM ID への既存の SoftLayer ユーザー名の切り替えを開始するには、以下のステップを実行します。

 1. {{site.data.keyword.slportal}} で、「ユーザー・プロファイルの編集」ページに移動し、**「IBM ID への切り替え (Switch to IBMid)」**をクリックします。
 2. マイグレーション・ウィザードのプロンプトに従って、IBM ID を作成します。IBM ID の作成後にその ID (E メール・アドレス) を変更することはできません。プロファイルに関連付けられている E メールを更新することはできますが、デフォルトでは、その値は IBM ID 用に定義したものに設定されます。ウィザードの完了後に、E メールが送信されます。
 3. E メールを受信したら、リンクをたどるか URL をブラウザーにコピーし、登録コードを入力します。コードは 7 日間有効であり、1 回限り使用できるコードです。使用後、再使用することはできません。IBM ID から SoftLayer ユーザーへのリンクをセットアップした後には、IBM ID でのみアカウントにログインできます。ログイン・ダイアログで、SoftLayer ユーザー名とパスワードを入力するのではなく、**「IBM ID でログイン」**ボタンを使用する必要があります。
 
新規のお客様の場合、オーダーをチェックアウトすると、既存の IBM ID アカウントの E メール・アドレスを入力するか、新規 IBM ID アカウントを作成するように求められます。 

### 単一の IBM ID への複数の SoftLayer アカウントのマップ
{: #map_multiple_accounts}

アカウントのセットアップ時に既存の IBM ID の E メール・アドレスを使用することで、単一の IBM ID を複数の SoftLayer アカウントに関連付けることができます。単一の IBM ID にマップできる各アカウントの SoftLayer ユーザーは 1 つのみです。IBM ID は、各 SoftLayer アカウント内で固有でなければなりません。ただし、複数の SoftLayer アカウントにアクセスできる単一のユーザーが、単一の IBM ID を使用して複数の SoftLayer アカウントにアクセスできます。

例えば、ある IBM ID をアカウント A と B のマスター・ユーザーにマップし、さらにアカウント C と D の追加ユーザーにマップできます。当該 IBM ID にマップされたアカウントの 1 つが、デフォルト・アカウントになります。通常、デフォルト・アカウントは、IBM ID に最初にマップされたアカウントです。ただし、カスタマー・ポータルのアカウント切り替え機能を使用して、デフォルトのアカウントにするアカウントを切り替えることができます。

2 要素認証が有効になっていて、複数のアカウントに IBM ID でアクセスできるユーザーの場合、アカウントのログインおよびアカウントの切り替え時に、アカウントごとに適切な 2 要素認証検証コードが必要になります。

## SoftLayer 資産での {{site.data.keyword.Bluemix_notm}} サービスの使用
{: #bluemix_services}

SoftLayer 資産で API ベースの公開 {{site.data.keyword.Bluemix_notm}} サービスを簡単に使用できます。すべての API はセキュアであり暗号化されているため、データが保護されます。
{:shortdesc}

例えば、SoftLayer からベア・メタル・サーバーで実行されているアプリに Watson のコグニティブ機能を追加したいと思ったことはありませんか。以下の簡単な 4 つのステップで、{{site.data.keyword.personalityinsightsshort}} などのサービスを追加して、アプリのユーザーを把握できるようにすることが可能です。

1. {{site.data.keyword.Bluemix_notm}} カタログでサービスを見つけます。
2. わずか数クリックで、サービスのインスタンスをプロビジョンします。
3. サービス資格情報をコピーし、アプリケーションに追加して、サービスが既存のコードで実行されるようにセットアップします。
4. アプリを更新した後に、SoftLayer インフラストラクチャーで新規バージョンをデプロイします。

SoftLayer のアプリから Watson API を呼び出して*洞察およびコグニティブ* の知識を得ることで、アプリをさらにパーソナライズできます。あるいは、*データおよび分析* サービスを使用して、アプリでハイパフォーマンス分析を利用できます。あるいは、DaaS (Database-as-a-Service) を選択し、管理を {{site.data.keyword.Bluemix_notm}} に任せることができます。

{{site.data.keyword.activedeployshort}} や {{site.data.keyword.deliverypipeline}} などのサービスとともにコンテナーを使用することで、アプリケーション開発を最新化できます。そうすると、{{site.data.keyword.vpn_short}} サービスを使用して SoftLayer にトンネルで戻し、プライベート・ネットワーク内のコンテナーを SoftLayer プライベート・ネットワークに接続できます。計算リソースおよびサービスの使用量に対するすべての課金は、{{site.data.keyword.Bluemix_notm}} 請求に反映されます。 

### API ベースの {{site.data.keyword.Bluemix_notm}} サービス
一部の {{site.data.keyword.Bluemix_notm}} サービスは、SoftLayer で使用できません。以下のサービスは、アプリケーション・コードを使用して実行するようにセットアップできます。
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**注:** これらのサービスの一部のプランは使用できません。リンクされたアカウントで使用できるのは、従量課金 (PAYG) アカウント用に有効になっているプランのみです。ただし、個別に請求される個別の {{site.data.keyword.Bluemix_notm}} アカウントがある場合は、これらのすべてのサービスのすべてのプランを使用できます。

## アカウントがリンクされている場合の {{site.data.keyword.Bluemix_notm}} 使用量に対する請求処理
{: #bill_usage}

{{site.data.keyword.Bluemix_notm}} と SoftLayer の請求アカウントをリンクすると、次の請求処理サイクルは、単一の {{site.data.keyword.Bluemix_notm}} 請求で課金されます。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} の使用量サイクルは暦月ベースであるため、アカウントは毎月、課金契約に設定された請求日に請求されます。SoftLayer では、使用量サイクルは、SoftLayer の使用を開始したときから始まるため、毎月、SoftLayer アカウントを登録したときと同じ日に請求されます。 

アカウントをリンクした場合、現行月のサイクルの間、{{site.data.keyword.Bluemix_notm}} の使用量が引き続き計測され、その使用量については {{site.data.keyword.Bluemix_notm}} の請求書で請求されます。翌月の初めから、{{site.data.keyword.Bluemix_notm}} と SoftLayer の課金が、{{site.data.keyword.Bluemix_notm}} 請求書で結合されるようになります。

例えば、4 月 16 日にアカウントをリンクした場合、4 月の使用量については Bluemix の請求書を受け取ります。アカウントをリンクしたタイミングによっては、SoftLayer 使用量に対して別個の請求書を受け取ることがあります。SoftLayer と {{site.data.keyword.Bluemix_notm}} の両方の 5 月の使用量は、{{site.data.keyword.Bluemix_notm}} アカウントを介して請求されます。

![Bluemix と SoftLayer のアカウントのリンクのサマリー](images/BluemixSoftLayerBill.svg)

請求書がリンクされた後には、{{site.data.keyword.Bluemix_notm}} 請求書には、以下の見出しで、使用した各リソースに対する別個の料金がリストされます。

* **ベア・メタル・サーバーと付属サービス**
* **仮想サーバーと付属サービス**
* **付属しないサービス**

{{site.data.keyword.Bluemix_notm}} の使用量を表示する方法については、『[使用量詳細の表示](https://console.ng.bluemix.net/docs/pricing/index.html#usage)』を参照してください。

