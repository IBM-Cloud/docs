{:new_window: target="_blank"}
{:codeblock: .codeblock}

*最終更新日: 2016 年 1 月 18 日*

# Node.js ビルドパックに対する最新の更新
{: #latest_updates}

Node.js ビルドパック内の最新の更新のリスト。

## 2015 年 12 月 16 日: 更新された Node.js ビルドパック v2.8-20151209-1403 および v3.0beta-20151211-2041

この Node.js ビルドパックのリリースには、v2.8 と v3.0beta という 2 つのバージョンが含まれています。これらバージョンのいずれにも、次の変更が含まれています。

Monitoring and Analytics サービスに対するバグ修正
IBM SDK for Node.js v4.2.3.0、v4.2.2.0、v1.2.0.8、および v1.2.0.7 (それぞれ、コミュニティー Node.js v4.2.3、v4.2.2、v0.12.9、および v0.12.8 に基づく) 用のキャッシュ・ランタイムの組み込み。さらに、v3.0beta ではデフォルトの Node.js ランタイムが v4.2.3 に変更されています。

IBM Node.js ビルドパック v3.0beta は、Node.js v4.2.3 をデフォルト・ランタイムとして Bluemix 上の非デフォルト・ビルドパックとしてリリースされました。ユーザーのアプリとサービスが引き続き Bluemix 上で機能するようにするために、ベータ版のビルドパックを使用してアプリケーションをプッシュしてください。30 日以上後に、v3 はデフォルト・ビルドパックになります。

v3.0beta を使用してアプリケーションをプッシュするには、以下のようにします。

* 以下のように、「cf push」コマンドで「-b」オプションを使用します。
```
 cf push -b sdk-for-nodejs-v3beta
```
{: codeblock}
* あるいは、以下のように、manifest.yml ファイルで「buildpack」オプションを使用します。
```
buildpack: sdk-for-nodejs-v3beta
```
{: codeblock}

アプリケーションの package.json 内に特定の Node.js のバージョンを構成している場合、このデフォルト・ランタイムの変更はユーザーのアプリケーションに影響を与えません。[使用可能なバージョン](index.html#available_versions)の説明にあるように、アプリケーションを実行する Node.js のバージョンは、package.json 内の engines.node 項目を使用していつでも指定できることに注意してください。

## 2015 年 11 月 23 日: 更新された Node.js ビルドパック v2.7-20151118-1003

2.7 では、IBM SDK for Node.js のバージョン 4.2.1.0 (Node v4.2.1 LTS に基づく) を組み込みました。これはまだデフォルトではありませんが、使用するように指定できます。これにより、以前使用可能だったオープン・ソース・ビルドが置き換えられることに注意してください。また、サービス拡張フレームワークの小規模なバグ修正も行いました。

## 2015 年 10 月 19 日: 更新された Node.js ビルドパック v2.6.1-20151015-1326

Node.js v2.6.1 では、[StrongPM アプリケーション管理ハンドラー](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)のバグ修正と、より一貫性のある NPM バージョンが導入されています。

## 2015 年 10 月 15 日: 更新された Node.js ビルドパック v2.6-20151006-1309

Node.js ビルドパックのこのリリースでの特徴はアプリケーション管理フィーチャーへの [StrongLoop Process Manager](https://strong-pm.io) の統合です。
詳しくは、ブログ投稿「[Bluemix 上で稼働する Node.js アプリケーション向けの StrongLoop DevOps (StrongLoop DevOps for Node.js Applications on Bluemix)](https://developer.ibm.com/bluemix/2015/10/15/strongloop-devops-on-bluemix/)」を参照してください。

## 2015 年 6 月 15 日: 更新された Node.js ビルドパック v2.0-20150608-1503

このリリースでは、IBM の Node.js ビルドパックと最新の [CF コミュニティー Node.js ビルドパック](https://github.com/cloudfoundry/nodejs-buildpack) (これにはコミュニティーからの多数の新規フィーチャーが付属しています) との同期が取られました。さらに、Node.js ビルドパックに含まれるアプリケーション管理フィーチャーが改善されました (このフィーチャーにより、shell、node-inspector、Bluemix Live Sync をはじめとするユーティリティーが使用可能になります)。詳しくは、[アプリ管理](../../manageapps/app_mng.html)を参照してください。

## 2015 年 5 月 5 日: 更新された Node.js ビルドパック v1.17-20150429-1033

* Node.js ビルドパックには [IBM SDK for Node.js v0.12.1](https://developer.ibm.com/node/sdk/) が付属するようになりました。
* アプリケーションが package.json ファイル内にランタイムを指定していない場合、アプリケーションは v0.10.x ではなく v0.12.1 を使用して開始するようになりました。前のバージョンを使用する必要がある場合は、以下のように package.json 内で v0.10.x を指定します。```
   "engines": {
"node": "0.10.x"
}
```
{: codeblock}
* v0.12.1 には以下のような既知の問題があります。
   * Bluemix Live Sync によって提供される Debug Tools フィーチャーを使用している場合、「一時停止」フィーチャーが失敗する。
   * MQ Light サービスに使用される mqlight モジュールは v0.12.x ではサポートされない。

* さまざまなセキュリティー脆弱性が解決されました。
  * IBM SDK for Node.js に影響を及ぼす OpenSSL の脆弱性が修正されました。[security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21701494) に詳しい説明があります。
  * IBM SDK for Node.js に影響を及ぼす RC4 Stream Cipher の脆弱性が修正されました。[security bulletin](http://www-01.ibm.com/support/docview.wss?uid=swg21882778) に詳しい説明があります。

##  2015 年 4 月 2 日: 更新された Node.js ビルドパック v1.15-20150331-2231

* Node.js ビルドパックには、再デプロイなしでデスクトップでの開発と同じように Bluemix での迅速な開発を支援する 3 つの新しいフィーチャーが含まれるようになりました。
  * デスクトップ同期: 任意の (Windows) デスクトップ・ツリーをクラウド・ベースのプロジェクト・ワークスペースに同期します。
  * Live Edit: Bluemix で稼働中の Node.js アプリケーションに変更を加え、その変更をブラウザーで直ちにテストできます。
  * デバッグ: シェルで環境に入り、デバッグします。Node Inspector というデバッガーを使用して、コードの動的な編集、ブレークポイントの挿入、コードのステップスルー、ランタイムの再始動などを行うことができます。
  * 詳しくは、[アプリ管理](../../manageapps/app_mng.html#Utilities)を参照してください。
* [Cloud Foundry の Node.js ビルドパック](https://github.com/cloudfoundry/nodejs-buildpack)から最新の変更が引き入れられました。これには、コミュニティーによって行われた多数のバグ修正および機能改善が付属しています。
* Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.13](https://developer.ibm.com/node/sdk/) が付属するようになりました。

## 2015 年 1 月 5 日: 更新された Node.js ビルドパック v1.9.1-20141208-1221

* Node.js ビルドパックには動的ログ設定サポートが含まれるようになりました。これによって、アプリケーションがロギングに log4js、bunyan、または ibmbluemix モジュールを使用している場合に、開発者はアプリケーションのログ・レベルを即時に変更できます。
* Node.js ビルドパックには [IBM SDK for Node.js v0.10.33](https://developer.ibm.com/node/sdk/) が付属するようになりました。これには、POODLE 問題に対するフィックスが含まれています。

## 2014 年 10 月 23 日: 更新済みの Node.js ビルドパック v1.6-20141013-1736

* Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.8](https://developer.ibm.com/node/sdk/) が付属するようになりました。つまり、アプリケーション v0.10.32 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されます。この最新の SDK には、サービス妨害となった組み込み qs モジュールの問題に対する修正が付属しています。 この SDK には、npm モジュールの更新されたバージョン、および http モジュールと url モジュールの他の改善点も含まれます。詳細については、[v0.10.32 の変更ログ](https://raw.githubusercontent.com/joyent/node/v0.10.32/ChangeLog)を参照してください。 
* このビルドパックには、デプロイメント中に顧客のアプリケーションに不正な index.html ファイルを追加したバグに対する修正も含まれています。

## 2014 年 9 月 30 日: 更新済みの Node.js ビルドパック v1.4-20140908-1746

* Node.js ビルドパックには [IBM SDK for Node.js v1.1.0.7](https://developer.ibm.com/node/sdk/) が付属するようになりました。つまり、アプリケーション v0.10.31 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されます。完全にサポートされる Node.js ランタイムを使用すると、顧客は IBM 製品で常に受けていたのと同じ手厚いサポートを受けながら、ビルドすることができます。
* ビルドパックには改善されたサービス・フレームワークが含まれます。具体的には、Monitoring and Analytics サービスをバインドすると動作が良くなり、失敗した場合は追加の診断情報が提供されます。

## 2014 年 8 月 28 日: 更新済みの Node.js ビルドパック v1.3-20140821-1143

* 最新の Node.js ビルドパックには、IBM SDK for Node.js v1.1.0.6 が付属するようになりました。つまり、アプリケーション v0.10.30 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されます。このランタイムは、[V8 のメモリー破損の脆弱性](http://blog.nodejs.org/2014/07/31/v8-memory-corruption-stack-overflow)を修正します。
* ビルドパックには、Monitoring and Analytics サービス拡張に対する改善点とバグ修正も組み込まれており、このサービスを使用してパフォーマンスとエラー状態を診断できます。

## 2014 年 7 月 29 日: 更新済みの Node.js ビルドパック v1.1-20140717-1447

Node.js ビルドパックには、IBM SDK for Node.js v1.1.0.5 が付属するようになりました。つまり、アプリケーション v0.10.29 に最新の安定した Node.js ランタイムを指定すると、完全にサポートされる IBM Node.js ランタイムが提供されます。IBM Node.js SDK の詳細については、[ここ](https://developer.ibm.com/node/sdk/)を参照してください。
