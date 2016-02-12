{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 12 日*

# Node.js ランタイム
{: #nodejs_runtime}

{{site.data.keyword.Bluemix}} の Node.js ランタイムでは sdk-for-nodejs ビルドパックが採用されています。
sdk-for-nodejs ビルドパックは、Node.js アプリのための完全なランタイム環境を提供します。
{: shortdesc}

Node.js ビルドパックは、アプリケーションのルート・ディレクトリーに **package.json** ファイルがある場合に使用されます。

## スターター・アプリケーション
{: #starter_application}

{{site.data.keyword.Bluemix}} は Node.js スターター・アプリケーションを提供します。Node.js スターター・アプリケーションは、ご使用のアプリに使用できるテンプレートを提供するシンプルな Node.js アプリです。このスターター・アプリを試し、Bluemix 環境に変更を加えてプッシュすることができます。スターター・アプリケーションの使用に関するヘルプについては、[「スターター・アプリケーションの使用 (Using the starter applications)」](../../cfapps/starter_app_usage.html)を参照してください。

## 始動コマンド
{: #starup_commmand}

Bluemix Node.js アプリケーションの始動コマンドを指定する方法として推奨されるのは、**Procfile** または **package.json** ファイルのいずれかを使用することです。

**Procfile** 内に以下の形式で始動コマンドを指定します。ここで、app.js は、アプリケーションの始動 js スクリプトです。```
web: node app.js```
{: codeblock}

**Procfile** はアプリケーションのルート・ディレクトリーに保存してください。

**Procfile** が存在しない場合、IBM Bluemix Node.js ビルドパックによって、**package.json** ファイルに scripts.start エントリーがあるかどうかが検査されます。下の例でも、app.js はアプリケーションの始動 js スクリプトです。```
{
  ...   
"scripts": {

    "start": "node app.js"
}
}
```
{: codeblock}

始動スクリプトのエントリーが **package.json** 内に存在する場合、**Procfile** が自動的に生成されます。以下に、自動生成された **Procfile** の内容を示します。
```
web: npm start```
{: codeblock}

**Procfile** および **package.json** ファイルについて詳しくは、[Tips for Node.js Applications ](https://docs.cloudfoundry.org/buildpacks/node/node-tips.html)を参照してください。

## Node.js アプリケーションのローカル側での実行に関するヒント
{: #hints}

この情報を使用することで、Node.js アプリケーションのローカル側および Bluemix 上での実行が容易になります。

次の例は、**js** ファイルのソースの部分を示しています。
```
var port = (process.env.VCAP_APP_PORT || 3000);
var host = (process.env.VCAP_APP_HOST || 'localhost');
```
{: codeblock}

このコードでは、アプリケーションを Bluemix で実行すると、VCAP_APP_HOST 環境変数と VCAP_APP_PORT 環境変数には、アプリが着信接続を listen する対象の、Bluemix 内部のホスト値とポート値が含まれます。アプリケーションをローカル側で実行すると、VCAP_APP_HOST および VCAP_APP_PORT は定義されていないため、**localhost** がホストとして使用され、**3000** がポート番号として使用されます。この方法で作成した場合、アプリケーションをテストのためにローカル側で実行したり、他の変更を行うことなく Bluemix 上で実行したりすることができます。

## アプリ管理

{{site.data.keyword.Bluemix}} は、Node.js アプリの管理およびデバッグ用のユーティリティーをいくつか提供しています。詳しくは、[アプリ管理](../../manageapps/app_mng.html)を参照してください。

## 使用可能なバージョン
{: #available_versions}

{{site.data.keyword.Bluemix}} は、[現在使用可能な Node.js ランタイム](http://nodejs.org/dist/)のすべてを提供します。IBM は、そのうちの、機能拡張およびバグ修正を含んだバージョンを提供します。詳しくは、[Node.js ビルドパックに対する最新の更新](updates.html)を参照してください。

IBM Node.js ビルドパックは、すべての IBM ランタイム・バージョンをキャッシュに入れます。そのため、IBM SDK for Node.js ランタイムをアプリケーションで使用する場合、アプリケーションを Bluemix にプッシュすると、アプリケーションのパフォーマンスが高速になります。

実行する Node.js ランタイムのバージョンを指定するには、**package.json** ファイル内の **engines** セクションの **node** パラメーターを使用します。

Node.js とバンドルされたバージョン以外の npm のバージョンを指定する必要がある場合は、**package.json** ファイル内の **engines** セクションの **npm** パラメーターを使用します。  

以下の例を参照してください。

```
{
  "name": "myapp",
  "description": "this is my app",
  "version": "0.1",
  "engines": {
     "node": "4.2.4"
     "npm": "2.11.3"
  }
}
```
{: codeblock}

ノード・バージョンは、常に **package.json** ファイルで指定する必要があります。指定しない場合は、最新のノード・バージョンが使用されます。

## 設定オプション
{: #configuration_options}

### NPM スクリプト
{: #npm_scripts}
NPM は、スクリプトの実行を可能にするスクリプティング機能を提供します。このスクリプトには、node_modules のインストールの前後に適用された **preinstall** および **postinstall** スクリプトも含まれます。詳しくは、[npm-scripts](https://docs.npmjs.com/misc/scripts) を参照してください。

### キャッシュ動作
{: #cache_behavior}
{{site.data.keyword.Bluemix}} はノード・アプリケーションごとにキャッシュ・ディレクトリーを保持し、これはビルド間で持続されます。キャッシュは解決済みの依存関係を保管するため、アプリをデプロイするたびに依存関係をダウンロードおよびインストールすることはありません。例えば、myapp が **express** に依存するとします。この場合、myapp が最初にデプロイされる際に **expess** モジュールがダウンロードされます。その後の myapp のデプロイメントでは、**express** のキャッシュされたインスタンスが使用されます。

NODE_MODULES_CACHE 変数は、ノード・ビルドパックが前のビルドのキャッシュを使用するか無視するかを決定するのに使用します。デフォルト値は true です。キャッシュを無効にするには、NODE_MODULES_CACHE を false に設定します。例えば cf コマンド・ラインでは次のようにします。
```
cf set-env myapp NODE_MODULES_CACHE false
```
{: codeblock}

アプリケーションに含まれている node_modules はキャッシュされないことにご注意ください。

**cacheDirectories** アレイを最上位の **package.json** で使用すると、どのモジュールをキャッシュするかについて詳細に制御することができます。**cacheDirectories** エレメントが **package.json** 内にある場合は、**cacheDirectories** アレイ内にあるモジュールのみがキャッシュされます。以下の例では、node_modules および bower_components のみがキャッシュされます。
```
{
  "cacheDirectories": ["node_modules","bower_components"],
  ...
}
```
{: codeblock}

## Node.js ビルドパック

Bluemix は複数のバージョンの Node.js ビルドパックを提供します。
* IBM が作成した **sdk-for-nodejs** ビルドパックは、Bluemix で Node.js アプリケーションに使用されるデフォルトのビルドパックです。
* **nodejs_buildpack** は、Cloud Foundry コミュニティーによって提供される外部ビルドパックです。

Bluemix では、**sdk-for-nodejs** ビルドパックが **nodejs_buildpack** に優先します。アプリケーションで **sdk-for-nodejs** ビルドパックではなく **nodejs_buildpack** を使用する場合、**cf push** コマンドで -b オプションを使用するなどしてビルドパックを指定する必要があります。

通常、現行の **sdk-for-nodejs** ビルドパックとバックレベル・バージョンが使用可能です。使用可能なビルドパックをすべて表示するには、**cf buildpacks** コマンドを使用します。例:```
cf buildpacks
Getting buildpacks...

buildpack                      position          enabled          locked          filename	
   
...
sdk_for_nodejs                            2          true      false    buildpack_sdk-for-nodejs_v2.8-20151209-1403.zip   
nodejs_buildpack                          5          true      false    nodejs_buildpack-cached-v1.5.0.zip   
sdk-for-nodejs_v2_7-20151118-1003         17         true      false    buildpack_sdk-for-nodejs_v2.7-20151118-1003.zip
```
{: codeblock}


## 関連リンク
{: #related_links}
* [Node.js ビルドパックに対する最新の更新](updates.html)
* [アプリ管理
](../../manageapps/app_mng.html)
* [Node.js](https://nodejs.org)
* [StrongLoop](https://strongloop.com)
