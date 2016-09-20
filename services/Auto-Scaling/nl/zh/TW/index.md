{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 開始使用 {{site.data.keyword.autoscaling}} 服務
{: #autoscaling}

*前次更新：2015 年 1 月 18 日*

在 {{site.data.keyword.Bluemix_notm}} 中，您可以自動管理應用程式產能。使用 {{site.data.keyword.autoscalingfull}} 服務可自動提高或降低應用程式的運算能力。
應用程式實例的數目會根據您定義的 {{site.data.keyword.autoscaling}} 原則動態調整。
{:shortdesc} 

## 使用 {{site.data.keyword.Bluemix_notm}} 中的 {{site.data.keyword.autoscaling}} 服務
{: #as-service}

若要使用 {{site.data.keyword.autoscaling}} 服務，請完成下列步驟：


1. 在 {{site.data.keyword.Bluemix_notm}} 的「儀表板」上，按一下*新增服務或 API*，然後從服務型錄中的 DevOps 區段選取 {{site.data.keyword.autoscaling}} 服務。會顯示新的視窗，以呈現 {{site.data.keyword.autoscaling}} 服務的概觀。
2. 選取您要連結 {{site.data.keyword.autoscaling}} 服務的應用程式，然後按一下*建立*。<br/>
*請記住：*您只能連結一個 {{site.data.keyword.autoscaling}} 服務至應用程式。如果應用程式已經與另一個 {{site.data.keyword.autoscaling}} 服務連結，在此步驟中請不要選取該應用程式。
否則，您將取得 CWSCV2004E 錯誤。<br/>即會顯示「重新編譯打包應用程式」視窗。
3. 在「重新編譯打包應用程式」視窗中，按一下*重新編譯打包*以重新編譯打包您的應用程式，然後才使用您剛新增的 {{site.data.keyword.autoscaling}} 服務。完成重新編譯打包應用程式之後，您可以開始為您的應用程式配置
						{{site.data.keyword.autoscaling}} 服務。
4. 若要為應用程式配置 {{site.data.keyword.autoscaling}}，請在 {{site.data.keyword.Bluemix_notm}} 使用者介面中，按一下 {{site.data.keyword.autoscaling}} 服務連結至的應用程式。
5. 在「儀表板」上的服務區段，按一下 *Auto-Scaling* 圖示。

6. 如果尚未完成，請按一下*建立 {{site.data.keyword.autoscaling}} 原則*來定義應用程式的 {{site.data.keyword.autoscaling}} 原則。

現在您可以配置 {{site.data.keyword.autoscaling}} 原則、查看度量統計資料，或檢視應用程式的調整歷程。
<dl>
<dt>原則配置</dt>
<dd>您可以使用本節來建立或編輯調整規則，以指定要觸發特定調整活動的狀況。<ul>
<li> 若為 Liberty for Java™ 應用程式，您可以定義 JVM 資料堆、記憶體及產量的調整規則。
<li> 若為 Node.js 應用程式，您可以定義記憶體的調整規則。<li> 若為
Ruby 應用程式，您可以定義記憶體的調整規則。</ul>
*附註：*您可以針對多個度量值類型定義多個調整規則。不過，{{site.data.keyword.autoscaling}} 服務不會偵測調整原則之間的衝突。
在您定義調整原則時，必須確定多個調整規則不會彼此衝突。
否則，您可能看到實例總數上下變動，因為應用程式前 1 分鐘可能橫向縮編，但在下一分鐘卻橫向擴充。<br/><br/>
如果應用程式的工作量在尖峰時間與空閒時間大幅變動，您可以建立調整排程來處理不同時段的不同調整需求。請使用排程中指定的實例計數下限參數，來定義應用程式實例數的基準線，而動態調整規則仍然適用於排程，可以觸發橫向縮編與橫向擴充動作。</dd>
<dt>度量值統計資料</dt>
<dd>顯示您的應用程式實例的度量值統計資料。
您可以看到平均統計資料，並選取特定的實例以查看其統計資料。
</dd>
<dt>調整歷程</dt>
<dd>顯示應用程式的調整歷程。<ul>
<li> 過去一星期：顯示過去一星期的調整歷程。<li> 過去一個月：顯示過去一個月的調整歷程。
<li> 自訂範圍：您可以設定時段。</ul>
*附註：*您可以選取「調整狀態」或「橫向縮編/擴充」來過濾歷程記錄。</dd>
</dl>


## {{site.data.keyword.autoscaling}} 服務的原則欄位
{: #policyfields}

| 欄位名稱  | 說明 |
|-------------|----------------------|
|*允許的實例計數上限* |	可以啟動的應用程式實例數目上限。
如果應用程式實例的現行數目等於此值，{{site.data.keyword.autoscaling}} 服務不會再橫向擴充應用程式。
預設實例計數下限：可以啟動的應用程式實例數目下限。如果實例數目等於此值，{{site.data.keyword.autoscaling}} 服務不會再橫向縮編應用程式。
 |
| *度量值類型*	| 	可以監視的受支援度量值類型。
如需相關資訊，請參閱表格 2。 |
| *橫向擴充* | 	指定觸發橫向擴充動作的臨界值，以及觸發橫向擴充動作時，要增加多少實例。 |
| *橫向縮編* |	指定觸發橫向縮編動作的臨界值，以及觸發橫向縮編動作時，要減少多少實例。 |
| *統計資料時間範圍* |	過去期間的長度，此時刻，收到的度量值視為有效。度量值只有在時間戳記落在這個期間內的情況下才會有效。「統計資料時間範圍」參數的單位是秒。 |
| *中斷持續時間*	| 過去期間的長度，此時刻，可能會觸發調整動作。調整動作會在收集的度量值高於上臨界值，或低於下臨界值，且維持時間超過指定的時間時觸發。「中斷持續時間」參數的單位是秒。 |
| *橫向縮編的冷卻期間* | 橫向縮編動作發生之後，在「橫向縮編的冷卻期間」參數所指定的期間長度內，會忽略其他調整要求。這個參數的單位是秒。 |
| *橫向擴充的冷卻期間*	| 橫向擴充動作發生之後，在「橫向擴充的冷卻期間」參數所指定的期間長度內，會忽略其他調整要求。這個參數的單位是秒。 |
| *時區*	| 排程適用的時區。 |
| *開始時間*  |	循環排程的開始時間。 |
| *結束時間*    |	循環排程的結束時間。	|
| *重複於*	|	在每週的星期幾套用循環排程。 |
| *實例計數下限* |	在排程的指定時段期間，可以為應用程式啟動的實例數下限。 |
| *開始日期和時間* |	在特定日期設定之排程的開始日期和時間。
 |
| *結束日期和時間* |	在特定日期設定之排程的結束日期和時間。
	|

表 1. 調整原則中的原則欄位

| 度量值名稱 | 說明 | 支援的應用程式類型 |
|-------------|----------------------| ------------------- |
| *JVM 資料堆* |	JVM 資料堆記憶體的用量百分比。	| Liberty for Java |
| *記憶體*   |	記憶體的用量百分比。	|  Liberty for Java<br/> Node.js <br/> Ruby <br/> |
| *產量* | 每秒處理的要求數。
| Liberty for Java |
| *回應時間* |	已處理要求的回應時間。	| Liberty for Java |

表 2. 支援的度量名稱

## 錯誤訊息
{: #errmsgs}
本節列出 {{site.data.keyword.autoscaling}} 服務所產生的警告及錯誤訊息。
 
### CWSCV2004E 另一個 {{site.data.keyword.autoscaling}} 服務已連結至應用程式。
**您只能連結一個 {{site.data.keyword.autoscaling}} 服務至一個應用程式。此錯誤發生在您要將 {{site.data.keyword.autoscaling}} 服務連結至已和另一個 {{site.data.keyword.autoscaling}} 服務連結的應用程式時。**

請選取另一個沒有連結任何其他 {{site.data.keyword.autoscaling}} 服務的應用程式，並將目標
{{site.data.keyword.autoscaling}} 服務連結至此應用程式。如果您在所有其他情況下遇到此錯誤，請聯絡「IBM 支援中心」。

### CWSCV6001E API 伺服器無法剖析 API 的輸入
JSON 字串：{0}。
**剖析輸入 JSON 字串時發生問題。**

利用 API 文件檢查「輸入 JSON」，並更正其中的錯誤。

### CWSCV6002E API 伺服器無法剖析 API 的輸出
JSON 字串：{0}。
**剖析輸入 JSON 字串時發生問題。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6003E API 的輸入 JSON：{1} 中，輸入 JSON 字串格式錯誤：{0}。
**剖析輸入 JSON 字串時發現格式錯誤。**

利用 API 文件檢查「輸入 JSON」，並更正其中的錯誤。

### CWSCV6004E API 的輸出 JSON：{1} 中，輸出 JSON 字串格式錯誤：{0}。
**剖析輸出 JSON 字串時發現格式錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6005E {0} 期間發生內部伺服器錯誤。
**處理要求時發生內部伺服器錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6006E 呼叫 CloudFoundry API 失敗：{0}
**呼叫 CloudFoundry API 時發生錯誤。**

如需相關資訊，請聯絡「雲端管理者」。

### CWSCV6007E 找不到應用程式：{0}
**找不到應用程式。**

如需相關資訊，請檢查應用程式資訊。

### CWSCV6008E 擷取應用程式 {0} 的資訊時發生下列錯誤：{1} 
**擷取應用程式資訊失敗，發生某些錯誤。**

如需相關資訊，請檢查應用程式資訊。

### CWSCV6009E 找不到應用程式 {1} 的服務：{0}。
**找不到此應用程式的服務。**

如需相關資訊，請檢查此應用程式的服務連結。

### CWSCV6010E 找不到應用程式 {0} 的原則
**找不到此應用程式的原則。**

如需相關資訊，請檢查應用程式配置。

### CWSCV6011E {0} 期間內部鑑別失敗
**「內部鑑別」失敗。**

如需相關資訊，請聯絡「雲端管理者」。


# 相關鏈結
## 範例
* [指導教學：在 {{site.data.keyword.Bluemix_notm}} 上讓您的應用程式具有彈性](http://www.ibm.com/developerworks/cloud/library/cl-autoscale-app/index.html){:new_window} 
* [Cloud Foundry 架構實驗室](https://developer.ibm.com/bluemix/docs/category/cloud-foundry-docs/){:new_window}

## sdk
* [IBM {{site.data.keyword.autoscaling}} for {{site.data.keyword.Bluemix_notm}} 的 Rest API](https://www.{DomainName}/docs/api/content/api/auto-scaling/index.html){:new_window} 

## 一般
* [{{site.data.keyword.Bluemix_notm}} 定價單](https://console.{DomainName}/pricing/){:new_window}
* [{{site.data.keyword.Bluemix_notm}} 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){:new_window}
* [{{site.data.keyword.autoscaling}} CLI](../../cli/plugins/auto-scaling/index.html){:new_window}

