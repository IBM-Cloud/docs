---

 

copyright:

  years: 2015, 2016

 

---

{:shortdesc: .shortdesc}

# VCAP 服務

*前次更新：2016 年 3 月 15 日*


VCAP_SERVICES 環境變數是含有資訊的 JSON 物件，而您可以使用這項資訊來與 {{site.data.keyword.Bluemix_notm}} 中的服務實例互動。
{:shortdesc}


## 擷取 VCAP_SERVICES 環境變數的值
{:retrieving}

VCAP_SERVICES 環境變數是含有資訊的 JSON 物件，而您可以使用這項資訊來與
{{site.data.keyword.Bluemix_notm}} 中的服務實例互動。這項資訊包括服務實例的服務實例名稱、認證及連線 URL。將應用程式連結至 {{site.data.keyword.Bluemix_notm}} 中的服務實例時，會將這些值移入 VCAP_SERVICES 環境變數中。

只有在將服務實例連結至應用程式時，才能使用 VCAP_SERVICES 環境變數的值。您可以使用下列指令來檢視應用程式環境變數：
```
cf env APP_NAME
```
