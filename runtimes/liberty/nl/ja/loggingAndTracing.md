---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ロギングとトレース
{: #logging_tracing}

## ログ・ファイル
{: #log_files}

標準 Liberty ログ (`messages.log` や `ffdc` ディレクトリーなど) が IBM Bluemix で使用可能であり、各アプリケーション・インスタンスの `logs` ディレクトリーにあります。これらのログには、IBM Bluemix コンソールから、または CF CLI を使用してアクセスできます。例えば、次のとおりです。

* アプリケーションの最新のログにアクセスするには、以下のコマンドを実行します。

  ```
  $ cf logs --recent <appname>
  ```
  {: codeblock}

* DEA ノードで実行されているアプリケーションの `messages.log` ファイルを表示するには、以下のコマンドを実行します。

  ```
  $ cf files <appname> logs/messages.log
  ```
  {: codeblock}

* Diego セルで実行されているアプリケーションの `messages.log` ファイルを表示するには、以下のコマンドを実行します。

  ```
  $ cf ssh <appname> -c "cat logs/messages.log"
  ```
  {: codeblock}

ログ・レベルおよびその他のトレース・オプションは、Liberty 構成ファイルで設定できます。詳しくは、[Liberty プロファイル: トレースおよびロギング](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)を参照してください。トレースは、IBM Bluemix コンソールを使用してアプリケーション・インスタンスの実行中に調整することもできます。

## トレース機能およびダンプ機能の使用
{: #using_trace_and_dump}

実行中のアプリケーション用に IBM Bluemix コンソールから直接、Liberty トレース構成を調整できます。コンソールには、スレッド・ダンプおよびヒープ・ダンプの要求およびダウンロードを行う機能もあります。トレース構成の調整またはダンプの要求を行うには、Bluemix コンソールで Liberty アプリケーションを選択し、ナビゲーションで`「ランタイム」`メニューを選択します。`「ランタイム」`ビューで、インスタンスを選択し、*「トレース」*ボタンまたは*「ダンプ」*ボタンを押します。トレース・レベルを調整する場合、トレース仕様の構文の詳細については、[Liberty プロファイル: ロギングおよびトレース](http://www.ibm.com/support/knowledgecenter/SSEQTP_liberty/com.ibm.websphere.wlp.doc/ae/rwlp_logging.html)を参照してください。

### Diego: SSH を介したダンプのトリガー

Diego セルで実行されているアプリケーションの場合、SSH フィーチャーを使用して CF CLI を介してスレッド・ダンプおよびヒープ・ダンプをトリガーすることも可能です。例えば、次のとおりです。

```
$ cf ssh <appname> -c "pkill -3 java"
```
{: codeblock}

生成されたダンプ・ファイルの表示およびダウンロードについて詳しくは、以下の説明を参照してください。

## ダンプ・ファイルのダウンロード
{: #download_dumps}

デフォルトでは、各種ダンプ・ファイルはアプリケーション・コンテナーの `dumps` ディレクトリーに置かれます。

### DEA アプリケーション

DEA ノードで実行されているアプリケーションのダンプ・ファイルの表示およびダウンロードを行うには、"cf files" 機能を使用します。

* 生成されたダンプを表示するには、以下のコマンドを実行します。

  ```
  $ cf files <appname> dumps
  ```
  {: codeblock}

* ダンプ・ファイルをダウンロードするには、以下のコマンドを実行します。

    1. アプリケーション GUID を取得します。

      ```
      $ cf app <appname> --guid
      ```
      {: codeblock}

    2. ダンプ・ファイルをダウンロードします。

      ```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```
      {: codeblock}

### Diego アプリケーション

Diego セルで実行されているアプリケーションのダンプ・ファイルの表示およびダウンロードを行うには、"cf ssh" 機能を使用します。

* 生成されたダンプを表示するには、以下のコマンドを実行します。

  ```
  $ cf ssh <appname> -c "ls -l dumps"
  ```
  {: codeblock}

* ダンプ・ファイルをダウンロードするには、以下のコマンドを実行します。

  ```
  $ cf ssh <appname> -i <instance_id> -c "cat dumps/<dump_file_name>" > <local_dump_file_name>
  ```
  {: codeblock}

`scp` およびその他の類似ツールを使用してダンプ・ファイルの表示およびダウンロードを行うことも可能です。詳しくは、[SSH を使用したアプリケーションへのアクセス ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) を参照してください。

# 関連リンク
{: #rellinks notoc}
## 一般
{: #general notoc}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
