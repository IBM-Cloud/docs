---

copyright:

  years: 2015, 2017

lastupdated: "2017-02-20"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 管理 CLI
{: #bluemixadmincli}


Cloud Foundry コマンド・ライン・インターフェースを {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインと共に使用することにより、{{site.data.keyword.Bluemix_notm}} Local 環境または {{site.data.keyword.Bluemix_notm}} Dedicated 環境を管理できます。例えば、LDAP レジストリーからユーザーを追加できます。{{site.data.keyword.Bluemix_notm}} パブリック・アカウントの管理に関する情報を探している場合は、『[管理](/docs/admin/adminpublic.html#administer)』を参照してください。

最初に、CF コマンド・ライン・インターフェースをインストールします。{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用する場合、CF バージョン 6.11.2 以降が必要です。[Cloud Foundry コマンド・ライン・インターフェースのダウンロード ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://github.com/cloudfoundry/cli/releases){: new_window} を行ってください。

**制限:** Cloud Foundry コマンド・ライン・インターフェースは、Cygwin ではサポートされていません。Cloud Foundry コマンド・ライン・インターフェースは Cygwin コマンド・ライン・ウィンドウ以外のコマンド・ライン・ウィンドウで使用してください。

**注**: {{site.data.keyword.Bluemix_notm}} 管理 CLI は、{{site.data.keyword.Bluemix_notm}} Local および {{site.data.keyword.Bluemix_notm}} Dedicated 環境でのみ使用されます。{{site.data.keyword.Bluemix_notm}} Public ではサポートされません。

## {{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインの追加

CF コマンド・ライン・インターフェースをインストール後、{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを追加できます。

**注**: 既に {{site.data.keyword.Bluemix_notm}} 管理プラグインをインストール済みの場合、プラグインをアンインストールし、リポジトリーを削除してから、再インストールして最新の更新を取得することが必要になる場合があります。

以下のステップを実行して、リポジトリーを追加し、プラグインをインストールします。


<ol>
<li>{{site.data.keyword.Bluemix_notm}} 管理プラグイン・リポジトリーを追加するには、以下のコマンドを実行します。
<br/><br/>
<code>
cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli
</code><br/><br/>
</li>
<li>{{site.data.keyword.Bluemix_notm}} 管理
CLI プラグインをインストールするには、以下のコマンドを実行します。<br/><br/>
<code>
cf install-plugin BluemixAdminCLI -r BluemixAdmin
</code>
</li>
</ol>

プラグインをアンインストールする必要がある場合は、以下のコマンドを使用できます。その後、更新されたリポジトリーを追加して、最新のプラグインをインストールできます。

* プラグインのアンインストール: `cf uninstall-plugin BluemixAdminCLI`
* プラグイン・リポジトリーの削除: `cf remove-plugin-repo BluemixAdmin`


## {{site.data.keyword.Bluemix_notm}} 管理
CLI プラグインの使用

{{site.data.keyword.Bluemix_notm}} 管理 CLI プラグインを使用すると、ユーザーの追加と削除、組織へのユーザーの割り当てと割り当て解除、といった管理タスクを実行できます。

コマンドのリストを表示するには、次のコマンドを実行します。


```
cf plugins
```
{: codeblock}

追加でコマンドのヘルプを表示するには、`-help` オプションを使用します。

### {{site.data.keyword.Bluemix_notm}} への接続とログイン

管理 CLI プラグインを使用する場合、まず接続とログインを行います (まだ行っていない場合)。

<ol>
<li>{{site.data.keyword.Bluemix_notm}} API エンドポイントに接続するには、次のコマンドを実行します。<br/><br/>
<code>
cf ba api https://console.&lt;subdomain&gt;.bluemix.net
</code>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">ご使用の {{site.data.keyword.Bluemix_notm}} インスタンス用 URL のサブドメインです。<br />
</dd>
</dl>
<p>正しい URL は、管理コンソールの「リソースおよび情報 (Resources and Information)」ページで確認できます。URL は**「API URL」**フィールドの「API 情報」セクションに表示されます。</p>
</li>
<li>次のコマンドを使用して、{{site.data.keyword.Bluemix_notm}} にログインします。
<br/><br/>
<code>
cf login
</code>
</li>
</ol>

## ユーザーの管理
{: #admin_users}

### ユーザーの追加
{: #admin_add_user}

ご使用環境のユーザー・レジストリーから {{site.data.keyword.Bluemix_notm}} 環境にユーザーを追加するには、以下のコマンドを使用します。

```
cf ba add-user <user_name> <organization> <first_name> <last_name>
```
{: codeblock}

**注**: ユーザーを特定の組織に追加するには、**users.write** (または **Superuser**) 許可を備えた**管理者**でなければなりません。組織管理者の場合、**enable-managers-add-users** コマンドを実行する Superuser から、組織にユーザーを追加する権限を付与してもらうこともできます。詳しくは、『[管理者へのユーザー追加権限の付与](index.html#clius_emau)』を参照してください。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">LDAP レジストリー内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーの追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;first_name&gt;</dt>
<dd class="pd">組織に追加するユーザーの名。</dd>
<dt class="pt dlterm">&lt;last_name&gt;</dt>
<dd class="pd">組織に追加するユーザーの姓。</dd>
</dl>

**ヒント:** **ba add-user** という長いコマンド名の別名として **ba au** を使用することもできます。

<!-- staging-only commands start. Live for interconnect -->

### ユーザーの検索
{: #admin_search_user}

ユーザーを検索するには、オプションの検索フィルター・パラメーター (name、permission、organization、および role) を指定して、以下のコマンドを使用します。

```
cf ba search-users -name=<user_name_value> -permission=<permission_value> -organization=<organization_value> -role=<role_value>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name_value&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;permission_value&gt;</dt>
<dd class="pd">ユーザーに割り当てられた許可。例えば、superuser、basic、catalog、user、および reports です。割り当てられたユーザー許可について詳しくは、『[許可](/docs/admin/index.html#permissions)』を参照してください。同じ照会内でこのパラメーターを organization パラメーターと一緒に使用することはできません。</dd>
<dt class="pt dlterm">&lt;organization_value&gt;</dt>
<dd class="pd">ユーザーが所属する組織の名前。同じ照会内でこのパラメーターを permission パラメーターと一緒に使用することはできません。</dd>
<dt class="pt dlterm">&lt;role_value&gt;</dt>
<dd class="pd">ユーザーに割り当てられた、組織の役割。例えば、組織の管理者、請求管理者、または監査員です。このパラメーターと一緒に組織を指定する必要があります。役割について詳しくは、『[ユーザー役割](/docs/admin/users_roles.html#userrolesinfo)』を参照してください。</dd>

</dl>

**ヒント:** **ba search-user** という長いコマンド名の別名として **ba su** を使用することもできます。

### ユーザーの許可の設定
{: #admin_setperm_user}

指定されたユーザーの許可を設定するには、以下のコマンドを使用します。

```
cf ba set-permissions <user_name> <permission> <access>
```
{: codeblock}

**注**: 一度に 1 つの許可を設定できます。

<dl class="parml">
<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>
<dt class="pt dlterm">&lt;permission&gt;</dt>
<dd class="pd">管理 (代替として「スーパーユーザー」が使用可能)、ログイン (代替として「基本」が使用可能)、カタログ (read または write のアクセス権限)、レポート(read または write のアクセス権限)、またはユーザー (read または write のアクセス権限) のユーザー許可を設定します。</dd>
<dt class="pt dlterm">&lt;access&gt;</dt>
<dd class="pd">許可が「カタログ」、「レポート」、または「ユーザー」の場合、アクセス・レベルも <code>read</code> または <code>write</code> として設定する必要があります。</dd>
</dl>

**ヒント:** **ba set-permissions** という長いコマンド名の別名として **ba sp** を使用することもできます。

<!-- staging-only commands end -->

### ユーザーの削除
{: #admin_remov_user}

{{site.data.keyword.Bluemix_notm}} 環境からユーザーを削除するには、以下のコマンドを使用します。

```
cf ba remove-user <user_name>
```
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">&lt;user_name&gt;</dt>
<dd class="pd">{{site.data.keyword.Bluemix_notm}} 内のユーザーの名前。</dd>

</dl>

**ヒント:** **ba remove-user** という長いコマンド名の別名として **ba ru** を使用することもできます。

### 管理者へのユーザー追加権限の付与
{: #clius_emau}

{{site.data.keyword.Bluemix_notm}} 環境で **Superuser** 許可がある場合、組織管理者が、自分が管理している組織にユーザーを追加できるようにすることが可能です。管理者がユーザーを追加できるようにするには、以下のコマンドを使用します。

```
cf ba enable-managers-add-users
```
{: codeblock}

**ヒント:** **ba enable-managers-add-users** という長いコマンド名の別名として **ba emau**を使用することもできます。

### 管理者のユーザー追加権限の無効化
{: #clius_dmau}

**enable-managers-add-users** によって組織管理者が {{site.data.keyword.Bluemix_notm}} 環境で管理している組織にユーザーを追加できるようになっている場合、**Superuser** 許可を備えていれば、この設定を削除できます。管理者によるユーザーの追加を不可にするには、以下のコマンドを使用します。

```
cf ba disable-managers-add-users
```
{: codeblock}

**ヒント:** **ba disable-managers-add-users** という長いコマンド名の別名として **ba dmau** を使用することもできます。

## 組織の管理
{: #admin_orgs}

### 組織の追加
{: #admin_add_org}

組織を追加するには、以下のコマンドを使用します。

```
cf ba create-org <organization> <manager>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">追加先となる {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;manager&gt;</dt>
<dd class="pd">組織のマネージャーのユーザー名。</dd>
</dl>

**ヒント:** **ba create-org** という長いコマンド名の別名として **ba co** を使用することもできます。

### 組織の削除
{: #admin_delete_org}

組織を削除するには、以下のコマンドを使用します。

```
cf ba delete-org <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba delete-org** という長いコマンド名の別名として **ba do** を使用することもできます。

### 組織へのユーザーの割り当て
{: #admin_ass_user_org}

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーを特定の組織に割り当てるには、以下のコマンドを使用します。

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
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割](/docs/admin/users_roles.html)を参照してください。
</dd>
</dl>

**ヒント:** **ba set-org** という長いコマンド名の別名として **ba so** を使用することもできます。

### 組織からのユーザーの割り当て解除
{: #admin_unass_user_org}

{{site.data.keyword.Bluemix_notm}} 環境内のユーザーを特定の組織から割り当て解除するには、以下のコマンドを使用します。


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
<dd class="pd">{{site.data.keyword.Bluemix_notm}} ユーザーの役割とそれぞれの説明については、[役割の割り当て](/docs/admin/users_roles.html)を参照してください。
</dd>
</dl>

**ヒント:** **ba unset-org** という長いコマンド名の別名として **ba uo** を使用することもできます。

#### 役割の割り当て

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
{: #admin_set_org_quota}

特定組織の使用量の割り当て量を設定するには、以下のコマンドを使用します。

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


### 組織のコンテナー割り当て量の判別
{: #admin_find_containquotas}

組織のコンテナーの割り当て量を判別するには、以下のコマンドを使用します。

```
cf bluemix-admin containers-quota <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix 内の組織の名前または ID。このパラメーターは必須です。</dd>
</dl>

**ヒント:** **bluemix-admin containers-quota** という長いコマンド名の別名として **ba cq** を使用することもできます。

### 組織のコンテナー割り当て量の設定
{: #admin_set_containquotas}

組織のコンテナーの割り当て量を設定するには、少なくとも 1 つのオプションを含めて以下のコマンドを使用します。

```
cf bluemix-admin set-containers-quota <organization> <options>
```
{: codeblock}

**注**: 複数のオプションを含められますが、少なくとも 1 つは含める必要があります。

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">Bluemix 内の組織の名前または ID。このパラメーターは必須です。</dd>
<dt class="pt dlterm">&lt;options&gt;</dt>
<dd class="pd">以下のオプションを 1 つ以上含めます。値は整数でなければなりません。
<ul>
<li>floating-ips-max &lt;value&gt;</li>
<li>floating-ips-space-default &lt;value&gt;</li>
<li>memory-max &lt;value&gt;</li>
<li>memory-space-default &lt;value&gt;</li>
<li>image-limit &lt;value&gt;</li>
</ul>
</dd>
</dl>

**ヒント:** 長いオプション名の別名として、以下の短い名前を使用することも可能です。
<dl class="parml">
<dt class="pt dlterm">floating-ips-max &lt;value&gt;</dt>
<dd class="pd"><strong>fim</strong></dd>
<dt class="pt dlterm">floating-ips-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>fisd</strong></dd>
<dt class="pt dlterm">memory-max &lt;value&gt;</dt>
<dd class="pd"><strong>mm</strong></dd>
<dt class="pt dlterm">memory-space-default &lt;value&gt;</dt>
<dd class="pd"><strong>msd</strong></dd>
<dt class="pt dlterm">image-limit &lt;value&gt;</dt>
<dd class="pd"><strong>il</strong></dd>
</dl>

オプションで、有効な JSON オブジェクトに固有の構成パラメーターを含むファイルを指定できます。**-file** オプションを使用すると、それが優先され、他のオプションは無視されます。オプションを設定する代わりにファイルを指定する場合は、以下のコマンドを使用します。

```
cf bluemix-admin set-containers-quota <organization> <-file path_to_JSON_file>
```
{: codeblock}

JSON ファイルには、以下の例に示したフォーマットが含まれる必要があります。

```
{
  "floating_ips_max": 10,
  "floating_ips_space_default": 0,
  "ram_max": 4096,
  "ram_space_default": 0,
  "image_limit": 10
}
```
{: codeblock}

**ヒント:** **bluemix-admin set-containers-quota** という長いコマンド名の別名として **ba scq** を使用することもできます。

## スペースの管理
{: #admin_spaces}

### 組織へのスペースの追加

組織でスペースを追加するには、以下のコマンドを使用します。

```
cf bluemix-admin create-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">スペースを追加する先の組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">組織に作成されるスペースの名前。</dd>
</dl>

**ヒント:** **ba create-space** という長いコマンド名の別名として **ba cs** を使用することもできます。

### 組織からスペースを削除

組織からスペースを削除するには、以下のコマンドを使用します。

```
cf bluemix-admin delete-space <organization> <space_name>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">スペースを削除する元の組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">組織から削除されるスペースの名前。</dd>
</dl>

**ヒント:** **ba delete-space** という長いコマンド名の別名として **ba cs** を使用することもできます。

### 指定した役割のユーザーをスペースに追加

指定した役割を持つユーザーをスペースに作成するには、以下のコマンドを使用します。

```
cf bluemix-admin set-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーを追加する先の組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">ユーザーを追加する先のスペースの名前。</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">追加するユーザーの名前。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">割り当てるユーザーの役割。この値には、Manager、Developer、または Auditor が可能です。スペース内での {{site.data.keyword.Bluemix_notm}} ユーザーの役割と説明については、[役割の割り当て](/docs/admin/users_roles.html)を参照してください。</dd>
</dl>

**ヒント:** **ba set-space** という長いコマンド名の別名として **ba ss** を使用することもできます。


### スペース内のユーザーの役割の削除 

スペース内のユーザーの役割を削除するには、以下のコマンドを使用します。

```
cf bluemix-admin unset-space <organization> <space_name> <user_name> <role>
```

{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">ユーザーを追加する先の組織の名前または GUID。</dd>
<dt class="pt dlterm">&lt;space_name&gt;</dt>
<dd class="pd">ユーザーを追加する先のスペースの名前。</dd>
<dt class="pt dlterm">&lt;user_anme&gt;</dt>
<dd class="pd">追加するユーザーの名前。</dd>
<dt class="pt dlterm">&lt;role&gt;</dt>
<dd class="pd">割り当てるユーザーの役割。この値には、Manager、Developer、または Auditor が可能です。スペース内での {{site.data.keyword.Bluemix_notm}} ユーザーの役割と説明については、[役割の割り当て](/docs/admin/users_roles.html)を参照してください。</dd>
</dl>

**ヒント:** **ba unset-space** という長いコマンド名の別名として **ba us** を使用することもできます。

## カタログの管理
{: #admin_catalog}

### すべての組織のサービスの有効化
{: #admin_ena_service_org}

すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を有効化するには、以下のコマンドを使用します。

```
cf ba enable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービス・プランの名前または GUID。非固有のサービス・プラン名 (例えば、「Standard」または「Basic」) を入力すると、サービス・プランを選択するように求めるプロンプトが出されます。サービス・プラン名を識別するには、ホーム・ページのサービス・カテゴリーを選択してから、**「追加」**を選択してそのカテゴリーのサービスを表示します。サービス名をクリックして詳細ビューを開くと、そのサービスで使用可能なサービス・プランの名前を表示できます。</dd>
</dl>

**ヒント:** **ba enable-service-plan** という長いコマンド名の別名として **ba esp** を使用することもできます。

### すべての組織のサービスの無効化
{: #admin_dis_service_org}

すべての組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示を無効化するには、以下のコマンドを使用します。

```
cf ba disable-service-plan <plan_identifier>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービス・プランの名前または GUID。非固有のサービス・プラン名 (例えば、「Standard」または「Basic」) を入力すると、サービス・プランを選択するように求めるプロンプトが出されます。サービス・プラン名を識別するには、ホーム・ページのサービス・カテゴリーを選択してから、**「追加」**を選択してそのカテゴリーのサービスを表示します。サービス名をクリックして詳細ビューを開くと、そのサービスで使用可能なサービス・プランの名前を表示できます。</dd>
</dl>

**ヒント:** **ba disable-service-plan<retrieve-report** という長いコマンド名の別名として **ba dsp**を使用することもできます。

### 組織に対するサービスの表示可能性の追加
{: #admin_addvis_service_org}

{{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できる組織のリストで、組織を追加できます。組織が {{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できるようにするには、以下のコマンドを使用します。

```
cf ba add-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービス・プランの名前または GUID。非固有のサービス・プラン名 (例えば、「Standard」または「Basic」) を入力すると、サービス・プランを選択するように求めるプロンプトが出されます。サービス・プラン名を識別するには、ホーム・ページのサービス・カテゴリーを選択してから、**「追加」**を選択してそのカテゴリーのサービスを表示します。サービス名をクリックして詳細ビューを開くと、そのサービスで使用可能なサービス・プランの名前を表示できます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストに追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba add-service-plan-visibility** という長いコマンド名の別名として **ba aspv** を使用することもできます。

### 組織に対するサービスの表示可能性の削除
{: #admin_remvis_service_org}

{{site.data.keyword.Bluemix_notm}} カタログで特定のサービスを表示できる組織のリストで、組織を削除できます。組織に対して {{site.data.keyword.Bluemix_notm}} カタログでのサービスの表示可能性を削除するには、以下のコマンドを使用します。

```
cf ba remove-service-plan-visibility <plan_identifier> <organization>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効にするサービス・プランの名前または GUID。非固有のサービス・プラン名 (例えば、「Standard」または「Basic」) を入力すると、サービス・プランを選択するように求めるプロンプトが出されます。サービス・プラン名を識別するには、ホーム・ページのサービス・カテゴリーを選択してから、**「追加」**を選択してそのカテゴリーのサービスを表示します。サービス名をクリックして詳細ビューを開くと、そのサービスで使用可能なサービス・プランの名前を表示できます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">サービスの表示可能性リストから削除する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。</dd>
</dl>

**ヒント:** **ba remove-service-plan-visibility<retrieve-report** という長いコマンド名の別名として **ba rspv**を使用することもできます。

### 組織に対するサービスの表示可能性の編集
{: #admin_editvis_service_org}

特定の組織が {{site.data.keyword.Bluemix_notm}} カタログで表示できるサービスのリストを編集および置換することができます。単一または複数の組織に対して既存のすべての表示されるサービスを置換するには、以下のコマンドを使用します。

```
cf ba edit-service-plan-visibilities <plan_identifier> <organization_1> <optional_organization_2>
```
{: codeblock}

**注:** このコマンドにより、指定した組織で表示される既存のサービスが、コマンドで指定したサービスに置換されます。

<dl class="parml">
<dt class="pt dlterm">&lt;plan_identifier&gt;</dt>
<dd class="pd">有効化するサービス・プランの名前または GUID。非固有のサービス・プラン名 (例えば、「Standard」または「Basic」) を入力すると、サービス・プランを選択するように求めるプロンプトが出されます。サービス・プラン名を識別するには、ホーム・ページのサービス・カテゴリーを選択してから、**「追加」**を選択してそのカテゴリーのサービスを表示します。サービス名をクリックして詳細ビューを開くと、そのサービスで使用可能なサービス・プランの名前を表示できます。</dd>
<dt class="pt dlterm">&lt;organization&gt;</dt>
<dd class="pd">表示可能性を追加する {{site.data.keyword.Bluemix_notm}} 組織の名前または GUID。コマンドに追加の組織名または GUID を入力することで、複数の組織に対してサービスの表示可能性を有効化できます。</dd>
</dl>

**ヒント:** **ba edit-service-plan-visibility** という長いコマンド名の別名として **ba espv** を使用することもできます。

## レポートの管理
{: #admin_add_report}

### レポートの追加
{: #admin_add_report}

セキュリティー・レポートを追加するには、以下のコマンドを使用します。

```
cf ba add-report <category> <date> <PDF|TXT|LOG> <RTF>
```
{: codeblock}

**注**: レポートの書き込みアクセス許可がある場合は、新規カテゴリーを作成し、ユーザー用に受け入れられるフォーマットのいずれかでレポートを追加できます。`category` パラメーターに新規カテゴリー名を入力するか、既存のカテゴリーに新規レポートを追加します。

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

### レポートの削除
{: #admin_del_report}

セキュリティー・レポートを削除するには、以下のコマンドを使用します。

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

### レポートの取得
{: #admin_retr_report}

セキュリティー・レポートを取得するには、以下のコマンドを使用します。

```
cf ba retrieve-report <search>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;search&gt;</dt>
<dd class="pd">レポートのファイル名。名前にスペースが含まれている場合は、引用符を使用して名前を囲んでください。</dd>
</dl>

**ヒント:** **ba retrieve-report** という長いコマンド名の別名として **ba rr**を使用することもできます。

## リソース・メトリック情報の表示
{: #cliresourceusage}

メモリー、ディスク、CPU 使用量など、リソース・メトリック情報を表示できます。使用可能な物理リソースと予約済みリソース、および物理リソースと予約済みリソースの使用量の要約を確認できます。Droplet Execution Agent (DEA) およびセル (Diego アーキテクチャー) の使用データおよび履歴のメモリーとディスク使用量を確認することもできます。デフォルトでは、メモリーおよびディスク使用量の履歴データは、週次で降順に表示されます。リソース・メトリック情報を表示するには、以下のコマンドを使用します。

```
cf ba resource-metrics <monthly> <weekly>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;monthly&gt;</dt>
<dd class="pd">一度に 1 カ月分ずつ、メモリーおよびディスク・スペースの履歴データを表示します。</dd>
<dt class="pt dlterm">&lt;weekly&gt;</dt>
<dd class="pd">一度に 1 週間分ずつ、メモリーおよびディスク・スペースの履歴データを表示します。これはデフォルト値です。</dd>
</dl>

**ヒント:** **ba resource-metrics** という長いコマンド名の別名として **ba rsm** を使用することもできます。


## サービス・ブローカーの管理
{: #admin_servbro}

### サービス・ブローカーのリスト
{: #clilistservbro}

すべてのサービス・ブローカーをリストするには、以下のコマンドを使用します。

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

### サービス・ブローカーの追加
{: #cliaddservbro}

サービス・ブローカーを追加して、{{site.data.keyword.Bluemix_notm}} カタログにカスタム・サービスを追加できるようにするには、以下のコマンドを使用します。

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

### サービス・ブローカーの削除
{: #clidelservbro}

サービス・ブローカーを削除して、{{site.data.keyword.Bluemix_notm}} カタログからカスタム・サービスを削除するには、以下のコマンドを使用します。

```
cf ba delete-service-broker <service_broker>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;service_broker&gt;</dt>
<dd class="pd">カスタム・サービス・ブローカーの名前または GUID。</dd>
</dl>

**ヒント:** **ba delete-service-broker** という長いコマンド名の別名として **ba dsb** を使用することもできます。

### サービス・ブローカーの更新
{: #cliupdservbro}

サービス・ブローカーを更新するには、以下のコマンドを使用します。

```
cf ba update-service-broker <broker_name> <user_name> <password> <broker_url>
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

**ヒント:** **ba update-service-broker** という長いコマンド名の別名として **ba usb**を使用することもできます。


## アプリケーション・セキュリティー・グループの管理
{: #admin_secgro}

アプリケーション・セキュリティー・グループ (ASG) に関して作業するには、ローカル環境または専用環境の全アクセス権限を持つ管理者でなければなりません。コマンドでターゲットとする組織に有効な ASG のリスト表示は、環境のすべてのユーザーが行えます。それに対し、ASG の作成、更新、バインドを行うには、{{site.data.keyword.Bluemix_notm}} 環境の管理者である必要があります。

ASG は、{{site.data.keyword.Bluemix_notm}} 環境内のアプリケーションからのアウトバウンド・トラフィックを制御する仮想ファイアウォールとして機能します。各 ASG は、外部ネットワークに対する特定のトラフィックおよび通信を許可するルールのリストから構成されます。1 つ以上の ASG を特定のセキュリティー・グループ・セット (例えば、グローバル・アクセスの適用に使用されるグループ・セットなど) にバインドすることや、{{site.data.keyword.Bluemix_notm}} 環境の組織内のスペースにバインドすることができます。

{{site.data.keyword.Bluemix_notm}} は最初、制限された外部ネットワークへのすべてのアクセス権限でセットアップされます。IBM が作成した 2 つのセキュリティー・グループ `public_networks` と `dns` をデフォルトの Cloud Foundry セキュリティー・グループ・セットにバインドした場合、これらのグループにより、外部ネットワークへのグローバル・アクセスが可能になります。グローバル・アクセスの適用に使用される Cloud Foundry 内の 2 つのセキュリティー・グループ・セットは、**デフォルト・ステージング**と**デフォルト実行**のグループ・セットです。これらのグループ・セットは、すべての実行アプリ、またはすべてのステージング・アプリに対するトラフィックを許可するためのルールを適用します。これらの 2 つのセキュリティー・グループ・セットにバインドしたくない場合は、Cloud Foundry グループ・セットからアンバインドし、セキュリティー・グループを特定スペースにバインドしてください。詳しくは、[アプリケーション・セキュリティー・グループのバインド ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window} を参照してください。

**注**: セキュリティー・グループに関する作業を可能にする以下のコマンドは、Cloud Foundry 1.6 バージョンをベースとしています。必須フィールドやオプション・フィールドなどの詳細については、[アプリケーション・セキュリティー・グループの作成 ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window} に関する Cloud Foundry 資料を参照してください。

### セキュリティー・グループのリスト
{: #clilissecgro}

* すべてのセキュリティー・グループをリストするには、以下のコマンドを使用します。

```
cf ba security-groups
```
{: codeblock}

**ヒント:** **ba security-groups** という長いコマンド名の別名として **ba sgs** を使用することもできます。

* 特定セキュリティー・グループの詳細を表示するには、以下のコマンドを使用します。

```
cf ba security-groups <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** `security-group` パラメーターを指定した **ba security-groups** という長いコマンド名の別名として **ba sg** を使用することもできます。


### セキュリティー・グループの作成
{: #clicreasecgro}

セキュリティー・グループの作成と、発信トラフィックを定義するルールについて詳しくは、[アプリケーション・セキュリティー・グループの作成 ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#creating-groups){: new_window} を参照してください。

セキュリティー・グループを作成するには、以下のコマンドを使用します。

```
cf ba create-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

IBM が作成したセキュリティー・グループと区別するため、ユーザーが作成した各セキュリティー・グループの名前には、接頭部 `adminconsole_` が追加されます。

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">ルール・ファイルの絶対パスまたは相対パス</dd>
</dl>

**ヒント:** **ba create-security-group** という長いコマンド名の別名として **ba csg**を使用することもできます。

### セキュリティー・グループの更新
{: #cliupdsecgro}

セキュリティー・グループを更新するには、以下のコマンドを使用します。

```
cf ba update-security-group <security-group> <path-to-rules-file>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
<dt class="pt dlterm">&lt;Path to rules file&gt;</dt>
<dd class="pd">ルール・ファイルの絶対パスまたは相対パス</dd>
</dl>

**ヒント:** **ba update-security-group** という長いコマンド名の別名として **ba usg** を使用することもできます。

### セキュリティー・グループの削除
{: #clidelsecgro}

セキュリティー・グループを削除するには、以下のコマンドを使用します。

```
cf ba delete-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** **ba delete-security-group** という長いコマンド名の別名として **ba dsg**を使用することもできます。


### セキュリティー・グループのバインド
{: #clibindsecgro}

セキュリティー・グループのバインドについて詳しくは、[アプリケーション・セキュリティー・グループのバインド ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#binding-groups){: new_window} を参照してください。

* デフォルト・ステージングのセキュリティー・グループ・セットにバインドするには、以下のコマンドを使用します。

```
cf ba bind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** **ba bind-staging-security-group** という長いコマンド名の別名として **ba bssg** を使用することもできます。

* デフォルト実行のセキュリティー・グループ・セットにバインドするには、以下のコマンドを使用します。

```
cf ba bind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** **ba bind-running-security-group** という長いコマンド名の別名として **ba brsg**を使用することもできます。

* セキュリティー・グループをスペースにバインドするには、以下のコマンドを使用します。

```
cf ba bind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">セキュリティー・グループをバインドする組織の名前</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">セキュリティー・グループをバインドする組織内のスペースの名前</dd>
</dl>

**ヒント:** **ba bind-security-group** という長いコマンド名の別名として **ba bsg**を使用することもできます。

### セキュリティー・グループのアンバインド
{: #cliunbindsecgro}

セキュリティー・グループのアンバインドについて詳しくは、[アプリケーション・セキュリティー・グループのアンバインド ![「外部リンク」アイコン](../../../icons/launch-glyph.svg)](https://docs.cloudfoundry.org/adminguide/app-sec-groups.html#unbinding-groups){: new_window} を参照してください。

* デフォルト・ステージングのセキュリティー・グループ・セットからアンバインドするには、以下のコマンドを使用します。

```
cf ba unbind-staging-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** **ba unbind-staging-security-group** という長いコマンド名の別名として **ba ussg** を使用することもできます。

* デフォルト実行のセキュリティー・グループ・セットからアンバインドするには、以下のコマンドを使用します。

```
cf ba unbind-running-security-group <security-group>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
</dl>

**ヒント:** **ba bind-running-security-group** という長いコマンド名の別名として **ba brsg**を使用することもできます。

* スペースに対してセキュリティー・グループをアンバインドするには、以下のコマンドを使用します。

```
cf ba unbind-security-group <security-group> <org> <space>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;Security group&gt;</dt>
<dd class="pd">セキュリティー・グループの名前</dd>
<dt class="pt dlterm">&lt;Org&gt;</dt>
<dd class="pd">セキュリティー・グループをバインドする組織の名前</dd>
<dt class="pt dlterm">&lt;Space&gt;</dt>
<dd class="pd">セキュリティー・グループをバインドする組織内のスペースの名前</dd>
</dl>

**ヒント:** **ba unbind-staging-security-group** という長いコマンド名の別名として **ba usg** を使用することもできます。

## ビルドパックの管理
{: #admin_buildpack}

### ビルドパックのリスト
{: #clilistbuildpack}

アプリ・カタログ書き込み許可がある場合、ビルドパックをリストできます。すべてのビルドパックをリストするか、または特定のビルドパックを表示するには、以下のコマンドを使用します。

```
cf ba buildpacks <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">表示する特定のビルドパックを指定するオプション・パラメーター。</dd>
</dl>

**ヒント:** **ba buildpacks** という長いコマンド名の別名として **ba lb** を使用することもできます。

### ビルドパックの作成およびアップロード
{: #clicreupbuildpack}

アプリ・カタログ書き込み許可がある場合、ビルドパックを作成およびアップロードできます。.zip ファイル・タイプの任意の圧縮ファイルをアップロードできます。ビルドパックをアップロードするには、以下のコマンドを使用します。

```
cf ba create-buildpack <buildpack_name> <file_path> <position>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">アップロードするビルドパックの名前。</dd>
<dt class="pt dlterm">&lt;file_path&gt;</dt>
<dd class="pd">ビルドパック圧縮ファイルのパス。</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">ビルドパックの自動検出時にビルドパックを検査する順序。</dd>
</dl>

**ヒント:** **ba create-buildpack** という長いコマンド名の別名として **ba cb**を使用することもできます。

### ビルドパックの更新
{: #cliupdabuildpack}

アプリ・カタログ書き込み許可がある場合、既存のビルドパックを更新できます。ビルドパックを更新するには、以下のコマンドを使用します。

```
cf ba update-buildpack <buildpack_name> <position> <enabled> <locked>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">更新するビルドパックの名前。</dd>
<dt class="pt dlterm">&lt;position&gt;</dt>
<dd class="pd">ビルドパックの自動検出時にビルドパックを検査する順序。</dd>
<dt class="pt dlterm">&lt;enabled&gt;</dt>
<dd class="pd">ビルドパックをステージング用に使用するのかどうかを示します。</dd>
<dt class="pt dlterm">&lt;locked&gt;</dt>
<dd class="pd">更新されないようにビルドパックをロックするのかどうかを示します。</dd>
</dl>

**ヒント:** **ba update-buildpack** という長いコマンド名の別名として **ba ub** を使用することもできます。

### ビルドパックの削除
{: #clidelbuildpack}

アプリ・カタログ書き込み許可がある場合、既存のビルドパックを削除できます。ビルドパックを削除するには、以下のコマンドを使用します。

```
cf ba delete-buildpack <buildpack_name>
```
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">&lt;buildpack_name&gt;</dt>
<dd class="pd">削除するビルドパックの名前。</dd>
</dl>

**ヒント:** **ba delete-buildpack** という長いコマンド名の別名として **ba db**を使用することもできます。
