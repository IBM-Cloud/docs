---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 建立適用於 Android 的未連結 {{site.data.keyword.mobilepushshort}} Service
{: #create_android_unbound}
前次更新：2017 年 1 月 11 日
{: .last-updated}

建立 {{site.data.keyword.mobilepushshort}} Service 實例。您可以使用 {{site.data.keyword.mobilepushshort}} Service 實例，而不連結至任何後端應用程式。

1. 將 {{site.data.keyword.mobilepushshort}} Service 實例連結至 Bluemix 應用程式。連結時，您可以看到所有與服務相關的詳細資料都會以 JSON 格式儲存在 VCAP_SERVICES 環境變數中。 

![連結 Push Notification Service](images/unbound_1.jpg)
 2. 按一下**連結**，然後選擇要連結的 {{site.data.keyword.mobilepushshort}} Service 實例。將應用程式連結至 {{site.data.keyword.mobilepushshort}} Service 時，服務的資訊會以 JSON 格式儲存在應用程式的 VCAP_SERVICES 環境變數中。例如： 
```
 	{
    "imfpush_Dev": [
   {
     "name": "myname_sampleUnbound",
         "label": "imfpush_Dev",
         "plan": "Basic",
         "credentials": null
      }
    ]
    }
```
	{: codeblock}
