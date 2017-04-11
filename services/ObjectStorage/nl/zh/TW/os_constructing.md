---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 建構 {{site.data.keyword.objectstorageshort}} URL 以使用 Swift REST API

您可以搭配使用 Swift REST API 與指令行用戶端介面（例如 cURL），或是從應用程式中呼叫 API。
{: shortdesc}


如需 {{site.data.keyword.objectstorageshort}} REST API 選項及範例的綜合性清單，請參閱 <a href="http://developer.openstack.org/api-ref-objectstorage-v1.html" target="_blank">OpenStack Swift API 完整參考資訊 <img src="../../icons/launch-glyph.svg" alt="外部鏈結圖示"></a>。



在可以組合您的 URL 之前，必須使用 Keystone [鑑別](/docs/services/ObjectStorage/os_authenticate.html)您的服務實例。請務必注意您的型錄回應。它將類似下列範例。

```
{
  "id" : "4207049680fa4effbecd044c7448a8cb",
  "region" : "dallas",
  "region_id" : "dallas",
  "url" : "https://dal.objectstorage.open.softlayer.com/v1/AUTH_4abf7d7bac2c4eda89c03dd3afa7a0a3",
  "interface" : "public"
},
```
{: codeblock}


請將您的容器和物件的名稱空間新增至 {{site.data.keyword.objectstorageshort}} URL 的結尾，如下圖所示。

![範例影像中所顯示的 {{site.data.keyword.objectstorageshort}} URL 部分](images/Swift_URL.png)

圖 1. {{site.data.keyword.objectstorageshort}} URL 範例
