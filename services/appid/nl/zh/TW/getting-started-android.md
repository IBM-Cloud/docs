---

copyright:
  years: 2017
lastupdated: "2017-04-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# 設定 Android SDK
{: #android-sdk}

使用 {{site.data.keyword.appid_short}} 用戶端 SDK 建置 Android 應用程式、起始設定 SDK、鑑別使用者，以及對受保護資源及未受保護資源提出要求。
{:shortdesc}


## 開始之前
{: #before-you-begin}

您需要下列資訊：
  * {{site.data.keyword.appid_short_notm}} 服務的實例。
  * 您的承租戶 ID。
    * 在服務儀表板的**服務認證**標籤中，按一下**檢視認證**。您的承租戶 ID 會顯示在 **tenantID** 欄位中。此值用於起始設定應用程式。
  * 您的 {{site.data.keyword.Bluemix}} 地區。您可以在使用者介面中尋找，以找到您的地區。此值用於起始設定應用程式。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 地區及對應的 SDK 值</caption>
    <tr>
      <th> Bluemix 地區</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美國南部</td>
      <td> AppID.REGION_US_SOUTH </td>
    </tr>
    <tr>
      <td> 雪梨</td>
      <td> AppID.REGION_SYDNEY </td>
    </tr>
    <tr>
      <td> 英國</td>
      <td> AppID.REGION_UK </td>
    </tr>
  </table>

  * 設定成使用 Gradle 的 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Android Studio 專案 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。

## 安裝用戶端 SDK
{: #install-appid-sdk}

1. 建立 Android Studio 專案，或開啟現有專案。
2.  將 JitPack 儲存庫新增至根 `build.gradle` 檔案。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. 開啟應用程式的 `build.gradle` 檔案。

    **附註**：請務必開啟您應用程式的檔案，而非專案 `build.gradle` 檔案。
4. 尋找檔案的 dependencies 區段，並新增 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 的編譯相依關係：

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. 尋找 defaultConfig 區段，並新增下列這幾行程式碼：

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. 將專案與 Gradle 同步化。按一下**工具** > **Android** > **將專案與 Gradle 檔案同步化**。

## 起始設定用戶端 SDK
{: #initialize-client-sdk}

將環境定義、承租戶 ID 及地區參數傳遞給起始設定方法，以起始設定用戶端 SDK。放置起始設定碼的一般（但非強制）位置是在 Android 應用程式中主要活動的 onCreate 方法。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. 將 "tenantId" 取代為 {{site.data.keyword.appid_short_notm}} 服務承租戶 ID。
2. 將 AppID.REGION_UK 取代為 {{site.data.keyword.Bluemix_notm}} 地區。


## 使用登入小組件鑑別使用者
{: #authenticate-login-widget}

登入小組件預設配置需要使用 Facebook 及 Google 兩者進行鑑別。如果您只配置其中一個，不會啟動登入小組件，並且會將使用者重新導向至已配置的 IDP 鑑別畫面。

起始設定 {{site.data.keyword.appid_short_notm}} 用戶端 SDK 之後，即可執行登入小組件來鑑別使用者。

  ```java
  LoginWidget loginWidget = AppID.getInstance().getLoginWidget();
  loginWidget.launch(this, new AuthorizationListener() {
        @Override
        public void onAuthorizationFailure (AuthorizationException exception) {
          //Exception occurred
        }

        @Override
        public void onAuthorizationCanceled () {
          //Authentication canceled by the user
        }

        @Override
        public void onAuthorizationSuccess (AccessToken accessToken, IdentityToken identityToken) {
          //User authenticated
        }
      });
  ```
  {:pre}


## 存取使用者屬性
{: #accessing}

取得存取記號時，即可存取使用者保護的屬性端點。您可以使用下列 API 方法來取得存取權：

  ```java
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

若未明確地傳遞存取記號，{{site.data.keyword.appid_short_notm}} 會使用最後一個收到的記號。

例如，您可以呼叫此程式碼來設定新屬性，或置換現有屬性：

  ```java
  appId.getUserAttributeManager().setAttribute(name, value, useThisToken,new UserAttributeResponseListener() {
		@Override
		public void onSuccess(JSONObject attributes) {
			//attributes received in JSON format on successful response
		}

		@Override
		public void onFailure(UserAttributesException e) {
			//Exception occurred
		}
	});
  ```
  {:pre}

### 匿名登入
{: #anonymous notoc}

使用 {{site.data.keyword.appid_short_notm}}，您可以[匿名](/docs/services/appid/user-profile.html#anonymous)登入。

  ```java
  appId.loginAnonymously(getApplicationContext(), new AuthorizationListener() {
		@Override
		public void onAuthorizationFailure(AuthorizationException exception) {
			//Exception occurred
		}

		@Override
		public void onAuthorizationCanceled() {
			//Authentication canceled by the user
		}

		@Override
		public void onAuthorizationSuccess(AccessToken accessToken, IdentityToken identityToken) {
			//User authenticated
		}
	});
  ```
  {:pre}

### 漸進鑑別
{: #progressive notoc}

若使用者保有匿名存取記號，將它傳遞給 `loginWidget.launch` 方法，即可識別。

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

匿名登入之後，即使因服務已使用最後一個收到的記號而在未傳遞存取記號的情況下呼叫登入小組件，還是會進行漸進鑑別。如果您要清除儲存的記號，請執行下列指令：

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## 後續步驟
{: #next-steps}

{{site.data.keyword.appid_short_notm}} 會在您一開始設定身分提供者時提供預設配置。您只能在開發模式中使用預設配置。發佈應用程式之前，請將預設 [Facebook](/docs/services/appid/identity-providers.html#facebook) 及 [Google](/docs/services/appid/identity-providers.html#google) 配置更新為您自己的認證。
