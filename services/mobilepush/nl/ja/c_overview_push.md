---

copyright:
 years: 2015, 2016

---

# {{site.data.keyword.mobilepushshort}}の概要
{: #overview-push}
最終更新日: 2016 年 8 月 16 日
{: .last-updated}

IBM {{site.data.keyword.mobilepushshort}}は、iOS デバイスおよび Android デバイスへの通知の送信に使用できるサービスです。通知は、すべてのアプリケーション・ユーザーをターゲットとすることも、タグを使用して特定のユーザーおよびデバイスの集合をターゲットとすることもできます。デバイス、タグ、およびサブスクリプションを管理できます。
クライアント・アプリケーションをさらに開発するために、SDK (software development kit) および Representational State Transfer (REST) アプリケーション・プログラム・インターフェース (API) を使用することもできます。 

{{site.data.keyword.mobilepushshort}}は、Bluemix 専用サービスとしても使用可能です。専用サービスの{{site.data.keyword.mobilepushshort}}については、[専用サービス](../../dedicated/index.html)を参照してください。なお、{{site.data.keyword.mobilepushshort}}のモニター・タブには、分析データは表示されません。

{{site.data.keyword.mobilepushshort}}サービスは、OpenWhisk 対応になりました。詳細については、[OpenWhisk](../../openwhisk/index.html) を参照してください。


## {{site.data.keyword.mobilepushshort}}サービスのプロセス
{: #overview_push_process}

モバイル・クライアントは、{{site.data.keyword.mobilepushshort}}サービスへのサブスクライブおよび登録を行うことができます。モバイル・アプリケーションは、開始時にそれ自体を{{site.data.keyword.mobilepushshort}}サービスに登録してサブスクライブします。通知は、Apple Push Notification Service (APNs) または Google Cloud Messaging (GCM) サーバーにディスパッチされ、その後、登録済みのモバイル・クライアントに送信されます。

![プッシュの概要](images/overview.jpg)


###モバイル・アプリケーション
{: mobile-applications}

モバイル・アプリケーションは、開始時にそれ自体を{{site.data.keyword.mobilepushshort}}サービスに登録してサブスクライブし、通知を受信できるようにします。

###バックエンド・アプリケーション
{: backend-applications}

バックエンド・アプリケーションは、オンプレミスまたはパブリック・クラウドに位置することができます。バックエンド・アプリケーションは、{{site.data.keyword.mobilepushshort}}サービスを使用して、コンテキストに依存した通知をモバイル・ユーザーに送信します。バックエンド・アプリケーションは、プッシュ通知を送信するためにモバイル・デバイスとユーザーの情報を維持し管理する必要はありません。代わりに、バックエンド・アプリケーションは{{site.data.keyword.mobilepushshort}}サービスを使用することができます。

###アプリ・バックエンド所有者
{: app-backend-owner}

アプリ・バックエンド所有者は、{{site.data.keyword.mobilepushshort}}サービスのインスタンスをバンドルするモバイル・バックエンド・アプリケーションを作成します。また、アプリ・バックエンド所有者は、{{site.data.keyword.mobilepushshort}}サービスが、{{site.data.keyword.mobilepushshort}}のターゲットであるモバイル・アプリケーションとともに、サービスを使用するバックエンド・アプリケーションに適合するように、その構成とセットアップも行います。

###{{site.data.keyword.mobilepushshort}}サービス
{: push-notification-service}

{{site.data.keyword.mobilepushshort}}サービスは、通知用に登録されたデバイスに関するすべての情報を管理します。このサービスは、異機種のモバイル・プラットフォームに通知を送信するテクノロジー詳細がアプリケーションに透過的になるようにし、その内部でそのすべてを処理します。

###ゲートウェイ
{: gateways}

Google Cloud Messaging (GCM) や Apple Push Notification Service (APNs) などのモバイル・デバイス・プラットフォーム固有のクラウド・サービスは、{{site.data.keyword.mobilepushshort}}サービスを使用してモバイル・アプリケーションに通知をディスパッチします。

###プッシュのセキュリティー
{: push-security}

{{site.data.keyword.mobilepushshort}} API は、2 つタイプの秘密鍵 i) appSecret ii) clientSecret によって保護されます。「appSecret」は、{{site.data.keyword.mobilepushshort}}を送信する API や設定を構成する API など、バックエンド・アプリケーションによって通常呼び出される API を保護します。「clientSecret」は、モバイル・クライアント・アプリケーションによって通常呼び出される API を保護します。現時点で、この「clientSecret」を必要とする、関連 UserId へのデバイスの登録に関する API は 1 つのみです。モバイル・クライアントから起動されるその他の API には、clientSecret は不要です。「appSecret」と「clientSecret」は、アプリケーションと{{site.data.keyword.mobilepushshort}}サービスのバインド時にすべてのサービス・インスタンスに割り振られます。秘密鍵がどのようにどんな API に受け渡されるかについて詳しくは、ReST API の資料を参照してください。

## {{site.data.keyword.mobilepushshort}}のタイプ
{: #overview-push-types}

###ブロードキャスト
{: broadcast}

モバイル・アプリケーションは、{{site.data.keyword.mobilepushshort}}サービスに登録されると、ブロードキャストの受信を開始できます。ブロードキャスト通知は、アプリケーションをインストールして、それを{{site.data.keyword.mobilepushshort}}サービス用に構成したすべてのデバイスをターゲットとしたメッセージです。ブロードキャスト通知は、{{site.data.keyword.mobilepushshort}}が有効になっているすべてのアプリケーションに、デフォルトで有効になっています。{{site.data.keyword.mobilepushshort}}サービスが有効になっているアプリケーションでは、Push.ALL タグへのサブスクリプションが事前定義されています。サーバーはこれを使用して、通知メッセージをすべてのデバイスにブロードキャストします。REST Push API を使用するブロードキャスト通知を送信する場合は、メッセージ・リソースに投稿する際に「target」が空の JSON ファイルであることを確認してください。


###タグ・ベースの通知
{: tag-based-notifications}

タグ通知は、特定のタグにサブスクライブしているすべてのデバイスをターゲットとするメッセージです。タグ・ベースの通知では、サブジェクト・エリアまたはトピックに基づいて通知を分割できます。通知の受信側は、関心のあるサブジェクトまたはトピックに関するものであった場合にのみ通知を受信するように選択できます。そのため、タグ・ベースの通知は、受信側を分割する手段を提供します。この機能により、タグを定義した後、タグ別にメッセージの送受信を行うことが可能になります。メッセージは、タグにサブスクライブしているデバイスのみをターゲットにします。まず、アプリケーションのタグを作成し、タグ・サブスクリプションをセットアップしてから、タグ・ベースの通知を開始する必要があります。REST API を使用するタグ・ベースの通知を送信する場合は、メッセージ・リソースに投稿する際に「tagNames」が指定されていることを確認してください。

###ユニキャスト通知
{: unicast-notifications}

ユニキャスト通知は、特定のデバイスまたはユーザーをターゲットとするメッセージです。デバイスをターゲットとするユニキャスト通知は、追加のセットアップを必要とせず、アプリケーションで{{site.data.keyword.mobilepushshort}}が有効になっている場合にデフォルトで有効になります。

ただし、ユーザーをターゲットとしたユニキャスト通知には、以下が必要です。

- モバイル・デバイスをプッシュ通知に登録するときに、ユーザー ID をデバイスと関連付ける。  

- バックエンド・アプリケーションを{{site.data.keyword.mobilepushshort}}サービスにバインドするときに割り振られる「clientSecret」を受け渡すことで、ユーザー ID 登録などの許可を行う。 

通常、モバイル・アプリケーションはまず、[Mobile Client Access](https://console.ng.bluemix.net/docs/services/mobileaccess/index.html) などの認証サービスに対してモバイル・アプリ・ユーザーを認証する認証サイクルを実行します。認証に成功すると、認証ユーザー ID が clientSecret とともにプッシュ・デバイス登録 API に渡されます。clientSecret の存在により、ユーザー ID とモバイル・デバイス登録の許可された関連付けのみが実行されます。
REST API を使用するユニキャスト通知を送信する場合は、メッセージ・リソースに投稿する際に deviceId または userId が指定されていることを確認してください。

###プラットフォーム・ベースの通知
{: platform-based-notifications}

特定のデバイス・プラットフォームに届くように通知のターゲットを設定することができます。例えば、すべての Android ユーザーにのみ通知を送信できます。
REST API を使用するプラットフォーム・ベースの通知を送信する場合には、メッセージ・リソースに投稿する際にターゲットのプラットフォームが指定されていることを確認してください。
プラットフォームを配列として指定します。サポートされるプラットフォームは、以下のとおりです。
* A (Apple) 
* G (Google)

## {{site.data.keyword.mobilepushshort}}のメッセージ・サイズ
{: #push-message-size}

{{site.data.keyword.mobilepushshort}}のメッセージ・ペイロード・サイズは、メディエーターによって異なります。 

###iOS
{: ios-message-size}

iOS 8 以降では、許容される最大サイズは 2 キロバイトです。Apple プッシュ通知サービスは、この制限を超える通知を送信しません。

###Android
{: android-message-size}

Android プラットフォームには、制限はありません。
