---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI は、組織全体のレジストリー・リソース (名前空間やイメージなど) を管理できるプラグインです。
{: shortdesc}

** の前提条件**
* レジストリー・コマンドを実行する前に、`bx login` コマンドを使用して {{site.data.keyword.Bluemix_short}} にログインし、{{site.data.keyword.Bluemix_short}} アクセス・トークンを生成して、セッションを認証します。

<table summary="コンテナー・レジストリーの管理">
<caption>表 1. {{site.data.keyword.Bluemix_short}} 上の {{site.data.keyword.registryshort}} を管理するためのコマンド
</caption>
 <thead>
 <th colspan="5">レジストリーを管理するためのコマンド</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login
](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list
](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
コマンドの実行対象のレジストリー API エンドポイントに関する詳細を返します。

```
bx cr api
```
{: codeblock}


## bx cr info
ログイン先のレジストリーの名前と組織を表示します。

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
特定のイメージに関する詳細を表示します。

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**パラメーター**
<dl>
<dt>--format FORMAT</dt>
<dd>(オプション) Go テンプレートを使用して、出力エレメントをフォーマットします。</dd>
<dt>IMAGE</dt>
<dd>検査するイメージへの絶対 {{site.data.keyword.Bluemix_short}} レジストリー・パス (namespace/image:tag 形式)。イメージ・パスにタグが指定されていない場合、`latest` というタグが付いたイメージが検査されます。このコマンドでは、各パスの間をスペースで区切って、それぞれの専用 {{site.data.keyword.Bluemix_short}} レジストリー・パスをリストすることにより、複数のイメージを検査できます。</dd>
</dl>


## bx cr image-list
{{site.data.keyword.Bluemix_short}} 組織内のすべてのイメージを表示します。

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**パラメーター**
<dl>
<dt>--no-trunc</dt>
<dd>(オプション) 出力を切り捨てません。</dd>
<dt>-q, --quiet</dt>
<dd>(オプション) イメージの固有 ID を 'repository:tag' 形式で表示します。</dd>
<dt>--include-ibm</dt>
<dd>(オプション) 出力に IBM 提供のパブリック・イメージを含めます。このオプションがない場合は、プライベート・イメージのみがリストされます。</dd>
<dt>--format FORMAT</dt>
<dd>(オプション) Go テンプレートを使用して、出力エレメントをフォーマットします。</dd>
</dl>


## bx cr image-rm
指定されたイメージをレジストリーから削除します。

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**パラメーター**
<dl>
<dt>IMAGE</dt>
<dd>削除するイメージへの絶対 {{site.data.keyword.Bluemix_short}} レジストリー・パス (namespace/image:tag 形式)。イメージのパスにタグが指定されていない場合、デフォルトで、`latest` というタグが付いたイメージが削除されます。このコマンドでは、各パスの間をスペースで区切って、それぞれの専用 {{site.data.keyword.Bluemix_short}} レジストリー・パスをリストすることにより、複数のイメージを削除できます。</dd>
</dl>


## bx cr login

Docker がインストールされている場合、このコマンドはレジストリーに対して `docker login` コマンドを実行します。`docker login` コマンドは、レジストリーに対して `docker push` または `docker pull` のコマンドを実行できるようにするために必要です。このコマンドは、その他の `bx cr` コマンドを実行するためには必要ではありません。Docker がインストールされていない場合、このコマンドはエラー・メッセージを返します。

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Bluemix 組織に名前空間を追加します。 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>NAMESPACE</dt>
<dd>追加する名前空間。名前空間は、すべての {{site.data.keyword.Bluemix_short}} 組織にわたって固有でなければなりません。</dd>
</dl>


## bx cr namespace-list

{{site.data.keyword.Bluemix_short}} 組織内のすべての名前空間を表示します。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
{{site.data.keyword.Bluemix_short}} 組織から名前空間を削除します。名前空間を削除すると、この名前空間内のイメージが削除されます。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>NAMESPACE</dt>
<dd>削除する名前空間。</dd>
</dl>
