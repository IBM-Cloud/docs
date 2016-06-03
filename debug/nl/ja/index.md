---

copyright:
  years: 2015, 2016

---


{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}


# デバッグ
{: #debugging}

*最終更新日: 2016 年 3 月 3 日*

{{site.data.keyword.Bluemix}} で問題が発生した場合、ログ・ファイルを確認して問題を調査し、エラーをデバッグすることができます。
{:shortdesc}

ログは、ジョブが正常に実行されているか失敗しているかなどの情報を提供します。また、問題の原因のデバッグおよび判別に使用できる関連情報も提供します。

ログは固定フォーマットで提供されます。詳細ログの場合、ログをフィルターに掛けたり、外部ロギング・ホストを使用してログを保管および処理したりできます。ログのフォーマット、ログの表示とフィルター処理、および外部ロギングの構成について詳しくは、『[Cloud Foundry で実行されているアプリのロギング](../monitor_log/monitoringandlogging.html#logging_for_bluemix_apps){: new_window}』を参照してください。


## ステージング・エラーのデバッグ
{: #debugging-staging-errors}
{{site.data.keyword.Bluemix_notm}} でアプリケーションをステージングする際に問題が発生する場合があります。
アプリがステージングに失敗した場合、ログを使用してエラーの原因を調べ、問題から回復することができます。

{{site.data.keyword.Bluemix_notm}} 上でアプリが失敗する場合の原因を理解するには、アプリがどのように {{site.data.keyword.Bluemix_notm}} にデプロイされ、実行されるかを把握する必要があります。詳細については、[「アプリケーション・デプロイメント (Application
deployment)」](../manageapps/depapps.html#appdeploy){: new_window}を参照してください。

以下の手順は、`cf
logs` コマンドを使用してステージング・エラーをデバッグする方法を示しています。以下のステップを実行する前に、cf コマンド・ライン・インターフェースがインストール済みであることを確認してください。cf コマンド・ライン・インターフェースのインストールについて詳しくは、[「cf コマンド・ライン・インターフェースのインストール」](../starters/install_cli.html){: new_window}を参照してください。

  1. cf コマンド・ライン・インターフェースに次のコードを入力して、{{site.data.keyword.Bluemix_notm}} に接続します。```
	 cf api https://api.ng.bluemix.net
	 ```
	 
  2. `cf login` を入力して {{site.data.keyword.Bluemix_notm}} にログインします。
  
  3. `cf logs appname --recent` を入力して、最近のログを取得します。詳細ログをフィルターに掛けたい場合は、`grep` オプションを使用してください。例えば、以下のコードを入力すれば、[STG] のログのみ表示することができます:
```
	cf logs appname --recent | grep '\[STG\]'
	```
  4. ログ内に表示された最初のエラーを確認します。
  
IBM Eclipse tools for {{site.data.keyword.Bluemix_notm}} プラグインを使用してアプリケーションをデプロイする場合、Eclipse ツールの**「コンソール」**タブに、cf logs 出力に似たログが表示されます。アプリケーションをデプロイするときに、`ログ`をトラッキングするために別の Eclipse ウィンドウを開くこともできます。

`cf
logs` コマンドに加えて、{{site.data.keyword.Bluemix_notm}} では、ログの詳細を収集するための Monitoring and Analytics サービスを使用することも可能です。また、Monitoring and Analytics サービスは、ご使用のアプリケーションのパフォーマンス、正常性、および可用性をモニターします。Node.js および
Liberty ランタイム・アプリケーションのログ分析も提供されます。  

### Node.js アプリケーションのステージング・エラーのデバッグ

以下の例は、`cf logs appname --recent` を入力した後に表示されるログを示しています。この例では、Node.js
 アプリケーションに対するステージング・エラーが発生したと想定しています。
```
2014-08-11T14:19:36.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({name"=>"SampleExpressApp"}
2014-08-11T14:20:44.17+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STOPPED"})
2014-08-11T14:20:44.19+0100 [App/0]   ERR
2014-08-11T14:20:44.43+0100 [DEA]     OUT Stopping app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:44.44+0100 [DEA]     OUT Stopped app instance (index 0) with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:48.97+0100 [DEA]     OUT Got staging request for app with id 6d80051d-eb56-4fc5-b499-e43d6fb87bc2
2014-08-11T14:20:50.94+0100 [API]     OUT Updated app with guid 6d80051d-eb56-4fc5-b499-e43d6fb87bc2 ({"state"=>"STARTED"})
2014-08-11T14:20:51.66+0100 [STG]     OUT -----> Download app package (4.1M)
2014-08-11T14:20:51.90+0100 [STG]     OUT -----> Download app buildpack cache (1.1M)
2014-08-11T14:20:52.78+0100 [STG]     OUT -----> Buildpack Version: v1.1-20140717-1447
2014-08-11T14:20:52.78+0100 [STG]     ERR parse error: Expected another key-value pair at line 18, column 3
2014-08-11T14:20:52.79+0100 [STG]     OUT 0 info it worked if it ends with ok
```
{: screen}


ログの最初のエラーが、ステージングが失敗した理由を示しています。この例では、最初のエラーはステージングの段階での DEA コンポーネントからの出力です。```
2014-08-11T14:20:52.78+0100 [STG]   ERR parse error: expected another key-value pair at line 18, column 3```
{: screen}


Node.js アプリケーションに対し、DEA は `package.json` ファイル内の情報を使用してモジュールをダウンロードします。このエラーから、モジュールに対してエラーが発生することが分かります。このため、`package.json` ファイルの 18 行目を確認する必要があるかもしれません。 

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*",
18   }
```
{: screen}


17 行目の末尾にコンマが置かれていることが分かります。これにより、18 行目では鍵と値のペアが予測されます。問題を修正するには、このコンマを削除してください。

```
15   "jade": "~1.3.0",
16   "mongodb": "*",
17   "monk":"*"
18   }
```
{: screen}


## ランタイム・エラーのデバッグ
{: #debugging-runtime-errors}
実行時にアプリケーションに関する問題が発生した場合、アプリケーション・ログがエラーの原因の特定と問題からの復旧に役立ちます。 

特に、STDOUT および STDERR へのロギングを使用可能にできます。
{{site.data.keyword.Bluemix_notm}} 組み込みビルドパックを使用してデプロイされたアプリケーション用のログ・ファイルの構成方法について詳しくは、以下のリストを参照してください。

  * Liberty for Java™ アプリケーションの場合は、『[Liberty Profile: Logging and Trace](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}』を参照してください。
  * Node.js アプリケーションの場合は、[「How to log in node.js」](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}を参照してください。 
  * PHP アプリケーションの場合は、 『[error_log](http://php.net/manual/en/function.error-log.php){: new_window}』を参照してください。
  * Python アプリケーションの場合は、 「[Logging
HOWTO](https://docs.python.org/2/howto/logging.html){: new_window}」を参照してください。
  * Ruby on Rails アプリケーションの場合は、[「The Logger」](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}を参照してください。
  * Ruby Sinatra アプリケーションの場合は、[「Logging」](http://www.sinatrarb.com/intro.html#Logging){: new_window}を参照してください。
  
cf コマンド・ライン・インターフェースに `cf logs appname --recent` と入力すると、最新のログのみが表示されます。以前に発生したエラーのログを表示するには、すべてのログを取得してエラーを検索する必要があります。ご使用のアプリケーションのログをすべて取得するには、以下のいずれかの方法を使用して下さい。
<dl> 
<dt><strong>{{site.data.keyword.Bluemix_notm}} Monitoring and Analytics サービス</strong></dt> 
<dd>Monitoring and Analytics サービスの統合されたログ・ファイル検索機能および分析機能は、エラーを素早く特定するのに役立ちます。詳しくは、<a href="../services/monana/index.html#gettingstartedtemplate" target="_blank">Monitoring and
Analytics</a> を参照してください。</dd> 
<dt><strong>サード・パーティー・ツール</strong></dt> 
<dd>アプリケーションからログを収集して、外部ログ・ホストにエクスポートすることができます。詳しくは、『<a href="../monitor_log/monitoringandlogging.html#thirdparty_logging" target="_blank">外部ロギングの構成</a>』を参照してください。</dd> 
<dt><strong>ログを収集しエクスポートするスクリプト</strong></dt> 
<dd>スクリプトを使用してログの収集と外部ファイルへのエクスポートを自動的に行うには、ご使用のコンピューターから {{site.data.keyword.Bluemix_notm}} サーバーへ接続する必要があります。また、ご使用のコンピューター上にログをダウンロードするために十分なスペースを確保しておく必要があります。詳しくは、『<a href="../support/index.html#collecting-diagnostic-information" target="_blank">診断情報の収集</a>』を参照してください。</dd>
</dl>

`stdout.log` ファイルおよび `stderr.log` ファイルは、以前は、デフォルトで、{{site.data.keyword.Bluemix_notm}} ダッシュボードのアプリケーション・ビューから**「ファイル」** > **「ログ」**を選択することによってアクセスできました。しかし、そのアプリケーションのロギングは、{{site.data.keyword.Bluemix_notm}} がホストされている現行バージョンの Cloud Foundry では使用不可になりました。stdout および stderr のアプリケーション・ロギングを、{{site.data.keyword.Bluemix_notm}} ダッシュボードで**「ファイル」** > **「ログ」**の下でアクセス可能にしておくために、使用しているランタイムに応じて、{{site.data.keyword.Bluemix_notm}} ファイル・システム内の他のファイルにロギングをリダイレクトできます。 

  * Liberty for Java アプリケーションの場合、stdout および stderr に向けられた出力は、logs ディレクトリー内の `messages.log` ファイルに既に含まれています。接頭部が SystemOut および
SystemErr のエントリーをそれぞれ探してください。
  * Node.js アプリケーションの場合、console.log 関数をオーバーライドして、明示的に logs ディレクトリー内のファイルに書き込むことができます。
  * PHP アプリケーションの場合、error_log 関数を使用して、logs ディレクトリー内のファイルに書き込むことができます。
  * Python アプリケーションの場合、次のように、ロガーを使用して logs ディレクトリー内のファイルに書き込むことができます: logging.basicConfig(filename='../../logs/example.log',level=logging.DEBUG)
  * Ruby アプリケーションの場合、ロガーを使用して logs ディレクトリー内のファイルに書き込むことができます。
 

# 関連リンク
{: #rellinks}

## 一般
{: #general}

  * [Droplet Execution Agent (DEA)](http://docs.cloudfoundry.org/concepts/architecture/execution-agent.html){: new_window}
  * [IBM Monitoring and Analytics for Bluemix サービス入門](../services/monana/index.html#gettingstartedtemplate){: new_window}
  * [Bluemix の動作](../public/index.html#howwork){: new_window}
  * [cf コマンド・ツールのインストール](../starters/install_cli.html){: new_window}
  * [ログの表示](../monitor_log/monitoringandlogging.html#viewing_logs){: new_window}
  
  
 














