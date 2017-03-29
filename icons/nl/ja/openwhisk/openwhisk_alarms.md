---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Alarm パッケージの使用
{: #openwhisk_catalog_alarm}

`/whisk.system/alarms` パッケージを使用して、指定した頻度でトリガーを発生させることができます。これは、1 時間ごとにシステム・バックアップ・アクションを起動するといった、ジョブやタスクの繰り返しをセットアップする際に便利です。

このパッケージには、以下のフィードが含まれています。

| エンティティー | タイプ  | パラメーター | 説明 |
| --- | --- | --- | --- |
| `/whisk.system/alarms` | パッケージ | - | アラームおよび定期的ユーティリティー |
| `/whisk.system/alarms/alarm` | フィード | cron、trigger_payload、maxTriggers | トリガー・イベントを定期的に発生させる |


## トリガー・イベントの定期的な発生
{: #openwhisk_catalog_alarm_fire}

 `/whisk.system/alarms/alarm` フィードは、
Alarm サービスを構成して、指定した頻度でトリガー・イベントを発生させます。パラメーターは次のとおりです。


- `cron`: トリガーを発生させるタイミングを協定世界時 (UTC) で示す、UNIX crontab 構文に基づいたストリング。このストリングは、`X X X X X` のようにスペースで区切られた 5 個のフィールドのシーケンスです。cron 構文の使用について詳しくは、http://crontab.org を参照してください。ストリングで示される頻度のいくつかの例を以下に示しま す。

  - `* * * * *`: 毎分の先頭。
  - `0 * * * *`: 毎時の先頭。
  - `0 */2 * * *`: 2 時間ごと (つまり、02:00:00、04:00:00、...)
  - `0 9 8 * *`: 毎月 8 日目の午前 9:00:00 (UTC)

- `trigger_payload`: このパラメーターの値は、
トリガーが発生するたびにトリガーのコンテンツになります。

- `maxTriggers`: この限界に達するとトリガーの発生を停止します。デフォルトは 1,000,000 です。無限 (-1) に設定できます。

以下は、トリガー・イベントに `name` と `place` の値を指定して、2 分ごとに 1 回発生するトリガーを作成する例です。

  ```
  wsk trigger create periodic \
    --feed /whisk.system/alarms/alarm \
    --param cron "*/2 * * * *" \
    --param trigger_payload "{\"name\":\"Odin\",\"place\":\"Asgard\"}"
  ```
  {: pre}

生成される各イベントは、`trigger_payload` の値に指定されるプロパティーをパラメーターとして含みます。この場合、各トリガー・イベントは、
パラメーター `name=Odin` と `place=Asgard` を含みます。

**注**: パラメーター `cron` も、6 個のフィールドのカスタム構文をサポートします。ここで、最初のフィールドは秒を表します。
このカスタム cron 構文の使用について詳しくは、https://github.com/ncb000gt/node-cron を参照してください。
以下は、6 個のフィールドの表記を使用した例です。
  - `*/30 * * * * *`: 30 秒ごと。

