---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 整合 {{site.data.keyword.DRA_short}} 與 Jenkins
{: #toolchain_configure_jenkins}

定義監視 {{site.data.keyword.DRA_full}} 的原則之後，下一步是將 {{site.data.keyword.DRA_short}} 新增至工具鏈，然後配置持續交付管線。
{:shortdesc}

<!--##Configuring a Jenkins project-->

您可以將 {{site.data.keyword.DRA_short}} 整合成一個 Jenkins 專案或跨數個相關的 Jenkins 專案。這可讓您在 {{site.data.keyword.DRA_short}} 儀表板上設定品質閘道，以及接收建置品質資料。

## 必要條件    
{: #DI_jenkins_prereqs}

* 您必須存取本端 Jenkins 專案，或正在執行 Jenkins 專案的伺服器。

## 安裝 {{site.data.keyword.DRA_short}} 外掛程式
{: #DI_jenkins_install}

若要在 Jenkins 專案中安裝 {{site.data.keyword.DRA_short}} 外掛程式，請遵循下列步驟：

  1. [從外掛程式的 GitHub 儲存庫中，下載 IBM DevOps Insight 外掛程式安裝檔案 (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi)。
  2. 在 Jenkins 安裝中，按一下**管理 Jenkins**，選取**管理外掛程式**，然後按一下**進階**標籤。
  3. 按一下**選擇檔案**，然後選取 DevOps Insight 外掛程式安裝檔案。
  4. 按一下**上傳**。
  5. 重新啟動 Jenkins，並驗證已安裝外掛程式。

## 整合 {{site.data.keyword.DRA_short}} 與 Jenkins    
{: #DI_jenkins_integrate}

在安裝外掛程式之後，但將 {{site.data.keyword.DRA_short}} 整合至 Jenkins 安裝之前，請移至[控制中心](https://control-center.stage1.ng.bluemix.net/)，然後至少建立一個原則。

針對每一個您已擁有且想要在其中使用 {{site.data.keyword.DRA_short}} 的工作，請執行下列動作：

1. 新增以下類型的後建置動作：**將建置資訊發佈至 {{site.data.keyword.DRA_short}}**、**將部署資訊發佈至 {{site.data.keyword.DRA_short}}** 或**將測試結果發佈至 {{site.data.keyword.DRA_short}}**。特定類型應該符合工作類型（建置、部署或測試）。完成必要欄位。
  * 在「認證」欄位中，選擇 Bluemix ID 及密碼。如果它們未以 Jenkins 儲存，請按一下**新增**按鈕進行新增及儲存。
  * 在「建置工作名稱」欄位中，指定與 Jenkins 完全相同的建置工作名稱。如果建置與測試工作一起發生，請讓此欄位保留為空欄位。如果建置工作是在 Jenkins 外部發生，請勾選**將在 Jenkins 外部完成建置**，然後指定建置號碼及建置 URL。
  * 針對「結果檔案位置」欄位，指定結果檔案的位置。如果測試未產生結果檔案，請讓此欄位保留為空欄位。外掛程式將根據現行測試工作的狀態來上傳預設結果檔案。
3. *選用項目*：如果您要測試工作中的 DRA 原則閘道來控制下游部署工作，請新增類型為 **DevOps 風險分析閘道**的另一個後建置動作，並完成必要欄位。如果測試工作無法符合關聯的原則，則閘道將造成下游工作無法執行。
4. 按一下**套用**，然後按一下**儲存**。

您可以按一下專案頁面中的**立即建置**，以執行專案。

建置執行之後，請移至[控制中心](https://control-center.stage1.ng.bluemix.net/)，以檢查儀表板中的建置狀態。如果您已配置原則閘道，則也可以在現行建置的「狀態」頁面上查看 {{site.data.keyword.DRA_short}} 結果。
