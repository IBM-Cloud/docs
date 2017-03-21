---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 外部ログ・ホストの構成
{: #thirdparty_logging}

{{site.data.keyword.Bluemix_notm}} は、限られた量のログ情報をメモリー内に保持します。情報がログに記録されると、古い情報が新しい情報に置き換えられます。すべてのログ情報を保持するには、外部ログ・ホスト (例えば、サード・パーティーのログ管理サービスまたはその他のホスト) にログを保存することができます。
{:shortdesc}

アプリおよびシステムから外部ログ・ホストにログをストリーミングするには、以下の手順を実行します。

  1. ロギング・エンドポイントを決定します。

	 Papertrail、Splunk、または Sumologic など、サード・パーティーのログ集約機能にログを送信できます。また、syslog ホスト、TLS (Transport Layer Security) で暗号化された syslog ホスト、または HTTPS POST エンドポイントにログを送信することもできます。ロギング・エンドポイントを取得する方法は、ログ・ホストによって異なります。

  2. ユーザー提供のサービス・インスタンスを作成します。

	 `cf create-user-provided-service` コマンド (または、短縮版コマンドの `cups`) を使用して、ユーザー提供のサービス・インスタンスを作成します。
	 ```
	 cf create-user-provided-service <service_name> -l <logging_endpoint>
	 ```
	 &lt;service_name&gt;
	 
	 ユーザー提供のサービス・インスタンスの名前。

	 &lt;logging_endpoint&gt;

	 {{site.data.keyword.Bluemix_notm}} がログを送信する先のロギング・エンドポイント。次の表を参照して、*logging_endpoint* を適切な値で置き換えてください。

	 <table>
	 <caption>表 1. ロギング・エンドポイントの値</caption>
     <thead>
     <tr>
     <th>ロギング・エンドポイント</th>
     <th>コマンド</th>
	 <th>注</th>
     </tr>
     </thead>
     <tbody>
     <tr>
     <td>syslog ホスト</td>
     <td>`cf cups my-logs -l syslog://HOST:PORT`</td>
	 <td>例えば、Papertrail へのロギングを有効にするには、`cf cups my-logs -l syslog://<papertrail-url>` と入力します。 `<papertrail-url>` を、Papertrail からのロギング・エンドポイントの URL に置き換えてください。</td>
     </tr>
	 <tr>
     <td>syslog-tls ホスト</td>
     <td>`cf cups my-logs -l syslog-tls://HOST:PORT`</td>
	 <td>証明書は認証局によって信頼されている必要があります。自己署名証明書を使用しないでください。</td>
     </tr>
	 <tr>
     <td>HTTPS POST</td>
     <td>`cf cups my-logs -l https://HOST:PORT`</td>
	 <td>このエンドポイントは、パブリック・インターネットにあり、{{site.data.keyword.Bluemix_notm}} によってアクセス可能でなければなりません。</td>
     </tr>
     </tbody>
     </table>
  3. サービス・インスタンスをアプリにバインドします。

	 サービス・インスタンスをアプリにバインドするには、以下のコマンドを使用します。

	 ```
	 cf bind-service <appname> <service_name>
	 ```
	 &lt;appname&gt;
	 
	 アプリの名前。

	 &lt;service_name&gt;

	 ユーザー提供のサービス・インスタンスの名前。

  4. アプリを再ステージングします。
     変更を有効にするために、`cf restage appname` を入力します。

