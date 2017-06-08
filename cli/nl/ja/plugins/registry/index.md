---



copyright:

  years: 2017

lastupdated: "2017-05-12"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI は、レジストリーと、アカウント用のレジストリー・リソースを管理するためのプラグインです。
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
 <td>[bx cr api](#bx_cr_api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list (bx cr images)](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login
](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list (bx cr namespaces)](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 <td>[bx cr token-add](#bx-cr-token-add)</td>
 </tr>
 <tr>
 <td>[bx cr token-get](#bx-cr-token-get)</td>
 <td>[bx cr token-list (bx cr tokens)](#bx-cr-token-list)</td>
 <td>[bx cr token-rm](#bx-cr-token-rm)</td>
 </tr>
 </tbody></table>



## bx cr api
{: #bx_cr_api}

コマンドの実行対象のレジストリー API エンドポイントに関する詳細を返します。

```
bx cr api
```
{: codeblock}


## bx cr info
ログイン先のレジストリーの名前とアカウントを表示します。

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
<dd>検査するイメージへの絶対 {{site.data.keyword.Bluemix_short}} レジストリー・パス (`namespace/image:tag` 形式)。イメージ・パスにタグが指定されていない場合、`latest` というタグが付いたイメージが検査されます。このコマンドでは、各パスの間をスペースで区切って、それぞれの専用 {{site.data.keyword.Bluemix_short}} レジストリー・パスをリストすることにより、複数のイメージを検査できます。</dd>
</dl>


## bx cr image-list (bx cr images)
{{site.data.keyword.Bluemix_short}} アカウント内のすべてのイメージを表示します。

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**パラメーター**
<dl>
<dt>--no-trunc</dt>
<dd>(オプション) イメージ・ダイジェストを切り捨てません。</dd>
<dt>-q, --quiet</dt>
<dd>(オプション) 各イメージが、`repository:tag` というフォーマットでリストされます。</dd>
<dt>--include-ibm</dt>
<dd>(オプション) 出力に IBM 提供のパブリック・イメージを含めます。このオプションを指定しない場合、デフォルトではプライベート・イメージのみがリストされます。</dd>
<dt>--format FORMAT</dt>
<dd>(オプション) Go テンプレートを使用して、出力エレメントをフォーマットします。</dd>

</dl>


## bx cr image-rm
指定された 1 つ以上のイメージをレジストリーから削除します。

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**パラメーター**
<dl>
<dt>IMAGE</dt>
<dd>削除するイメージへの絶対 {{site.data.keyword.Bluemix_short}} レジストリー・パス (フォーマットは `namespace/image:tag`)。イメージのパスにタグが指定されていない場合、デフォルトで、`latest` というタグが付いたイメージが削除されます。このコマンドでは、各パスの間をスペースで区切って、それぞれの専用 {{site.data.keyword.Bluemix_short}} レジストリー・パスをリストすることにより、複数のイメージを削除できます。</dd>
</dl>


## bx cr login

このコマンドはレジストリーに対して `docker login` コマンドを実行します。`docker login` コマンドは、レジストリーに対して `docker push` または `docker pull` のコマンドを実行できるようにするために必要です。このコマンドは、その他の `bx cr` コマンドを実行するためには必要ではありません。Docker がインストールされていない場合、このコマンドはエラー・メッセージを返します。

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
{{site.data.keyword.Bluemix_short}} アカウントに名前空間を追加します。

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>NAMESPACE</dt>
<dd>追加する名前空間。名前空間は、同じ地域内のすべての {{site.data.keyword.Bluemix_short}} アカウントにわたって固有でなければなりません。</dd>
</dl>


## bx cr namespace-list (bx cr namespaces)
{{site.data.keyword.Bluemix_short}} アカウントが所有するすべての名前空間を表示します。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
{{site.data.keyword.Bluemix_short}} アカウントから名前空間を削除します。名前空間を削除すると、この名前空間内のイメージが削除されます。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**パラメーター**
<dl>
<dt>NAMESPACE</dt>
<dd>削除する名前空間。</dd>
</dl>


## bx cr token-add
レジストリーへのアクセスを制御するために使用できるトークンを追加します。

```
bx cr token-add [--description VALUE] [-q, --quiet] [--non-expiring] [--readwrite]
```

{: codeblock}


**パラメーター**
<dl>
<dt>--description VALUE</dt>
<dd>(オプション) トークンの説明としての値を指定します。これは、`bx cr token-list` を実行すると表示されます。トークンが IBM Bluemix Container Service によって自動的に作成される場合、この説明は Kubernetes クラスター名に設定されます。この場合、クラスターが除去されると、トークンは自動的に削除されます。</dd>
<dt>-q, --quiet</dt>
<dd>(オプション) 周囲のテキストを含めずに、トークンのみを表示します。</dd>
<dt>--non-expiring</dt>
<dd>(オプション) 有効期限が切れないアクセス権限を指定してトークンを作成します。このパラメーターを設定しないと、デフォルトでは、トークンからのアクセスは 24 時間後に期限切れになります。</dd>
<dt>--readwrite</dt>
<dd>(オプション) 読み取り権限および書き込み権限を付与するトークンを作成します。このオプションを指定しないと、デフォルトでは、アクセス権限は読み取り専用になります。</dd>
</dl>


## bx cr token-get
指定されたトークンをレジストリーから取得します。

```
bx cr token-get TOKEN
```

{: codeblock}

**パラメーター**
<dl>
<dt>TOKEN</dt>
<dd>(オプション) 取得するトークンの固有 ID。</dd>
</dl>


## bx cr token-list (bx cr tokens)
{{site.data.keyword.Bluemix_short}} アカウント用に存在するすべてのトークンを表示します。

```
bx cr token-list --format FORMAT
```
{: codeblock}

**パラメーター**
<dl>
<dt>--format FORMAT</dt>
<dd>(オプション) Go テンプレートを使用して、出力エレメントをフォーマットします。</dd>
</dl>


## bx cr token-rm
指定された 1 つ以上のトークンを削除します。

```
bx cr token-rm TOKEN [TOKEN]
```
{: codeblock}

**パラメーター**
<dl>
<dt>TOKEN</dt>
<dd>(オプション) TOKEN には、トークン自体またはトークンの固有 ID (`bx cr token-list` で表示される) のいずれかを指定できます。複数のトークンを、スペースで区切って指定できます。</dd>
</dl>


</dd>
</dl>


