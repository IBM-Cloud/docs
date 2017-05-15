---

copyright:
  years: 2015, 2016
  
lastupdated: "2016-08-12"

---



{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}


# 服務疑難排解
{: #services}


{{site.data.keyword.Bluemix}} 服務問題可能包括刪除服務實例時發生的閘道逾時錯誤。您可以遵循一些簡單的步驟，從這些問題中回復。
{:shortdesc}

## 刪除服務實例時發生服務分配管理系統錯誤
{: #ts_service_broker}

嘗試刪除已從雲端控制器刪除的服務實例時，您可能會收到錯誤訊息。
{:shortdesc}

嘗試刪除服務實例時，您會看到下列服務分配管理系統錯誤訊息：
{: tsSymptoms}
`閘道逾時`

如果服務實例已從雲端控制器刪除，則會發生此問題。
{: tsCauses}

請建立具有相同服務名稱的服務實例，然後將它連結至應用程式。然後，您就可以刪除服務實例以及使用該服務的應用程式。   
{: tsResolve}
