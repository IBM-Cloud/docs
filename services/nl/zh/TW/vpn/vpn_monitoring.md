---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 監視狀態和資料流量流程
{: #monitor}  
*前次更新：2016 年 3 月 17 日*  

使用監視特性可檢視內部部署或 SoftLayer 伺服器 VPN 閘道與 {{site.data.keyword.vpn_short}} 閘道之間的連線狀態和資料流量流程速率。
{:shortdesc}  
##在服務儀表板上監視
{: #dashboard}

選取**監視**標籤，可檢視下列連線統計資料。

* **連線狀態：**內部部署或 SoftLayer 伺服器 VPN 閘道與 IBM VPN 閘道之間的 VPN 連線狀態。值：1=UP、-1=DOWN 
* **出埠資料流量速率（以「位元組/秒」和「封包/秒」為單位）：**從 IBM VPN 閘道到內部部署或 SoftLayer 伺服器 VPN 閘道的資料流量速率。  
* **入埠資料流量速率（以「位元組/秒」和「封包/秒」為單位）：**從內部部署或 SoftLayer 伺服器 VPN 閘道到 IBM VPN 閘道的資料流量速率。  

監視統計資料會以圖形顯示，其中包含過去 48 小時的資料。這些圖形每 20 分鐘會自動更新一次。不過，只要離開後重新返回監視標籤，即可隨時提取最新資料。

**附註：**這些圖形使用世界標準時間 (UTC)，而非當地時間。  
##在 Logmet 上監視
{: #logmet}

使用 [Logmet](https://logmet.{DomainName}) 可檢視詳細的連線統計資料。 

1. 使用您的 Bluemix 認證以及建立 IBM VPN 服務實例的空間和組織名稱進行登入。  
2. 選取右上方的資料夾圖示 (![](images/folder.png))。
3. 從儀表板清單中選取 **VPN 服務監視**，以檢視圖形。這些圖形會使用當地時間。  

**附註：**您必須在 IBM VPN 服務儀表板上至少選取一次**監視**標籤才能向 Logmet 傳送查詢，進而在 Logmet 中建立 VPN 服務儀表板。建立 VPN 連線之後，Logmet 需要最多 10 分鐘來顯示連線統計資料。


