---

copyright:
  years: 2016, 2017
lastupdated:  "2017-01-17"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

{{site.data.keyword.mobilefoundation_long}} 可加速設定 {{site.data.keyword.mfp_full}} 環境，您可以從該環境中開發、測試及操作企業行動應用程式。
{{site.data.keyword.mobilefoundation_short}} 在兩個不同的服務方案中提供：Developer 和 Professional 1 Application。
{:shortdesc}

<!-- The Professional 1 Application plan allows the {{site.data.keyword.mobilefoundation_short}} server to be deployed on a scalable container group.--> 使用 Professional 1 Application 方案，即可管理在任何或所有支援作業平台（例如 Android、iOS、Windows 或行動 Web）上建置的單一應用程式。Developer 方案<!-- does not support {{site.data.keyword.mobilefoundation_short}} deployment on a container group with more than 1 node. This plan -->主要適用於開發及測試。



## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Developer 方案

建立 {{site.data.keyword.mobilefoundation_short}}: Developer 的實例之後，只要按幾下，就可以開始建置行動通道。

*	若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

  `基本伺服器實例包括單一節點及 1 GB 的記憶體。`

* 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p1.html#using_mfs_advanced_p1)。

## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 方案

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務的實例之後，只要完成下列步驟，就可以開始建置行動通道。

1.  連接至 {{site.data.keyword.Bluemix_notm}} 上的現有 {{site.data.keyword.dashdbshort}} for Transactions 服務。

    1.  選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Organization`。

    + 從所選取 `Organization` 中可用的空間清單，選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Space`。

    + 選取 {{site.data.keyword.dashdbshort_notm}} `Service Name` 和 `Credentials`，以連接至現有的 {{site.data.keyword.dashdbshort_notm}} 服務實例。

    + 按一下**測試連線**，以測試與所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務實例的連線。

    + 按一下**新增**，接著在要求確認所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務的蹦現視窗上按一下**繼續**。此動作會在配置的 {{site.data.keyword.dashdbshort_notm}} 資料庫服務實例中建立必要的表格。

    **附註：**將 {{site.data.keyword.dashdbshort_notm}} 連線新增至 {{site.data.keyword.mobilefoundation_short}} 實例之後，即無法進行變更。

2.  建立及啟動伺服器。

    * 若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

      `基本伺服器實例包括單一節點及 1 GB 的記憶體。`

    * 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p2.html#using_mfs_advanced_p2)。

## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Developer Pro 方案

在建立 {{site.data.keyword.mobilefoundation_short}}: Developer Pro 服務的實例之後，您可以完成下列步驟來開始建置行動通道。

  1.  連接至 {{site.data.keyword.Bluemix_notm}} 上的現有 {{site.data.keyword.dashdbshort}} for Transactions 服務。

      1.  選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Organization`。

      + 從所選取 `Organization` 中可用的空間清單，選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Space`。

      + 選取 {{site.data.keyword.dashdbshort_notm}} `Service Name` 和 `Credentials`，以連接至現有的 {{site.data.keyword.dashdbshort_notm}} 服務實例。

      + 按一下**測試連線**，以測試與所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務實例的連線。

      + 按一下**新增**，接著在要求確認所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務的蹦現視窗上按一下**繼續**。此動作會在配置的 {{site.data.keyword.dashdbshort_notm}} 資料庫服務實例中建立必要的表格。

      **附註：**將 {{site.data.keyword.dashdbshort_notm}} 連線新增至 {{site.data.keyword.mobilefoundation_short}} 實例之後，即無法進行變更。

  2.  建立及啟動伺服器。

      * 若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

      * 此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：

          - 具有 1 GB 記憶體的單一節點。此大小就足以進行開發、控管測試活動及小規模正式作業工作負載。

          -	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

      * 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p3.html#using_mfs_advanced_p3)。

## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 方案

在建立 {{site.data.keyword.mobilefoundation_short}}: Professional Per Capacity 服務的實例之後，您可以完成下列步驟來開始建置行動通道。

  1.  連接至 {{site.data.keyword.Bluemix_notm}} 上的現有 {{site.data.keyword.dashdbshort}} for Transactions 服務。

      1.  選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Organization`。

      + 從所選取 `Organization` 中可用的空間清單，選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `Space`。

      + 選取 {{site.data.keyword.dashdbshort_notm}} `Service Name` 和 `Credentials`，以連接至現有的 {{site.data.keyword.dashdbshort_notm}} 服務實例。

      + 按一下**測試連線**，以測試與所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務實例的連線。

      + 按一下**新增**，接著在要求確認所選取 {{site.data.keyword.dashdbshort_notm}} for Transactions 服務的蹦現視窗上按一下**繼續**。此動作會在配置的 {{site.data.keyword.dashdbshort_notm}} 資料庫服務實例中建立必要的表格。

      **附註：**將 {{site.data.keyword.dashdbshort_notm}} 連線新增至 {{site.data.keyword.mobilefoundation_short}} 實例之後，即無法進行變更。

  2.  建立及啟動伺服器。

      * 若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

      * 此選項會使用下列設定佈建 {{site.data.keyword.mfserver_long_notm}}：
          -  2 個節點，各具有 1 GB 記憶體。此大小適合進行開發、控管測試活動及小規模正式作業工作負載。

          -	自動產生 `username` 及 `password`。您可以在伺服器啟動並執行時存取它們。

      * 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p4.html#using_mfs_advanced_p4)。

移至[使用 Mobile Foundation 服務來設定 MobileFirst Server<!-- on IBM Containers--> ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/bluemix/using-mobile-foundation/ "外部鏈結圖示"){: new_window}，來進一步瞭解如何開始使用 {{site.data.keyword.mobilefoundation_short}}。

##  已知限制

* {{site.data.keyword.mobilefoundation_short}} 服務使用者介面不會以使用者選取的語言環境特有型樣來顯示數字。


# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

*	[IBM MobileFirst Platform Foundation 8.0.0 版產品說明文件 ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html "外部鏈結圖示"){: new_window}
*	[IBM MobileFirst Platform Developer Center ![外部鏈結圖示](../../icons/launch-glyph.svg "外部鏈結圖示")](https://mobilefirstplatform.ibmcloud.com "外部鏈結圖示"){: new_window}
