---

copyright:
  years: 2015, 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}


# SDK for Nodejs
{: #nodejs_runtime}
*最終更新日時: 2016 年 3 月 16 日*

{{site.data.keyword.Bluemix}} の Node.js ランタイムには sdk-for-nodejs ビルドパックが採用されています。
sdk-for-nodejs ビルドパックは、Node.js アプリケーションのための完全なランタイム環境を提供します。
{: shortdesc}

sdk-for-nodejs ビルドパックは、アプリケーションのルート・ディレクトリーに **package.json** ファイルが含まれている場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} には、Node.js スターター・アプリケーションが用意されています。Node.js スターター・アプリケーションは、アプリケーションで使用可能なテンプレートを提供する、シンプルな Node.js アプリケーションです。スターター・アプリケーションを試し、Bluemix 環境に対して変更を行い、プッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[『スターター・アプリケーションの使用』](../../cfapps/starter_app_usage.html)を参照してください。

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
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

このコードでは、アプリケーションが Bluemix 上で実行される場合、VCAP_APP_HOST および VCAP_APP_PORT の環境変数には、Bluemix に対して内部であり、アプリケーションが着信接続を listen するホスト値およびポート値が含まれます。アプリケーションがローカルに実行される場合、VCAP_APP_HOST および VCAP_APP_PORT は定義されないため、**localhost** がホストとして、また **3000** がポート番号として使用されます。このような方法でコードを書くと、アプリケーションをテスト目的でローカルに実行でき、またさらに変更を行うことなく Bluemix 上で実行できます。

## アプリケーション管理
{{site.data.keyword.Bluemix}} には、Node.js アプリケーションを管理およびデバッグするために数多くのユーティリティーが用意されています。詳しくは、[『アプリケーション管理』](../../manageapps/app_mng.html)を参照してください。

## 使用可能なバージョン
{: #available_versions}

{{site.data.keyword.Bluemix}} は、[現在使用可能な Node.js ランタイム](http://nodejs.org/dist/)のすべてを提供します。これらのうち、IBM では機能拡張およびバグ修正を含むバージョンを提供しています。詳しくは、[『Node.js ビルドパックに対する最新の更新』](../../runtimes/nodejs/updates.html)を参照してください。

IBM Node.js ビルドパックは、すべてのバージョンの IBM ランタイムをキャッシュに入れます。そのため、IBM SDK for Node.js ランタイムをアプリケーションで使用している場合は、アプリケーションを Bluemix にプッシュすると、アプリケーションのパフォーマンスが向上します。

実行したい Node.js ランタイムのバージョンを指定するには、**package.json** ファイルの **engines** セクションで **node** パラメーターを使用します。

Node.js にバンドルされたバージョン以外の npm のバージョンを指定する必要がある場合は、**package.json** ファイルの **engines** セクションで **npm** パラメーターを使用します。  

以下の例を参照してください。

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4",
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
{{site.data.keyword.Bluemix}} は、ノード・アプリケーションごとにキャッシュ・ディレクトリーを維持します。これはビルド間でも存続します。キャッシュには解決された依存関係が格納されるため、これらはアプリケーションがデプロイされるたびにダウンロードもインストールもされることはありません。例えば、myapp が **express** に依存しているとします。myapp の初回デプロイ時に、**expess** モジュールがダウンロードされます。myapp のそれ以降のデプロイ時には、**express** のキャッシュされたインスタンスが使用されます。デフォルトの動作では、NPM によってインストールされた node_modules と、bower によってインストールされた bower_components がすべてキャッシュされます。

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

Nodejs ビルドパック v3.2-20160315-1257 以降では [FIPS](https://en.wikipedia.org/wiki/Federal_Information_Processing_Standards) がサポートされます。FIPS を有効にするには、環境変数 FIPS_MODE を true に設定します。
例えば、以下のように指定します。

```
    $ cf set-env myapp FIPS_MODE true
```
{: codeblock}

FIPS_MODE が true の場合、**[MD5](https://en.wikipedia.org/wiki/MD5) を使用するノード・モジュールが失敗する**ことを理解することが重要です。例えば、[Express](http://expressjs.com/) モジュールは失敗します。Expess アプリケーションで  [etag](http://expressjs.com/en/api.html) を false に設定すると、こうした失敗への対処に役立つ可能性があります。例えば、コードで以下のようにすることができます。
```
    app.set('etag', false);
```
{: codeblock}
詳しくは、[stackoverflow の投稿](http://stackoverflow.com/questions/15191511/disable-etag-header-in-express-node-js)を参照してください。

アプリケーションで FIPS_MODE が true であるかどうか確認するには、**process.versions.openssl** の値を確認します。例えば、次のように指定します。
```
    console.log('ssl version is [' +process.versions.openssl +']');
```
{: codeblockd}

SSl バージョンに「fips」が含まれている場合、このアプリケーションは FIPS モードで実行されています。    


## Node.js buildpacks

Bluemix は、複数バージョンの Node.js ビルドパックを提供します。
* IBM 作成の **sdk-for-nodejs** ビルドパックは、Bluemix 内の Node.js アプリケーションで使用されるデフォルト・ビルドパックです。
* **nodejs_buildpack** は、Cloud Foundry コミュニティーによって提供される外部ビルドパックです。

**sdk-for-nodejs** ビルドパックは、Bluemix 内の **nodejs_buildpack** に優先します。**sdk-for-nodejs** ビルドパックの代わりに **nodejs_buildpack** をアプリケーションで使用したい場合は、例えば **cf push** コマンドで -b オプションを使用してビルドパックを指定する必要があります。

一般的には、現行 **sdk-for-nodejs** ビルドパックとバックレベル・バージョンが使用可能です。使用可能なすべてのビルドパックを確認するには、**cf buildpacks** コマンドを使用してください。例えば、以下のように指定します。
<pre>
      cf buildpacks
      Getting buildpacks...

      buildpack                                 position   enabled   locked   filename   

      sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
      nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
      sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
</pre>
{: codeblock}

# 関連リンク
## 一般
* [Node.js ビルドパックに対する最新の更新](../../runtimes/nodejs/updates.html)
* [アプリケーション管理](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
