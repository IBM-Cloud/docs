---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# トラブルシューティング
{: #errors}
最終更新日: 2017 年 4 月 12 日
{: .last-updated}

このトピックでは、プッシュ通知サービスの使用時に発生することがあるエラー・シナリオを識別し、解決する方法について説明します。

## 一般的なプッシュ通知の問題の解決
{: #troubleshooting_notification_errors}

### 内部サーバー・エラーが発生しました。管理者に連絡してください。(内部エラー・コード: PUSHD102E)
{: #troubleshooting_notification_internal}

**説明**: このエラーは、2015 年 11 月より前にプッシュ・インスタンスを作成した場合に発生する可能性があります。  

**ユーザー応答**: 問題を解決するには、プッシュ・インスタンスを削除して、新しいプッシュ・インスタンスを作成します。プッシュ・インスタンスを削除すると、タグは保持されないことに注意してください。


### UnauthorizedRegistration
{: #troubleshooting_notification_unauth}

**説明**: Chrome Web Push は、Firebase Cloud Messaging (FCM) キーでは動作しません。GCM から FCM への移行後に Chrome 上で Web プッシュ通知を受け取れない場合、その原因は Web サイトが以前に GCM プロジェクトで動作するように構成されており、新規プロジェクトは FCM で作成されていることにあります。ブラウザーを識別する生成済みトークンは、Chrome ブラウザーによってキャッシュされます。

**ユーザー応答**: Cookie を削除し、ブラウザーの許可を再設定することで、この問題を解決できます。この場合、Push Notifications を有効にするための許可を要求することになります。 


### このブラウザーでは Service Worker はサポートされません
{: #troubleshooting_notification_service_workers}

**説明**: Service Worker を使用する `BMSPushSDK.js` の一部として組み込まれた SDK が使用できません。 

**ユーザー応答**: Service Worker をサポートするブラウザーに切り替えることをお勧めします。サポートされるブラウザーのバージョンは、Firefox バージョン 49 以降と Chrome バージョン 53 (64 ビット) 以降です。


### SecurityError: この操作は安全ではありません
{: #troubleshooting_notification_insecure}

**説明**:  このエラーは、Firefox で Web コンソールを有効にした時に表示されることがあります。プッシュ通知サービスの Web プッシュ・サポートでは、`http` プロトコルではなく `https` プロトコルを使用して Web サイトにアクセスする必要があります。

**ユーザー応答**: ブラウザーから `https` を使用して Web サイトへの接続を試行することをお勧めします。


## Web プッシュ構成エラーの解決
{: #troubleshooting_configuration_errors}

Web プッシュ構成に関連したエラーは、`BMSPushSDK.js` ファイルの中身を調べることで診断できます。このファイルには、失敗に関する情報が含まれています。 

コールバックで返されたエラーを解析するには、以下のサンプル・コードを検討してください。

```
function showStatus(response) {
 if(response.statusCode == 200 || response.statusCode == 201) {
   		document.getElementById("status").innerHTML = "Response is " + response.response;
   	}
   	else if(response.statusCode == 0) {
  		if(response.response) {
  			document.getElementById("status").innerHTML = response.response;	
    		}
    		else {
    			document.getElementById("status").innerHTML = "There is a possible CORS or access issue while attempting the request.";	
   		}   		
   	}
   	else {
   		document.getElementById("status").innerHTML = "Response is " + response.response + " with the error "
		+ response.error + " and the status code " + response.statusCode;
   	}
 	}
```
	{: codeblock}


- `applicationId` が誤って構成されていると {{site.data.keyword.mobilepushshort}} サービスへの初期要求が失敗し、それにより statusCode はゼロ (0) に設定されます。
- 状況コード 200 または 201 は、正常な応答を示しています。
- `clientSecret` が無効な場合、statusCode に 401 応答が設定されます。`response.reponse` エレメントには、エラーの説明が含まれます。


## プッシュ通知サービスのエラー・メッセージの解決
{: #troubleshooting_service_errors}

以下の {{site.data.keyword.mobilepushshort}} エラー・メッセージは、REST API 要求に対する応答として返されます。

エラー応答の例は以下のとおりです。
```
	{
		"message": "Missing APNs credentials",
		"docUrl": "https://www.ng.bluemix.net/docs/troubleshoot/errors/mobilepush/index.html#FPWSE0003E",
		"code":   "FPWSE0003E"
	}
```
		    {: codeblock}

エラーに関する追加情報を入手するには、資料で関連のエラー・コードを検索してください。

### FPWSE0001E
{: #error_fpwse0001e}

**説明**: 照会しようとしているリソース (タグやサブスクリプションなど) は、このサーバー上では使用不可です。

**ユーザー応答**: メッセージで報告されたリソースを作成してください。代わりに、正しい ID を指定してリソースを照会することもできます。


### FPWSE0002E
{: #error_fpwse0002e}

**説明**: 作成しようとしているリソースは、既にサーバーで使用可能になっています。この場合のリソースは、タグやサブスクリプションなどです。

**ユーザー応答**: 異なる ID を使用してリソースを作成してください。


### FPWSE0003E
{: #error_fpwse0003e}

**説明**: {{site.data.keyword.mobilepushshort}} サービスの前提条件となる構成が完了していません。Apple Push Notification サービス (APNs) の資格情報をまだ構成していないのに取得しようとしている可能性があります。

**ユーザー応答**: {{site.data.keyword.mobilepushshort}}  サービスが APNs 用の有効なセキュリティー証明書を使用して構成されているようにしてください。詳しくは、[通知プロバイダーの資格情報の構成 ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](t__main_push_config_provider.html){: new_window}を参照してください。


### FPWSE0004E
{: #error_fpwse0004e}

**説明**: 要求に含まれる JSON 本体が無効です。


**ユーザー応答**: 要求では有効な JSON 構文を使用してください。



### FPWSE0005E
{: #error_fpwse0005e}

**説明**: {{site.data.keyword.mobilepushshort}} サーバーに対する要求が正しくないか、または不完全です。API 要求を実行するために必要なプロパティー値が JSON 本体に含まれていません。例えば、パスワードが無効であるか、またはデバイス・トークンが欠落しています。


**ユーザー応答**: メッセージを確認して、欠落しているプロパティー値または無効なプロパティー値を調べ、必要な情報を入力してください。



### FPWSE0006E
{: #error_fpwse0006e}

**説明**: 要求の JSON 本体に、{{site.data.keyword.mobilepushshort}} サーバーが理解できないパラメーターが含まれています。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



### FPWSE0007E 
{: #error_fpwse0007e}

**説明**: 要求 URL に、認識されないパラメーターが含まれる照会ストリングがあります。例えば、サブスクリプションを削除する要求に deviceId と tagName 以外のパラメーターが含まれている場合に、このエラーが発生する可能性があります。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



### FPWSE0008E
{: #error_fpwse0008e}

**説明**: 要求 URL に、必須パラメーターが欠落している照会ストリングがあります。例えば、サブスクリプションを削除する要求から deviceId パラメーターや tagName パラメーターが欠落していることが考えられます。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



### FPWSE0009E
{: #error_fpwse0009e}

**説明**: 通知を送信しようとしましたが、アプリケーションに登録されているデバイスがありません。

**ユーザー応答**: 通知を送信する前に、アプリケーションにデバイスを登録しておくようにしてください。



### FPWSE0010E
{: #error_fpwse0010e}

**説明**: サーバーに実行依頼された要求により、例外条件が発生しました。このエラーの原因は、以下のいずれかの条件である可能性があります。

- {{site.data.keyword.mobilepushshort}} が使用する内部サブシステムが応答していない。
- 要求の結果が、{{site.data.keyword.mobilepushshort}} によって処理できない可能性のあるエラー条件になった。
- {{site.data.keyword.mobilepushshort}} サービスには管理者による対応が必要である。

**ユーザー応答**: 要求を再試行してください。問題が解決しない場合は、IBM ソフトウェア・サポートにお問い合わせください。



### FPWSE0011E
{: #error_fpwse0011e}

**説明**: タグのサブスクリプションがサーバー上に既に存在しています。例えば、既に存在しているサブスクリプションを作成しようとした場合です。

**ユーザー応答**: 固有のタグ名を使用してサブスクリプションを作成してください。



### FPWSE0012E
{: #error_fpwse0012e}

**説明**: タグのサブスクリプションがサーバー上に存在しません。存在しないサブスクリプションを取得または削除する要求を処理依頼した場合に、このエラーが発生します。


**ユーザー応答**: 要求では正しいタグ名とデバイス ID を使用してください。



### FPWSE0013E
{: #error_fpwse0013e}

**説明**: 要求に含まれる JSON ペイロードが無効です。


**ユーザー応答**: JSON ペイロードが有効になるようにしてください。


### FPWSE0025E
{: #error_fpwse0025e}

**説明**: 現在サーバーは要求を処理できません。

**ユーザー応答**: しばらく時間をおいてから要求を再サブミットしてください。


### FPWSE1007E 
{: #error_fpwse1007e}

**説明**: {{site.data.keyword.mobilepushshort}} サービスがこのアプリケーションでは使用不可になっています。原因は料金の請求にあるか、あるいは管理者によってアプリが無効にされたことが考えられます。


**ユーザー応答**: Bluemix の資料にあるトラブルシューティング関連のトピックを参照して、サービス状況の確認、トラブルシューティング情報の検討、またはヘルプの取得に関する情報を確認してください。



### FPWSE1079E
{: #error_fpwse1079e}

**説明**: 照会操作のために指定されたオフセット値が無効です。

**ユーザー応答**: オフセット値は 0 (ゼロ) 以上になるようにしてください。



### FPWSE1080E 
{: #error_fpwse1080e}

**説明**: 照会操作のために指定されたサイズ値が無効です。

**ユーザー応答**: サイズ値は 0 (ゼロ) より大きくなるようにしてください。


