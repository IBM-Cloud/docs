---

copyright:
  years: 2014, 2016

---

{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} の使用開始 {: #using-object-storage}

*最終更新日: 2016 年 8 月 13 日*
{: .last-updated}


## {{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの使用 {: #using-object-storage-ui}

### UI エレメントとナビゲーション
{{site.data.keyword.objectstorageshort}} がプロビジョンされると、{{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} サービス・インスタンス・ダッシュボードにインスタンス情報が表示されます。ダッシュボードから {{site.data.keyword.objectstorageshort}} インスタンスを選択すると、詳細情報を含むパネルが表示されます。  
#### 使用量データ
アプリケーションのホーム・ページに、インスタンスのストレージ使用量情報が表示されます。**ストレージ・コンテナー**の現在数と、全コンテナー内の**オブジェクト**の総数も示されます。メモリー使用量はメガバイト単位でリストされます。**「消費済みストレージ」**は、現在使用されているスペースの量を表します。
#### アクション
最新の使用量データを取得するには、**「最新表示」**ボタンをクリックします。   
####オブジェクト・ブラウザー
オブジェクト・ブラウザーを使用して、オブジェクト・ストレージのコンテナーおよびオブジェクトを管理します。コンテナーの作成、ファイルのアップロード、コンテナーの削除、ファイルの削除をはじめとするアクションを行えます。


## {{site.data.keyword.Bluemix_notm}} アプリからの {{site.data.keyword.objectstorageshort}} の使用 {: #using-object-storage-from-bluemix-app}

### {{site.data.keyword.objectstorageshort}} サービスを作成後にアプリケーションにバインドする方法 {: #bind-object-storage-to-application}
1.	{{site.data.keyword.Bluemix_notm}} ダッシュボードで、バインドするアプリを選択します。
2.	アプリ概要で**「サービスまたは API のバインド」**をクリックします。
3.	サービスのリストから {{site.data.keyword.objectstorageshort}} インスタンスを選択し、**「追加」**をクリックします。
4.	プロンプトが表示されたら、**「再ステージ」**をクリックします。新しいサービスを使用するには、アプリの再ステージが必要です。

### バインド済みコンテキスト

{{site.data.keyword.objectstorageshort}} をバインド済みコンテキストで使用する場合は、アプリケーションのバインド・プロセスを通じてクラウド資格情報が間接的に提供されます。サービス・インスタンスがアプリケーションに正常にバインドされると、次の例のような構成が `VCAP_SERVICES` 環境変数に追加されます。


```
{
"Object-Storage": [
{
  "name": "Object-Storage - YP",
  "label": "Object-Storage",
  "plan": "Free",
  "credentials": {
     "auth_url": "https://identity.open.softlayer.com",
     "project": "object_storage_d049255b",
     "projectId": "0f47b41b06d047f9aae3b33f1db061ed",
     "region": "dallas",
     "userId": "ad78b2a3f843466988afd077731c61fc",
     "username": "user_202db1f8a7aa3f3ac51ec68f10dbe7dc29070bc7",
     "password": "K/jyIi2jR=1?D.TP",
     "domainId": "2df6373c549e49f8973fb6d22ab18c1a",
     "domainName": "639347"
    }
   }
  ]
}
```

## Swift CLI を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-cli}

インターネット経由で、または IBM {{site.data.keyword.Bluemix_notm}} 内のアプリケーションまたは仮想サーバーから、{{site.data.keyword.objectstorageshort}} サービスにアクセスできます。{{site.data.keyword.objectstorageshort}} サービスの一般的なユース・ケースは、以下のとおりです。

* インスタンスからのボリューム・データのバックアップ
* 大量のデータを転送する場合の中継場所として使用
* 直接接続されていない環境間でのデータの転送
* 中央リポジトリーとして機能

{{site.data.keyword.objectstorageshort}} サービスは OpenStack Swift に基づいており、互換性のある任意のクライアント・アプリケーションを使用してアクセスできます。このセクションでは、Python Swift クライアント ({{site.data.keyword.objectstorageshort}} API のコマンド・ライン・インターフェース (CLI) とその拡張機能) を使用してコンテナーおよびファイルを処理する方法について説明します。

### Swift クライアントのインストール {: #install-swift-client}

以下の前提ソフトウェアがまだインストールされていない場合は、インストールします。詳細については、[OpenStack Documentation](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window} を参照してください。
* Python 2.7 以降
* setuptools パッケージ
* pip パッケージ

Python pip を使用して、Python Swift クライアントをインストールします。

```
	sudo pip install python-swiftclient
```

次のコマンドを実行して、Python Keystone クライアントをインストールします。

```
	sudo pip install python-keystoneclient
```

### クライアントのセットアップ {: #setup-swift-client}

Swift クライアントは、以下の環境変数から認証情報を取得します。
* `OS_AUTH_URL` は、エンドポイント URL
* `OS_USER_ID` は、ユーザー名
* `OS_PASSWORD` は、パスワード

認証情報を以下のように設定します。

```
export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
export OS_PASSWORD=aaa55AAAaaaaa]?,
export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
export OS_AUTH_URL=https://identity.open.softlayer.com/v3
export OS_REGION_NAME=dallas
export OS_IDENTITY_API_VERSION=3
export OS_AUTH_VERSION=3
```

{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの**「サービス資格情報」**ページで、{{site.data.keyword.objectstorageshort}} サービスの資格情報値を検索できます。

**注:** Swift クライアントの環境変数 `OS_AUTH_URL` を構成する際には、必ず {{site.data.keyword.objectstorageshort}} ユーザー・インターフェース内の資格情報から取得した `auth_url` に `/v3` を追加してください。


### コンテナーの処理 {: #work-with-containers}

コンテナーのリスト:
```
	swift list
```
コンテナーの作成:
```
	swift post <container_name>
```
コンテナーの内容のリスト:
```
	swift list <container_name>
```
### オブジェクトの処理 {: #work-with-objects}

#### コンテナーへのファイルの追加
```
	swift upload <container_name> <file_name>
```
#### コンテナーへの 5 GB を超えるファイルの追加

5 GB を超えるファイルをアップロードする場合は、小さいチャンクに分割する必要があります。以下のように `-segment-size` パラメーターを指定することによって、こうしたアップロードの処理を Swift クライアントに指示することができます。
```
	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
```
各セグメントは、`<container_name>_segments` という名前の個別のコンテナーに並列でアップロードされます。すべてのセグメントがアップロードされた後、Swift はマニフェスト・ファイルを作成して、複数のセグメントを元のコンテナー `<container_name>` から単一ファイルに、元のファイル名 `<file_name>` でダウンロードできるようにします。
例えば、次のコマンドは、名前が `test_container` というコンテナーから、セグメント・サイズが `1073741824` で名前が `large_file` というファイルをアップロードします。
```
	swift upload test_container -S 1073741824 large_file
```
このファイルをダウンロードするには、以下のコマンドを実行します。
```
	swift download test_container large_file
```
#### ファイルのダウンロード
```
	swift download <container_name> <file_name>
```
#### コンテナーへのディレクトリーの追加

Swift には、真のディレクトリー構造はありませんが、ディレクトリーのレイアウトを表すネーミングを使用しています。コンテナーにディレクトリーを追加するには、次のコマンドを実行します。
```
	swift upload <container_name> <directory_name>
```
このコマンドは、ディレクトリー構造全体を相対パスとしてアップロードします。例えば、`/mnt/volume1` と指定すると、ディレクトリー構造の mnt/volume1 がすべてのファイル名に付加されて、ディレクトリー構造を示します。
#### ディレクトリーのダウンロード

ディレクトリー構造をダウンロードするには、`-prefix` パラメーターを使用して、ダウンロードするディレクトリーまたはディレクトリー構造を示します。
```
	swift download <container_name> --prefix <directory>
```
#### ファイルの削除
```
	swift delete <container_name> <file_name>
```
### オブジェクトのバージョン管理の処理 {: #work-with-object-versioning}

`X-Versions-Location` フラグを使用して、コンテナー内の各オブジェクトのバージョンをセットアップできます。これを行うには、以下のように、オブジェクトの古いバージョンを保存するための追加コンテナーを作成します。

swift クライアントを使用する場合は、次のようにセットアップします。
```
	swift post container_one -H "X-Versions-Location:container_two"
```
curl を使用する場合は、次のようにセットアップします。
```
	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one
```
この例では、`container_two` は、`container_one` に保管されたオブジェクトの古いバージョンを含めるようにセットアップされています。したがって、`container_one` には最新バージョンのオブジェクトが入り、`container_two` には古いバージョンのオブジェクトが入ります。バージョン管理が機能するためには、必ず `container_two` が存在するようにしてください。

バージョン管理がセットアップされた状態で、`container_one` にオブジェクトをアップロードしたときに、そのオブジェクトの既存のバージョンが存在する場合、新しいバージョンが `container_one` に作成される時点で、既存のバージョンは `container_two` に移動されます。`container_one` からオブジェクトを削除した場合は、前のバージョンのオブジェクトが `container_two` から `container_one` に戻されます。

`container_two` 内のオブジェクトには、
`<Length><Object_name>/<Timestamp>` というフォーマットで自動的に名前が付けられます。

`Length` は、オブジェクトの名前の長さを表します。これは、ゼロが埋め込まれた 3 文字の 16 進数です。`Object_name` は、オブジェクトの名前です。`Timestamp` は、この特定のバージョンのオブジェクトが最初にアップロードされたときのタイム・スタンプです。

バージョン管理を無効にするには、`X-Remove-Versions-Location` フラグを以下のように使用します。
```
	swift post container_one -H "X-Remove-Versions-Location:"
```
または
```
	cURL -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one
```
バージョン管理の完全な使用例を以下に示します。
1. コンテナーの作成:
```
		$ swift post container_one
		$
```
2. container_one のバージョン管理のセットアップ:
```
		$ swift post container_one -H "X-Versions-Location:container_two"
		$
```
3. container_two の作成:
```
		$ swift post container_two
		$
```
4. container_one への初回のオブジェクトのアップロード:
```
		$ swift upload container_one object
		object
		$
```
5. container_one 内のオブジェクトのリスト:
```
		$ swift list container_one
		object
		$
```
6. container_two 内のオブジェクトのリスト:
```
		$ swift list container_two
		$
```
7. オブジェクトの新しいバージョンを container_one にアップロード:
```
		$ swift upload container_one object
		object
		$
```
8. container_one 内のオブジェクトのリスト:
```
		$ swift list container_one
		object
		$
```
9. container_two 内のオブジェクトのリスト:
```
		$ swift list container_two
		006object/1457456909.27383
		$
```
10. container_one 内のオブジェクトの削除:
```
		$ swift delete container_one object
		object
		$
```
11. 両方のコンテナーのリスト:
```
		$ swift list container_one
		object
		$ swift list container_two
		$
```

### オブジェクトの削除のスケジューリング {: #schedule-object-deletion}

指定の期限にオブジェクトの有効期限が切れるように設定できます。つまり、オブジェクトの削除をスケジュールに入れることができます。これを行うには、`X-Delete-At` ヘッダーまたは `X-Delete-After` ヘッダーのどちらかを使用します。`X-Delete-At` ヘッダーは、オブジェクトを削除するエポック時刻を表す整数値です。`X-Delete_After` ヘッダーは、オブジェクトが削除されるまでに経過する秒数を表す整数値です。

swift クライアントを使用して、コンテナー内のオブジェクトに対して post を実行する場合は、以下の例を参照してください。

* 「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、次のコマンドを使用します。
```
		swift post -H "X-Delete-At:1459515600" container object
```
* 今から 1 時間後にオブジェクトを削除するように設定するには、次のコマンドを使用します。
```
		swift post -H "X-Delete-After:3600" container object
```
これを行った後に `swift stat container object` コマンドを実行すると、適切な有効期限がエポック時刻で示された `X-Delete-At` ヘッダーが表示されます。
* オブジェクトから有効期限を削除するには、次のコマンドを使用します。
```
		swift post -H "X-Remove-Delete-After:" container object
```
cURL を使用する場合、コマンドは以下のようになります。
* 「2016/04/01 08:00:00」にオブジェクトを削除するように設定するには、次のコマンドを使用します。
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object
```
* 今から 1 時間後にオブジェクトを削除するように設定するには、次のコマンドを使用します。
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object
```
* オブジェクトにヘッダーが付いているかどうかを確認するには、次のコマンドを使用します。
```
		cURL -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object
```
* 有効期限を削除するには、次のコマンドを使用します。
```
		cURL -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object
```
**注:** オブジェクトの実際の削除は、指示された正確な時刻に行われるとは限りません。ただし、オブジェクトは実際に指定の時刻に期限切れになり、それ以降は到達不能になります。実際の削除は、swift クラスターに構成されている swift-object-expirer デーモンの次回の実行時に行われます。






### 一時 URL の作成 {: #create-temporary-url}

一時 URL は、指定された期間、追加の認証を必要とせずにオブジェクトをダウンロードするために使用できる、推測が困難な長い URL です。一時 URL の生成は、以下の手順で行います。

1. 認証アカウントを識別します。
2. 秘密鍵を設定します。
3. 一時 URL を作成します。

#### 認証アカウントの確認

Swift `stat` コマンドを実行すると、アカウントに関する情報が出力されます。
```
	swift stat
```
「アカウント」フィールドを見つけて、*Account*: の後ろの `AUTH_` を含むすべての文字列をメモします。
#### 秘密鍵の設定

この鍵は自由に選択できますが、ベスト・プラクティスは、ランダムで推測が困難な長いストリングを選択することです。
```
	swift post -m "Temp-URL-Key:<key>"
```
Swift `stat` コマンドを実行して、`Temp-URL-Key` が正常に設定されたことを確認します。
```
	swift stat
```

#### 一時 URL の作成

Swift `tempurl` コマンドでは、以下の定位置引数を使用します。

* [method] ダウンロードを許可する場合は GET。アップロードを許可する場合は PUT。
* [seconds] 一時 URL が使用可能な時間 (秒数)。
* [path] オブジェクトの絶対パス (`/v1/<auth_account>/<container_name>/<object_name>` として表示)。詳細については、[『{{site.data.keyword.objectstorageshort}} URL』](#access-points)を参照してください。
* [key] ステップ 2 で設定した鍵。

```
swift tempurl GET <seconds> <path> <key>
```

このコマンドによって返される URL をクラスター名に付加すると、完全な URL が得られます。互換性のある HTTP クライアント (curl、wget、Firefox など) を使用してオブジェクトをダウンロードするには、完全な URL を使用します。

## Swift REST API を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-restapi}

コマンド・ライン・クライアント・インターフェース (cURL など) で Swift REST API を使用することも、アプリケーションから API を呼び出すこともできます。  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

{{site.data.keyword.objectstorageshort}} API と相互作用するには、 {{site.data.keyword.objectstorageshort}} URL を次のように構成します。
```
	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>
```


この URL は、5 つの部分で構成されています。`<API version>` は v1 です。{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースから、{{site.data.keyword.objectstorageshort}} の `<project ID>`、`<container namespace>`、および `<object namespace>` を検索できます。`<access point>` については、次の表を参照してください。


| **地域**  |   **パブリック・アクセス・ポイント**                     |
|-------------|-----------------------------------------------|
| ダラス      | https://dal.objectstorage.open.softlayer.com/ |
| ロンドン      | https://lon.objectstorage.open.softlayer.com/ |


*表 1. {{site.data.keyword.objectstorageshort}} アクセス・ポイント*


### {{site.data.keyword.objectstorageshort}} API

{{site.data.keyword.objectstorageshort}} REST API のオプションおよび例の包括的なリストについては、[OpenStack Swift API Complete Reference](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window} を参照してください。

## 複数地域間での {{site.data.keyword.objectstorageshort}} の使用 {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} サービスは、「ダラス」と「ロンドン」のストレージ地域をサポートしています。これらのストレージ地域は、{{site.data.keyword.objectstorageshort}} サービス・インスタンスが作成される {{site.data.keyword.Bluemix_notm}} 地域 (「米国南部」や「英国」など) から独立しています。例えば、米国南部 {{site.data.keyword.Bluemix_notm}} 地域に {{site.data.keyword.objectstorageshort}} インスタンスを作成した場合、「ダラス」と「ロンドン」のどちらのストレージ地域ともデータの読み取り/書き込みが行えます。  

米国南部 {{site.data.keyword.Bluemix_notm}} 地域では、「ダラス」ストレージ地域がデフォルトです。英国 {{site.data.keyword.Bluemix_notm}} 地域では、「ロンドン」ストレージ地域がデフォルトです。{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースは、常に {{site.data.keyword.Bluemix_notm}} 地域のデフォルトのストレージ地域を起動します。地域を切り替えるには、「{{site.data.keyword.objectstorageshort}} 地域」ドロップダウン・リストをクリックして、別の地域を選択します。

**注:** {{site.data.keyword.objectstorageshort}} サービスは、ストレージ地域間の複製をサポートしません。

### 複数地域アクセス

{{site.data.keyword.objectstorageshort}} サービスを使用するには、[OpenStack Keystone に対する認証](#keystone-authentication)が必要です。正常に認証された後、`X-Subject-Token` および {{site.data.keyword.objectstorageshort}} エンドポイントが応答内で使用可能になります。

例えば、「ダラス」ストレージ地域に `my_container` という名前のコンテナーを作成するには、curl コマンドで「ダラス」アクセス・ポイントを次のように指定します。
```
	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```

「ロンドン」ストレージ地域に `my_container` という名前のコンテナーを作成するには、curl コマンドで「ロンドン」アクセス・ポイントを次のように指定します。
```
	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT
```
**注:** Keystone から取得した `X-Subject-Token` は、全ストレージ地域で機能します。
異なる地域のアクセス・ポイントについての詳細は、[「Object Storage アクセス・ポイント」](#access-points)表を参照してください。


## 認証と資格情報の理解 {: #understanding-authentication-credentials}

### アプリケーションをバインドせずに {{site.data.keyword.objectstorageshort}} 資格情報を生成

{{site.data.keyword.Bluemix_notm}} アプリケーションの外部で使用する {{site.data.keyword.objectstorageshort}} クラウド資格情報を生成するには、{{site.data.keyword.objectstorageshort}} インスタンス用のサービス・キーを生成する必要があります。新しいキーの生成は、ユーザー・インターフェースのサイドバーから**「サービス資格情報」**を選択するか、Cloud Foundry CLI (バージョン 6.11.3 以降) を使用して行うことができます。{{site.data.keyword.objectstorageshort}} インスタンスのサービス・キーを生成して取得した後、クラウド統合情報を使用して OpenStack SDK または OpenStack Identity API で Keystone トークンを要求したり、Swift アカウントを使用してオブジェクトの管理を開始したりできます。

Cloud Foundry CLI を使用してキーを作成するには、ログインして次のコマンドを実行します。
 ```
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>
```
Cloud Foundry CLI からサービス資格情報を取得するには、次のコマンドを実行します。
```
	cf service-key <object_storage_instance_name> <unique_name_for_this_key>
```

### クラウドのプロジェクトおよびユーザー
新しい {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョンすると、IBM Public Cloud に独立した Keystone プロジェクトが作成されます。{{site.data.keyword.objectstorageshort}} インスタンスに新しいアプリケーションをバインドすると、プロジェクトへのアクセス権限を持つ新しい Keystone ユーザーが作成されます。インスタンスをプロビジョン解除すると、プロジェクトとユーザーは削除されます。

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
アプリケーションに最適な OpenStack トークン要求メソッドまたは OpenStack SDK を選択できるように、資格情報構成には全セットの属性が含まれています。

推奨される v3 トークン要求は、以下の curl コマンドに示されているように、https://identity.open.softlayer.com/v3/auth/tokens への POST 要求です。
```
	curl -i \
	  -H "Content-Type: application/json" \
	  -d '
	{
		"auth": {
			"identity": {
				"methods": [
					"password"
				],
				"password": {
					"user": {
						"id": "ad78b2a3f843466988afd077731c61fc",
						"password": "K/jyIi2jR=1?D.TP"
					}
				}
			},
			"scope": {
				"project": {
					"id": "0f47b41b06d047f9aae3b33f1db061ed"
				}
			}
		}
	}' \
	  https://identity.open.softlayer.com/v3/auth/tokens ; echo
```
応答ヘッダーの `X-Subject-Token` フィールドの値を、{{site.data.keyword.objectstorageshort}} サービスへの要求を行うときに `X-Auth-Token` フィールドとして使用します。
応答の例を以下に示します。この応答は、{{site.data.keyword.objectstorageshort}} 関連の情報のみを示すために切り取られています。

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json
```
	{
	  "token" : {
	    "roles" : [
	      {
	        "id" : "f61f06a84f6443e880210fa986bd8691",
	        "name" : "ObjectStorageOperator"
	      }
	    ],
	    "catalog" : [
	      {
	        "endpoints" : [
	          {
	            "id" : "20cbfa6ff22b4a67a1484d30235bfc80",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "38b8c081b11a452bb951698c334a406d",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          },
	          {
	            "id" : "4207049680fa4effbecd044c7448a8cb",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "8a65a0cf38ac4211ad6a3c9c0eb337ff",
	            "region" : "london",
	            "region_id" : "london",
	            "url" : "https:\/\/lon.objectstorage.open.softlayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "public"
	          },
	          {
	            "id" : "a60cf32be624491d89170ef8264de5e8",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "admin"
	          },
	          {
	            "id" : "c769862200124a308d6748e418c971ba",
	            "region" : "dallas",
	            "region_id" : "dallas",
	            "url" : "https:\/\/dal.objectstorage.service.open.networklayer.com\/v1\/AUTH_3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	            "interface" : "internal"
	          }
	        ],
	        "id" : "896e4064cbe742afbf9a543c15f27ac0",
	        "type" : "object-store",
	        "name" : "swift"
	      },
	    ],
	    "extras" : {

	    },
	    "user" : {
	      "id" : "0b8aebd924ef4cc7aa9232f07e47e874",
	      "name" : "user_87c094ce47a9feae3a137ffcbbfa098a888c12a8",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "expires_at" : "2016-02-29T22:03:42.061343Z",
	    "audit_ids" : [
	      "cbA-iL2dSheyB72PHd7q8Q"
	    ],
	    "issued_at" : "2016-02-29T21:03:42.000000Z",
	    "project" : {
	      "id" : "3ecf7d7bac2c4eda89c03dd3afa7a0a3",
	      "name" : "object_storage_c1d8b3a1",
	      "domain" : {
	        "id" : "8753ff40ac1a4f4a9f162ad8026b6ce0",
	        "name" : "757955"
	      }
	    },
	    "methods" : [
	      "password"
	    ]
	  }
	}
```

{{site.data.keyword.objectstorageshort}} URL は、サービス・カタログ内にあります。サービス・カタログは、トークン要求の応答本体に含まれています。応答は、使用可能な OpenStack サービスの完全なカタログです。サービス・カタログから、タイプが `object-store` で、地域が、資格情報の地域フィールドに一致しているエンドポイントを選択します。

**注:** パブリック・インターフェース (`publicURL`) を使用してください。内部インターフェース (`internalURL`) は、{{site.data.keyword.Bluemix_notm}} からアクセスできません。



## 微細化されたアクセス制御によるファイルの保護 {: #fine-grained-access-control}

微細化されたアクセス制御リストは、複数のユーザーが同じコンテナー内に複数のファイルを保管している場合に、ファイルを保護するのに役立ちます。

注: 本書に概説されている手順を実行するには、Swift CLI が必要です。詳細については、[using {{site.data.keyword.objectstorageshort}} with the Swift CLI](https://console.ng.bluemix.net/docs/services/ObjectStorage/objectstorge_usingobjectstorage.html#using-swift-cli) を参照してください。


### アクセスのタイプ {: #access-types}

サービスへのアクセスは、ユーザーの役割とコンテナーのアクセス制御リストによって制御されます。{{site.data.keyword.objectstorageshort}} のユーザーは、管理ユーザーまたは非管理ユーザーのいずれかです。アクセス制御リストは、管理ユーザーによってコンテナー・レベルで有効にされ、サービス・インスタンス、ストレージ・アカウント、およびプロジェクト・レベルでは使用できません。

<table>
  <tr>
    <th> 管理ユーザー (管理者) </th>
    <th> 非管理ユーザー (メンバー) </th>
  </tr>
  <tr>
    <td> アクセス制御を管理 </td>
    <td> デフォルトでは、サービスおよびコンテナーに対するアクセス権限がない </td>
  </tr>
  <tr>
    <td> コンテナーの作成および削除が可能 </td>
    <td> コンテナーの読み取り/書き込み ACL に基づいてアクションを実行可能 </td>
  </tr>
  <tr>
    <td> コンテナーの読み取りおよび書き込みが可能 </td>
    <td> 管理者の決定に従ってアクションを実行可能 </td>
  </tr>
</table>

*表 1: 定義済みのユーザー役割*

{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース、Cloud Foundry API、または Cloud Foundry CLI を使用して、{{site.data.keyword.objectstorageshort}} ユーザーを管理できます。



### {{site.data.keyword.objectstorageshort}} サービス資格情報の生成 {: #generating}

新規 {{site.data.keyword.Bluemix_notm}} コンソールから、{{site.data.keyword.objectstorageshort}} ユーザーの新しいサービス資格情報を生成できます。新規コンソールを表示するには、**「Try the new {{site.data.keyword.Bluemix_notm}}」**をクリックします。

1.  開発者の役割を持つユーザーとして、{{site.data.keyword.Bluemix_notm}} にログインします。ユーザーは管理対象のサービス・インスタンスのスペース内にいる必要があります。
2. **「サービス資格情報」**タブをクリックします。
3. **「新しい資格情報」**をクリックします。
4. 資格情報の名前を指定します。
5. **「インライン構成パラメーターの追加」**テキスト・フィールドに、作成する役割の資格情報を入力します。この情報は、JSON ペイロードとしてフォーマット設定する必要があります。
  - 管理ユーザーを作成する場合: `{"role":"admin"}`
  - 非管理ユーザーを作成する場合: `{"role":"member"}`
5. **「追加」**をクリックします。

cURL コマンドまたは Swift CLI を使用してサービス資格情報を生成するには、以下の手順を使用します。

1. 開発者の役割を持つユーザーとして、{{site.data.keyword.Bluemix_notm}} にログインします。ユーザーは管理対象のサービス・インスタンスのスペース内にいる必要があります。

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```

2. サービス資格情報を生成します。`service-key-name` は、資格情報の名前です。Cloud Foundry コマンドまたは cURL コマンドのいずれかを使用できます。

  Cloud Foundry コマンド:
  ```
  cf create-service-key "<object_storage_service_instance_name>" <service-key-name> -c '{"role":"<object_storage_role>"}'
  ```

  例:

  ```
  cf create-service-key "Object-Storage-AclTest" GeorgeKey -c '{"role":"member"}'

  ```
  cURL コマンド:
  ```
  curl "https://api.ng.bluemix.net/v2/service_keys" -d '{   "service_instance_guid": "<service_instance_guid>",   "name": "<user_name>", "role": "member"}' -X POST -H "Authorization: <bearer_token>" -H "Content-Type: " -H "Cookie: "
  ```

3. 作成したサービス・キーの資格情報を検証します。

  Cloud Foundry コマンド:
  ```
  cf service-key <service_key_name> <member_name>
  ```
  例:
  Object-Storage-Acl-Test という名前のサービス・インスタンスのメンバー・サービス・キーを作成します。
  ```
  {
    "auth_url": "https://identity.open.softlayer.com",
    "domainId": "8753ff40ac1a4f4a9f162ad8026b6ce0",
    "domainName": "757955",
    "password": "xxxxxxxx",
    "project": "object_storage_6046b6e2_ee53_4884_916f_89c65e4d408e",
    "projectId": "c727d7e248b448f6b268f31a1bd8691e",
    "region": "dallas",
    "role": "member",
    "userId": "3c5b516655e4479881d3d216895faedb",
    "username": "member_2afbeea1d58b1867f46c699553d1e4513e7df83a"
  }
  ```
  cURL コマンド:
  ```
  curl "https://api.ng.bluemix.net/v2/service_instances/b9656309-d994-4dec-a71f-8eac6e2fc7dc/service_keys" -X GET  -H "Authorization: <bearer_token>" -H "Cookie: "
  ```



### アクセス権限の割り当て {: #assigning-access}  

管理者の役割を持つ {{site.data.keyword.objectstorageshort}} ユーザーのみが、別のユーザーに対してコンテナーの読み取り権限または書き込み権限を付与することができます。

CLI で読み取り権限を付与するには、`--read-acl` オプションまたは `-r` オプションを使用します。

1. 作成したサービス資格情報内の情報を使用して、資格情報を認証します。出力として、Object Storage URL と認証トークンを受け取ります。

  Swift コマンド:
  ```
  export OS_USER_ID=<user_id>
  export OS_PASSWORD=<password>
  export OS_TENANT_ID=<project_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL コマンド:
  ```
  curl -i -H "X-Auth-User: <user_id>" -H "X-Auth-Key: <password>" <auth_url>
  ```
3. 以下のコマンドを実行して、読み取り権限を付与します。

  Swift コマンド:
  ```
  swift post <container_name> --read-acl "<user_id>:<project_id>"
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: <tenant_id>:<project_id>" -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
4. 読み取り ACL 値を検証します。

  Swift コマンド:
  ```
  swift stat <container_name>
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```
  出力例:
  ```
  HTTP/1.1 204 No Content
  Content-Length: 0
  X-Container-Object-Count: 1
  Accept-Ranges: bytes
  X-Storage-Policy: standard
  X-Container-Read: c727d7e248b448f6b268f31a1bd8691e:3c5b516655e4479881d3d216895faedb
  X-Container-Bytes-Used: 31512
  X-Timestamp: 1462818314.11220
  Content-Type: text/plain; charset=utf-8
  X-Trans-Id: txad7fe001da274b9ba39a6-005772e4d6
  Date: Tue, 28 Jun 2016 20:57:58 GMT
  ```

読み取り ACL の組み合わせを操作できます。

<table>
  <tr>
    <th> 許可 </th>
    <th> 読み取り ACL オプション </th>
  </tr>
  <tr>
    <td> アカウントの加入に関係なくすべての参照者に対する読み取り</td>
    <td> `.r,*` </td>
  </tr>
  <tr>
    <td> すべての参照者に対する読み取りとリストおよびリスト作成 </td>
    <td> `.r:*,.rlistings` </td>
  </tr>
  <tr>
    <td> 特定のプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> `< project_id>:< user_id>` </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトの指定されたユーザーに対する読み取りとリスト </td>
    <td> `<*>:< user_id>` </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> `< project_id>:<*>` </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する読み取りとリスト</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 2: オプション別の読み取りアクセス許可*

注: アクセス制御リストを区切るには、コンマ (,) を使用します。例: `-read-acl project id:user_id1, project_id2:user_id2`。


書き込み権限を付与するには、Swift CLI で `--write-acl` オプションまたは `-w` オプションを使用します。

1. 作成したサービス資格情報内の情報を使用して、資格情報を認証します。出力として、Object Storage URL と認証トークンを受け取ります。

  Swift コマンド:
  ```
  export OS_USER_ID="<user_id>"
  export OS_PASSWORD="<password>"
  export OS_TENANT_ID=<tenant_id>
  export OS_AUTH_URL=https://identity.open.softlayer.com/v3
  export OS_REGION_NAME=<region>
  export OS_IDENTITY_API_VERSION=3
  export OS_AUTH_VERSION=3

  swift auth
  ```
  cURL コマンド:
  ```
  curl -i -H "X-Auth-User:< user_id>" -H "X-Auth-Key:< password>" https://identity.open.softlayer.com/v3
  ```
2. 以下のコマンドを実行して、書き込み権限を付与します。

  Swift コマンド:
  ```
  swift post <container_name> --write-acl "<user_id>:<project_id>"
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: <user_id>: <project_id>" -H "X-Auth-Token:<OS_AUTH_TOKEN>"

  ```
3. 書き込み ACL 値を検証します。

  Swift コマンド:
  ```
  swift stat <container_name>
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token:<OS_AUTH_TOKEN>"
  ```


書き込み ACL の組み合わせを操作できます。

<table>
  <tr>
    <th> 許可 </th>
    <th> 書き込み ACL オプション </th>
  </tr>
  <tr>
    <td> 特定のプロジェクトの指定されたユーザーに対する書き込み</td>
    <td> `<project_id>:<user_id>` </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトの指定されたユーザーに対する書き込み</td>  
    <td> `*:<user_id>` </td>
  </tr>
  <tr>
    <td> 指定されたプロジェクトのすべてのユーザーに対する書き込み</td>
    <td> `<project_id>:<*>` </td>
  </tr>
  <tr>
    <td> すべてのプロジェクトのすべてのユーザーに対する書き込み</td>
    <td> `<*>:<*>` </td>
  </tr>
</table>

*表 3: オプション別の書き込みアクセス許可*

注: アクセス制御リストを区切るには、コンマ (,) を使用します。例: `-write-acl project id:user_id1, project_id2:user_id2`。




### アクセス権限の削除 {: #removing-access}

コンテナーから読み取り ACL を削除するには、以下のようにします。

  Swift コマンド:
  ```
  swift post <container_name> --read-acl “”
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

コンテナーから書き込み ACL を削除するには、以下のようにします。

  Swift コマンド:
  ```
  swift post <container_name> --write-acl “”
  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```

ACL が削除されたことを確認するには、以下のようにします。

  Swift コマンド:
  ```
  swift stat <container_name>
  ```

  出力例:
  ```
         Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
       Container: Test
         Objects: 1
           Bytes: 31512
        Read ACL:
       Write ACL:
         Sync To:
        Sync Key:
   Accept-Ranges: bytes
X-Storage-Policy: standard
     X-Timestamp: 1462818314.11220
      X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
    Content-Type: text/plain; charset=utf-8

  ```
  cURL コマンド:
  ```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```




## {{site.data.keyword.objectstorageshort}} のアンバインドおよびプロビジョン解除 {: #deprovisioning-object-storage}

### {{site.data.keyword.objectstorageshort}} サービスのプロビジョン解除方法
1.	{{site.data.keyword.Bluemix_notm}} ダッシュボードからサービスを選択します。  
2.	歯車アイコンをクリックして、**「サービスの削除」**を選択します。

**注意:**
{{site.data.keyword.objectstorageshort}} for
{{site.data.keyword.Bluemix_notm}} サービス・インスタンスをプロビジョン解除すると、クラウド・プロジェクトおよび Swift アカウントが削除されます。プロビジョン解除されたインスタンス内のすべてのコンテナーおよびオブジェクトが Swift から削除され、復元できません。

### アプリケーションのアンバインドまたはサービス・キーの削除

{{site.data.keyword.objectstorageshort}} インスタンスからアプリケーションをアンバインドするか、サービス・キーを削除すると、資格情報が削除されます。{{site.data.keyword.objectstorageshort}} アカウントは、{{site.data.keyword.objectstorageshort}} インスタンスがプロビジョン解除されるまで削除されません。[サービス・キーを再バインドまたは作成](#bind-object-storage-to-application)することによって、新しいクラウド資格情報を生成できます。
