---

copyright:
  year: 2016

---

# Web アプリケーション用の Facebook 認証の使用可能化

最終更新日: 2016 年 7 月 27 日
{: .last-updated}

Facebook を使用して、Web アプリのユーザーを認証します。{{site.data.keyword.amashort}} セキュリティー機能を追加します。 

## 開始する前に
{: #facebook-auth-android-before}
以下が必要です。

* Web アプリ。 
* {{site.data.keyword.amashort}} サービスによって保護された {{site.data.keyword.Bluemix_notm}} アプリケーションのインスタンス。{{site.data.keyword.Bluemix_notm}} バックエンド・アプリケーションの作成方法について詳しくは、[入門](index.html)を参照してください。




* (許可プロセス完了後の) 最終リダイレクトのための URI。


## Web サイト用の Facebook アプリケーションの構成
Web サイトで Facebook を ID プロバイダーとして使用するには、Facebook アプリケーションで Web サイトのプラットフォームを追加して構成する必要があります。

1. [Facebook Developers ポータル](https://developers.facebook.com)にログインします。
2. アプリを開くか、または作成します。
3. **Application ID** および **App Secret** をメモします。{{site.data.keyword.amashort}} ダッシュボードで Facebook 認証用に Web プロジェクトを構成するときに、これらの値が必要になります。
4. **Website** プラットフォームが存在しない場合は、追加します。
5. **Facebook Login** を追加するか、プロダクトのリストから開きます。
6. **「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**ボックスに、許可サーバーのコールバック・エンドポイント URI を入力します。この許可リダイレクト URI は、以降の {{site.data.keyword.amashort}} ダッシュボード構成のステップで見つけることができます。
7. 変更を保存します。




## Facebook 認証用の {{site.data.keyword.amashort}} の構成
Facebook Application ID および App Secret を取得し、Web クライアントに対して機能するよう Facebook アプリケーションを構成した後、{{site.data.keyword.Bluemix_notm}} ダッシュボードで Facebook 認証を使用可能にすることができます。

1. {{site.data.keyword.Bluemix_notm}}ダッシュボードを開きます。
2. 関連するアプリのタイルをクリックして、アプリをロードします。
3. {{site.data.keyword.amashort}} サービスのタイルをクリックします。
4. **「Facebook」**パネルの**「構成」**ボタンをクリックします。
5. **「Facebook Developer Console の Mobile Client Access リダイレクト URI (Mobile Client Access Redirect URI for Facebook Developer Console)」**テキスト・ボックス内の値をメモします。この値は、Web サイトの Facebook アプリケーション構成のステップ 6 で Facebook Developers ポータルの**「Facebook Login」**の**「有効な OAuth リダイレクト URI (Valid OAuth redirect URIs)」**ボックスに追加する必要があります。
6. Facebook **Application ID** および **App Secret** を入力します。
7. リダイレクト URI を**「Web アプリケーションのリダイレクト URI (Your Web Application Redirect URIs)」**に入力します。この値は、許可プロセス完了後にアクセスされるリダイレクト URI であり、開発者によって決定されます。
8. **「保存」**をクリックします。




## ID プロバイダーとして Facebook を使用した {{site.data.keyword.amashort}} 許可フローの実装

`VCAP_SERVICES` 環境変数が {{site.data.keyword.amashort}} サービス・インスタンスごとに自動的に作成され、許可プロセスに必要なプロパティーが含まれます。この環境変数は 1 つの JSON オブジェクトから成り、アプリケーションの**「環境変数」**をクリックすることによって表示できます。<!--the left-side navigator of-->

許可プロセスを開始するには、以下のようにします。

1. `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、許可エンドポイント (`authorizationEndpoint`) とクライアント ID (`clientId`) を取り出します。 

    **注:** Web サポートが追加される前に {{site.data.keyword.amashort}} サービスを作成した場合、サービス資格情報に許可エンドポイントが含まれていないことがあります。この場合、Bluemix 地域に基づいて、以下の許可エンドポイントを使用してください。
  
  米国南部: 
  ```
  https://mobileclientaccess.ng.bluemix.net/oauth/v2/authorization 
  ```
  ロンドン:
   ``` 
  https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/authorization 
  ```
  シドニー:
    ```
  https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/authorization 
  ```
2. 照会パラメーターとして `response_type("code")`、`client_id`、および `redirect_uri` を使用して、許可サーバー URI を構築します。 
3. Web アプリから、生成された URI へリダイレクトします。



次の例は、`VCAP_SERVICES` 変数からパラメーターを取り出し、URL を構築し、リダイレクト要求を送信します。

  ```Java
  var cfEnv = require("cfenv"); 

  app.get("/protected", checkAuthentication, function(req, res, next){  
      res.send("Hello from protected endpoint"); 
    }
  ); 
  
  function checkAuthentication(req, res, next){
  // Check if user is authenticated 
  
    if (req.session.userIdentity){   
       next()  
     } else {   
  // If not - redirect to authorization server   
        var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials;   
        var authorizationEndpoint = mcaCredentials.authorizationEndpoint;   
        var clientId = mcaCredentials.clientId;   
        var redirectUri = "http://some-server/oauth/callback"; 
         // Your web application redirect URI   

        var redirectUrl = authorizationEndpoint + "?response_type=code";
        redirectUrl += "&client_id=" + clientId;   
        redirectUrl += "&redirect_uri=" + redirectUri;   
  
        res.redirect(redirectUrl);  
  
      } 
  }
  
 ```

   `redirect_uri` パラメーターは、Facebook での認証が成功または失敗した後のリダイレクト用の URI です。
   

 許可エンドポイントへのリダイレクトの後、ユーザーに Facebook からログイン・フォームが示されます。ユーザーの ID が Facebook によって認可された後、{{site.data.keyword.amashort}} サービスは、照会パラメーターとして認可コードを提供して Web アプリケーション・リダイレクト URI を呼び出します。  

## トークンの取得

次のステップでは、前に受け取った認可コードを使用してアクセス・トークンと識別トークンを取得します。

 1.  `VCAP_SERVICES` 環境変数に保管されたサービス資格情報から、トークンの `tokenEndpoint`、`clientId`、および `secret` を取り出します。 
 
    **注:** Web サポートが追加される前に {{site.data.keyword.amashort}} を使用した場合は、サービス資格情報にトークン・エンドポイントが含まれていないことがあります。代わりに、Bluemix 地域に応じて、以下の URL を使用します。 

    米国南部: 
    ```
     https://mobileclientaccess.ng.bluemix.net/oauth/v2/token   
 ```
    ロンドン:
      ```
     https://mobileclientaccess.eu-gb.bluemix.net/oauth/v2/token
 ```
    シドニー:
      ```
     https://mobileclientaccess.au-syd.bluemix.net/oauth/v2/token 
 ```

 1. 認可タイプ ("authorization_code")、`clientId`、およびリダイレクト URI をフォーム・パラメーターとして使用して、トークン・サーバー URI に POST 要求を送信します。`clientId` および `secret` を基本 HTTP 認証資格情報として送信します。
 
以下のコードは、必要な値を取り出し、それらを POST 要求で送信します。

  ```Java
  var cfEnv = require("cfenv");
  var base64url = require("base64url ");
  var request = require('request');
  
  app.get("/oauth/callback", function(req, res, next){ 
    var mcaCredentials = cfEnv.getAppEnv().services.AdvancedMobileAccess[0].credentials; 
    var tokenEndpoint = mcaCredentials.tokenEndpoint; 
    var formData = { 
      grant_type: "authorization_code", 
      client_id: mcaCredentials.clientId, 
      redirect_uri: "http://some-server/oauth/callback",
     // Your web application redirect uri 
      code: req.query.code 
   } 

 
    request.post({ 
        url: tokenEndpoint, 
    formData: formData 
    }, function (err, response, body){ 
      var parsedBody = JSON.parse(body); 
        req.session.accessToken = parsedBody.access_token; 
        req.session.idToken = parsedBody.id_token; 
        var idTokenComponents = parsedBody.id_token.split("."); // [header, payload, signature] 
      var decodedIdentity= base64url(idTokenComponents[1]);
      req.session.userIdentity = JSON.parse(decodedIdentity)["imf.user"]; 
      res.redirect("/"); 
    }
    ).auth(mcaCredentials.clientId, mcaCredentials.secret); 
  }
); 
   
  ```
 
 `redirect_uri` パラメーターは、前に許可要求に使用された `redirect_uri` と一致している必要があることに注意してください。`code` パラメーター値は、許可要求から応答で受け取った認可コードである必要があります。認可コードが有効なのは 10 分間のみであり、それを過ぎると新しいコードの取得が必要です。

応答本体には、アクセス・コードとトークン ID が JWT フォーマット (https://jwt.io/) で含まれます。

アクセス・トークンを取得し、識別トークンを受け取ったら、Web セッションに認証済みのフラグを立てることができ、オプションでこれらのトークンを永続的に保持できます。  

##取得したアクセス・トークンおよび識別トークンの使用 

識別トークンには、ユーザー ID に関する情報が含まれます。Facebook 認証の場合、このトークンには、ユーザーが共有することに同意したすべての情報 (氏名、年齢グループ、プロファイル写真の URL など) が含まれます。  

アクセス・トークンは、{{site.data.keyword.amashort}} 許可フィルターによって保護されたリソースとの通信を可能にします。[リソースの保護](protecting-resources.html)を参照してください。


保護リソースへの要求を行うには、以下の構造の許可ヘッダーを要求に追加します。 

`Authorization=Bearer <accessToken> <idToken>`

#### ヒント
{: tips} 

* `accessToken` と `idToken` は空白で分離する必要があります。

* `idToken` はオプションです。識別トークンを提供しない場合、保護リソースはアクセス可能ですが、許可ユーザーに関する情報を受け取ることはありません。 
 



