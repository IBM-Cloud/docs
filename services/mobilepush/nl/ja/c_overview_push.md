---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}}の概要
{: #overview-push}
最終更新日: 2017 年 1 月 18 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}} は、デバイスおよびプラットフォームに通知を送信するために使用できるサービスです。通知は、すべてのアプリケーション・ユーザーをターゲットとすることも、タグを使用して特定のユーザーおよびデバイスの集合をターゲットとすることもできます。デバイス、タグ、およびサブスクリプションを管理できます。
  

以下のいずれかのオプションを使用して、バインドまたはアンバインドされたサービスを作成することができます。

- カタログから MobileFirst Services Starter ボイラープレートを使用して Bluemix アプリケーションを作成する。これにより、Bluemix バックエンド・アプリケーションにバインドされた Push Notifications (プッシュ通知) サービスが作成されます。
- モバイル・カタログから直接、アンバウンド Push Notifications (プッシュ通知) サービスを作成する。後でアプリケーションにバインドするか、アンバウンドの状態で使用するよう選択することもできます。 
- [モバイル・ダッシュボード![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://console.ng.bluemix.net/docs/mobile/services.html "外部リンク・アイコン"){: new_window}を使用する。

なお、{{site.data.keyword.mobilepushshort}}のモニター・タブには、分析データは表示されません。

{{site.data.keyword.mobilepushshort}}サービスは、OpenWhisk 対応になりました。詳細については、[OpenWhisk](/docs/openwhisk/index.html) を参照してください。


## {{site.data.keyword.mobilepushshort}}サービスのプロセス
{: #overview_push_process}

モバイル・クライアント、Web ブラウザー・クライアント、および Google Chrome アプリケーションおよびエクステンションは、{{site.data.keyword.mobilepushshort}} サービスをサブスクライブし、登録することができます。クライアント・アプリケーションは、開始時、{{site.data.keyword.mobilepushshort}}サービスにそれぞれを登録してサブスクライブします。通知は、Apple Push Notification Service (APNs) または Firebase Cloud Messaging (FCM)/Google Cloud Messaging (GCM) サーバーにディスパッチされ、その後、登録済みのモバイル・クライアントまたはブラウザー・クライアントに送信されます。

![プッシュの概要](images/overview.jpg)


###モバイル・アプリケーションとブラウザー・アプリケーション
{: mobile-applications}

クライアント・アプリケーションは、通知を受け取るために、開始時に {{site.data.keyword.mobilepushshort}} サービスにそれぞれを登録してサブスクライブします。

###バックエンド・アプリケーション
{: backend-applications}

バックエンド・アプリケーションは、オンプレミスまたはパブリック・クラウドに位置することができます。バックエンド・アプリケーションは、{{site.data.keyword.mobilepushshort}}サービスを使用して、コンテキストに依存した通知をモバイル・アプリケーション・ユーザーとブラウザー・アプリケーション・ユーザーに送信します。バックエンド・アプリケーションは、プッシュ通知を送信するためにモバイル・デバイス、ブラウザー・エージェント、およびユーザーに関する情報を維持し管理する必要はありません。代わりに、バックエンド・アプリケーションは、それらを管理および維持する{{site.data.keyword.mobilepushshort}}サービスを使用することができます。

###アプリ・バックエンド所有者
{: app-backend-owner}

アプリ・バックエンド所有者は、{{site.data.keyword.mobilepushshort}}サービスのインスタンスをバンドルするモバイル・バックエンド・アプリケーションを作成します。また、アプリ・バックエンド所有者は、{{site.data.keyword.mobilepushshort}}サービスとこのサービスのターゲットとなるモバイル・アプリケーションおよびブラウザー・アプリケーションとを使用するバックエンド・アプリケーションに合うように、{{site.data.keyword.mobilepushshort}}サービスの構成とセットアップも行います。

###{{site.data.keyword.mobilepushshort}}サービス
{: push-notification-service}

{{site.data.keyword.mobilepushshort}}サービスは、通知用に登録されたモバイル・デバイスと Web ブラウザー・クライアントに関するすべての情報を管理します。このサービスは、異機種のモバイル・プラットフォームおよび Web ブラウザー・プラットフォームに通知を送信するテクノロジー詳細がアプリケーションに透過的になるようにし、サービス内部でそのすべてを処理します。

###ゲートウェイ
{: gateways}

モバイル・アプリケーションやブラウザー・アプリケーションに通知をディスパッチするために IBM {{site.data.keyword.mobilepushshort}} サービスが使用する、FCM/GCM または Apple Push Notification Service (APNs) などのプラットフォーム固有のプッシュ通知クラウド・サービス。

###プッシュのセキュリティー
{: push-security}

{{site.data.keyword.mobilepushshort}} API は、次の 2 つのタイプの secret によって保護されています。

- **appSecret**: 「appSecret」は、バックエンド・アプリケーションによって通常呼び出される API を保護します。例えば、{{site.data.keyword.mobilepushshort}}を送信する API や設定を構成する API などです。
- **clientSecret**:  「clientSecret」は、モバイル・クライアント・アプリケーションによって通常呼び出される API を保護します。この「clientSecret」を必要とする関連付けられた UserId を持つデバイスの登録に関与する API は 1 つだけです。その他の API は、clientSecret を必要とするモバイル・クライアントからは呼び出されません。 

「appSecret」と「clientSecret」は、アプリケーションと{{site.data.keyword.mobilepushshort}}サービスのバインド時にすべてのサービス・インスタンスに割り振られます。secret の受け渡しの方法や、対象の API について詳しくは、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/ "外部リンク・アイコン") の資料を参照してください。

**注**: 以前のアプリケーションでは、userId フィールドが設定されたデバイスを登録または更新する場合にのみ、clientSecret の受け渡しが必要とされました。モバイル・クライアントおよびブラウザー・クライアントによって呼び出されるその他のすべての API では、clientSecret は不要でした。これらの古いアプリケーションでは引き続き、デバイスの登録や呼び出しの更新時にオプションで clientSecret を使用できます。ただし、すべてのクライアント API 呼び出しで clientSecret チェックを実施することを強くお勧めします。これを既存のアプリケーションでも実施するために、新規の「verifyClientSecret」API が公開されています。新規アプリケーションの場合、clientSecret チェックがすべてのクライアント API 呼び出しに対して実施され、この動作は「verfiyClientSecret」API を使用して変更することはできません。

デフォルトでは、クライアント秘密鍵検証は新規アプリケーションに対してのみ実施されます。既存のアプリケーションと新規アプリケーションはどちらも、verifyClientSecret REST API を使用して、クライアント秘密鍵検証を使用可能または使用不可にすることができます。applicationId および deviceId を知っている可能性のあるユーザーにデバイスが公開されないようにするために、クライアント秘密鍵検証を実施することをお勧めします。

「clientSecret」は常に機密とし、モバイル・アプリケーションへのハードコーディングは絶対に行わないでください。アプリケーションの実行時に「clientSecret」を動的にプルするために使用できる、さまざまなアプリケーション初期化パターンがあります。以下のシーケンス図に、可能なパターンの概要を示します。![通知の使用可能化](images/init_client_secret.jpg) 

## {{site.data.keyword.mobilepushshort}}のタイプ
{: #overview-push-types}

###ブロードキャスト
{: broadcast}

クライアント・アプリケーションは、{{site.data.keyword.mobilepushshort}} サービスに自身を登録すると、ブロードキャストの受信を開始できます。ブロードキャスト通知は、モバイル・デバイスおよびブラウザーの全体にインストールされているか Chrome アプリケーションまたはエクステンションとして実装されていて、かつ {{site.data.keyword.mobilepushshort}} サービス用に構成されている、1 つのアプリケーションのすべてのインスタンスをターゲットとしたメッセージです。ブロードキャスト通知は、{{site.data.keyword.mobilepushshort}}が有効になっているすべてのアプリケーションに、デフォルトで有効になっています。{{site.data.keyword.mobilepushshort}}サービスが有効になっているアプリケーションでは、Push.ALL タグへのサブスクリプションが事前定義されています。サーバーはこれを使用して、通知メッセージをすべてのデバイスにブロードキャストします。REST Push API を使用するブロードキャスト通知を送信する場合は、メッセージ・リソースに投稿する際に「target」が空の JSON ファイルであることを確認してください。


###タグ・ベースの通知
{: tag-based-notifications}

タグ通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとするメッセージです。タグ・ベースの通知では、サブジェクト・エリアまたはトピックに基づいて通知を分割できます。通知の受信側は、関心のあるサブジェクトまたはトピックに関するものであった場合にのみ通知を受信するように選択できます。そのため、タグ・ベースの通知は、受信側を分割する手段を提供します。この機能により、タグを定義した後、タグ別にメッセージの送受信を行うことが可能になります。メッセージは、タグにサブスクライブしている (モバイル上、ブラウザー上、あるいはアプリケーションまたはエクステンションとしての) クライアント・アプリケーション・インスタンスのみをターゲットにします。まず、アプリケーションのタグを作成し、タグ・サブスクリプションをセットアップしてから、タグ・ベースの通知を開始する必要があります。REST API を使用するタグ・ベースの通知を送信する場合は、メッセージ・リソースに投稿する際に「tagNames」が指定されていることを確認してください。

###ユニキャスト通知
{: unicast-notifications}

ユニキャスト通知は、特定のデバイスまたはユーザーをターゲットとするメッセージです。デバイスをターゲットとするユニキャスト通知は、追加のセットアップを必要とせず、アプリケーションで{{site.data.keyword.mobilepushshort}}が有効になっている場合にデフォルトで有効になります。

ただし、ユーザーをターゲットとするユニキャスト通知では、{{site.data.keyword.mobilepushshort}} 用のクライアント・モバイル・デバイスまたは Web ブラウザー、あるいは Chrome アプリケーションおよびエクステンションの登録時に、ユーザー ID をデバイスと関連付ける必要があります。   

通常、クライアント・アプリケーションは、最初に認証サイクルを実行します。この認証サイクルで、モバイル・アプリケーション・ユーザーは [Mobile Client Access](docs/services/mobileaccess/index.html) などの認証サービスと照合して認証されます。認証に成功すると、認証済みユーザー ID がプッシュ・デバイス登録 API に渡されます。REST API を使用するユニキャスト通知を送信する場合は、メッセージ・リソースに投稿する際に deviceId または userId が指定されていることを確認してください。

###プラットフォーム・ベースの通知
{: platform-based-notifications}

特定のデバイス・プラットフォームに届くように通知のターゲットを設定することができます。例えば、すべての Android ユーザーまたは Google Chrome ユーザーにのみ通知を送信するようにできます。REST API を使用するプラットフォーム・ベースの通知を送信する場合には、メッセージ・リソースに投稿する際にターゲットのプラットフォームが指定されていることを確認してください。
プラットフォームを配列として指定します。サポートされるプラットフォームは、以下のとおりです。
* A (Apple) 
* G (Google)
* WEB_CHROME (Google Chrome ブラウザーの Web プッシュ)
* WEB_FIREFOX (Mozilla Firefox ブラウザーの Web プッシュ)
* WEB_SAFARI (Safari ブラウザーの Web プッシュ)
* APPEXT_CHROME (Google Chrome アプリケーション & エクステンション)

## {{site.data.keyword.mobilepushshort}}のメッセージ・サイズ
{: #push-message-size}

{{site.data.keyword.mobilepushshort}} のメッセージ・ペイロード・サイズは、ゲートウェイ (FCM/GCM、APNs) およびクライアント・プラットフォームによって課せられる制約に依存します。 

### iOS および Safari
{: ios-message-size}

iOS 8 以降では、許容される最大サイズは 2 キロバイトです。Apple プッシュ通知サービスは、この制限を超える通知を送信しません。

###Android、Firefox ブラウザー、Chrome ブラウザー、および Chrome アプリケーション & エクステンション
{: android-message-size}

メッセージ・ペイロードの許容される最大サイズとして、4 キロバイトの制限があります。  
