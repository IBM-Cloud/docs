---

copyright:
  years: 2017
lastupdated: "2017-03-16"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# Android SDK のセットアップ
{: #android-sdk}

{{site.data.keyword.appid_short}} Client SDK を使用して Android アプリを構築し、SDK を初期化し、ユーザーを認証し、保護リソースや無保護リソースへの要求を実行します。
{:shortdesc}


## 開始する前に
{: #before-you-begin}

以下の情報が必要です。
  * {{site.data.keyword.appid_short_notm}} サービスのインスタンス。
  * テナント ID。
    * サービスのダッシュボードの**「サービス資格情報」**タブの**「資格情報の表示」**をクリックします。**「テナント ID (tenant ID)」**フィールドに、テナント ID が表示されます。その値をアプリの初期化に使用します。
  * {{site.data.keyword.Bluemix}} 地域。地域は UI に表示されています。その値をアプリの初期化に使用します。<table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地域と対応する SDK 値</caption>
    <tr>
      <th> Bluemix 地域</th>
      <th> SDK 値</th>
    </tr>
    <tr>
      <td> 米国南部</td>
      <td> AppID.REGION_US_SOUTH</td>
    </tr>
    <tr>
      <td> シドニー</td>
      <td> AppID.REGION_SYDNEY</td>
    </tr>
    <tr>
      <td> 英国</td>
      <td> AppID.REGION_UK</td>
    </tr>
  </table>

  * Gradle と連動して機能するようにセットアップされた Android Studio プロジェクト。
    * Android 開発環境のセットアップ方法について詳しくは、<a href="https://developers.google.com/web/tools/setup/" target="_blank">Google 開発者ツールの資料<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>を参照してください。

## Client SDK のインストール
{: #install-appid-sdk}

1. Android Studio プロジェクトを作成するか、既存のプロジェクトを開きます。
2.  JitPack リポジトリーをルートの `build.gradle` ファイルに追加します。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. アプリケーションの `build.gradle` ファイルを開きます。

    **注**: プロジェクトの `build.gradle` ファイルではなくアプリのファイルを開いてください。
4. ファイルの従属関係セクションを見つけ、{{site.data.keyword.appid_short_notm}} Client SDK 用のコンパイル従属関係を追加します。

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. defaultConfig セクションを見つけ、以下のコード行を追加します。

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. プロジェクトを Gradle と同期化します。**「ツール」** > **「Android」** > **「プロジェクトを Gradle ファイルと同期 (Sync Project with Gradle Files)」**をクリックします。

## Client SDK の初期化
{: #initialize-client-sdk}

context、tenant ID、region パラメーターを initialize メソッドに渡して、Client SDK を初期化します。初期化コードの配置場所として一般的な (必須ではありません) 場所は、Android アプリケーションのメイン・アクティビティーの onCreate メソッド内です。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. 「tenantId」を {{site.data.keyword.appid_short_notm}} サービスの tenantId に置き換えます。
2. AppID.REGION_UK を、該当する {{site.data.keyword.Bluemix_notm}} 地域に置き換えます。


## ログイン・ウィジェットを使用したユーザーの認証
{: #authenticate-login-widget}

ログイン・ウィジェットのデフォルト構成では、Facebook と Google の両方を認証に使用する必要があります。一方だけを構成した場合、ログイン・ウィジェットは起動せず、ユーザーは構成済みの IDP 認証画面にリダイレクトされます。

{{site.data.keyword.appid_short_notm}} Client SDK が初期化されたら、ログイン・ウィジェットを実行してユーザーを認証できるようになります。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //例外の発生
        }

        @Override
        public void onAuthorizationCanceled () {
          //ユーザーによる認証の取り消し
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //ユーザーの認証
        }
      });
  ```
  {:pre}


## ユーザー属性へのアクセス
{: #accessing}

アクセス・トークンを取得すれば、ユーザーの保護された属性のエンドポイントにアクセスできます。以下の API メソッドを使用してアクセスできます。

  ```   
  void setAttribute(@NonNull String name, @NonNull String value, UserAttributeResponseListener listener);
  void setAttribute(@NonNull String name, @NonNull String value, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void getAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void deleteAttribute(@NonNull String name, UserAttributeResponseListener listener);
  void deleteAttribute(@NonNull String name, @NonNull AccessToken accessToken, UserAttributeResponseListener listener);

  void getAllAttributes(@NonNull UserAttributeResponseListener listener);
  void getAllAttributes(@NonNull AccessToken accessToken, @NonNull UserAttributeResponseListener listener);
  ```
  {:pre}

アクセス・トークンを明示的に渡さないと、{{site.data.keyword.appid_short_notm}} は最後に受け取ったトークンを使用します。

例えば、以下のコードを呼び出して、新しい属性を設定したり既存の属性をオーバーライドしたりできます。

  ```
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//正常な応答から受け取った JSON 形式の属性
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//例外の発生
		}
	});
  ```
  {:pre}

### 匿名ログイン
{: #anonymous notoc}

{{site.data.keyword.appid_short_notm}} では匿名によるログインが可能です。[匿名 ID](/docs/services/appid/user-profile.html#anonymous) を参照してください。

  ```
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//例外の発生
		}

		@Override
		public void onAuthorizationCanceled() {
			//ユーザーによる認証の取り消し
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//ユーザーの認証
		}
	});
  ```
  {:pre}

### 段階的な認証
{: #progressive notoc}

匿名のアクセス・トークンを保持しているユーザーを、トークンを `loginWidget.launch` メソッドに渡して識別することができます。

  ```
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

匿名ログインの後には、アクセス・トークンを渡さずにログイン・ウィジェットを呼び出した場合であっても段階的な認証が行われます。最後に受け取ったトークンがサービスで使用されるからです。保管されているトークンをクリアする場合は、以下のコマンドを実行します。

  ```
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## 次のステップ
{: #next-steps}

初めて ID プロバイダーをセットアップするときに、{{site.data.keyword.appid_short_notm}} からデフォルト構成が示されます。このデフォルト構成は開発モードのみで使用できます。アプリケーションを公開する前に、デフォルトの [Facebook](/docs/services/appid/identity-providers.html#facebook) と [Google](/docs/services/appid/identity-providers.html#google) の構成を自分の資格情報に更新してください。
