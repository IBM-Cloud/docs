---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-09"

---

<!-- Attribute definitions --> 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

#服務管理儀表板
{: #service-dashboard}


您可以從服務管理儀表板看到 {{site.data.keyword.geospatialshort_Geospatial}} 服務實例的狀態，以及停止或重新啟動它。您可以按一下
{{site.data.keyword.geospatialshort_Geospatial}} 儀表板上的 {{site.data.keyword.geospatialshort_Geospatial}} 磚來到達服務管理儀表板。
如果您使用範例應用程式，然後服務實例到達事件限制並停止，您可以重新啟動服務。
停止服務會移除事件限制。它會繼續接收事件，直到您停止服務為止。服務管理儀表板也會顯示服務實例的狀態和統計資料。
{:shortdesc}

##{{site.data.keyword.geospatialshort_Geospatial}} 地區檢查

{{site.data.keyword.geospatialshort_Geospatial}} 會從物聯網監視移動中的裝置。
每台受監視的裝置都會傳送裝置訊息，其中包含唯一 ID 及其現行位置（包含緯度和經度）。會針對每個已定義的地理區域座標來檢查裝置位置。
然後服務會在裝置進入、離開或「停留在」特定地區時產生事件。


地區檢查用來作為測量 {{site.data.keyword.geospatialfull}} 用量的單位。針對每則裝置訊息，如果有針對該地區指定偵測進入、離開或同時偵測進入與離開，便會執行一次地區檢查。
針對每則裝置訊息，如果有針對該地區指定偵測停留，便會執行一次地區檢查。
如果未定義任何地區，則針對每則裝置訊息，會計數一次地區檢查，就彷彿有 1 個地區一樣。這表示，如果您有 100 個地區定義了檢查進入、離開和停留，那麼單一則裝置訊息會產生
200 次地區檢查。
