---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# CF アプリを使用したランタイム・アプリケーションのロギング
{: #logging_writing_to_log_from_cf_app}

{{site.data.keyword.Bluemix}} で Cloud Foundry アプリとそのランタイムのログ・データを永続化するには、ログを STDOUT と STDERR に書き込む必要があります。
{:shortdesc}

{{site.data.keyword.Bluemix_notm}} で、STDOUT と STDERR のログ・レコードは、次のように自動的に収集されます。

* STDOUT (標準出力) は一般情報を提供します。  
* STDERR (標準エラー) は、エラー・メッセージや他の診断警告を含む情報を提供します。 

Loggregator は、標準出力と標準エラーのデータを自動的にピックアップします。Loggregator は、Cloud Foundry 内部からログを転送するコンポーネントです。 

以下に例を示します。 

**Liberty Cloud Foundry アプリ**の場合、Liberty サーバーのデフォルト console.log は、Loggregator によって自動的にピックアップされます。 

* console.log には、JVM プロセスからのリダイレクトされた STDOUT と STDERR が含まれます。デフォルトの consoleLogLevel 構成を使用した場合、コンソール出力には主要なイベントおよびエラーが含まれます。デフォルトの copySystemStreams 構成を使用した場合は、system.out と system.err のストリームに書き込まれたメッセージも、コンソール出力に含まれます。コンソール出力には、-verbose:gc 出力などの、JVM プロセスによって直接書き込まれるメッセージが必ず含まれます。Liberty のロギング・レベルは server.xml で調整できます。
* consoleLogLevel は、console.log ハンドラーのフィルター・レベルを設定します。consoleLogLevel を INFO に設定すると、INFO、AUDIT、WARNING、ERROR のすべてのメッセージが console.log ファイルに書き込まれます。**注:** FINE、FINER、FINEST のログ項目は、trace.log ファイルにのみ書き込まれます。

Liberty for Java™ アプリケーションについて詳しくは、『[Liberty Profile: Logging and Trace ![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://www-01.ibm.com/support/knowledgecenter/was_beta_liberty/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html){: new_window}』を参照してください。

**Node.js Cloud Foundry アプリ** の場合、組み込みのコンソール・ロギング・モジュールを使用して、{{site.data.keyword.Bluemix}} でランタイムのロギングを構成できます。STDOUT と STDERR の両方にメッセージを書き込むことができます。

* console.log('message') はメッセージを STDOUT ストリームに送信します
* console.error('error_message') はエラーを STDERR ストリームに送信します

Node.js アプリケーションについて詳しくは、『[How to log in node.js![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://docs.nodejitsu.com/articles/intermediate/how-to-log){: new_window}』を参照してください。


**Ruby on Rails アプリケーション**について詳しくは、『[The Logger![外部リンク・アイコン](../../../icons/launch-glyph.svg "外部リンク・アイコン")](http://guides.rubyonrails.org/debugging_rails_applications.html#the-logger){: new_window}』を参照してください。

以下の表に、いくつかのアプリケーション・ランタイム・ログと、Loggregator によって自動的にピックアップされるログのマッピングをリストします。

| **ランタイム** |    **STDOUT**     | **STDERR** |
|-----------------|-------------------|-------------------|
| Liberty | system.out | system.err |
| Node.js | console.log、console.info | console.error、console.warn |
| Ruby | stdout| stderr |
{: caption="表 1. いくつかのアプリケーション・ランタイム・ログと、Loggregator によって自動的にピックアップされるログ間のマッピング" caption-side="top"}

