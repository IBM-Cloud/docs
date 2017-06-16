---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-13"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 檢視儀表板及報告
{: #DRA_toolchain_reports}

{{site.data.keyword.DRA_short}} 提供有關專案的豐富可採取動作資訊。
{:shortdesc}

## {{site.data.keyword.DRA_short}} 儀表板    
{: #DI_toolchain_dashboards}

{{site.data.keyword.DRA_short}} 提供可顯示 Bluemix 組織效能相關資訊的儀表板。若要查看它們，請在開啟 {{site.data.keyword.DRA_short}} 之後，按一下**建置驗證**或**部署驗證**。

儀表板會自動移入管線的 {{site.data.keyword.DRA_short}} 測試工作中的最新資訊。按一下儀表板內的元素，以取得其相關資訊。

### 建置中的關鍵績效指標    
{: #DI_key_performance_indicators}

**建置驗證**頁面所含的三個圖形包含所選取開發分支性能的相關資訊：

<table>
<thead>
<tr>
<th>圖形</th>
<th>說明</th>
</tr>
</thead>

<tbody>
<tr>
<td>最新建置</td>
<td>與最近建置總數相較之下的已完成最近建置數目。</td>
</tr>
<tr>
<td>測試</td>
<td>與測試總數相較之下的已通過測試數目。</td>
</tr>
<tr>
<td>程式碼涵蓋面</td>
<td>測試所呼叫的程式碼陳述式及函數的百分比。</td>
</tr>
</tbody></table>

## 檢視決策報告    
{: #DI_decision_reports}

管線執行之後，{{site.data.keyword.DRA_short}} 會開始收集並分析其測試結果，以建立基準線。每個後續執行的資料，會加以收集並將與先前的結果進行比較。決策閘道使用此資料來判斷何時停止部署。 

若要從管線檢視閘道的決策報告，請完成下列步驟：

   1. 在包含要檢查之閘道的階段上，按一下**檢視日誌與歷程**。

   2. 從階段的工作視窗中，按一下閘道的名稱。

   3. 在日誌視圖中，尋找 `Check {{site.data.keyword.DRA_short}} report here` 訊息，然後按一下提供的鏈結來開啟報告。
