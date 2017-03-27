---



copyright:

  years: 2015，2017

lastupdated: "2011-01-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Auto-Scaling CLI
{: #autoscalingcli}


{{site.data.keyword.autoscaling}} サービスは、{{site.data.keyword.autoscaling}} CLI for {{site.data.keyword.Bluemix_notm}} を使用して構成することができます。{{site.data.keyword.autoscaling}} CLI は Linux64、Win64、および OSX をサポートしており、Auto-Scaling RESTful API が提供する機能と同様の機能を提供します。
{: shortdesc}

始めに、{{site.data.keyword.Bluemix_notm}} CLI をインストールします。手順については、[{{site.data.keyword.Bluemix_notm}} CLI のダウンロード ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](http://plugins.ng.bluemix.net/ui/home.html){: new_window} を参照してください。

## {{site.data.keyword.Bluemix_notm}} CLI プラグインの追加

{{site.data.keyword.Bluemix_notm}} CLI のインストールが終われば、{{site.data.keyword.autoscaling}} CLI プラグインを追加できます。

以下のステップを実行して、リポジトリーを追加し、プラグインをインストールします。
1. {{site.data.keyword.Bluemix_notm}} CLI プラグインのリポジトリーを追加するため、以下のコマンドを実行します。
```
bluemix plugin repo-add bluemix-plugin-repo https://plugins.ng.bluemix.net
```
2. {{site.data.keyword.autoscaling}} CLI プラグインをインストールするため、以下のコマンドを実行します。
```
bluemix plugin install auto-scaling -r bluemix-plugin-repo
```

## Auto-Scaling ポリシーの添付

Auto-Scaling ポリシーを特定のアプリに添付することができます。次のコマンドを実行します。

```
bx as policy-attach <APP_NAME> -p <policy_file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーの添付先アプリの名前。</dd>
<dt class="pt dlterm">&lt;policy_file&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーが記述されている JSON ファイルの名前。詳しくは、「<a href="https://new-console.{DomainName}/apidocs/48" target="_blank">{{site.data.keyword.autoscaling}} RESTful API 資料 (Auto-Scaling RESTful API doc)</a>」を参照してください。</dd>
</dl>


## Auto-Scaling ポリシーの生成

Auto-Scaling ポリシーは、コマンド・ライン・インターフェースで質問に答えていけば生成できます。入力内容によっては、Auto-Scaling ポリシーの定義が含まれた JSON ファイルは、ユーザーが入力する名前を付けて保存されます。ファイル名を入力しなければ、ポリシーのコンテンツは直接コマンド・ラインに表示され、ファイルには保存されません。次のコマンドを実行します。

```
bx as policy-create
```
{: codeblock}


## Auto-Scaling ポリシーの表示

アプリの Auto-Scaling ポリシーを表示することができます。ポリシーのコンテンツは直接コマンド・ラインに表示されます。次のコマンドを実行します。

```
bx as policy-show <APP_NAME> [--json]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーを表示したいアプリの名前。デフォルトでは、JSON 構造は人間が読める一連の出力に変換されます。</dd>
</dl>

**ヒント:** 元の JSON 応答を人間が読めるように整形して表示するには、**--json** オプションを使用することもできます。


## Auto-Scaling ポリシーの切り離し

Auto-Scaling ポリシーをアプリから削除することができます。次のコマンドを実行します。

```
bx as policy-detach <APP_NAME>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーを切り離したいアプリの名前。</dd>
</dl>


## Auto-Scaling ポリシーの有効化と無効化

特定のアプリの Auto-Scaling ポリシーを有効にしたり無効にしたりできます。次のコマンドを実行します。

```
bx as policy-enable|policy-disable <APP_NAME>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーを有効または無効にしたいアプリの名前。</dd>
</dl>


## アプリの Auto-Scaling 履歴の表示

特定のアプリの Auto-Scaling アクティビティー履歴を表示することができます。Auto-Scaling 履歴レコードの表がコマンド・ライン・インターフェースに表示されます。

```
bx as history-show <APP_NAME>  [--start-date=<start_timestamp>]  [--end-date=<end_timestamp>]  [--json]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;APP_NAME&gt;</dt>
<dd class="pd">Auto-Scaling ポリシーの履歴を表示したいアプリの名前。
<dt class="pt dlterm">&lt;start_timestamp&gt;</dt>
<dd class="pd">履歴範囲の開始のタイム・スタンプ。サポートされているフォーマットは `yyyy-MM-ddTHH:mm:ss+/-hhmm, または yyyy-MM-ddTHH:mm:ssZ` です。デフォルトでは、このタイム・スタンプは現在時刻の 50 時間前に設定されます。タイム・スタンプのフォーマットについて詳しくは、「<a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a>」を参照してください。
<dt class="pt dlterm">&lt;end_timestamp&gt;</dt>
<dd class="pd">履歴範囲の終了のタイム・スタンプ。サポートされているフォーマットは `yyyy-MM-ddTHH:mm:ss+/-hhmm, または yyyy-MM-ddTHH:mm:ssZ` です。デフォルトでは、このタイム・スタンプは現在時刻に設定されます。タイム・スタンプのフォーマットについて詳しくは、「<a href="https://www.w3.org/TR/NOTE-datetime" target="_blank">W3C Date and Time Formats standard</a>」を参照してください。
</dl>



**ヒント:** 元の JSON 応答を人間が読めるように整形して表示するには、**--json** オプションを使用することもできます。

# 関連リンク
{: rellinks}
## 一般
{: general}
* [{{site.data.keyword.autoscaling}} サービス](/docs/services/Auto-Scaling/index.html)
* [{{site.data.keyword.Bluemix_notm}} CLI ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](http://plugins.ng.bluemix.net/ui/home.html){: new_window}
* [W3C Date and Time Formats standard ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://www.w3.org/TR/NOTE-datetime){: new_window}
