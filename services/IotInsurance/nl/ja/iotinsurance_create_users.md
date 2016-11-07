---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# ユーザーとシールド関連付けの作成
{: #gettingstartedtemplate}
最終更新日: 2016 年 9 月 15 日
{: .last-updated}

{{site.data.keyword.iotinsurance_short}} サービスを作成して必要なサポート・サービスとアプリをデプロイした後、許可ユーザーとシールドの関連付けを作成してサービスをテストすることができます。
{:shortdesc}

**前提条件:** 始めに、以下の前提条件が満たされていることを確認します。

- [Node.js](https://nodejs.org/en/) がコンピューターにインストールされている。  
- Node.js に対応するランタイム環境 (Eclipse など)。
- Git ソフトウェアおよび [API サンプルの GitHub ソース・コード・リポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)へのアクセス。あるいは、[ソース・コード・ファイルを含むアーカイブ](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)をダウンロードすることもできます。
- 準備しておいたソース・コード。
ソース・コードを準備するには、以下のステップを実行します。
  1. [GitHub ソース・コードのリポジトリー](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)をコンピューターに複製またはダウンロードします。
  2. コマンド・プロンプトを使用して、複製されたソース・コード・ファイルが含まれるフォルダーに移動し、`npm install` コマンドを実行して、プロジェクトのオープン・ソース前提条件をインストールします。

ダッシュボードとサンプル・モバイル・アプリの機能をテストするために使用できるユーザーを作成します。

1. {{site.data.keyword.iotinsurance_short}} システムでユーザーを作成します。
  1. createUser.js ファイルを編集して、**user** 変数の値を固有のユーザー情報で置き換えます。
  2. ファイルを保存します。
  3. `node createUser.js` を実行します。このプロセスは、完了するまで少し時間がかかります。
  4. ユーザー名をメモします。これは次のステップで必要になります。
2. ユーザーのシールド関連付けを作成します。
  1. createUserShieldAssociation.js ファイルを編集して、前のステップのユーザー名を **username** 変数に追加します。
  2. ファイルを保存します。
  3. `node createUserShieldAssociation.js` を実行します。シールドについて詳しくは、[コンポーネント](iotinsurance_overview.html#components)を参照してください。
3. (オプション) 分析エンジンは自動的に更新されますが、正しいデータが表示されない場合は、`node updateAnalyticsEngine.js` を実行して分析エンジンを更新してください。
4. (オプション) ユーザーに対するハザード・イベントをシミュレートします。
  1. simulateHazard.js ファイルを編集して、前のステップのユーザー名を **usr** 変数に追加します。
  2. ファイルを保存します。
  3. `node simulateHazard.js` を実行します。
5. (オプション) `node createHistoricalData.js` を実行して、シミュレートした履歴データのセットを作成します。


# 関連リンク
{: #rellinks}

## API リファレンス
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API サンプル](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 関連リンク
{: #general}
* [開発者サポート・フォーラム](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow サポート・フォーラム](http://stackoverflow.com/questions/tagged/ibm-bluemix)
