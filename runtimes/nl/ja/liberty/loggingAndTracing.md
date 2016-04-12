---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ロギングとトレース
{: #logging_tracing}

*最終更新日時: 2016 年 3 月 23 日*

## ログ・ファイル
{: #log_files}

標準 Liberty ログ (messages.log  または ffdc directory など) は、IBM Bluemix の各アプリケーション・インスタンスのログ・ディレクトリーにあります。これらのログは、IBM Bluemix コンソールから、または cf logs および cf files コマンドを使用して、アクセスできます。例えば、messages.log ファイルを表示するには、次のコマンドを実行します。
```
    $ cf files <yourappname> logs/messages.log
```
{: codeblock}

ログ・レベルおよびその他のトレース・オプションは、Liberty 構成ファイルで設定できます。詳しくは、[Liberty プロファイル: トレースおよびロギング](http://www.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.multiplatform.doc/ae/rwlp_logging.html?cp=SSAW57_8.5.5%2F3-17-0-0)を参照してください。トレースは、IBM Bluemix コンソールを使用してアプリケーション・インスタンスの実行中に調整することもできます。

## トレース機能およびダンプ機能の使用
{: #using_trace_and_dump}

IBM Bluemix ユーザー・インターフェースには、トレース機能およびダンプ機能があります。
* トレースを使用すると、実行しているアプリケーション・インスタンスの Liberty ロギングおよびトレース仕様を表示および更新できます。
* ダンプを使用すると、実行しているアプリケーション・インスタンスのスレッド・ダンプおよびヒープ・ダンプを作成および操作できます。

このアクションを行うには、ユーザー・インターフェースで Liberty アプリケーションを選択します。
左側のナビゲーションにあるランタイムの下で、インスタンス詳細を開くことができます。1 つまたは複数のインスタンスを選択してください。
「アクション」メニューの下で、TRACE または DUMP を選択できます。

# 関連リンク
## 一般
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
