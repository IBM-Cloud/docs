---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#{{site.data.keyword.geospatialshort_Geospatial}} 疑難排解 
{: #ts_geospatial}


取得在 {{site.data.keyword.Bluemix_short}} 上使用 {{site.data.keyword.geospatialshort_Geospatial}} 的幾個常見問題的回答。
{:shortdesc}

##當我停止應用程式時，服務仍在監視地區
{: #stop-monitoring}


停止應用程式並不會自動停止 {{site.data.keyword.geospatialshort_Geospatial}}。
{:shortdesc}


您已停止使用 {{site.data.keyword.geospatialshort_Geospatial}} 的應用程式，但在服務管理儀表板上看到服務仍在監視應用程式中指定的地區。
{: tsSymptoms}


如果您停止應用程式，您的 {{site.data.keyword.geospatialshort_Geospatial}} 服務實例將繼續執行。服務會繼續監視地區，直到您停止服務為止，而不論您的應用程式是否在執行中。
{: tsCauses}


請從服務管理儀表板停止 {{site.data.keyword.geospatialshort_Geospatial}}。或者，您可以使用 REST API 修改應用程式以停止服務，然後將您的變更推送回 {{site.data.keyword.Bluemix_short}}。
{: tsResolve}

##服務正在監視我未在應用程式中指定的地區
{: #unspecified-region}



如果您有多個應用程式連結至相同的服務實例，則另一個應用程式可能已新增這些地區。
{:shortdesc}



當您在服務管理儀表板上檢視 {{site.data.keyword.geospatialshort_Geospatial}} 實例時，您看到它正在監視的地區比其中一個應用程式中所指定地區還要多。
{: tsSymptoms}

{{site.data.keyword.geospatialshort_Geospatial}} 的單一實例會監視連結到它的所有應用程式的地區。這表示，當您檢視服務管理儀表板時，將看到所有應用程式所指定之地區的資訊。
{: tsCauses}

若要停止 {{site.data.keyword.geospatialshort_Geospatial}} 不再監視特定地區，請執行下列動作：

1. 停止服務。
2. 修改應用程式以移除那些地區。
3. 將應用程式推送回 {{site.data.keyword.Bluemix_short}}。
{: tsResolve}


##從服務管理儀表板進行疑難排解
{: #dashboard}

在您對應用程式進行疑難排解時，可以移至服務管理儀表板檢查服務實例的狀態。如果它不在處理資料，您可能可以藉由停止並重新啟動服務來修正問題。
{:shortdesc}

{{site.data.keyword.geospatialshort_Geospatial}} 服務實例的狀態與應用程式的狀態是分開的，數個應用程式可以連結至相同的服務實例。 

服務管理儀表板提供 {{site.data.keyword.geospatialshort_Geospatial}} 狀態的相關資訊，而不是連結到它的應用程式相關資訊。服務實例與應用程式的個別狀態，表示如果您停止應用程式，您的 {{site.data.keyword.geospatialshort_Geospatial}} 服務實例會繼續執行。服務會繼續監視您選擇的地區，直到您移除它們為止，而不論您的應用程式是否在執行中。
