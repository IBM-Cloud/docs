---

copyright:
  years: 2015, 2017
lastupdated: "2016-09-09"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 開始使用 {{site.data.keyword.GlobalizationPipeline_short}}
{: #globalizationpipeline}


{{site.data.keyword.GlobalizationPipeline_full}} 是一項服務，提供快速翻譯 Web 或行動使用者介面的機器翻譯和編輯功能。使用其儀表板、RESTful API 以及與您應用程式之 Delivery Pipeline 的整合，您可以發行給全球客戶，而不需要重建或重新部署應用程式。
{:shortdesc}

您可以在 {{site.data.keyword.Bluemix}} 中搭配使用 {{site.data.keyword.GlobalizationPipeline_short}} 服務與任何應用程式，或自行取消連結。使用最少的工作量，並且不需要離開 DevOps 環境，即可快速地建立、維護和修訂翻譯。

從 {{site.data.keyword.GlobalizationPipeline_short}} 介面中，您可以快速地翻譯 {{site.data.keyword.Bluemix_notm}} 應用程式。如需使用 RESTful API 翻譯應用程式的相關資訊，請參閱 [API 參考資料](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}。 


## 建立軟體組
{: #globalizationpipeline_creatingbundles}

使用 {{site.data.keyword.GlobalizationPipeline_short}} 服務，您所建立的軟體組可包括將翻譯之應用程式的資源檔。資源檔可以是 Java Properties、AMD I18N 或 JSON 檔案，而且必須包含代表應用程式中使用者介面字串之鍵值組形式的內容。如需所支援檔案類型的詳細資料和範例，請參閱[使用軟體組](./bundles.html){: new_window}。

若要建立軟體組，請完成下列步驟：

<ol>
<li>從<strong>概觀</strong>標籤中，按一下<strong>新建軟體組</strong>。</li>

<li>提供您軟體組的相關資訊：</li>
<table>
<thead>
<tr>
<th>欄位</th>
<th>必要</th>
<th>說明</th>
</tr>
</thead>
<tbody>
<tr>
<td><strong>軟體組 ID</strong></td>
<td>是</td>
<td>用來識別軟體組的唯一名稱。</td>
</tr>
<tr>
<td><strong>來源語言</strong></td>
<td>是</td>
<td>來源檔的國家語言。</td>
</tr>
<tr>
<td><strong>資源檔</strong></td>
<td>否</td>
<td>要翻譯的<a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/bundles.html>資源檔</a>。檔案大小上限限制為 2MB。將會上傳指定的資源檔。</td>
</tr>
<tr>
<td><strong>檔案格式</strong></td>
<td>否</td>
<td>正在上傳的檔案類型。</td>
</tr>
<tr>
<td><strong>目標語言</strong></td>
<td>否</td>
<td>您想要翻譯的語言。</td>
</tr>
</tbody>
</table>

<p><strong>附註：</strong>若要變更提供軟體組之機器翻譯的語言服務，請按一下 <a href=https://new-console.ng.bluemix.net/docs/services/GlobalizationPipeline/managing_translations.html#globalizationpipeline_service_to_service>MT 配置</a>標籤，以檢視其他支援的機器翻譯引擎。</p>

<li>按一下<strong>儲存</strong></li></ol>


建立軟體組之後，上傳的資源檔會翻譯為所有您指定的目標語言。新的軟體組會新增至「軟體組」標籤，您可以在其中執行下列動作：

* 新增或移除語言
* 編輯產生的翻譯
* 更新軟體組中所使用的來源檔，然後重新產生翻譯

## 匯入已翻譯的軟體組
{: #globalizationpipeline_importtranslatedbundlesintoservice}

或者，如果您已有已翻譯的資源檔，則可以將它們匯入至新的軟體組。如需相關資訊，請參閱 [Java Client Tools for {{site.data.keyword.GlobalizationPipeline_short}}](https://github.com/IBM-Bluemix/gp-java-tools)。

**附註：**如果已更新原始來源檔，則該檔案中所定義的索引鍵和值會與來源檔的最新版本同步，因此僅翻譯已變更的索引鍵和值。

## 預估 {{site.data.keyword.GlobalizationPipeline_short}} 資料使用量
{: #globalizationpipeline_documentpricing}

{{site.data.keyword.GlobalizationPipeline_short}} 會將您的翻譯儲存在後端資料庫中。若要預估作用中資料大小，您可以參照資料儲存空間預估公式：

`<預期資源資料儲存空間大小（以 MB 為單位）> ˜= 0.0005 * <來源資源中的鍵值組數目> * <語言數目（包括來源語言）>`

根據公式，一般軟體組大小為`（索引鍵長度 + UTF-8 格式的值長度 = ˜40 個位元組）`。

例如，如果您有 100 個鍵值組，並將它們翻譯成 9 種語言，則預估的儲存空間大小為 0.0005 100 (9+1) = 0.5 MB。根據與翻譯一起儲存的實際鍵值大小和 meta 資料，實際大小可能會不同。

使用 Bluemix [定價計算機](https://console.ng.bluemix.net/?direct=classic/#/pricing/cloudOEPaneId=pricing&paneId=pricingSheet&orgGuid=127a45f4-4461-4d5b-a26b-6dc2fdd1a3a2&spaceGuid=208fb1ff-413b-4fd9-9615-e8226062d0f3)，來判斷每月服務成本。


# 相關鏈結
{: #rellinks}
## 指導教學和範例
{: #samples}

* [Node.js 範例](https://github.com/IBM-Bluemix/gp-nodejs-sample){: new_window}
* [Ruby 範例](https://github.com/IBM-Bluemix/gp-ruby-sample){: new_window}

## SDK
{: #sdk}

* [Java 用戶端](https://github.com/IBM-Bluemix/gp-java-client){: new_window}
* [Java 工具](https://github.com/IBM-Bluemix/gp-java-tools){: new_window}
* [JavaScript 用戶端](https://github.com/IBM-Bluemix/gp-js-client){: new_window}
* [AngularJS 用戶端](https://github.com/IBM-Bluemix/gp-angular-client){: new_window}
* [Ruby 用戶端](https://github.com/IBM-Bluemix/gp-ruby-client){: new_window}
* [Python 用戶端](https://github.com/IBM-Bluemix/gp-python-client){: new_window}

## API 參考資料
{: #api}

* [IBM Globalization Pipeline RESTful API](https://gp-rest.ng.bluemix.net/translate/swagger/index.html){: new_window}

## 相關鏈結
{: #general}

* [整合 Globalization Pipeline 與 Delivery Pipeline](https://hub.jazz.net/docs/deploy_ext/#globalize){: new_window}
* [IBM Bluemix 定價單](https://www.ng.bluemix.net/#/pricing){: new_window}
* [IBM Bluemix 必要條件](https://developer.ibm.com/bluemix/support/#prereqs){: new_window}
