---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-09"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# ロギングとトレース
{: #logging_tracing}

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
* ダンプを使用すると、実行しているアプリケーション・インスタンスのスレッド・ダンプおよびヒープ・ダンプを作成できます。

このアクションを行うには、ユーザー・インターフェースで Liberty アプリケーションを選択します。
ナビゲーションにあるカテゴリー「ランタイム」で、インスタンスの詳細を開くことができます。1 つまたは複数のインスタンスを選択してください。
「アクション」メニューで、TRACE または DUMP を選択できます。

## ダンプ・ファイルのダウンロード
{: #download_dumps}

<strong>前提条件:</strong>
* [CF CLI のインストール](https://docs.cloudfoundry.org/cf-cli/install-go-cli.html)
* [Diego-Enabler プラグインのインストール](https://github.com/cloudfoundry-incubator/Diego-Enabler) (アプリケーションを Diego で実行する場合)

<strong>アプリケーションを DEA で実行する場合、以下の手順を使用します。</strong>
  
1. app_guid を取得します
```
$ cf app <app_name> --guid
```

2. ダンプ・ファイルをダウンロードします
```
$ cf curl /v2/apps/<app_guid>/instances/<instance_id>/files/dumps/<dump_file_name> --output <local_dump_file_name>
```

<strong>アプリケーションを Diego で実行する場合、以下の手順を使用します。</strong>
  
1. app_guid を取得します
```
$ cf app <app_name> --guid
```

2. app_ssh_endpoint(host および port) および app_ssh_host_key_fingerprint を取得します
```
$ cf curl /v2/info
```

3. scp コマンド用の ssh-code を取得します
```
$ cf ssh-code
```

4. scp を実行してリモート・ダンプ・ファイルをローカルにコピーし、パスワードを要求されたら ssh-code を使用します
```
$ scp -P <app_ssh_endpoint_port> -o User=cf:<app_guid>/<instance_id> <app_ssh_endpoint_host>:/home/vcap/dumps/<dump_file_name> <local_dump_file_name>
```

詳しくは、[Accessing Apps with SSH](https://docs.cloudfoundry.org/devguide/deploy-apps/ssh-apps.html) を参照してください。


# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Liberty ランタイム](index.html)
* [Liberty プロファイル概要](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)

