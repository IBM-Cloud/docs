---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-14"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} の Node.js ランタイムには sdk-for-nodejs ビルドパックが採用されています。
sdk-for-nodejs ビルドパックは、Node.js アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

sdk-for-nodejs ビルドパックは、アプリケーションのルート・ディレクトリーに **package.json** ファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Node.js スターター・アプリケーションが用意されています。Node.js スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Node.js アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](/docs/cfapps/starter_app_usage.html)を参照してください。

## 開始コマンド
{: #starup_commmand}

Bluemix Node.js アプリケーションの開始コマンドを指定するための推奨方法は、**Procfile** ファイルまたは **package.json** ファイルを使用することです。

下記の形式で、**Procfile** に開始コマンドを指定します。app.js は、アプリケーション用の開始 js スクリプトです。

```
web: node app.js
```
{: codeblock}

**Procfile** をアプリケーションのルート・ディレクトリーに保存します。

**Procfile** がない場合、IBM Bluemix Node.js ビルドパックは **package.json** ファイルの scripts.start 項目を検査します。下の例でも、app.js はアプリケーション用の開始 js スクリプトです。

```
{
    ...   
    "scripts": {
      "start": "node app.js"
    }
}
```
{: codeblock}

開始スクリプト項目が **package.json** にある場合は、**Procfile** が自動的に生成されます。自動生成された **Procfile** の内容は次のようになります。

```
web: npm start
```
{: codeblock}

**Procfile** ファイルおよび **package.json** ファイルについて詳しくは、[『Tips for Node.js Applications』](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)を参照してください。

## Node.js アプリケーションをローカルに実行するためのヒント
{: #hints}

この情報は、Node.js アプリケーションをローカルと Bluemix 上の両方で容易に実行するために使用します。

次の例は、**js** ファイルのソースの一部を示しています。

```
var port = (process.env.PORT || 3000);
```
{: codeblock}

このコードでは、アプリケーションが Bluemix 上で実行される場合、PORT 環境変数には、アプリケーションが着信接続を listen する Bluemix 内部のポート値が入ります。アプリケーションがローカルに実行される場合、PORT は定義されないため、ポート番号として **3000** が使用されます。このような方法でコードを書くと、アプリケーションをテスト目的でローカルに実行でき、またさらに変更を行うことなく Bluemix 上で実行できます。

## オフライン モード
{: #offline_mode}

ビルドパックの外部サイトへのアクセスの制御については、[『オフライン・モード』](offlineMode.html)を参照してください。 

## アプリケーション管理
{{site.data.keyword.Bluemix}} には、Node.js アプリケーションを管理およびデバッグするために数多くのユーティリティーが用意されています。詳しくは、[『アプリケーション管理』](/docs/manageapps/app_mng.html)を参照してください。

## 使用可能なバージョン
{: #available_versions}

{{site.data.keyword.Bluemix}} は、[現在使用可能な Node.js ランタイム](http://nodejs.org/dist/)のすべてを提供します。これらのうち、IBM では機能拡張およびバグ修正を含むバージョンを提供しています。詳しくは、[『Node.js ビルドパックに対する最新の更新』](/docs/runtimes/nodejs/updates.html)を参照してください。

IBM Node.js ビルドパックは、IBM ランタイム・バージョンをキャッシュに入れます。そのため、IBM SDK for Node.js ランタイムをアプリケーションで使用している場合は、アプリケーションを Bluemix にプッシュすると、アプリケーションのパフォーマンスが向上します。

実行したい Node.js ランタイムのバージョンを指定するには、**package.json** ファイルの **engines** セクションで **node** パラメーターを使用します。

Node.js にバンドルされたバージョン以外の npm のバージョンを指定する必要がある場合は、**package.json** ファイルの **engines** セクションで **npm** パラメーターを使用します。  

以下の例を参照してください。

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {"node": "4.2.4",
     "npm": "2.11.3"
  }
}
```
{: codeblock}

ノード・バージョンは常に **package.json** ファイルで指定される必要があります。指定されていない場合は、最新のノード・バージョンが使用されます。

## 構成オプション
{: #configuration_options}

### NPM スクリプト
{: #npm_scripts}
NPM は、スクリプトの実行を可能にするスクリプティング機能を備えています。これには、node_modules のインストール前後に適用される **preinstall** スクリプトおよび **postinstall** スクリプトが含まれます。詳しくは、[『npm-scripts』](https://docs.npmjs.com/misc/scripts)を参照してください。

### キャッシュの動作
{: #cache_behavior}
{{site.data.keyword.Bluemix}} は、ノード・アプリケーションごとにキャッシュ・ディレクトリーを維持します。これはビルド間でも存続します。キャッシュには解決された依存関係が格納されるため、これらはアプリケーションがデプロイされるたびにダウンロードもインストールもされることはありません。例えば、myapp が **express** に依存しているとします。その場合、myapp の初回デプロイ時に、**express** モジュールがダウンロードされます。myapp のそれ以降のデプロイ時には、**express** のキャッシュされたインスタンスが使用されます。デフォルトの動作では、NPM によってインストールされた node_modules と、bower によってインストールされた bower_components がすべてキャッシュされます。

Node ビルドパックが以前のビルドからのキャッシュを使用するか無視するかを決定するには、NODE_MODULES_CACHE 変数を使用します。デフォルト値は true です。キャッシングを無効にするには、NODE_MODULES_CACHE を (例えば cf コマンド・ラインで) false に設定します。

```
    $ cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

アプリケーションに組み込まれている node_modules はキャッシュされないことに注意してください。

最上位の **package.json** で **cacheDirectories** 配列を使用して、どのモジュールをキャッシュするかを細かく制御できます。**cacheDirectories** エレメントが **package.json** にある場合は、**cacheDirectories** 配列内のモジュールのみがキャッシュされます。次の例では、node_modules および bower_components のみがキャッシュされます。

```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

### FIPS MODE
{: #fips_mode}

Nodejs ビルドパック v3.2-20160315-1257 以降では [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards) がサポートされます。FIPS 対応ノード・エンジンを使用するには、環境変数 FIPS_MODE を true に設定します。
例えば、以下のように指定します。

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

FIPS_MODE が true の場合、一部のノード・モジュールが機能しない可能性があることを認識しておくことが重要です。例えば、[Express](http://expressjs.com/) のように、**[MD5](https://en.wikipedia.org/wiki/MD5) を使用するノード・モジュールは失敗します**。Express の場合、Expess アプリケーションで [etag](http://expressjs.com/en/api.html) を false に設定すると、こうした失敗を回避するのに役立つことがあります。例えば、コードで以下のようにすることができます。

```
    app.set('etag', false);
```
{: codeblock}
詳しくは、[stackoverflow の投稿](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)を参照してください。**注:** [アプリケーション管理](/docs/manageapps/app_mng.html)と FIPS_MODE は、同時にはサポートされ*ません*。BLUEMIX_APP_MGMT_ENABLE 環境変数が設定され、かつ FIPS_MODE 環境変数が true に設定されると、アプリケーションはステージングに失敗します。

FIPS_MODE の状態を確認するには、以下のようにさまざまな方法があります。
<ul>
<li> アプリケーションの staging_task.log で、以下に似たメッセージを確認できます。    

  <pre>
  Installing FIPS-enabled IBM SDK for Node.js (4.4.3) from cache
  </pre>
  {: codeblock}

このメッセージは、FIPS 対応の node.js エンジンが実行中であるが、必ずしもその FIPS が実行されているとは限らないことを示します。
</li>

<li> **process.versions.openssl** の値を確認できます。例えば、次のように指定します。
<pre>
  console.log('ssl version is [' +process.versions.openssl +']');
  </pre>
  {: codeblock}

SSL バージョンに「fips」が含まれている場合、使用されているバージョンの SSL は FIPS をサポートしています。  
</li>

<li> node.js バージョン 6 以降の場合、以下のようなコードで crypto.fips によって返された値を確認できます。<pre>
  console.log('crypto.fips== [' +crypto.fips +']');
  </pre>
  {: codeblock}

戻り値が 1 の場合は、FIPS が使用されています。なお、node.js バージョン 6 より前では、crypto.fips は *undefined* を返します。
</li>
</ul>

#### Nodejs v4
{: #nodejs_v4_fips}

次の表は、FIPS を使用する node.js v4 の動作を説明しています。

|                 | 結果        |
| :-------------- | :------------ |
|FIPS_MODE=true   |成功 (1)    |
|FIPS_MODE !=true |成功 (2)    |

* 成功 (1)
  * FIPS は使用中です。
  * staging_task.log にメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
* 成功 (2)
  * FIPS は使用されて*いません*。
  * staging_task.log に、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * process.versions.openssl によって返される値に「fips」は含まれ*ません*。

#### Nodejs v6
{: #nodejs_v6_fips}

Node.js バージョン 6 を使用して FIPS モードで実行するには、**FIPS_MODE=true** の設定に加えて、次の例のように、開始コマンドに **--enable-fips** を含めることも必要です。
```
{
    ...   
    "scripts": {
      "start": "node --enable-fips app.js"
    }
}
```
{: codeblock}

次の表は、FIPS を使用する node.js v6 の動作を説明しています。

|                 |--enable-fips  |--enable-fips なし |
| :-------------- | :------------ | :-------------- |
|FIPS_MODE=true   |成功 (1)    |成功 (2)      |
|FIPS_MODE !=true |失敗 (3)    |成功 (4)      |

* 成功 (1)
  * FIPS は使用中です。
  * staging_task.log にメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
  * crypto.fips は 1 を返し、FIPS が使用中であることを示します。
* 成功 (2)
  * FIPS は使用されて*いません*。
  * staging_task.log にメッセージ *Installing FIPS-enabled IBM SDK for Node.js* が含まれます。
  * process.versions.openssl によって返される値に「fips」が含まれます。
  * crypto.fips は 0 を返し、FIPS が使用されて*いない*ことを示します。
* 失敗 (3)
  * FIPS は使用されて*いません*。
  * staging_task.log に、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * ステージングは失敗し、メッセージ「ERR node: bad option: --enable-fips」が出されます。
* 成功 (4)
  * FIPS は使用されて*いません*。
  * staging_task.log に、メッセージ *Installing FIPS-enabled IBM SDK for Node.js* は含まれ*ません*。
  * process.versions.openssl によって返される値に「fips」は含まれ*ません*。
  * crypto.fips は 0 を返し、FIPS が使用されて*いない*ことを示します。


## Node.js buildpacks

Bluemix は、複数バージョンの Node.js ビルドパックを提供します。
* IBM 作成の **sdk-for-nodejs** ビルドパックは、Bluemix 内の Node.js アプリケーションで使用されるデフォルト・ビルドパックです。
* **nodejs_buildpack** は、Cloud Foundry コミュニティーによって提供されるコミュニティー・ビルドパックです。

**sdk-for-nodejs** ビルドパックは、Bluemix 内の **nodejs_buildpack** に優先します。**sdk-for-nodejs** ビルドパックの代わりに **nodejs_buildpack** をアプリケーションで使用したい場合は、例えば **cf push** コマンドで -b オプションを使用してビルドパックを指定する必要があります。

一般的には、現行 **sdk-for-nodejs** ビルドパックとバックレベル・バージョンが使用可能です。使用可能なすべてのビルドパックを確認するには、**cf buildpacks** コマンドを使用してください。例えば、以下のように指定します。
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip</pre>
{: codeblock}

# 関連リンク
{: #rellinks}
## 一般
{: #general}
* [Node.js ビルドパックに対する最新の更新](/docs/runtimes/nodejs/updates.html)
* [アプリケーション管理](/docs/manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [IBM API Connect](https://strongloop.com/)
