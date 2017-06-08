---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-10"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# API キーの管理
{: #manapikey}

アプリケーション・プログラミング・インターフェース・キー (API キー) は、呼び出し側プログラム、その開発者、またはそのユーザーを Web サイトが識別できるように、アプリケーション・プログラミング・インターフェース (API) を呼び出すコンピューター・プログラムによって渡されるコードです。API キーは、API の使用方法を追跡して制御するため (例えば、サービスのご利用条件に定義されているような、API の悪用または不正利用を防止するため) に使用されます。API キーは、多くの場合、認証用の固有 ID と秘密トークンの両方として機能し、通常はそのキーに関連付けられた API に対する一連のアクセス権限を持ちます。API キーは、各ユーザーに固有であることを保証するために、汎用固有 ID (UUID) システムに基づくことができます。

{{site.data.keyword.Bluemix_notm}} ユーザーは、プログラムまたはスクリプトを使用可能にする際に、パスワードをスクリプトに配布せずに、API キーを使用できます。API キーを使用する利点は、ユーザーまたは組織が異なるプログラム用に複数の API キーを作成し、暗号漏えいが発生した場合、他の API キーやユーザーを妨害せずに、個別に API キーを削除できることです。さらに、[フェデレーテッド・ユーザー](/docs/admin/adminpublic.html#federatedid)は、ログインに API キーを使用できます。ログインのための API キーの使用について詳しくは、『[{{site.data.keyword.Bluemix_notm}} CLI `bluemix login` コマンド](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login)』および『[cf CLI `cf login` コマンド](/docs/cli/reference/cfcommands/index.html#cf_login)』を参照してください。

「Bluemix API キー」ウィンドウで、{{site.data.keyword.Bluemix_notm}} API キーを管理できます。説明および日付を含む API キーのリストを確認するには、**「管理」** &gt; **「セキュリティー」** &gt; **「Bluemix API キー」**に移動します。このページで、API キーの作成、編集、または削除を行うことができます。

API キーを作成するには、以下の手順を実行します。

1. **「管理」** &gt; **「セキュリティー」** &gt; **「Bluemix API キー」**に移動します。
2. **「API キーの作成」**をクリックします。
3. API キーの名前と説明を入力します。
4. **「API キーの作成」**をクリックします。
5. 次に、**「表示」**をクリックして API キーを表示し、後で使用するためにコピーして保存するか、または**「API キーのダウンロード」**をクリックします。

**注**: API キーは、作成時にのみ表示またはダウンロードできます。API キーが失われた場合は、新規 API キーを作成する必要があります。

API キーを編集するには、以下の手順を実行します。

1. **「管理」** &gt; **「セキュリティー」** &gt; **「Bluemix API キー」**に移動します。
2. 表にリストされた API キーの**「アクション」**メニューで、**「名前および説明の編集 (Edit the name & description)」**をクリックします。 
3. API キーの情報を更新します。
4. **「API キーの更新」**をクリックします。

API キーを削除するには、以下の手順を実行します。 

1. **「管理」** &gt; **「セキュリティー」** &gt; **「Bluemix API キー」**に移動します。
2. 表にリストされた API キーの**「アクション」**メニューで、**「削除」**をクリックします。
3. 次に、**「キーの削除」**をクリックして、削除を確認します。

{{site.data.keyword.Bluemix_notm}} CLI を使用して、API キーを管理することもできます。キーのリスト表示、キーの作成、キーの更新、またはキーの削除を行えます。詳しくは、[`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) コマンドのセクションを参照してください。

