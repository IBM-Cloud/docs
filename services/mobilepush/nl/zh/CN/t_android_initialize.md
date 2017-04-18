---

copyright:
 years: 2015, 2016

---

# 为 Android 应用程序初始化推送 SDK
{: #android_initialize}

在 Android 应用程序中，通常会将初始化代码放置在主活动的 onCreate 方法中。

单击 Bluemix 应用程序仪表板中的**移动选项**链接，以获取应用程序路径和应用程序 GUID。将这些值用于您的路径和应用程序 GUID。修改代码片段以使用 Bluemix 应用程序的 appRoute 和 appGUID 参数。


## 初始化核心 SDK

```
// Initialize the SDK for Java (Android) with IBM Bluemix AppGUID and route
BMSClient.getInstance().initialize(getApplicationContext(), "applicationRoute","applicationGUID", bluemixRegion:"Location where your app Hosted");
```


**appRoute**

指定分配给在 Bluemix 上创建的服务器应用程序的路径。

**AppGUID**

指定分配给在 Bluemix 上创建的应用程序的唯一键。此值区分大小写。

**bluemixRegionSuffix**

指定托管应用程序的位置。可以使用以下三个值中的一个值：

- BMSClient.REGION_US_SOUTH
- BMSClient.REGION_UK
- BMSClient.REGION_SYDNEY

## 初始化客户机推送 SDK

```
//Initialize client Push SDK for Java
MFPPush push = MFPPush.getInstance();
push.initialize(getApplicationContext());
```
