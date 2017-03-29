---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-13"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# {{site.data.keyword.openwhisk_short}} CLI

{{site.data.keyword.openwhisk_short}} には、システムのすべての局面を完全に管理できる強力なコマンド・ライン・インターフェースがあります。

## {{site.data.keyword.openwhisk_short}} CLI のセットアップ 

{{site.data.keyword.openwhisk_short}} コマンド・ライン・インターフェース (CLI) を使用して、名前空間および許可鍵をセットアップできます。[「CLI の構成」](https://new-console.{DomainName}/openwhisk/cli){: new_window}に移動し、手順に従ってインストールしてください。

CLI を使用するためには、以下の 2 つの必須プロパティーを構成する必要があります。

1. 使用したい {{site.data.keyword.openwhisk_short}} デプロイメントの **API ホスト** (名前または IP アドレス)。
2. {{site.data.keyword.openwhisk_short}} API へのアクセスを認可する**許可鍵** (ユーザー名とパスワード)。

API ホストを設定するには、以下のコマンドを実行します。

```
wsk property set --apihost openwhisk.ng.bluemix.net
```
{: pre} 

許可鍵が分かっている場合、それを使用するように CLI を構成できます。 

許可鍵を設定するには、以下のコマンドを実行します。

```
wsk property set --auth <authorization_key>
```
{: pre}

**ヒント:** デフォルトでは、OpenWhisk CLI は、設定されたプロパティーを `~/.wskprops` に保管します。このファイルの場所は、`WSK_CONFIG_FILE` 環境変数を設定することにより変更できます。 

CLI セットアップを確認するため、[アクションを作成して実行](./index.html#openwhisk_start_hello_world)してみてください。

## {{site.data.keyword.openwhisk_short}} CLI の使用 

環境を構成した後、{{site.data.keyword.openwhisk_short}} CLI の使用を開始して、以下を行うことができます。

* 自身のコード・スニペット (アクション) を {{site.data.keyword.openwhisk_short}} で実行します。『[アクションの作成と起動](./openwhisk_actions.html)』を参照してください。
* トリガーおよびルールを使用して、アクションがイベントに対応できるようにします。『[トリガーおよびルールの作成](./openwhisk_triggers_rules.html)』を参照してください。
* パッケージがアクションをどのようにバンドルし、外部イベント・ソースを構成するのかを学習します。『[パッケージの使用と作成](./openwhisk_packages.html)』を参照してください。
* パッケージ・カタログを検討し、[Cloudant イベント・ソース](./openwhisk_cloudant.html)などの外部サービスでアプリケーションを強化します。『[OpenWhisk 対応サービスの使用](./openwhisk_catalog.html)』を参照してください。

## HTTPS プロキシーを使用するための CLI の構成

HTTPS プロキシーを使用するように CLI をセットアップできます。HTTPS プロキシーをセットアップするには、`HTTPS_PROXY` という名前の環境変数を作成する必要があります。この変数をフォーマット `{PROXY IP}:{PROXY PORT}` を使用して HTTPS プロキシーのアドレスとそのポートに設定する必要があります。
