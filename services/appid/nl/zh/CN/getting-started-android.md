---

copyright:
  years: 2017
lastupdated: "2017-03-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:pre: .pre}

# 设置 Android SDK
{: #android-sdk}

使用 {{site.data.keyword.appid_short}} 客户端 SDK 构建 Android 应用程序，初始化该 SDK，认证用户，然后对受保护和不受保护的资源发起请求。
{:shortdesc}


## 开始之前
{: #before-you-begin}

您需要以下信息：
  * {{site.data.keyword.appid_short_notm}} 服务的实例。
  * 您的租户标识。
    * 在服务仪表板的**服务凭证**选项卡中，单击**查看凭证**。您的租户标识会显示在**租户标识**字段中。此值用于初始化应用程序。
  * 您所在的 {{site.data.keyword.Bluemix}} 区域。您可以通过查看 UI 来找到您所在的区域。此值用于初始化应用程序。
    <table> <caption> 表 1. {{site.data.keyword.Bluemix_notm}} 区域及对应的 SDK 值</caption>
    <tr>
      <th> Bluemix 区域</th>
      <th> SDK 值</th>
    </tr>
    <tr>
      <td> 美国南部</td>
      <td> AppID.REGION_US_SOUTH</td>
    </tr>
    <tr>
      <td> 悉尼</td>
      <td> AppID.REGION_SYDNEY</td>
    </tr>
    <tr>
      <td> 英国</td>
      <td> AppID.REGION_UK</td>
    </tr>
  </table>

  * Android Studio 项目，设置为使用 Gradle。
    * 有关如何设置 Android 开发环境的更多信息，请参阅 <a href="https://developers.google.com/web/tools/setup/" target="_blank">Google Developer Tools 文档 <img src="../../icons/launch-glyph.svg" alt="外部链接图标"></a>。

## 安装客户端 SDK
{: #install-appid-sdk}

1. 创建 Android Studio 项目或打开现有项目。
2.  将 JitPack 存储库添加到根 `build.gradle` 文件。

  ```gradle
    allprojects {
	    repositories {
		    ...
		    maven { url 'https://jitpack.io' }
	    }
    }
  ```
  {:pre}

3. 打开应用程序的 `build.gradle` 文件。

    **注：**请确保打开应用程序的这一文件，而不是项目的 `build.gradle` 文件。
4. 找到该文件的 dependencies 部分，并为 {{site.data.keyword.appid_short_notm}} 客户端 SDK 添加新的编译依赖项：

  ```gradle
   dependencies {
       compile group: 'com.github.ibm-cloud-security:appid-clientsdk-android:1.+'
   }
  ```
  {:pre}

5. 找到 defaultConfig 部分，并添加以下代码行：

  ```gradle
  defaultConfig {
  ...
  manifestPlaceholders = ['appIdRedirectScheme': android.defaultConfig.applicationId]
  }
  ```
  {:pre}

6. 使用 Gradle 同步项目。单击**工具 ** > **Android ** > **使用 Gradle 文件同步项目**。

## 初始化客户端 SDK
{: #initialize-client-sdk}

通过将上下文、租户标识和区域参数传递到 initialize 方法来初始化客户端 SDK。在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中，但这不是强制性的。

  ```java
  AppID.getInstance().initialize(getApplicationContext(), <tenantId>, AppID.REGION_UK);
  ```
  {:pre}

1. 将“tenantId”替换为 {{site.data.keyword.appid_short_notm}} 服务 tenantId。
2. 将 AppID.REGION_UK 替换为您所在的 {{site.data.keyword.Bluemix_notm}} 区域。


## 使用登录窗口小部件认证用户
{: #authenticate-login-widget}

登录窗口小部件缺省配置要求同时使用 Facebook 和 Google 进行认证。如果仅配置了其中一项，那么登录窗口小部件不会启动，并且用户会重定向到已配置的 IDP 认证屏幕。

初始化 {{site.data.keyword.appid_short_notm}} 客户端 SDK 后，可以通过运行登录窗口小部件来对用户进行认证。

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


## 访问用户属性
{: #accessing}

获取访问令牌时，还可获取对用户保护的属性端点的访问权。您可以使用以下 API 方法来获取访问权：

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

未显式传递访问令牌时，{{site.data.keyword.appid_short_notm}} 会使用最后一次收到的令牌。

例如，可以调用以下代码来设置新属性，或者覆盖现有属性：

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

### 匿名登录
{: #anonymous notoc}

通过 {{site.data.keyword.appid_short_notm}}，您可以匿名登录；请参阅[匿名用户](/docs/services/appid/user-profile.html#anonymous)。

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

### 渐进式认证
{: #progressive notoc}

用户持有匿名访问令牌时，可以通过将令牌传递到 `loginWidget.launch` 方法来得到识别。

  ```java
  void launch (@NonNull final Activity activity, @NonNull final AuthorizationListener authorizationListener, String accessTokenString);
  ```
  {:pre}

匿名登录后，会执行渐进式认证，即便在未传递访问令牌的情况下调用了登录窗口小部件时也是如此，因为服务使用的是最后一次收到的令牌。如果要清除存储的令牌，请运行以下命令：

  ```java
  	appIDAuthorizationManager = new AppIDAuthorizationManager(this.appId);
  appIDAuthorizationManager.clearAuthorizationData();
  ```
  {:pre}


## 后续步骤
{: #next-steps}

初始设置身份提供者时，{{site.data.keyword.appid_short_notm}} 提供了缺省配置。缺省配置只能用于开发方式。在发布应用程序之前，请将缺省 [Facebook](/docs/services/appid/identity-providers.html#facebook) 和 [Google](/docs/services/appid/identity-providers.html#google) 配置更新为您自己的凭证。
