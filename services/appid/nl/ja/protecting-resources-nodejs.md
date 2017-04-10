---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Node.js リソースの保護
{: #protecting-resources-nodejs}

{{site.data.keyword.appid_short}} Server SDK を使用して、Node.js アプリ内のリソースを保護することができます。{:shortdesc}

## 開始する前に
{: #before-you-begin}

* {{site.data.keyword.Bluemix_notm}} での Node.js アプリケーションの開発に精通している必要があります。
* {{site.data.keyword.appid_short_notm}} Server SDK には、Node.js サーバーが <a href="http://expressjs.com/" target="_blank">Express フレームワーク<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>を使用して実装されていることが必要です。

**注**: `Express` フレームワークを使用するフレームワークは他にもあります (LoopBack など)。{{site.data.keyword.appid_short_notm}} Server SDK は、それらのどのフレームワークでも使用できます。

## Server SDK について
{: #about}

{{site.data.keyword.appid_short_notm}} Server SDK には、{{site.data.keyword.Bluemix_notm}} にデプロイされたバックエンド・アプリケーションで使用する ApiStrategy パスポート戦略が用意されています。ご使用のアプリを無許可アクセスから保護するには、Node.js サーバーに ApiStrategy を装備する必要があります。`appid-serversdk-nodejs npm モジュール`には、ApiStrategy パスポート戦略の他に、{{site.data.keyword.appid_short_notm}} から発行されたアクセス・トークンと ID トークンを検証するための検証メソッドも用意されています。

{{site.data.keyword.appid_short_notm}} Server SDK は Passport フレームワークを使用して許可を実施します。<a href="http://passportjs.org/" target="_blank">Passport フレームワーク<img src="../../icons/launch-glyph.svg" alt="External link icon"></a>を参照してください。


## Server SDK のインストール
{: #protecting-resources-serversdk}

1. コマンド・ラインを使用して、Node.js アプリのディレクトリーを開いてください。
2. 以下のコマンドを実行します。

  ```
  npm install -save express
  npm install -save passport
  npm install -save bluemix-appid
  ```
  {:pre}

## Node.js のリソースの保護
{: #protecting-resources-nodesdk}

以下のスニペットは、`APIStrategy` を単純な Express アプリケーションで使用して、`/protected` エンドポイント GET メソッドを保護する方法を示しています。

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var APIStrategy = require('bluemix-appid').APIStrategy;

  passport.use(new APIStrategy());
  var app = express();
  app.use(passport.initialize());

  app.get('/protected', passport.authenticate('APIStrategy.STRATEGY_NAME', {session: false }),
      function(request, response){
          console.log("Securty context", request.securityContext)    
          response.send(200, "Success!");
      }
  );

  app.listen(process.env.PORT);
```
  {:pre}

`WebAppStrategy` を使用して Web アプリケーション・リソースを保護できます。

  ```JavaScript

  var express = require('express');
  var passport = require('passport');
  var WebAppStrategy = require('bluemix-appid').WebAppStrategy;
  ```
  {:pre}

詳細については、<a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">{{site.data.keyword.appid_short_notm}}Node.js GitHub リポジトリー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。
