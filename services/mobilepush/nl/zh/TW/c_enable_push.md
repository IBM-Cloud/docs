---

copyright:
years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 啟用行動裝置的通知
{: #c_enable_push-notifications}
前次更新：2017 年 4 月 12 日
{: .last-updated}

請確定您已通過[配置通知提供者的認證](t__main_push_config_provider.html)。

本節說明如何啟用用戶端應用程式（行動裝置、Web 瀏覽器應用程式以及 Chrome Apps and Extensions）來接收推送通知、如何建立基本通知、取得及起始設定 SDK 或外掛程式，以及如何登錄裝置或瀏覽器來接收推送通知。您也可以使用 [REST API](t_restapi.html)，讓行動及 Web 瀏覽器應用程式接收推送通知。

**附註**：對於裝置、瀏覽器及 Chrome Apps and Extensions 登錄，{{site.data.keyword.mobilepushshort}} Service 會對從通知提供者（APNs for Apple 或 FCM for Google）發出的記號保持唯一參照。
{{site.data.keyword.mobilepushshort}} Service 通知提供者可基於數個原因，而讓這些記號失效。 

例如，解除安裝裝置上的應用程式期間。在這種情境中，當嘗試根據裝置失效的提供者回應遞送通知時，{{site.data.keyword.mobilepushshort}} Service 將移除裝置或 Web 瀏覽器登錄。接著，這將限制隨後不得將通知傳送至失效裝置。


## 啟用 Android 應用程式來接收推送通知
{: #tag_based_notifications}


您可以啟用 Android 應用程式來接收傳送至您裝置的推送通知。Android Studio 是必備項目，而且是建置 Android 專案的建議方法。對 Android Studio 的基本瞭解十分重要。

### 使用 Gradle 安裝 Client Push SDK
{: #android_install}

本節說明如何安裝及使用 Client Push SDK 來進一步開發 Android 應用程式。

您可以使用 [Gradle ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/tools/building/configuring-gradle.html){: new_window} 來新增 {{site.data.keyword.Bluemix}} Mobile Services Push SDK，而 Gradle 會從儲存庫中自動下載構件，並讓它們可供 Android 應用程式使用。請確定您已正確設定 [Android Studio ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.android.com/tools/studio/index.html) 及 Android Studio SDK。 

建立並開啟行動應用程式之後，請使用 Android Studio 來完成下列步驟。

1. 將相依關係新增至「模組」層次 **build.gradle** 檔案。 	

	- 新增下列相依關係，以將 Bluemix™ Mobile Services Push Client SDK 及 Google Play Services SDK 包含在您的編譯範圍相依關係。
	```
	com.ibm.mobilefirstplatform.clientsdk.android:push:3.+
	```
    	{: codeblock}
	
	- 將下列相依關係新增至 import 陳述式，程式碼 Snippet 需要這些 import 陳述式。
	```
	import com.ibm.mobilefirstplatform.clientsdk.android.core.api.BMSClient;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushException;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushResponseListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationListener;
	import com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPSimplePushNotification;
	```
    	{: codeblock}

	- 最後，將下列相依關係新增至「模組」層次 **build.gradle** 檔案。
	```
		apply plugin: 'com.google.gms.google-services'
	```
		{: codeblock}
3. 將下列相依關係新增至「專案」層次 **build.gradle** 檔案。
```
dependencies {
    classpath 'com.android.tools.build:gradle:2.2.3'
    classpath 'com.google.gms:google-services:3.0.0'
}
``` 
    {: codeblock}
5. 在 **AndroidManifest.xml** 檔案中，新增下列許可權。若要檢視範例資訊清單，請參閱 [Android helloPush 範例應用程式 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/src/main/AndroidManifest.xml){: new_window}。若要檢視範例 Gradle 檔案，請參閱[範例建置 Gradle 檔案 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-samples-android-hellopush/blob/master/helloPush/app/build.gradle){: new_window}。
```
	<uses-permission android:name="android.permission.INTERNET"/>
	<uses-permission android:name="android.permission.GET_ACCOUNTS" />
	<uses-permission android:name="android.permission.USE_CREDENTIALS" />
	<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
	<uses-permission android:name="android.permission.ACCESS_WIFI_STATE"/>
```
	{: codeblock}
 您可以在這裡瞭解 [Android 許可權 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](http://developer.android.com/guide/topics/security/permissions.html){: new_window}。

4. 新增活動的通知目的設定。此設定會在使用者按一下通知區域中的接收通知時啟動應用程式。
```
	<intent-filter>
	<action android:name="Your_Android_Package_Name.IBMPushNotification"/>
	<category  android:name="android.intent.category.DEFAULT"/>
</intent-filter>
```
	{: codeblock}
**附註**：將先前動作中的 *Your_Android_Package_Name* 取代為您應用程式中所使用的應用程式套件名稱。

5. 針對 RECEIVE 及 REGISTRATION 事件通知，新增 Firebase Cloud Messaging (FCM) 或 Google Cloud Messaging (GCM) 目的服務及目的過濾器。
```
	<service android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushIntentService"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.MESSAGING_EVENT" />
    </intent-filter>
	</service>
<service
    android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPush"
    android:exported="true" >
    <intent-filter>
        <action android:name="com.google.firebase.INSTANCE_ID_EVENT" />
    </intent-filter>
	</service>
```
    {: codeblock}

6. {{site.data.keyword.mobilepushshort}} Service 支援從通知匣擷取個別通知。對於從通知匣存取的通知，只會提供給您所點選之通知的控點。正常開啟應用程式時，會顯示所有通知。請使用下列 Snippet 來更新 **AndroidManifest.xml** 檔案，以使用此功能：

```
	<activity android:name="
com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationHandler"
android:theme="@android:style/Theme.NoDisplay"/>
```
    {: codeblock}

請確定您已通過[配置通知提供者的認證](t__main_push_config_provider.html)，可以設定 FCM 專案並取得認證。請使用 Firebase Cloud Messaging (FCM) 主控台來完成下列步驟。

1. 在 Firebase 主控台中，按一下**專案設定**圖示。
	![Firebase 專案設定](images/FCM_4.jpg)

3. 從應用程式窗格的「一般」標籤中，選取**新增應用程式**或**將 Firebase 新增至 Android 應用程式**圖示。![將 Firebase 新增至 Android](images/FCM_5.jpg)

4. 在「將 Firebase 新增至 Android 應用程式」視窗中，新增 **com.ibm.mobilefirstplatform.clientsdk.android.push** 作為「套件名稱」。應用程式暱稱欄位是選用性的。按一下**新增應用程式**。  
    ![「將 Firebase 新增至 Android」視窗](images/FCM_1.jpg)

5. 在「將 Firebase 新增至 Android 應用程式」視窗中輸入套件名稱，以包含應用程式的套件名稱。應用程式暱稱欄位是選用性的。按一下**新增應用程式**。 

	![新增應用程式的套件名稱](images/FCM_2.jpg)

6. 會產生 `google-services.json` 檔案。將 `google-services.json` 檔案複製到您的 Android 應用程式模組根目錄。請注意，`google-service.json` 檔案包含已新增的套件名稱。

    ![將 json 檔案新增至應用程式的根目錄](images/FCM_7.jpg)

5. 在「將 Firebase 新增至 Android 應用程式」視窗中，按一下**繼續**，然後按一下**完成**。 

  

建置並執行應用程式。

### 起始設定 Push SDK for Android 應用程式
{: #android_initialize}

放置起始設定碼的一般位置位於 Android 應用程式之主要活動的 onCreate 方法中。SDK 有兩個需要起始設定的元件。一個是核心 SDK，另一個則是以核心 SDK 為建置基礎的推送 SDK。

#### 起始設定 Core SDK
{: #initz_core_sdk}

```
// Initialize the SDK for Android
    BMSClient.getInstance().initialize(this, BMSClient.REGION_US_SOUTH);
```
    {: codeblock}

#### bluemixRegionSuffix
{: #bluemixRegionSuffix}

指定管理應用程式的位置。您可以使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

#### 起始設定 Client Push SDK
{: #initiz_client_pushSDK}

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext(), "appGUID", "clientSecret");
```
	{: codeblock}

#### AppGUID
{: #appguid_initialize_client_push_sdk}

這是 {{site.data.keyword.mobilepushshort}} Service 的 AppGUID 金鑰。此值區分大小寫。開啟 Push Notification 儀表板，然後選取「配置」標籤。您可以從 Push Notification Service 儀表板上「配置」標籤的「行動選項」中取得此值。 

### 登錄 Android 裝置
{: #android_register}

使用 `MFPPush.register()` API，以向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置。如需登錄 Android 裝置，請在 Bluemix {{site.data.keyword.mobilepushshort}} Service 配置儀表板中新增 Firebase Cloud Messaging (FCM) 資訊。如需相關資訊，請參閱[配置通知提供者的認證](t__main_push_config_provider.html)。

將下列程式碼 Snippet 複製到 Android 行動應用程式。

```
	//Register Android devices
	push.registerDevice(new MFPPushResponseListener<String>() {
    	@Override
    	public void onSuccess(String response) {
    		//handle success here
    	}
		@Override
    	public void onFailure(MFPPushException ex) {
    		//handle failure here
		}
		});
```
	{: codeblock}


```
	//Handles the notification when it arrives
	MFPPushNotificationListener notificationListener = new MFPPushNotificationListener() {
    @Override
    public void onReceive (final MFPSimplePushNotification message){
		// Handle Push Notification
   		 }
		};
```
	{: codeblock}

### 在 Android 裝置上接收推送通知
{: #android_receive}

1. 若要向 Push Notifications Service 登錄 notificationListener 物件，請使用 `MFPPush.listen()` 方法。此方法一般是透過處理推送通知之活動的 `onResume()` 及 `onPause` 方法所呼叫。
```
	@Override
	protected void onResume(){
   	super.onResume();
   	if(push != null) {
       push.listen(notificationListener);
   }
	}
```
	{: codeblock}
```
	@Override
	protected void onPause() {
    super.onPause();
    if (push != null) {
        push.hold();
    }
}
```
	{: codeblock}

2. 建置專案，並在裝置或模擬器上執行該專案。在 register() 方法中呼叫回應接聽器的 onSuccess() 方法時，它會確認已順利向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置，而且您現在可以傳送推送通知。
3. 驗證您的裝置已接收到通知。如果應用程式是在前景中，則 `MFPPushNotificationListener` 會處理通知。如果應用程式是在背景中，則會在通知列中顯示一則訊息。

### 在 Android 裝置上監視推送通知
{: #android_monitor}

若要監視應用程式內的現行通知狀態，您可以實作 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 介面，並定義方法 onStatusChange(String messageId, MFPPushNotificationStatus status)。 

`messageId` 是從伺服器傳送之訊息的 ID。`MFPPushNotificationStatus` 以值來定義通知的狀態：

- RECEIVED - 應用程式已收到通知。 
- QUEUED - 應用程式將通知置入佇列以便呼叫通知接聽器。 
- OPENED - 使用者開啟通知的方式是按一下系統匣中的通知，或是從應用程式圖示或在應用程式處於前景時啟動它。 
- DISMISSED - 使用者清除/跳出系統匣中的通知。

您需要向 MFPPush 登錄 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationStatusListener` 類別。

```
	push.setNotificationStatusListener(new MFPPushNotificationStatusListener() {
@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
// Handle status change
}
});
```
    {: codeblock}


#### 接聽 DISMISSED 狀態
{: #android_monitor_listen}

您可以選擇在下列任一狀況接聽 DISMISSED 狀態：

- 當應用程式在作用中（在前景或背景執行）時

  將 Snippet 新增至您的 `AndroidManifest.xml` 檔案：

```
	<receiver android:name="com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
</intent-filter>
	</receiver>
```
	{: codeblock}

- 當應用程式在作用中（在前景或背景執行）以及不在執行中（已關閉）時

請延伸 `com.ibm.mobilefirstplatform.clientsdk.android.push.api.MFPPushNotificationDismissHandler` 廣播接收端，並置換 `onReceive()` 方法，其中應該先登錄 `MFPPushNotificationStatusListener`，再呼叫基礎類別的 `onReceive()` 方法。

```
	public class MyDismissHandler extends MFPPushNotificationDismissHandler {
@Override
public void onReceive(Context context, Intent intent) {
MFPPush.getInstance().setNotificationStatusListener(new MFPPushNotificationStatusListener() {
@Override
public void onStatusChange(String messageId, MFPPushNotificationStatus status) {
// Handle status change
}
});
super.onReceive(context, intent);
}
}
```
    {: codeblock}


將下列 Snippet 新增至您的 `AndroidManifest.xml` 檔案：

```
	<receiver android:name="Your_Android_Package_Name.Your_Handler">
<intent-filter>
<action android:name="Your_Android_Package_Name.Cancel_IBMPushNotification"/>
</intent-filter>
	</receiver>
```
    {: codeblock}

### 傳送基本推送通知
{: #send-basic-notification}

開發應用程式之後，您可以傳送基本推送通知。

若要傳送基本推送通知，請完成下列步驟：

1. 選取**傳送通知**，然後選擇**傳送至**選項來編寫訊息。支援的選項是**依標籤的裝置**、**裝置 ID**、**使用者 ID**、**Android 裝置**、**iOS 裝置**、**Web 通知**及**所有裝置**。
**附註**：當您選取**所有裝置**選項時，所有已訂閱 {{site.data.keyword.mobilepushshort}} 的裝置都會接收到通知。![通知畫面](images/tag_notification.jpg)

2. 在**訊息**欄位中，編寫訊息。視需要選擇配置選用設定。
3. 按一下**傳送**。
3. 驗證您的裝置已接收到通知。

下列擷取畫面顯示在 Android 裝置的前景中處理推送通知的警示框。



![Android 上的前景推送通知](images/Android_Screenshot.jpg)

下列擷取畫面顯示 Android 背景中的推送通知。
	

![Android 上的背景推送通知](images/background.jpg)

### 傳送通知的選用 Android 設定
{: #send_otpional_setting}

您可以進一步自訂 {{site.data.keyword.mobilepushshort}} 設定，以將通知傳送給 Android 裝置。支援下列選用自訂選項：![Android 自訂設定](images/android_custom_settings.jpg)

- 收合金鑰：收合金鑰會附加至通知。如果多個具有相同收合金鑰的通知在裝置離線時循序到達，則會予以收合。當裝置上線時，會接收到來自 FCM/GCM 伺服器的通知，並且只會顯示含有相同收合金鑰的最新通知。如果未設定收合金鑰，則會儲存新舊訊息，以供未來遞送。
- 音效：指出要在收到通知時播放的音效短片。支援預設值或應用程式中所組合的音效資源名稱。
- 圖示：指定要針對通知顯示的圖示名稱。請確定您已將圖示與用戶端應用程式包裝至 `res/drawable` 資料夾。
- 優先順序：指定用於指派訊息遞送優先順序的選項。優先順序 `high` 或 `max` 將會導致提前通知，而 `low` 或 `default` 優先順序訊息則不會在休眠裝置上開啟網路連線。針對選項設為 `min` 的訊息，它會是無聲自動通知。
- 可見性：您可以選擇將通知可見性選項設為 `public` 或 `private`。`private` 選項會限制公用檢視，因此，如果您的裝置使用 PIN 碼或型樣保護，且通知設定設為**隱藏機密通知內容**，則可以選擇啟用它。可見性設為 `private` 時，必須提及 `redact` 欄位。只有 `redact` 欄位中所指定的內容才會顯示在裝置的安全鎖定畫面上。選擇 `public` 則會呈現可自由讀取的通知。
- 存活時間：此值是以秒為單位來設定。如果未指定此參數，則 FCM/GCM 伺服器會儲存訊息四週，並嘗試遞送。有效性會在四週後到期。可能值範圍是從 0 到 2,419,200 秒。
- 閒置時延遲：將此值設為 `true` 時，指示 FCM/GCM 伺服器不要在裝置閒置時遞送通知。將此值設為 `false`，則可確保遞送通知，即使裝置閒置也是一樣。
- 同步：透過將此選項設為 `true`，所有已登錄裝置的通知就會同步。如果具有使用者名稱的使用者有多個已安裝相同應用程式的裝置，則讀取某個裝置上的通知可確保刪除其他裝置中的通知。您需要確定已使用 userId 向 {{site.data.keyword.mobilepushshort}} Service 進行登錄，此選項才能運作。
- 其他有效負載：指定通知的自訂有效負載值。


### 後續步驟
{: #next_steps_tag_based_notifications}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 Push Notifications Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。若要使用進階通知選項，請參閱[啟用進階推送通知](t_advance_badge_sound_payload.html)。


## 讓 Cordova 應用程式可接收推送通知
{: #cordova_enable}


Cordova 是一個平台，可使用 JavaScript、CSS 及 HTML 來建置混合式應用程式。{{site.data.keyword.mobilepushshort}} Service 支援開發 Cordova 型 iOS 及 Android 應用程式。

您可以啟用 Cordova 應用程式來接收傳送至您裝置的推送通知。

### 安裝 Cordova Push 外掛程式
{: #cordova_install}

安裝及使用 Client Push 外掛程式來進一步開發 Cordova 應用程式。這也會安裝起始設定您的 Bluemix 連線的 Cordova Core 外掛程式。

1. 下載最新的 Android Studio SDK 及 Xcode 版本。
1. 設定您的模擬器。若為 Android Studio，請使用支援 Google Play API 的模擬器。
1. 安裝 Git 指令行工具。若為 Windows，請確保選取**從 Windows 命令提示字元執行 Git** 選項。如需如何下載及安裝此工具的相關資訊，請參閱 [Git ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://git-scm.com/downloads){: new_window}。
1. 安裝 Node.js 及「Node 套件管理程式 (NPM)」工具。NPM 指令行工具與 Node.js 組合在一起。如需如何下載及安裝 Node.js 的相關資訊，請參閱 [Node.js ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://nodejs.org/en/download/){: new_window}。
1. 從指令行中，使用 **npm install -g cordova** 指令來安裝 Cordova 指令行工具。若要使用 Cordova Push 外掛程式，這是必要動作。如需如何安裝 Cordova 以及設定 Cordova 應用程式的相關資訊，請參閱 [Cordova Apache ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://cordova.apache.org/#getstarted){: new_window}。如需相關資訊，請參閱 Cordova Push 外掛程式 [Readme 檔 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-cordova-plugin-push){: new_window}。
1. 切換至您要在其中建立 Cordova 應用程式的資料夾，並執行下列指令來建立 Cordova 應用程式。如果您有現存的 Cordova 應用程式，請移至步驟 3。
```
cordova create your_app_name
cd your_app_name
```
	{: codeblock}
- 選用項目：您可以編輯 **config.xml** 檔案，並將 <name> 元素中的應用程式名稱變更為您選擇的名稱，而不是預設 HelloCordova 名稱。

請確定您指定正確的「軟體組 ID」。如果指定不正確的「軟體組 ID」，則下列錯誤訊息可能會導致 Xcode。

* 以無效的授權簽署執行檔。
* 應用程式的「程式碼簽署授權」檔案中指定的授權，不符合佈建設定檔中指定的授權。若要修正此問題，請在 Xcode 或 Cordova 應用程式 **config.xml** 檔案中指定正確的「軟體組 ID」。

1. 將最低支援的 API 或部署目標宣告新增至 Cordova 應用程式的 config.xml 檔案。minSdkVersion 值必須高於 15。targetSdkVersion 值必須一律反映可從 Google 取得的最新 Android SDK。
	
	* Android - 使用編輯器來開啟 **config.xml** 檔案，並將
`<platform name="android">` 元素更新為最小及目標 SDK 版本：

	```
	<platform name="android">
    	<preference name="android-minSdkVersion" value="15" />
    	<preference name="android-targetSdkVersion" value="23" />
    	<!-- add minimum and target Android API level declaration -->
	</platform> 
	```
    	{: codeblock}

   * iOS - 使用部署目標宣告更新 <platform name="ios"> 元素：

	```
	<platform name="ios">
	    <preference name="deployment-target" value="8.0" />
	    <!-- add deployment target declaration -->
	</platform>
	```
		{: codeblock}

1. 從 Cordova 指令行介面 (CLI) 中，使用下列指令新增平台：iOS 及（或）Android：
```
cordova platform add ios
cordova platform add android
```
	{: codeblock}

1. 從 Cordova 應用程式根目錄中，輸入下列指令來安裝 Cordova Push 外掛程式：**cordova plugin add bms-push**。根據您新增的平台，您可能會看到：
```
Installing "bms-push" for android
Installing "bms-push" for ios
```
	{: codeblock}

1. 從 your-app-root-folder 中，使用下列指令，驗證已順利安裝 Cordova Core 及 Push 外掛程式：**cordova plugin list**。根據您新增的平台，您可能會看到：
```
bms-core <version> "BMSCore"
bms-push <version> "BMSPush" 
```
	{: codeblock}

1. 配置您的 iOS 開發環境。
2. 使用 Xcode 建置並執行應用程式。
1. 下載針對 Android 使用的 Firebase `google-services.json`，並且將他們放置在 Cordova 專案的根資料夾：[your-app-name]/platforms/android。
	1. 請移至 `[your-app-name]/platforms/android`。
	2. 開啟 `build.gradle` 檔案（路徑：platform > android > build.gradle）。
	3. 在 `build.gradle` 檔案中尋找 `buildscript` 文字。
	4. 在類別路徑行之後，新增此行：classpath 'com.google.gms:google-services:3.0.0'
	5. 然後，尋找 "dependencies"。選取 `compile` 文字的相依關係以及選取要於何處結束該相依關係，在此之後，新增此行 :apply plugin: 'com.google.gms.google-services'。
	6. 準備及建置您的 Cordova Android 專案。
		```
		cordova prepare android
		cordova build android
		```
			{: codeblock}
	**附註**：在 Android Studio 中開啟專案之前，請先透過 Cordova CLI 建置 Cordova 應用程式。這將有助於避免建置錯誤。

### 起始設定 Cordova 外掛程式
{: #cordova_initialize}

您需要透過傳遞應用程式路徑及應用程式 GUID 來起始設定 {{site.data.keyword.mobilepushshort}} Service Cordova 外掛程式，才能使用該外掛程式。在起始設定外掛程式之後，您可以連接至在 Bluemix 儀表板中所建立的伺服器應用程式。Cordova 外掛程式是 Android 及 iOS Client SDK 的封套，可讓 Cordova 應用程式與 Bluemix 服務通訊。

1. 複製下列程式碼 Snippet，並將其貼入您的主要 JavaScript 檔案（通常位於 **www/js** 目錄下），以起始設定 BMSClient。

```
onDeviceReady: function() {
	app.receivedEvent('deviceready');
	BMSClient.initialize("YOUR APP REGION");
	var category =  {};
	BMSPush.initialize(appGUID,clientSecret,category);
	var success = function(message) { console.log("Success: " + message); };
	var failure = function(message) { console.log("Error: " + message); };
	BMSPush.registerDevice({}, success, failure);
	var showNotification = function(notif)
	{
	alert(JSON.stringify(notif));
	};
	BMSPush.registerNotificationsCallback(showNotification);
    } 
```
	{: codeblock}

傳入應用程式的地區。會提供以下常數：

```
REGION_US_SOUTH // ".ng.bluemix.net";
REGION_UK //".eu-gb.bluemix.net";
REGION_SYDNEY // ".au-syd.bluemix.net";
```

例如：

```
BMSClient.initialize(BMSClient.REGION_US_SOUTH);
```

**附註**：如果您已使用 Cordova CLI（例如，Cordova create app-name 指令）建立 Cordova 應用程式，請將此 JavaScript 程式碼放置在 index.js 檔案中 onDeviceReady: function() 函數內的 app.receivedEvent 函數後面，以起始設定 `BMSClient`。 


### 登錄裝置
{: #cordova_register}


若要向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置，請呼叫 register 方法。將下列程式碼 Snippet 複製至 Cordova 應用程式，以登錄裝置。

```
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
```
	{: codeblock}

下列 JavaScript 程式碼 Snippet 顯示如何起始設定 Bluemix Mobile Services Push Client SDK、向 {{site.data.keyword.mobilepushshort}} Service 登錄裝置，以及接聽推送通知。請在 Javascript 檔案中包含此程式碼。

在 **onDeviceReady: function()** 內。

```
onDeviceReady: function() {
app.receivedEvent('deviceready');
BMSClient.initialize("YOUR APP REGION");
var success = function(message) { console.log("Success: " + message); };
var failure = function(message) { console.log("Error: " + message); };
BMSPush.registerDevice({}, success, failure);
 var showNotification = function(notif)
 {
 alert(JSON.stringify(notif));
 };
BMSPush.registerNotificationsCallback(showNotification);
```
	{: codeblock}

將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。

```
// Register the device token with Bluemix Push Notification Service
func application(application: UIApplication,
  didRegisterForRemoteNotificationsWithDeviceToken deviceToken: NSData) {
   CDVBMSPush.sharedInstance().didRegisterForRemoteNotificationsWithDeviceToken(deviceToken)
} 
// Handle error when failed to register device token with APNs
func application(application: UIApplication,
    didFailToRegisterForRemoteNotificationsWithError error: NSErrorPointer) {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(error)
} 
```
	{: codeblock}

### 後續步驟
{: #cordova_register_next}

使用下列指令建置專案，然後執行專案：

#### Android
{: #android-next-steps}

```
cordova build android
```
	{: codeblock}

```
cordova run android
```
	{: codeblock}

#### iOS
{: #ios-next-steps}

```
cordova build ios
```
	{: codeblock}

```
cordova run ios
```
	{: codeblock}

### 在裝置上接收推送通知
{: #cordova_receive}

複製下列程式碼 Snippet，以在裝置上接收推送通知。

#### JavaScript
{: #jvscrpt}

將下列 JavaScript 程式碼 Snippet 新增至 Cordova 應用程式的 Web 組件。
```
var showNotification = function(notif) {
  alert(JSON.stringify(notif));
        };
        BMSPush.registerNotificationsCallback(showNotification); 
```
	{: codeblock}

#### Android 通知內容
{: #And_notif}

下節列出 Android 通知內容：

* **message** - 推送通知訊息
* **payload** - 包含通知有效負載的 JSON 物件


#### iOS 通知內容
{: #ios_notif}

下節列出 iOS 通知內容：

* **message** - 推送通知訊息
* **payload** - 包含通知有效負載的 JSON 物件
* **action-loc-key** - 此字串用來作為索引鍵，在現行本地化中取得一個本地化字串，以用於適當的按鈕標題，而取代 `View`。
* **badge** - 顯示為應用程式圖示徽章的號碼。如果沒有此內容，則不會變更徽章。若要移除徽章，請將此內容的值設為 0。
* **sound** - 應用程式組合或者應用程式資料容器之 Library/Sounds 資料夾中的音效檔名稱。


將下列 Swift 程式碼 Snippet 新增至應用程式委派類別。
```
// Handle receiving a remote notification
func application(application: UIApplication,
   didReceiveRemoteNotification userInfo: [NSObject : AnyObject],  fetchCompletionHandler completionHandler: ) {
   CDVBMSPush.sharedInstance().didReceiveRemoteNotificationWithNotification(userInfo)
}
```
	{: codeblock}

```
// Handle receiving a remote notification on launch
func application(application: UIApplication, didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
  {
  let remoteNotif = launchOptions?[UIApplicationLaunchOptionsKey.remoteNotification] as? NSDictionary
  if remoteNotif != nil {
    CDVBMSPush.sharedInstance().didReceiveRemoteNotificationOnLaunchWithLaunchOptions(launchOptions)
  }
} 
```
	{: codeblock}

### 傳送基本推送通知
{: #push-send-notifications}

開發應用程式之後，您可以傳送基本推送通知。

若要傳送基本推送通知，請完成下列步驟：

1. 選取**傳送通知**，然後選擇**傳送至**選項來編寫訊息。支援的選項是**依標籤的裝置**、**裝置 ID**、**使用者 ID**、**Android 裝置**、**iOS 裝置**、**Web 通知**及**所有裝置**。
**附註**：當您選取**所有裝置**選項時，所有已訂閱 {{site.data.keyword.mobilepushshort}} 的裝置都會接收到通知。![通知畫面](images/tag_notification.jpg)

2. 在**訊息**欄位中，編寫訊息。視需要選擇配置選用設定。
3. 按一下**傳送**。
3. 驗證您的裝置已接收到通知。

下列擷取畫面顯示在 Android 及 iOS 裝置的前景中處理 {{site.data.keyword.mobilepushshort}} 的警示框。

![Android 上的前景推送通知](images/Android_Screenshot.jpg)

![iOS 上的前景推送通知](images/iOS_Screenshot.jpg)

   下列影像在 Android 的背景中顯示 {{site.data.keyword.mobilepushshort}}。  
![Android 上的背景推送通知](images/background.jpg)

#### 後續步驟
{: #next_steps_basic_notifications}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將 {{site.data.keyword.mobilepushshort}} Service 特性新增至您的應用程式。若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。若要使用進階通知選項，請參閱[啟用進階推送通知](t_advance_badge_sound_payload.html)。


## 啟用 iOS 應用程式來傳送推送通知
{: #enable-push-ios-notifications}

您可讓 iOS 應用程式傳送 {{site.data.keyword.mobilepushshort}} 至您的裝置。


### 安裝 CocoaPods
{: #enable-push-ios-notifications-install}

針對現有的 Xcode 專案，您可以使用 CocoaPods 相依關係管理工具來設定 Bluemix Mobile Services Client SDK。替代方案是手動安裝 SDK。

若要檢視 Swift Push Readme 檔，請移至 [Readme ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}。



1. 在 Mac 終端機中，使用下列指令來安裝 CocoaPods。
	```
		$ sudo gem install cocoapods
```
	{: codeblock}
2. 在終端機中輸入 `pod init` 指令，以起始設定 CocoaPods。請確定您從 Xcode 專案所在的目錄執行指令。`pod init` 指令會建立 Podfile。  
3. 在產生的 Podfile 中，新增必要 SDK 相依關係。請複製下列 Podfile。
   
	```
		source 'https://github.com/CocoaPods/Specs.git'
	// Copy the following list as is and remove the dependencies you do not need.
	use_frameworks!
	target 'MyApp' do
	    platform :ios, '8.0'
	    pod 'BMSCore'
	    pod 'BMSPush'
      pod 'BMSAnalyticsAPI'
	end
	```
		{: codeblock}

3. 從終端機中，移至您的專案資料夾，並使用 `pod update` 指令來安裝相依關係。

此指令會安裝相依關係並建立新的 Xcode 工作區。  
**附註**：請確定您一律開啟新的 Xcode 工作區，而不是原始 Xcode 專案檔：
```
$ open App.xcworkspace
```
	{: codeblock}

工作區會包含原始專案以及包含相依關係的 Pods 專案。若要修改 Bluemix Mobile Services 來源資料夾，您可以在 Pods 專案的 `Pods/yourImportedSourceFolder` 下找到它，例如：`Pods/BMSPush`。

### 使用 Carthage 新增架構
{: #carthage}

使用 [Carthage ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window}，將架構新增至您的專案。請注意，不支援 Xcode8 形式的 Carthage。

1. 在 Cartfile 中新增 `BMSPush` 架構：
	```
	github "github "ibm-bluemix-mobile-services/bms-clientsdk-swift-push" ~> 1.0"
```
	{: codeblock}
2. 執行 `carthage update` 指令。建置完成時，請將 `BMSPush.framework`、`BMSCore.framework` 及 `BMSAnalyticsAPI.framework` 拖曳至 Xcode 專案。
3. 遵循在 [Carthage ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/Carthage/Carthage#if-youre-building-for-ios-tvos-or-watchos){: new_window} 網站的指示，以完成整合。

### 設定 iOS SDK
{: #ios-sdk}

設定 iOS SDK，並新增下列程式碼至應用程式中的 **AppDelegate.swift** 檔案。請注意，這也會使用 APNs 登錄。  
```
func application(_ application: UIApplication,
didFinishLaunchingWithOptions launchOptions: [NSObject: AnyObject]?) -> Bool
 {
 BMSPushClient.sharedInstance.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE")
  }
```
    {: codeblock}

### 使用匯入的架構和來源資料夾
{: #using-imported-frameworks}

在您的程式碼中參照 SDK。請確定已具備下列必備項目。

- iOS 8.0 或以上版本	
- Xcode 7

撰寫相關標頭的 `#import` 指引，例如：
```
	 //swift
import BMSCore
import BMSPush
```
		{: codeblock}

若要閱讀 Swift Push Readme 檔案，請參閱 [Readme ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://github.com/ibm-bluemix-mobile-services/bms-clientsdk-swift-push/tree/master){: new_window}。

**附註**：使用 CocoaPods 指令 `pod install` 或 `pod update` 更新 Pods 專案時，可能會置換 Bluemix Mobile Services 來源資料夾。如果您要保留原始檔案的自訂版本，請確保先進行備份，然後再發出下列其中一個指令。


### 建置設定
{: #build-settings}

移至 **Xcode > 建置設定 > 建置選項，然後將啟用位元碼**設為**否**。

**注意**：自 iOS 9 開始，對「應用程式傳輸安全 (ATS)」特性進行的變更可能會影響您處理鑑別處理程序的方式。下列部落格文章說明這些變更的相關資訊：[ATS and Bitcode in iOS 9 ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/mobilefirstplatform/2015/09/09/ats-and-bitcode-in-ios9/){: new_window} and [Connect your iOS 9 app to Bluemix today ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://developer.ibm.com/bluemix/2015/09/16/connect-your-ios-9-app-to-bluemix/){: new_window}。

### 起始設定 Push SDK for iOS 應用程式
{: #enable-push-ios-notifications-initialize}

放置起始設定碼的一般位置位於 iOS 應用程式的應用程式委派中。按一下「Push 儀表板」中的**行動選項**鏈結，以取得應用程式路徑及 GUID。

#### 起始設定 Core SDK
{: #Initializing-the-core-sdk}

若要使用 IBM Bluemix GUID、路徑及地區起始設定 Core SDK for Swift，請使用下列程式碼 Snippet。
```
	let myBMSClient = BMSClient.sharedInstance
	myBMSClient.initialize(bluemixRegion: "Location where your app is hosted.") 
```
	{: codeblock}

#### 路徑、GUID 及 Bluemix 地區
{: #route-guid-bluemix-region}


- **appRoute**：指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。


- **GUID**：指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。


- **bluemixRegionSuffix**：指定管理應用程式的位置。`bluemixRegion` 參數指定您所使用的 Bluemix 部署。您可以使用 `BMSClient.REGION` 靜態內容設定此值，然後使用下列三個值的其中一個：

	- BMSClient.Region.usSouth 
	- BMSClient.Region.unitedKingdom
	- BMSClient.Region.sydney


- **AppGUID**：指定指派給您在 Bluemix 上所建立之 {{site.data.keyword.mobilepushshort}} Service 的唯一 AppGUID 索引鍵。

#### 起始設定 Client Push SDK
{: #initializing-the-client-Push-SDK}

```
	let push = BMSPushClient.sharedInstance
	push.initializeWithAppGUID("appGUID", clientSecret:"clientSecret")
```
	{: codeblock}


### 登錄 iOS 應用程式及裝置
{: #enable-push-ios-notifications-register}

在裝置上安裝應用程式之後，應用程式必須向 APNs 登錄才能接收遠端通知。在應用程式接收到 APNs 所產生的裝置記號之後，必須將裝置記號傳回給 {{site.data.keyword.mobilepushshort}} Service。

若要登錄 iOS 應用程式及裝置，您需要：

1. 建立後端應用程式。
2. 將記號傳遞至 {{site.data.keyword.mobilepushshort}}。


#### 建立後端應用程式
{: #create-a-backend-app}

在 Bluemix® 型錄的「樣板」區段中建立後端應用程式，以自動將 {{site.data.keyword.mobilepushshort}} Service 連結至此應用程式。如果您已建立後端應用程式，請確定將應用程式連結至 {{site.data.keyword.mobilepushshort}} Service。


#### 將記號傳遞至 Push Notifications
{: #pass-token-push-notifications}

從 APNs 接收到記號之後，將記號傳遞至 {{site.data.keyword.mobilepushshort}}，這是 `registerWithDeviceToken` 方法的一部分。

```
func application (_application: UIApplication, didRegisterForRemoteNotificationsWithDeviceToken deviceToken: Data){
   let push =  BMSPushClient.sharedInstance
   push.registerWithDeviceToken(deviceToken) { (response, statusCode, error) -> Void in
      if error.isEmpty {
           print( "Response during device registration : \(response)")
            print( "status code during device registration : \(statusCode)")
       }
        else{
            print( "Error during device registration \(error) ")
            print( "Error during device registration \n  - status code: \(statusCode) \n Error :\(error) \n")
        }
    }
  }
```
	{: codeblock}


### 在 iOS 裝置上接收推送通知
{: #enable-push-ios-notifications-receiving}

若要在 iOS 裝置上接收推送通知，請將下列 Swift 方法新增至應用程式的應用程式委派。

```
   func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) 
  { //UserInfo dictionary will contain data sent from the server }
```
	{: codeblock}

### 監視 iOS 裝置上的推送通知
{: #ios-monitoring}


您可以監視已送出推送通知的計數及現行狀態。若要啟用監視，請根據事件，將下列任一 Swift 方法新增至應用程式的應用程式委派。



- 在按一下通知以開啟應用程式時傳送通知狀態。
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any]) { 					let push =  BMSPushClient.sharedInstance
				let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
				let data = respJson.data(using: String.Encoding.utf8)
				let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		    	push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
    		  print("Send message status to the Push server")
    	 }
		}
	```
			{: codeblock}



- 在應用程式處於背景模式時，傳送通知狀態。
	```
		func application(_ application: UIApplication, didReceiveRemoteNotification userInfo: [AnyHashable : Any], fetchCompletionHandler completionHandler: @escaping (UIBackgroundFetchResult) -> Void) {
 let payLoad = ((((userInfo as NSDictionary).value(forKey: "aps") as! NSDictionary).value(forKey: "alert") as! NSDictionary).value(forKey: "body") as! NSString)
	 	 	let push =  BMSPushClient.sharedInstance
			let respJson = (userInfo as NSDictionary).value(forKey: "payload") as! String
 let data = respJson.data(using: String.Encoding.utf8)
 let jsonResponse:NSDictionary = try! JSONSerialization.jsonObject(with: data! , options: JSONSerialization.ReadingOptions.allowFragments) as! NSDictionary
 let messageId:String = jsonResponse.value(forKey: "nid") as! String
		push.sendMessageDeliveryStatus(messageId: messageId) { (res, ss, ee) in
       completionHandler(UIBackgroundFetchResult.newData)
	}
	}
	```
			{: codeblock}


### 傳送基本推送通知
{: #send}

開發應用程式之後，您可以傳送基本推送通知。

若要傳送基本推送通知，請完成下列步驟：

1. 選取**傳送通知**，然後選擇**傳送至**選項來編寫訊息。支援的選項是**依標籤的裝置**、**裝置 ID**、**使用者 ID**、**Android 裝置**、**iOS 裝置**、**Web 通知**及**所有裝置**。  
**附註**：當您選取**所有裝置**選項時，所有已訂閱 {{site.data.keyword.mobilepushshort}} 的裝置都會接收到通知。![通知畫面](images/tag_notification.jpg)

2. 在**訊息**欄位中，編寫訊息。視需要選擇配置選用設定。
3. 按一下**傳送**。
3. 驗證您的裝置已接收到通知。

下列影像顯示處理 {{site.data.keyword.mobilepushshort}} iOS 裝置的警示框。

![iOS 上的前景推送通知](images/iOS_Screenshot.jpg) 

#### 傳送通知的選用設定
{: #send_ios_otpional_setting}

您可以進一步自訂 {{site.data.keyword.mobilepushshort}} 設定，以將通知傳送給 iOS 裝置。支援下列選用自訂選項。


- **徽章**：指出應用程式徽章上所顯示的號碼。預設值是零 (0)，而且這不會顯示徽章。 
- **音效**：指出要在收到通知時播放的音效短片。支援預設值或應用程式中所組合的音效資源名稱。
- **其他有效負載**：指定通知的自訂有效負載值。

### 啟用互動式通知
{: #enb_snd_ios_otpional}

現在，您可以使用更多詳細資料強化您的 iOS 通知，例如透過啟用互動式通知來新增影像、地圖或回應按鈕。這樣可提供更多環境定義給客戶，並且能夠立即採取動作而不需要離開現行環境定義。  

若要啟用互動式通知，請使用下列程式碼：



- 定義按鈕動作
	```
		let actionOne = BMSPushNotificationAction(identifierName: "ACCEPT", buttonTitle: "Accept", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
 let actionTwo = BMSPushNotificationAction(identifierName: "DECLINE", buttonTitle: "Decline", isAuthenticationRequired: false, defineActivationMode: UIUserNotificationActivationMode.background)
```
		{: codeblock}


- 定義按鈕的種類
	```
		let category = BMSPushNotificationActionCategory(identifierName: "category", buttonActions: [actionOne, actionTwo])
	```
		{: codeblock}


- 更新登錄以包括按鈕
	```
		Pass the defined category into iOS BMSPushClientOptions
		let notificationOptions = BMSPushClientOptions(categoryName: [category])
		let push = BMSPushClient.sharedInstance
		push.initializeWithAppGUID(appGUID: "APP-GUID-HERE", clientSecret:"CLIENT-SECRET-HERE", options: notificationOptions)
	```
		{: codeblock}

若要傳送互動式通知，請完成下列步驟：

1. 在「組合」區段的「傳送至」下拉清單，選取 **iOS 裝置**。
2. 輸入您可能想要傳送的通知訊息。
3. 在「選用性設定」區段中，選取**行動**然後按一下 **iOS**。
4. 在「類型」下拉清單中，選取**混合**。
5. 在「種類」欄位中，指定您已在應用程式定義的通知類型。 

![iOS 的互動式通知](images/push_ios_notification_interactive.jpg) 

#### 後續步驟
{: #next_steps_02}

順利設定基本通知之後，您就可以配置標籤型通知及進階選項。

將這些 Push Notifications Service 特性新增至您的應用程式。
若要使用標籤型通知，請參閱[標籤型通知](c_tag_basednotifications.html)。若要使用進階通知選項，請參閱[啟用進階推送通知](t_advance_badge_sound_payload.html)。
