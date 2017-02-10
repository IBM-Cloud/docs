---

copyright:
 years: 2015, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 针对 Android 创建未绑定 {{site.data.keyword.mobilepushshort}} 服务
{: #create_android_unbound}
上次更新时间：2017 年 1 月 11 日
{: .last-updated}

创建 {{site.data.keyword.mobilepushshort}} 服务实例。您可以在未绑定任何后端应用程序的情况下使用 {{site.data.keyword.mobilepushshort}} 服务实例。

1. 将 {{site.data.keyword.mobilepushshort}} 服务实例绑定到 Bluemix 应用程序。在绑定时，您将能够看到与该服务相关的所有详细信息以 JSON 格式存储在 VCAP_SERVICES 环境变量中。 

![绑定 Push Notification 服务](images/unbound_1.jpg)
 2. 单击**绑定**并选择要绑定的 {{site.data.keyword.mobilepushshort}} 服务实例。当应用程序绑定到 {{site.data.keyword.mobilepushshort}} 服务时，有关该服务的信息将以 JSON 格式存储在应用程序的 VCAP_SERVICES 环境变量中。例如： 
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
