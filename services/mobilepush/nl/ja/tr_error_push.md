---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# {{site.data.keyword.mobilepushshort}} サービスのエラー・メッセージ
{: #errors}
最終更新日: 2017 年 2 月 13 日
{: .last-updated}


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

## FPWSE0001E
{: #error_fpwse0001e}

**説明**: 照会しようとしているリソース (タグやサブスクリプションなど) は、このサーバー上では使用不可です。

**ユーザー応答**: メッセージで報告されたリソースを作成してください。代わりに、正しい ID を指定してリソースを照会することもできます。


## FPWSE0002E
{: #error_fpwse0002e}

**説明**: 作成しようとしているリソースは、既にサーバーで使用可能になっています。この場合のリソースは、タグやサブスクリプションなどです。

**ユーザー応答**: 異なる ID を使用してリソースを作成してください。


## FPWSE0003E
{: #error_fpwse0003e}

**説明**: {{site.data.keyword.mobilepushshort}} サービスの前提条件となる構成が完了していません。Apple Push Notification サービス (APNs) の資格情報をまだ構成していないのに取得しようとしている可能性があります。

**ユーザー応答**: {{site.data.keyword.mobilepushshort}}  サービスが APNs 用の有効なセキュリティー証明書を使用して構成されているようにしてください。詳細情報については、[APNs の資格情報の構成![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](t_push_provider_ios.html){: new_window}を参照してください。


## FPWSE0004E
{: #error_fpwse0004e}

**説明**: 要求に含まれる JSON 本体が無効です。


**ユーザー応答**: 要求では有効な JSON 構文を使用してください。



## FPWSE0005E
{: #error_fpwse0005e}

**説明**: {{site.data.keyword.mobilepushshort}} サーバーに対する要求が正しくないか、または不完全です。API 要求を実行するために必要なプロパティー値が JSON 本体に含まれていません。例えば、パスワードが無効であるか、またはデバイス・トークンが欠落しています。


**ユーザー応答**: メッセージを確認して、欠落しているプロパティー値または無効なプロパティー値を調べ、必要な情報を入力してください。



## FPWSE0006E
{: #error_fpwse0006e}

**説明**: 要求の JSON 本体に、{{site.data.keyword.mobilepushshort}} サーバーが理解できないパラメーターが含まれています。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



## FPWSE0007E 
{: #error_fpwse0007e}

**説明**: 要求 URL に、認識されないパラメーターが含まれる照会ストリングがあります。例えば、サブスクリプションを削除する要求に deviceId と tagName 以外のパラメーターが含まれている場合に、このエラーが発生する可能性があります。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



## FPWSE0008E
{: #error_fpwse0008e}

**説明**: 要求 URL に、必須パラメーターが欠落している照会ストリングがあります。例えば、サブスクリプションを削除する要求から deviceId パラメーターや tagName パラメーターが欠落していることが考えられます。


**ユーザー応答**: 要求内の JSON 本体が、{{site.data.keyword.mobilepushshort}} サーバーで予想されている要求の形式に従っていることを確認してください。詳細情報については、[REST API ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://mobile.{DomainName}/imfpush/){: new_window}を参照してください。



## FPWSE0009E
{: #error_fpwse0009e}

**説明**: 通知を送信しようとしましたが、アプリケーションに登録されているデバイスがありません。

**ユーザー応答**: 通知を送信する前に、アプリケーションにデバイスを登録しておくようにしてください。



## FPWSE0010E
{: #error_fpwse0010e}

**説明**: サーバーに実行依頼された要求により、例外条件が発生しました。このエラーの原因は、以下のいずれかの条件である可能性があります。

- {{site.data.keyword.mobilepushshort}} が使用する内部サブシステムが応答していない。
- 要求の結果が、{{site.data.keyword.mobilepushshort}} によって処理できない可能性のあるエラー条件になった。
- {{site.data.keyword.mobilepushshort}} サービスには管理者による対応が必要である。

**ユーザー応答**: 要求を再試行してください。問題が解決しない場合は、IBM ソフトウェア・サポートにお問い合わせください。



## FPWSE0011E
{: #error_fpwse0011e}

**説明**: タグのサブスクリプションがサーバー上に既に存在しています。例えば、既に存在しているサブスクリプションを作成しようとした場合です。

**ユーザー応答**: 固有のタグ名を使用してサブスクリプションを作成してください。



## FPWSE0012E
{: #error_fpwse0012e}

**説明**: タグのサブスクリプションがサーバー上に存在しません。存在しないサブスクリプションを取得または削除する要求を処理依頼した場合に、このエラーが発生します。


**ユーザー応答**: 要求では正しいタグ名とデバイス ID を使用してください。



## FPWSE0013E
{: #error_fpwse0013e}

**説明**: 要求に含まれる JSON ペイロードが無効です。


**ユーザー応答**: JSON ペイロードが有効になるようにしてください。


## FPWSE0025E
{: #error_fpwse0025e}

**説明**: 現在サーバーは要求を処理できません。

**ユーザー応答**: しばらく時間をおいてから要求を再サブミットしてください。


## FPWSE1007E 
{: #error_fpwse1007e}

**説明**: {{site.data.keyword.mobilepushshort}} サービスがこのアプリケーションでは使用不可になっています。原因は料金の請求にあるか、あるいは管理者によってアプリが無効にされたことが考えられます。


**ユーザー応答**: Bluemix の資料にあるトラブルシューティング関連のトピックを参照して、サービス状況の確認、トラブルシューティング情報の検討、またはヘルプの取得に関する情報を確認してください。



## FPWSE1079E
{: #error_fpwse1079e}

**説明**: 照会操作のために指定されたオフセット値が無効です。

**ユーザー応答**: オフセット値は 0 (ゼロ) 以上になるようにしてください。



## FPWSE1080E 
{: #error_fpwse1080e}

**説明**: 照会操作のために指定されたサイズ値が無効です。

**ユーザー応答**: サイズ値は 0 (ゼロ) より大きくなるようにしてください。



