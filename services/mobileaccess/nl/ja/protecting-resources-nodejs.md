---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-15"

---

{:shortdesc: .shortdesc}
{:codeblock:.codeblock}

{{site.data.keyword.amafull}} サービスは {{site.data.keyword.appid_full}} サービスに置き換えられます。

# {{site.data.keyword.amashort}} を使用した Node.js リソースの保護
{: #protecting-resources-nodejs}


{{site.data.keyword.amashort}} Server SDK を使用して、Node.js アプリ内のリソースを保護することができます。

## 開始する前に
{: #before-you-begin}

* {{site.data.keyword.Bluemix_notm}} での Node.js アプリケーションの開発に精通している必要があります。詳細情報については、[SDK for Node.js を使用したアプリの作成](https://console.{DomainName}/docs/runtimes/nodejs/index.html#nodejs_runtime)を参照してください。
* {{site.data.keyword.amashort}} Server SDK では、Node.js サーバーが `Express` フレームワークを使用して実装されていることが要求されます。`Express` フレームワークを使用するフレームワークは、LoopBack など、他にあります。{{site.data.keyword.amashort}} Server SDK は、それらのどのフレームワークでも使用できます。Express フレームワークについて詳しくは、[Expressjs.com ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://expressjs.com/){: new_window}を参照してください。

## Server SDK について
{: #about}

{{site.data.keyword.amashort}} Server SDK では、IBM {{site.data.keyword.Bluemix_notm}} にデプロイされるバックエンド・アプリケーションで使用される `MCABackendStrategy` Passport Strategy が提供されています。ご使用のアプリを無許可アクセスから保護し、モニタリング情報を取得するには、Node.js サーバーに `MCABackendStrategy` を装備する必要があります。`bms-mca-token-validation-strategy` npm モジュールは、`MCABackendStrategy` Passport Strategy と、{{site.data.keyword.amashort}} によって発行されたアクセス・トークンと ID トークンを検証するための検証メソッドを提供しています。このモジュールはまた、セキュリティー・イベントに関するモニタリング情報も自動的に提供します。

{{site.data.keyword.amashort}} Server SDK は `Passport` フレームワークを使用して許可を実施します。詳しくは、[Passportjs.org ![外部リンク・アイコン](../../icons/launch-glyph.svg "外部リンク・アイコン")](http://passportjs.org/){: new_window}を参照してください。

## Server SDK のインストール
{: #protecting-resources-serversdk}

コマンド・ラインで Node.js アプリケーションのディレクトリーを開き、以下のコマンドを実行します。

```
npm install -save express
npm install -save passport
npm install -save bms-mca-token-validation-strategy
```
{: codeblock}

## Node.js のリソースの保護
{: #protecting-resources-nodesdk}

以下のスニペットは、`MCABackendStrategy` を単純な Express アプリケーションで使用して、`/protected` エンドポイントの GET メソッドを保護する方法を示しています。

```JavaScript
var express = require('express');
var passport = require('passport');
var MCABackendStrategy = require('bms-mca-token-validation-strategy').MCABackendStrategy;

passport.use(new MCABackendStrategy());

var app = express();
app.use(passport.initialize());

app.get('/protected', passport.authenticate('mca-backend-strategy', {session: false }),
    function(request, response){
		console.log("Securty context", request.securityContext)    
		response.send(200, "Success!");
    }
);

app.listen(process.env.PORT);
```
{: codeblock}
