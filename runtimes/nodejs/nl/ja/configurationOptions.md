---

copyright:
  years: 2015, 2017
lastupdated: "2017-03-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 構成オプション
{: #configuration_options}
{: shortdesc}

sdk-for-nodejs ビルドパックを構成するために、さまざまなオプションが使用可能です。

## NPM スクリプト
{: #npm_scripts}
NPM は、スクリプトの実行を可能にするスクリプティング機能を備えています。これには、node_modules のインストール前後に適用される **preinstall** スクリプトおよび **postinstall** スクリプトが含まれます。完全な詳細説明については、[npm-scripts ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](https://docs.npmjs.com/misc/scripts) を参照してください。

## キャッシュの動作
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
