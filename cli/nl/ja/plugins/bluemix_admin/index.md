---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 管理 CLI
{: #bluemixadmincli}

*最終更新日: 2016 年 3 月 3 日*

Cloud Foundry コマンド・ライン・インターフェースを {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインと共に使用することにより、{{site.data.keyword.Bluemix_notm}} Local 環境または {{site.data.keyword.Bluemix_notm}} Dedicated 環境のユーザーを管理できます。例えば、LDAP レジストリーからユーザーを追加できます。{{site.data.keyword.Bluemix_notm}} パブリック・アカウントの管理に関する情報を探している場合は、『[管理](../../../admin/adminpublic.html#administer)』を参照してください。

最初に、CF コマンド・ライン・インターフェースをインストールします。{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用する場合、CF バージョン 6.11.2 以降が必要です。[Cloud Foundry コマンド・ライン・インターフェースのダウンロード](https://github.com/cloudfoundry/cli/releases){: new_window}

**制限:** Cloud Foundry コマンド・ライン・インターフェースは、Cygwin ではサポートされていません。Cloud Foundry コマンド・ライン・インターフェースは Cygwin コマンド・ライン・ウィンドウ以外のコマンド・ライン・ウィンドウで使用してください。

## {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインの追加

CF コマンド・ライン・インターフェースをインストール後、{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを追加できます。

**注**: 既に {{site.data.keyword.Bluemix_notm}} 管理プラグインをインストール済みの場合、プラグインをアンインストールし、リポジトリーを削除してから、再インストールして最新の更新を取得することが必要になる場合があります。

以下のステップを実行して、リポジトリーを追加し、プラグインをインストールします。


<ol>
<li>{{site.data.keyword.Bluemix_notm}} 管理プラグイン・リポジトリーを追加するには、以下のコマンドを実行します:<br/><br/> <code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">ご使用の {{site.data.keyword.Bluemix_notm}} インスタンス用 URL のサブドメインです。</dd>
</dl>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインをインストールするには、以下のコマンドを実行します:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

## {{site.data.keyword.Bluemix_notm}} 管理
CLI プラグインの使用

{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用すると、ユーザーの追加と削除、組織へのユーザーの割り当てと割り当て解除、といった管理タスクを実行できます。コマンドのリストを表示するには、次のコマンドを実行します。


```
cf plugins
```
{: codeblock}

追加でコマンドのヘルプを表示するには、`-help` オプションを使用します。

### {{site.data.keyword.Bluemix_notm}} への接続とログイン

管理 CLI プラグインを使用してユーザーを管理する場合、まず接続とログインを行います (まだ行っていない場合)。

<ol>
<li>{{site.data.keyword.Bluemix_notm}} API エンドポイントに接続するには、以下のコマンドを実行します:<br/><br/> <code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">ご使用の {{site.data.keyword.Bluemix_notm}} インスタンス用 URL のサブドメインです。<br />
</dd>
</dl>
<p>正しい URL は、管理コンソールの「リソースおよび情報 (Resources and Information)」ページで確認できます。URL は**「API URL」**フィールドの「API 情報」セクションに表示されます。</p>
</li>
<li>以下のコマンドを使用して {{site.data.keyword.Bluemix_notm}} にログインします:<br/><br/>
<code>
cf login
</code>
</li>
</ol>

### ユーザーの追加

LDAP レジストリーから {{site.data.keyword.Bluemix_notm}} 環境にユーザーを追加できます。次のコマンドを入力します。


```
cf ba add-user <user_name> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP レジストリー内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba add-user** という長いコマンド名の別名として **ba au** を使用することもできます。

<!-- staging-only commands start. Live for interconnect -->

### ユーザーの検索

ユーザーを検索できます。次のコマンドを入力します。


```
cf ba search-users <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>

</dl>

**ヒント:** **ba search-user** という長いコマンド名の別名として **ba su** を使用することもできます。

### Set permissions for a user

指定されたユーザーに対する許可を設定できます。次のコマンドを入力します。


```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**注**: 一度に 1 つの許可を設定できます。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">ユーザーに対する許可 (管理、ログイン、カタログ (読み取りまたは書き込みアクセス)、レポート (読み取りまたは書き込みアクセス)、またはユーザー (読み取りまたは書き込みアクセス)) を設定します。</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">許可が「カタログ」、「レポート」、または「ユーザー」の場合、アクセス・レベルも <code>read</code> または <code>write</code> として設定する必要があります。</dd>
</dl>

**ヒント:** **ba set-permissions** という長いコマンド名の別名として **ba sp** を使用することもできます。

<!-- staging-only commands end -->

### ユーザーの削除

次のコマンドを入力して、{{site.data.keyword.Bluemix_notm}} 環境からユーザーを削除できます。

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>

</dl>

**ヒント:** **ba remove-user** という長いコマンド名の別名として **ba ru** を使用することもできます。

### 組織の追加および削除

組織を追加および削除できます。

* 組織を追加するには、以下のコマンドを入力します。

```
cf ba create-organization <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">組織のマネージャーのユーザー名。</dd>
</dl>

**ヒント:** **ba create-organization** という長いコマンド名の別名として **ba co** を使用することもできます。

* 組織を削除するには、以下のコマンドを入力します。

```
cf ba delete-organization <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba delete-organization** という長いコマンド名の別名として **ba do** を使用することもできます。

### 組織へのユーザーの割り当て

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーを特定の組織に割り当てることができます。次のコマンドを入力します。


```
cf ba set-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの割り当て先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割](../../../admin/adminpublic.html#orgsandspaces)を参照してください。
</dd>
</dl>

**ヒント:** **ba set-org** という長いコマンド名の別名として **ba so** を使用することもできます。

### 組織からのユーザーの割り当て解除

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーについて、特定の組織への割り当てを解除することができます。次のコマンドを入力します。


```
cf ba unset-org <user_name> <organization> [<role>]
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの割り当て先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割](../../../admin/adminpublic.html#orgsandspaces)を参照してください。
</dd>
</dl>

**ヒント:** **ba unset-org** という長いコマンド名の別名として **ba uo** を使用することもできます。

### 役割

<dl class="parml">
<dt class="pt dlterm">OrgManager</dt>
<dd class="pd">組織管理者。組織管理者には、次のアクションを行う権限があります。<ul>
<li>組織内のスペースの作成、削除。</li>
<li>組織へのユーザーの招待とユーザーの管理。</li>
<li>組織のドメインの管理。</li>
</ul>
</dd>
<dt class="pt dlterm">BillingManager</dt>
<dd class="pd">請求管理者。請求管理者は、組織におけるランタイムおよびサービスの使用率情報を表示できます。
</dd>
<dt class="pt dlterm">OrgAuditor</dt>
<dd class="pd">組織監査員。組織監査員は、スペース内のアプリケーションとサービスの内容を表示できます。
</dd>
</dl>

### 組織の割り当て量の設定

特定の組織の使用量の割り当て量を設定できます。

```
cf ba set-quota <organization> <plan>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">割り当て量を設定する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;plan&gt;</dt>
<dd class="pd">組織の割り当て量プラン。</dd>
</dl>

**ヒント:** **ba set-quota** という長いコマンド名の別名として **ba sq** を使用することもできます。

### レポートの追加、削除、および取得

セキュリティー・レポートを追加、削除、および取得できます。
* レポートを追加するには、以下のコマンドを入力します。

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;PDF|TXT|LOG&gt;</dt>
<dd class="pd">アップロードするレポート PDF、テキスト・ファイル、またはログ・ファイルのパス。</dd>
<dt class="pt dlterm">&lt;RTF&gt;</dt>
<dd class="pd">PDF の RTF (リッチ・テキスト・フォーマット) バージョンを含めるためのオプション。このオプションが適用されるのは、レポート PDF のパスを含めた場合のみです。RTF バージョンは、索引付けおよび検索に使用されます。</dd>
</dl>

**ヒント:** **ba add-report** という長いコマンド名の別名として **ba ar** を使用することもできます。

* レポートを削除するには、以下のコマンドを入力します。

```
cf ba delete-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">レポートの名前。</dd>
</dl>

**ヒント:** **ba delete-report** という長いコマンド名の別名として **ba dr** を使用することもできます。

* レポートを取得するには、以下のコマンドを入力します。

```
cf ba retrieve-report <category> <date> <name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;category&gt;</dt>
<dd class="pd">レポートのカテゴリー。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
<dt class="pt dlterm">&lt;date&gt;</dt>
<dd class="pd"><samp class="ph codeph">YYYYMMDD</samp> という形式のレポート日付。</dd>
<dt class="pt dlterm">&lt;name&gt;</dt>
<dd class="pd">レポートの名前。</dd>
</dl>

**ヒント:** **ba retrieve-report** という長いコマンド名の別名として **ba rr**を使用することもできます。

### すべての組織のサービスの有効化および無効化

すべての組織に対して、{{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を有効化または無効化できます。

* すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を有効化するには、以下のコマンドを入力します。

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
</dl>

**ヒント:** **ba enable-service-plan** という長いコマンド名の別名として **ba esp** を使用することもできます。

* すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を無効化するには、以下のコマンドを入力します。

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">無効化するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
</dl>

**ヒント:** **ba disable-service-plan<retrieve-report** という長いコマンド名の別名として **ba dsp**を使用することもできます。

### 組織に対するサービスの表示可能性の追加、削除、および編集

{{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できる組織のリストで、組織を追加または削除できます。特定の組織が {{site.data.keyword.Bluemix_notm}} カタログで表示できるサービスのリストを編集および置換することもできます。

* 組織が {{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できるようにするには、以下のコマンドを入力します。

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示可能性を追加するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストに追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba add-service-plan-visibility** という長いコマンド名の別名として **ba aspv** を使用することもできます。

* 組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示可能性を削除するには、以下のコマンドを入力します。

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示可能性を削除するサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストから削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba remove-service-plan-visibility<retrieve-report** という長いコマンド名の別名として **ba rspv**を使用することもできます。

* 単一または複数の組織に対して既存のすべての表示されるサービスを置換するには、以下のコマンドを使用します。

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**注:** このコマンドにより、指定した組織で表示される既存のサービスが、コマンドで指定したサービスに置換されます。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">表示されるようにするサービスの名前または GUID。非固有のサービス名を入力すると、サービス・プランを選択するように求められます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">表示可能性を追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。コマンドに追加の組織名または GUID を入力することで、複数の組織に対してサービスの表示可能性を有効化できます。</dd>
</dl>

**ヒント:** **ba edit-service-plan-visibility** という長いコマンド名の別名として **ba espv** を使用することもできます。

### サービス・ブローカーの操作

すべてのサービス・ブローカーのリスト、サービス・ブローカーの追加または削除、あるいはサービス・ブローカーの更新を行うには、以下のコマンドを使用します。

* サービス・ブローカーをリストするには、次のコマンドを入力します。

```
cf ba service-brokers <broker_name>
```
{: codeblock}

**注**: すべてのサービス・ブローカーをリストするには、`broker_name` パラメーターを指定せずにコマンドを入力します。 

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">オプション: カスタム・サービス・ブローカーの名前。特定のサービス・ブローカーの情報を入手したい場合は、このパラメーターを使用します。</dd>
</dl>

**ヒント:** **ba service-brokers** という長いコマンド名の別名として **ba sb**を使用することもできます。

* サービス・ブローカーを追加して、{{site.data.keyword.Bluemix_notm}} カタログにカスタム・サービスを追加できるようにするには、次のコマンドを入力します。

```
cf ba add-service-broker <broker_name> <user_name> <password> <broker_url>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">カスタム・サービス・ブローカーの名前。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">サービス・ブローカーに対するアクセス権限を持つアカウントのユーザー名。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">サービス・ブローカーに対するアクセス権限を持つアカウントのパスワード。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">サービス・ブローカーの URL。</dd>
</dl>

**ヒント:** **ba add-service-broker** という長いコマンド名の別名として **ba asb** を使用することもできます。

* サービス・ブローカーを削除して、{{site.data.keyword.Bluemix_notm}} カタログからカスタム・サービスを除去するには、次のコマンドを入力します。

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">カスタム・サービス・ブローカーの名前または GUID。</dd>
</dl>

**ヒント:** **ba delete-service-broker** という長いコマンド名の別名として **ba dsb** を使用することもできます。

* サービス・ブローカーを更新するには、次のコマンドを入力します。

`cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;broker_name&gt;</dt>
<dd class="pd">カスタム・サービス・ブローカーの名前。</dd>
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">サービス・ブローカーに対するアクセス権限を持つアカウントのユーザー名。</dd>
<dt class="pt dlterm">&lt;password&gt;</dt>
<dd class="pd">サービス・ブローカーに対するアクセス権限を持つアカウントのパスワード。</dd>
<dt class="pt dlterm">&lt;broker_url&gt;</dt>
<dd class="pd">サービス・ブローカーの URL。</dd>
</dl>

**ヒント:** **ba update-service-broker** という長いコマンド名の別名として **ba usb**を使用することもできます。
