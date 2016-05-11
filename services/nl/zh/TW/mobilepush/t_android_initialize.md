---

copyright:
 years: 2015, 2016

---

# 起始設定 Push SDK for Android 應用程式
{: #android_initialize}

放置起始設定碼的一般位置位於 Android 應用程式之主要活動的 onCreate 方法中。

按一下「Bluemix 應用程式儀表板」中的**行動式選項**鏈結，以取得應用程式的路徑及應用程式 GUID。將這些值用於您的路徑和應用程式 GUID。修改程式碼 Snippet，以使用 Bluemix 應用程式 appRoute 及 appGUID 參數。


##起始設定 Core SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

指定指派給您在 Bluemix 上所建立之伺服器應用程式的路徑。

**AppGUID**

指定指派給您在 Bluemix 上所建立之應用程式的唯一索引鍵。此值區分大小寫。

**bluemixRegionSuffix**

指定管理應用程式的位置。您可以使用下列三個值的其中一個：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

##起始設定 Client Push SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
