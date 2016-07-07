---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 開始使用 {{site.data.keyword.mobilefoundation_short}}
{: #gettingstartedtemplate}

*前次更新：2016 年 6 月 15 日*
{: .last-updated}

{{site.data.keyword.mobilefoundation_long}} 可加速設定 {{site.data.keyword.mfp_full}} 環境，您可以從該環境中開發、測試及操作企業行動應用程式。
{{site.data.keyword.mobilefoundation_short}} 在兩個不同的服務方案中提供：Developer 和 Professional 1 Application。
{:shortdesc}

Professional 1 Application 方案容許 {{site.data.keyword.mobilefoundation_short}} 伺服器部署在可擴充的容器群組。使用 Professional 1 Application 方案，便可以管理在任何或所有支援作業平台（例如 Android、iOS、Windows 或行動 Web）建置的單一應用程式。Developer 方案不支援在具有多個節點的容器群組上部署 {{site.data.keyword.mobilefoundation_short}}。此方案最適合開發及測試。

## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Developer 方案

建立 {{site.data.keyword.mobilefoundation_short}}: Developer 的實例之後，只要按幾下，就可以開始建置行動通道。

*	若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

  `基本伺服器實例包括單一節點、1 GB 的記憶體及 64 GB 的儲存空間容量。`

* 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p1.html#using_mfs_advanced_p1)。

## 開始使用 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 方案

建立 {{site.data.keyword.mobilefoundation_short}}: Professional 1 Application 服務的實例之後，只要完成下列步驟，就可以開始建置行動通道。

1.  連接至 {{site.data.keyword.Bluemix_notm}} 上的現有 {{site.data.keyword.dashdbshort}}: Enterprise Transactional 服務。

    1.  從現行`組織`中可用的空間清單，選取 {{site.data.keyword.dashdbshort_notm}} 服務實例所存在的 {{site.data.keyword.Bluemix_notm}} `空間`。

    2.  選取 {{site.data.keyword.dashdbshort_notm}} `服務名稱`和`認證`，以連接至現有的 {{site.data.keyword.dashdbshort_notm}} 服務實例。

    3.  按一下**測試連線**，以測試與所選取 {{site.data.keyword.dashdbshort_notm}}: Enterprise Transactional 服務實例的連線。

    4.  按一下**新增**，接著在要求確認所選取 {{site.data.keyword.dashdbshort_notm}} 服務的蹦現視窗上按一下**繼續**。此動作會在配置的 {{site.data.keyword.dashdbshort_notm}} 資料庫服務實例中建立必要的表格。

2.  建立及啟動伺服器。

    * 若要使用預設配置建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**啟動基本伺服器**。

      `基本伺服器實例包括單一節點、1 GB 的記憶體及 64 GB 的儲存空間容量。`

    * 若要使用拓蹼、安全及其他伺服器配置的進階配置來建立 {{site.data.keyword.mobilefirst_notm}} 伺服器實例，請按一下**使用進階配置啟動伺服器**。如需相關資訊，請參閱[設定進階配置](c_using_mfs_p2.html#using_mfs_advanced_p2)。

移至[使用 Mobile Foundation 服務在 IBM Containers 上設定 MobileFirst Server](https://mobilefirstplatform.ibmcloud.com/tutorials/en/foundation/8.0/ibm-containers/using-mobile-foundation/)，以進一步瞭解如何開始使用 {{site.data.keyword.mobilefoundation_short}}。

# 相關鏈結
{: #rellinks}

## 相關鏈結
{: #general}

*	[IBM MobileFirst Platform Foundation 8.0.0 版產品說明文件](https://www.ibm.com/support/knowledgecenter/SSHS8R_8.0.0/wl_welcome.html){: new_window}
*	[IBM MobileFirst Platform 開發人員中心](https://mobilefirstplatform.ibmcloud.com){: new_window}
