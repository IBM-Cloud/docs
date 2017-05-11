---

copyright:
  years: 2015, 2017
lastupdated: "2016-07-12"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 機器翻譯提示
{: #globalizationpipeline_tips}


機器翻譯可用於提供原始文字的近似意義。不過，機器翻譯的品質和使用性會根據目標語言和所使用的機器翻譯引擎而有極大的不同。機器翻譯品質的其中一個重要因素是來源本身的品質。可能無法精確地翻譯在載入時內含口語用詞、不完整句子、不正確標點符號以及不明確單字和詞組的來源文字。
{:shortdesc}

當您建立 {{site.data.keyword.Bluemix_notm}} 應用程式使用者介面時，請遵循一些基本撰寫準則，同時改善來源語言和機器翻譯品質。

此外，請要求以該語言為母語的人員來檢閱和編輯機器翻譯。同時，收集您應用程式使用者的意見；他們可能是翻譯使用性和精確度的最佳裁判員。

## 撰寫樣式提示
{: #writingstyletips}

* **使用短到中長度的簡單句（5 - 20 個字）：**機器翻譯引擎通常很難翻譯複合句和複雜句（包括含分號的句子）。一個句子傳達一種想法。如果句子包含兩個主動動詞來傳達兩種想法，請將該句子分成兩個句子。機器翻譯引擎也很難剖析太短而無法提供足夠上下文的句子。
* **避免使用詞組：**盡可能使用完整句子。詞組可以用於標題和子標題，但避免撰寫電報標題樣式。請使用完整句子來建立清單。
* **避免使用慣用句、俚語和專門術語：**取代文字翻譯無意義的詞組。例如，將 "on the fly" 取代為 "dynamic"、將 "on the other hand" 取代為 "alternatively"，以及將 "keep in mind" 取代為 "remember"。
* **避免使用幽默、諷刺、口語用詞、表情符號和隱喻。**
* **簡潔：**移除不必要的文字和冗餘項目。例如，將 "It is useful to remember that large values increase the response time" 取代為 "Large values increase the response time"。
* **避免使用完全以大寫撰寫的句子：**大寫提供該單字意義的線索。例如，如果您撰寫 "BILL"，則機器翻譯引擎會無法判斷它是名字 "Bill" 還是 "bill" 這個單字。
* **避免使用不明確的單字：**例如，請不要使用 "once" 來取代 "after" 或 "when"。請不要使用 "while" 來取代 "although" 或 "whereas"。若您的意思是 "might" 或 "can"，請不要使用 "may"。
* **避免使用代名詞：**盡可能重複名詞或名詞詞組。代名詞 "it" 特別有問題。
* **盡可能撰寫主動語態：**主動句通常會比被動句更為清楚。例如，撰寫 "The utility determines which path is most efficient"，而非 "The most efficient path is determined"。
* **避免使用文化特定資訊。**
* **請注意，機器翻譯引擎可能會翻譯產品名稱：**許多國家/地區會保留原始英文產品名稱，但機器翻譯引擎可能會嘗試翻譯產品名稱，特別是名稱包含實際單字時。請先測試產品名稱的翻譯，再使用該產品名稱。如果發現問題，請從而修改文字或翻譯。
* **確定使用一種語言撰寫所有資訊：**機器翻譯引擎可能會假設所有資訊都是使用單一語言，即使文字包括另一種語言的一個以上單字。例如，如果文字包括 "en route"（法文），則機器翻譯引擎仍然會嘗試將這些單字當成英文單字來進行翻譯。
* **避免使用銷售廣告詞：**銷售廣告詞通常會根據使用對象對特定文化的瞭解。因為機器翻譯引擎可能無法精確地翻譯這些類型的廣告詞，所以請避免使用它們。
* **確定清單項目完整且相似：**例如，如果其中一個項目的開頭是動詞，請確定所有項目的開頭都是動詞。
* **避免使用 please 和 thank you：**這些單字並不恰當，在某些文化中甚至有屈尊俯就的意思。
* **以非數值格式撰寫日期：**數值日期格式會根據國家/地區而不同。寫下月份名稱、日和年份。例如，使用 1 September 2003 而非 9/01/03，後者可能會解譯為 2003 年 9 月 1 日或 2003 年 1 月 9 日。

## 文法提示
{: #grammartips}

* **使用適當的標點符號：**省略句點和逗點可能會導致機器翻譯引擎錯誤地解譯資訊。
* **確定主詞與其動詞一致：**確定複數主詞具有複數動詞，而單數主詞具有單數動詞。
* **使用簡單現在式動詞：**許多其他語言沒有英文動詞的特質（例如語態和時態）。盡可能避免使用未來式和過去式。例如，您可以將 "If you run this program, DB2® will return an error message" 重寫為 "If you run this program, DB2 returns an error message"。
* **確定代名詞與其先行詞一致：**例如，"A user should first determine their tasks" 應該重寫為 "Users should first determine their tasks"。
* **避免使用垂懸修飾語：**適當地放置修飾語，以修飾預期名詞。例如，"While typing in commands, the program does not send any messages to you" 可以重寫為 "While typing in commands, you do not receive any messages from the program"。
* **避免使用雙重否定：**例如，"Do not omit the date" 可以取代為 "Include the date"。
* **避免在句子開頭使用不定詞 (to write)、現在分詞 (writing) 和過去分詞 (wrote) 形式的動詞：**這些動詞形式通常不明確而且很難翻譯。
* **避免使用名詞字串：**將複合名詞詞組（例如 "special filter factor estimate considerations"）限制成不超過三個單字。
* **避免使用屬於多文法種類的單字：**在英文中，許多單字（例如 "default"）可能是名詞，也可能是動詞。此結構不適用於許多其他語言。請統一每一個單字的使用方式。例如，一律將 "default" 當成名詞使用。
* **確定句子元素的相似：**例如，在 in-sentence 清單中全部使用名詞或動詞；請不要混合使用名詞和動詞。
* **不要省略必要單字：**例如，使用 "The file names are displayed in uppercase characters and the file extensions are displayed in lowercase characters"，而非 "The file names are displayed in uppercase characters and the file extensions in lowercase"。請使用 "that" 這個字，以在必要時釐清。例如，將 "If you determine the problem is a missing file" 取代為 "If you determine that the problem is a missing file"。
* **不要附加性地插入橫線：**例如，請不要撰寫 "When you get to this point - the point when all data has been loaded - you need to test the system"。請將橫線取代為逗點，或重寫句子。
 
## 術語提示
{: #terminologytips}

* **一致地使用術語：**避免使用多個術語來參照同一個事項。避免使用單一術語來參照多個事項。
* **包括任何特殊化術語的說明。**
* **避免使用在其他環境和上下文中有不同意義的術語：**這些術語包括 "billion"、"domestic" 和 "foreign"。
* **使用一致且標準化的大小寫、連字號和單字結構：**例如，寫成 "fix pack"，而不要寫成 "fixpack"。
* **除非術語是專有名詞，否則請使用小寫。**
* **避免使用特殊符號：**如果您需要使用 # 符號，請不要將它稱為井號。而是將它稱為數字符號 (#)。
* **避免使用縮寫：**機器翻譯引擎可以辨識常見縮寫（例如 IBM 和 DB2），但無法辨識所有縮寫。盡可能避免使用縮寫。請不要使用拉丁文縮寫（例如 "i.e." 和 "etc."）。

## 標點符號提示
{: #punctuationtips}

* **避免使用斜線來表示 "and or"：**重寫句子，指出確切意義。例如，您可以將 "You can view the draft copy and/or the review copy" 重寫為 "You can view the draft copy, the review copy, or both"。
* **不要加 (s) 來表示複數：**請使用詞組 "one or more" 或僅使用複數形式。
* **不要使用 '&' 符號 (&) 來表示 and。**
* **使用逗點區隔 in-sentence 清單中的項目，並在清單中的連接詞前面放置逗點：**例如，"Select your company, location, and profession"。

## 拼字提示
{: #spellingtips}

* **檢查拼字：**錯誤拼字可能會導致翻譯錯誤。請一律檢查是否有打字錯誤！
* **拼法一致：**請確定一律以相同的方式拼出術語、字首語和專有名稱（包括使用大寫和小寫字母）。

## 視覺化呈現提示
{: #visualtips}

* **避免在圖形中使用文字。**
* **避免使用格式化來進行強調。**

