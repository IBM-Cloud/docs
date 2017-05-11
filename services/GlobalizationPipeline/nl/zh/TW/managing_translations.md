---

copyright:
  years: 2015, 2017
lastupdated: "2016-10-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理翻譯
{: #globalizationpipeline_managingtranslations}


在您建立軟體組並開始產生應用程式的翻譯之後，即可依現狀使用或進一步修改機器產生的內容。您也可以選擇使用預設值以外的機器翻譯。本節說明如何變更執行軟體組翻譯的機器翻譯引擎、如何執行人工翻譯後處理編輯，以及如何將使用者角色和存取限制指派給需要存取翻譯的人員。
{:shortdesc}

## 機器翻譯配置
{: #globalizationpipeline_service_to_service}

{{site.data.keyword.GlobalizationPipeline_full}} 支援整合替代機器翻譯服務來執行軟體組之機器翻譯的能力。如果 {{site.data.keyword.GlobalizationPipeline_short}} 所使用的預設引擎未提供您所需的特定語言，或者您偏好不同引擎所產生的機器翻譯，則新增替代服務可能十分有幫助。替代服務條款涵蓋這些服務的使用和費用。

若要新增和配置 {{site.data.keyword.GlobalizationPipeline_short}} 的替代機器翻譯服務，請從 {{site.data.keyword.GlobalizationPipeline_short}} 儀表板中選取**機器翻譯配置**標籤。

* 若要新增 {{site.data.keyword.Bluemix_notm}} 型錄中的機器翻譯服務（**Watson 語言翻譯程式**），則必須先將該服務新增至 {{site.data.keyword.Bluemix_notm}} 空間。

* 若要新增協力廠商服務，請在**機器翻譯配置**標籤上選取該服務的按鈕，並提供存取服務所需的使用者認證。

已將機器翻譯服務新增至 {{site.data.keyword.GlobalizationPipeline_short}} 之後，請完成其餘步驟來完成該服務的整合。

1. 按一下**啟用**，以開啟與該服務的整合。

2. 按一下**更新語言**，以檢視已更新的所支援目標語言清單。

3. 從目標語言清單中，選取應該執行翻譯的機器翻譯引擎。

4. 按一下**儲存**，以回到**機器翻譯配置**標籤。

使用 {{site.data.keyword.GlobalizationPipeline_short}} 配置替代服務之後，將使用該引擎開始產生已指派給該引擎的所有目標語言。 

若要停止使用替代機器翻譯引擎，請執行下列動作：

1. 從**機器翻譯配置**標籤中，按一下您要停止使用之服務的**停用**按鈕。

停用替代機器翻譯服務之後，服務已產生的所有翻譯將會保留在軟體組內。不過，如果目前已啟用的機器翻譯引擎不再支援目標語言，則未來更新可能無法再翻譯為特定目標語言。

<!-- Review comment: When you disable an engine, do you need to go back and reconfigure the languages?? Does it go back to the default engine? What happens? -->

## 檢視和編輯翻譯
{: #globalizationpipeline_translations}

{{site.data.keyword.GlobalizationPipeline_short}} 服務提供人工翻譯後處理編輯功能。專業翻譯人員或瞭解任何目標語言的人員都可以編輯產生的翻譯。您可以編輯以改善翻譯的品質或一致性，或替換偏好的用語。例如，您可能要改寫產品名稱的翻譯。

若要檢視和編輯目標語言的翻譯，請執行下列動作：

1. 從**軟體組詳細資料**頁面中選取目標語言，或按一下「動作」直欄中的**檢視翻譯**圖示 ![選取「檢視翻譯」圖示以檢視目標語言的翻譯](images/viewProjectDetailIcon.png)。
2. 翻譯會以顯示索引鍵、來源和翻譯資訊的表格形式呈現。
 * **索引鍵：**代表資源檔中具有關聯值的屬性。
 * **來源：**代表已上傳資源檔中所含的可翻譯字串。
 * **翻譯：**代表來源值的已翻譯版本。
3. 在「動作」直欄中，按一下**修改翻譯**圖示 ![選取「修改翻譯」圖示以編輯特定鍵值組的翻譯。](images/editIcon.png) 以編輯機器翻譯的值。
4. 編輯翻譯，然後按一下**更新**，利用編輯來更新原始翻譯值。

![修改翻譯對話框視窗提供一種編輯翻譯的簡單方法。](images/editTranslation.png) 

***提示：***當您使用包括許多可翻譯索引鍵的大型軟體組時，可能很難找到特定值。在目標語言翻譯頁面上，您可以使用**搜尋...** 方框來快速搜尋所有索引鍵、來源和翻譯。

![使用目標語言翻譯頁面上所提供的搜尋方框，來搜尋目標語言內的索引鍵、來源、翻譯或上述三個項目。](images/search.png) 


## 新增 API 使用者
{: #globalizationpipeline_users}

當您管理翻譯時，可能要根據其他 API 使用者需要執行的作業來授與存取權。例如，您可能要讓翻譯人員可編輯翻譯，但無法修改軟體組資訊。

| 角色類型 | 檢視翻譯？ | 編輯翻譯？ | 修改軟體組資訊？ |
|-----------|--------------------|--------------------|----------------------------|
| 讀者 | 是 | 否 | 否 |
| 翻譯人員 | 是 | 是 | 否 |
| 管理者 | 是 | 是 | 是 |

如果您建立多位 API 使用者，則可以限制他們對一個以上特定軟體組的存取權，或授與他們所有可用軟體組的存取權。

若要授與 API 使用者 {{site.data.keyword.GlobalizationPipeline_short}} 服務實例中的軟體組存取權，請執行下列動作：

1. 在 {{site.data.keyword.GlobalizationPipeline_short}} 儀表板上，按一下 **API 使用者**標籤。
2. 按一下**新建 API 使用**。
3. 鍵入**顯示名稱**和**註解**，以說明新的 API 使用者。
4. 選擇新 API 使用者的**類型**。
5. 選擇授與 API 使用者所有軟體組或僅所選取軟體組的存取權。
6. 按一下**儲存**。

![完成討論區，以建立新的 API 使用者。](images/newUser.png)

即會產生並顯示 API 使用者 ID 和密碼。請複製並儲存這些認證；在您關閉此視窗之後，就無法再存取它們。透過 [SDK](https://github.com/IBM-Bluemix/gp-common)，可以將認證用於 RESTful 服務。 

若要重設 API 使用者密碼，請執行下列動作：

1. 在 {{site.data.keyword.GlobalizationPipeline_short}} 儀表板上，按一下 **API 使用者**標籤。
2. 按一下**重設密碼**圖示 ![選取此圖示以重設 API 使用者密碼](images/resetPW.png)，以重設特定使用者 ID 的密碼。 
3. 按一下**是**。 
