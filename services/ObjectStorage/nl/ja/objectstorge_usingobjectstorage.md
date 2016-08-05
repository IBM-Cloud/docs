{:new_window: target="_blank"}

# {{site.data.keyword.objectstorageshort}} の使用の開始 {: #using-object-storage} 

*最終更新日: 2016 年 6 月 24 日*
{: .last-updated}


## {{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの使用 {: #using-object-storage-ui}

### UI エレメントとナビゲーション
{{site.data.keyword.objectstorageshort}} がプロビジョンされると、{{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} サービス・インスタンス・ダッシュボードにインスタンス情報が表示されます。ダッシュボードから {{site.data.keyword.objectstorageshort}} インスタンスを選択すると、詳細情報を含むパネルが表示されます。  
#### 使用量データ
アプリケーションのホーム・ページに、インスタンスのストレージ使用量の情報が表示されます。**ストレージ・コンテナー**の現在数と、全コンテナー内の**オブジェクト**の総数も示されます。メモリー使用量がメガバイト単位でリストされます。**ストレージ消費**は、使用されているスペースの現在量を示します。 
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

{{site.data.keyword.objectstorageshort}} をバインド済みコンテキストで使用したい場合、アプリケーションのバインド・プロセスを通じてクラウド資格情報が間接的に提供されます。サービス・インスタンスがアプリケーションに正常にバインドされると、次の例のような構成が `VCAP_SERVICES` 環境変数に追加されます。


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


## Swift CLI を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-cli}

{{site.data.keyword.objectstorageshort}} サービスには、インターネットを介してアクセスすることも、IBM {{site.data.keyword.Bluemix_notm}} 内のアプリケーションおよび仮想サーバーからアクセスすることもできます。{{site.data.keyword.objectstorageshort}} サービスの一般的なユース・ケースは次のとおりです。

* インスタンスからボリューム・データをバックアップする
* 大容量のデータを転送する際の仲介場所として使用する
* 直接接続されていない環境間でデータを転送する
* 中央リポジトリーとして機能する

{{site.data.keyword.objectstorageshort}} サービスは OpenStack Swift に基づいており、互換性のある任意のクライアント・アプリケーションを使用してアクセスできます。このセクションでは、{{site.data.keyword.objectstorageshort}} API およびその拡張機能のコマンド・ライン・インターフェース (CLI) である Python Swift クライアントを使用してコンテナーおよびファイルを操作する方法について説明します。

### Swift クライアントのインストール {: #install-swift-client}

まだインストールされていない場合は、以下の前提ソフトウェアをインストールしてください。詳しくは、[OpenStack 資料](http://docs.openstack.org/user-guide/common/cli_install_openstack_command_line_clients.html#install-the-prerequisite-software){: new_window}を参照してください。 
* Python 2.7 以降
* setuptools パッケージ
* pip パッケージ

Python pip を使用して Python Swift クライアントをインストールします。

	sudo pip install python-swiftclient

### クライアントのセットアップ {: #setup-swift-client}

Swift クライアントは、以下の環境変数から認証情報を取得します。
* ```OS_AUTH_URL``` はエンドポイント URL です
* ```OS_USER_ID``` はユーザー名です
* ```OS_PASSWORD``` はパスワードです

認証情報を次のように設定してください。 

	export OS_USER_ID=24a20b8e4e724f5fa9e7bfdc79ca7e85
	export OS_PASSWORD=aaa55AAAaaaaa]?,
	export OS_PROJECT_ID=383ec90b22ff4ba4a78636f4e989d5b1
	export OS_AUTH_URL=https://identity.open.softlayer.com/v3
	export OS_REGION_NAME=dallas
	export OS_IDENTITY_API_VERSION=3
	export OS_AUTH_VERSION=3

{{site.data.keyword.objectstorageshort}} サービス用の資格情報値は {{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの**「サービス資格情報」**ページで見つけることができます。 

**注:** Swift クライアント用に環境変数 ```OS_AUTH_URL``` を構成するときには、{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの資格情報からの ```auth_url``` に、必ず ```/v3``` を追加してください。


### コンテナーの操作 {: #work-with-containers}

コンテナーをリスト表示する

	swift list
	
コンテナーを作成する

	swift post <container_name>
	
コンテナーの内容をリスト表示する

	swift list <container_name>

### オブジェクトの操作 {: #work-with-objects}

#### コンテナーへのファイルの追加

	swift upload <container_name> <file_name>

#### コンテナーへの 5 GB より大きいファイルの追加

5 GB より大きいファイルをアップロードする場合は、小さいチャンクに分割する必要があります。```-segment-size``` パラメーターを指定することで、そのようなアップロードを処理するよう Swift クライアントに指示することができます。

	swift upload <container_name> <file_name> --segment-size <size_in_bytes>
	
各セグメントが、```<container_name>_segments``` と名付けられた別々のコンテナーに並行してアップロードされます。すべてのセグメントのアップロードが終わった後、Swift は、それらのセグメントを元のファイル名 ```<file_name>``` を使用して単一ファイルで元のコンテナー ```<container_name>``` からダウンロードできるように、マニフェスト・ファイルを作成します。

例えば、次のコマンドは、```test_container``` という名前のコンテナーから、```large_file``` という名前のファイルをセグメント・サイズ ```1073741824``` でアップロードします。

	swift upload test_container -S 1073741824 large_file

次のコマンドを実行して、このファイルをダウンロードできます。

	swift download test_container large_file

#### ファイルのダウンロード

	swift download <container_name> <file_name>
	
#### コンテナーへのディレクトリーの追加

Swift には本当のディレクトリー構造はありませんが、ディレクトリー・レイアウトを表す命名法が使用されています。コンテナーにディレクトリーを追加するには、次のコマンドを実行します。

	swift upload <container_name> <directory_name>
	
このコマンドによって、ディレクトリー構造全体が相対パスとしてアップロードされます。例えば、```/mnt/volume1``` と指定すると、ディレクトリー構造 mnt/volume1 がすべてのファイル名に付加されてこのディレクトリー構造が示されます。

	
#### ディレクトリーのダウンロード

ディレクトリー構造をダウンロードするには、```-prefix``` パラメーターを使用して、ダウンロードしたいディレクトリーまたはディレクトリー構造を指定します。

	swift download <container_name> --prefix <directory>
	
#### ファイルの削除

	swift delete <container_name> <file_name>

### オブジェクト・バージョン管理の操作 {: #work-with-object-versioning}

```X-Versions-Location``` フラグを使用して、コンテナー内の各オブジェクトのバージョンをセットアップできます。これを行うには、以下のようにして、古いバージョンのオブジェクトを保持するためのコンテナーを追加で作成します。 

Swift クライアントを使用している場合は、以下のようにしてセットアップできます。

	swift post container_one -H "X-Versions-Location:container_two"

curl を使用している場合は、以下のようにしてセットアップできます。

	curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Versions-Location:container_two" https://<object-storage_url>/container_one

この例では、```container_one``` に保管されていた古いバージョンのオブジェクトが ```container_two``` に入るようにセットアップされました。これにより、```container_one``` には最新バージョンのオブジェクトが入り、```container_two``` には古いバージョンのオブジェクトが入ります。バージョン管理を機能させるために、必ず、```container_two``` が存在することを確認してください。

バージョン管理がセットアップされている状態でオブジェクトを ```container_one``` にアップロードし、そのオブジェクトの既存バージョンがあった場合、新規バージョンが ```container_one``` に作成されるため、既存バージョンは ```container_two``` に移されます。```container_one``` からオブジェクトを削除すると、そのオブジェクトの前のバージョンが ```container_two``` から ```container_one``` に戻されます。

```container_two``` 内のオブジェクトには、以下の形式の名前が自動的に付けられます。```<Length><Object_name>/<Timestamp>```

```Length``` は、オブジェクト名の長さを指します。これは、ゼロ埋めされる 3 文字の 16 進数です。```Object_name``` はオブジェクトの名前です。```Timestamp``` は、オブジェクトのこの特定バージョンが最初にアップロードされた際のタイム・スタンプです。

バージョン管理を無効にするには、以下のように ```X-Remove-Versions-Location``` フラグを使用します。

	swift post container_one -H "X-Remove-Versions-Location:"

または

	curl -i -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Versions-Location: anyvalue" https://<object-storage_url>/container_one

以下に、バージョン管理の全使用例を示します。

1. コンテナーを作成します。

		$ swift post container_one
		$

2. container_one にバージョン管理をセットアップします。

		$ swift post container_one -H "X-Versions-Location:container_two"
		$

3. container_two を作成します。

		$ swift post container_two
		$

4. container_one にオブジェクトの 1 回目のアップロードを行います。

		$ swift upload container_one object
		object
		$

5. container_one 内のオブジェクトをリストします。

		$ swift list container_one
		object
		$

6. container_two 内のオブジェクトをリストします。

		$ swift list container_two
		$

7. このオブジェクトの新しいバージョンを container_one にアップロードします。

		$ swift upload container_one object
		object
		$

8. container_one 内のオブジェクトをリストします。

		$ swift list container_one
		object
		$

9. container_two 内のオブジェクトをリストします。

		$ swift list container_two
		006object/1457456909.27383
		$

10. container_one 内のオブジェクトを削除します。

		$ swift delete container_one object
		object
		$

11. 両方のコンテナーをリストします。

		$ swift list container_one
		object
		$ swift list container_two
		$

### オブジェクト削除のスケジューリング {: #schedule-object-deletion}

オブジェクトが一定時間で期限切れになるように設定することができます。つまり、オブジェクト削除のスケジューリングが可能です。これを行うには、```X-Delete-At``` または ```X-Delete-After``` のヘッダーを利用します。```X-Delete-At``` ヘッダーには、オブジェクトを削除するエポック時刻を表す整数を指定します。```X-Delete_After``` ヘッダーには、オブジェクトを削除するまでの秒数を表す整数を指定します。

Swift クライアントを使用している場合、コンテナー内のオブジェクトに post を実行します。以下の例を参照してください。

* オブジェクトが「2016/04/01 08:00:00」に削除されるように設定するには、次のコマンドを使用します。

		swift post -H "X-Delete-At:1459515600" container object

* オブジェクトが今から 1 時間後に削除されるように設定するには、次のコマンドを使用します。

		swift post -H "X-Delete-After:3600" container object

  これを行った後に ```swift stat container object``` コマンドを実行すると、エポック時刻での適切な有効期限が示された ```X-Delete-At``` ヘッダーが表示されます。

* オブジェクトの有効期限時刻を削除するには、次のコマンドを使用します。

		swift post -H "X-Remove-Delete-After:" container object

curl を使用している場合のコマンドは、以下のとおりです。 

* オブジェクトが「2016/04/01 08:00:00」に削除されるように設定するには、次のコマンドを使用します。

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-At:1459515600" https://<object-storage_url>/container/object

* オブジェクトが今から 1 時間後に削除されるように設定するには、次のコマンドを使用します。

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Delete-After:3600" https://<object-storage_url>/container/object

* オブジェクトにこのヘッダーがあるかどうかを確認するには、次のコマンドを使用します。

		curl -I -H "X-Auth-Token: <token>" https://<object-storage_url>/container/object

* 有効期限時刻を削除するには、次のコマンドを使用します。

		curl -X POST -H "X-Auth-Token: <token>" -H "X-Remove-Delete-At:" https://<object-storage_url>/container/object

**注:** オブジェクトの実際の削除は、指定された正確な時刻に行われない場合があります。それでも、オブジェクトは指定された時刻に事実上有効期限切れになり、以降、アクセス不能になります。実際の削除は、Swift クラスターに構成された swift-object-expirer デーモンの次回実行時に行われます。





### 一時 URL の作成 {: #create-temporary-url}

一時 URL は、追加の認証を必要とせずにオブジェクトをダウンロードするために指定期間だけ使用できる、推測が難しい長い URL です。以下の手順で一時 URL を生成します。

1. 認証アカウントを識別します。
2. 秘密鍵を設定します。
3. 一時 URL を作成します。

#### 認証アカウントの識別

Swift ```stat``` コマンドは、アカウントに関する情報を出力します。

	swift stat

「Account」フィールドを見つけて、*Account*: の後ろの ```AUTH_``` を含むすべての文字列をメモします。

#### 秘密鍵の設定

この鍵は任意のものを選択できますが、ベスト・プラクティスは、ランダムで長く、推測しにくいストリングを選択することです。

	swift post -m "Temp-URL-Key:<key>"
	
Swift ```stat``` コマンドを実行して、```Temp-URL-Key``` が正しく設定されていることを検証します。

	swift stat


#### 一時 URL の作成

Swift ```tempurl``` コマンドには、以下の定位置引数を指定します。

* [method] ダウンロードを許可する場合は GET。アップロードを許可する場合は PUT。
* [seconds] 一時 URL が使用可能になる時間 (秒単位)。
* [path] ```/v1/<auth_account>/<container_name>/<object_name>``` で表される、オブジェクトの絶対パス。詳しくは、[{{site.data.keyword.objectstorageshort}} URL](#access-points) を参照してください。 
* [key] ステップ 2 で設定した鍵。

```
swift tempurl GET <seconds> <path> <key>
```

このコマンドによって URL が返され、それをクラスター名の後ろに付けると完全な URL を取得できます。その完全な URL を使用して、任意の互換 HTTP クライアント (curl、wget、Firefox など) でオブジェクトをダウンロードできます。

## Swift REST API を使用した {{site.data.keyword.objectstorageshort}} へのアクセス {: #using-swift-restapi}

コマンド・ライン・クライアント・インターフェース (例えば cURL) で Swift REST API を使用するか、アプリケーションから API を呼び出すことができます。  

### {{site.data.keyword.objectstorageshort}} URL {: #access-points}

{{site.data.keyword.objectstorageshort}} API と対話するためには、{{site.data.keyword.objectstorageshort}} URL を次のように組み立てます。

	https://<access point>/<API version>/AUTH_<project ID>/<container namespace>/<object namespace>



URL は 5 つの部分からなります。```<API version>``` は v1 です。{{site.data.keyword.objectstorageshort}} の ```<project ID>```、```<container namespace>```、および ```<object namespace>``` は、{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースから調べられます。```<access point>``` については、以下の表を参照してください。 


| ** 地域 **  |   **パブリック・アクセス・ポイント**                     |
|-------------|-----------------------------------------------|
| ダラス      | https://dal.objectstorage.open.softlayer.com/ | 
| ロンドン      | https://lon.objectstorage.open.softlayer.com/ |


*表 1. {{site.data.keyword.objectstorageshort}} アクセス・ポイント*


### {{site.data.keyword.objectstorageshort}} API

{{site.data.keyword.objectstorageshort}} REST API オプションの完全なリストおよび例については、[OpenStack Swift API の完全なリファレンス](http://developer.openstack.org/api-ref-objectstorage-v1.html){: new_window}を参照してください。

## 複数地域にまたがる {{site.data.keyword.objectstorageshort}} の使用 {: #multi-regions}  

IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} サービスは、ストレージ地域「ダラス」と「ロンドン」をサポートしています。これらのストレージ地域は、{{site.data.keyword.objectstorageshort}} サービス・インスタンスが作成される {{site.data.keyword.Bluemix_notm}} 地域 (「米国南部」や「英国」) とは関係ありません。例えば、{{site.data.keyword.Bluemix_notm}} 地域「米国南部」で {{site.data.keyword.objectstorageshort}} インスタンスを作成する場合、ストレージ地域「ダラス」または「ロンドン」のいずれかでデータを読み書きできます。  

{{site.data.keyword.Bluemix_notm}} 地域が「米国南部」の場合、「ダラス」ストレージ地域がデフォルトです。{{site.data.keyword.Bluemix_notm}} 地域が「英国」の場合、「ロンドン」ストレージ地域がデフォルトです。{{site.data.keyword.objectstorageshort}} ユーザー・インターフェースの起動時には、常に {{site.data.keyword.Bluemix_notm}} 地域のデフォルトのストレージ地域になります。地域を切り替えるには、{{site.data.keyword.objectstorageshort}} 地域のドロップダウン・リストをクリックして、別の地域を選択します。

**注:** {{site.data.keyword.objectstorageshort}} サービスは、異なるストレージ地域間での複製をサポートしません。

### 複数地域のアクセス

{{site.data.keyword.objectstorageshort}} サービスを使用するには、[OpenStack Keystone への認証](#keystone-authentication)を行う必要があります。正常に認証されたら、それ以降は ```X-Subject-Token``` および {{site.data.keyword.objectstorageshort}} エンドポイントが応答内で使用可能になります。

例えば、```my_container``` という名前のコンテナーをストレージ地域「ダラス」に作成するには、以下のようにダラスのアクセス・ポイントを curl コマンドに指定します。

	# curl -i https://dal.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT


```my_container``` という名前のコンテナーをストレージ地域「ロンドン」に作成するには、以下のようにロンドンのアクセス・ポイントを curl コマンドに指定します。

	# curl -i https://lon.objectstorage.open.softlayer.com/v1/AUTH_3c9c89a2edbb458da74a9e81e215da9e/my_container -X PUT -H "Content-Length: 0" -H "X-Auth-Token: gAAAAABWlw5mwttbb_6G3LnTiGusyoOSEHXMG7oTnDYWN1vBZB6XAxUEhz4ehGkdw6Qm_I9ZFFXr8fwcc2KaEbpWbQoglhAvrYTXbrkn8MvErLdnbcT0XK2t5N7lEZyyKQlsgmQWcrch8VOO_OiSKKToORYR7luI-2TrR_JIVZm-8AAS6hLhk9"

	HTTP/1.1 201 Created
	Content-Length: 0
	Content-Type: text/html; charset=UTF-8
	X-Trans-Id: tx4a640ca81c7240ea8f812-00569712fc
	Date: Thu, 14 Jan 2016 03:16:13 GMT

**注:** Keystone から取得した ```X-Subject-Token``` は、ストレージ地域をまたがって機能します。 

各地域のアクセス・ポイントについて詳しくは、表「[Object Storage アクセス・ポイント](#access-points)」を参照してください。


## 認証および資格情報の理解 {: #understanding-authentication-credentials}

### アプリケーションのバインドなしの {{site.data.keyword.objectstorageshort}} 資格情報の生成

{{site.data.keyword.Bluemix_notm}} アプリケーションの外部で使用するための {{site.data.keyword.objectstorageshort}} クラウド資格情報を生成するには、{{site.data.keyword.objectstorageshort}} インスタンスのサービス・キーを生成する必要があります。新規キーは、ユーザー・インターフェースのサイドバーから**「サービス資格情報」**を選択することによって、または、Cloud Foundry CLI (バージョン 6.11.3 以降) を使用することによって生成できます。{{site.data.keyword.objectstorageshort}} インスタンスのサービス・キーを生成して取得した後は、クラウド統合情報を使用して OpenStack SDK または OpenStack Identity API で Keystone トークンを要求することができ、また、Swift アカウントを使用したオブジェクトの管理を開始することができます。
   
Cloud Foundry CLI を使用してキーを作成するには、ログインして次のコマンドを実行します。
 
    cf create-service-key <object_storage_instance_name> <unique_name_for_this_key>

Cloud Foundry CLI からサービス資格情報を取得するには、次のコマンドを実行します。

	cf service-key <object_storage_instance_name> <unique_name_for_this_key>


### クラウドのプロジェクトおよびユーザー
新しい {{site.data.keyword.objectstorageshort}} インスタンスをプロビジョンすると、IBM Public Cloud 内に独立した Keystone プロジェクトが作成されます。その {{site.data.keyword.objectstorageshort}} インスタンスに新しいアプリケーションをバインドすると、このプロジェクトへのアクセス権限を持つ新規 Keystone ユーザーが作成されます。インスタンスをプロビジョン解除すると、プロジェクトとユーザーは削除されます。

### OpenStack Identity (Keystone) v3 {: #keystone-authentication}
資格情報構造には、アプリケーションに最適の OpenStack トークン要求メソッドまたは OpenStack SDK の選択を可能にする、属性の完全なセットが含まれています。 
 
推奨される v3 トークン要求は、以下の curl コマンドで示されているような https://identity.open.softlayer.com/v3/auth/tokens への POST 要求です。

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

応答ヘッダーの ```X-Subject-Token``` フィールドの値を、{{site.data.keyword.objectstorageshort}} サービスへの要求を行うときに ```X-Auth-Token``` フィールドとして使用します。

以下に、応答例を示します。この応答は、{{site.data.keyword.objectstorageshort}} の関連情報のみを表示するために切り取ったものです。

	HTTP/1.1 201 Created
	Date: Mon, 29 Feb 2016 21:03:41 GMT
	Server: Apache/2.4.6 (CentOS) OpenSSL/1.0.1e-fips mod_wsgi/3.4 Python/2.7.5
	X-Subject-Token: gAAAAABW1LIubUgqKl-eInzhZUHWEnXijp7t6_5inl4DTRLxDhNbJ25ly2X7bASNvH7ocxinaJu_kdhSfnHNRwPAeYY77Ii2Cwp02-bvxUA1S9lV_knT6EyCOW2mSBl_HuuDD2cEgdiKmyZTVt-RvDxhPKYD-rHkJz-dHO4Folg8TVXotilb1uw
	Vary: X-Auth-Token
	x-openstack-request-id: req-01e096c8-5393-4f98-8ff6-029c55e42524
	Content-Length: 12051
	Content-Type: application/json

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
	        "endpoints": [
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


{{site.data.keyword.objectstorageshort}} URL はサービス・カタログ内にあります。サービス・カタログは、トークン要求の応答本体に含まれています。応答は、使用可能な OpenStack サービスの完全なカタログです。サービス・カタログから、タイプ ```object-store```、および資格情報内の地域フィールドに一致する地域のエンドポイントを選択します。

**注:** パブリック・インターフェース (`publicURL`) を使用してください。{{site.data.keyword.Bluemix_notm}} から内部インターフェース (`internalURL`) にはアクセスできません。


## {{site.data.keyword.objectstorageshort}} のアンバインドおよびプロビジョン解除 {: #deprovisioning-object-storage}

### {{site.data.keyword.objectstorageshort}} サービスのプロビジョン解除方法
1.	{{site.data.keyword.Bluemix_notm}} ダッシュボードからサービスを選択します。  
2.	歯車アイコンをクリックして**「サービスの削除」**を選択します。
	
**警告:** IBM {{site.data.keyword.objectstorageshort}} for {{site.data.keyword.Bluemix_notm}} サービス・インスタンスをプロビジョン解除すると、クラウド・プロジェクトと Swift アカウントが削除されます。プロビジョン解除されたインスタンス内のすべてのコンテナーおよびオブジェクトが Swift から削除されます。リストアすることはできません。

### アプリケーションのアンバインドまたはサービス・キーの削除

{{site.data.keyword.objectstorageshort}} インスタンスからアプリケーションをアンバインドするか、サービス・キーを削除すると、資格情報が削除されます。{{site.data.keyword.objectstorageshort}} アカウントは、{{site.data.keyword.objectstorageshort}} インスタンスがプロビジョン解除されるまで削除されません。[再バインドまたは新規サービス・キーの作成](#bind-object-storage-to-application)によって、新しいクラウド資格情報を生成できます。

