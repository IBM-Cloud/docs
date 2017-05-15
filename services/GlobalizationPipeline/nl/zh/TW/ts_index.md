---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.GlobalizationPipeline_short}} 疑難排解
{: #globalizationpipelinets}


以下是 {{site.data.keyword.GlobalizationPipeline_short}} 常見使用問題的一些回答。
{:shortdesc}


## 未正確地翻譯我的應用程式的名稱
{: #problem1}

特定字串的產生翻譯不如預期。
{:shortdesc}

翻譯資源檔時，可能未適當地翻譯包含產品名稱或其他專有名詞的字串。
{: tsSymptoms}

產品名稱或專有名詞通常不會適當地翻譯成其他語言，特別是名稱包含實際單字時。翻譯這些類型的單字和詞組時，根據這些單字在特定語言的意義，翻譯文字可能會與英文名稱的意義不同。
{: tsCauses}

請先測試產品名稱的翻譯，再使用它們，而且，如果發現問題，請從而修改文字或翻譯。如需使用機器翻譯的撰寫樣式提示，請參閱[機器翻譯提示](./tips.html#globalizationpipeline_tips)。
{: tsResolve}



## 我無法上傳資源檔
{: #problem2}

不接受我正在嘗試上傳的資源檔。
{:shortdesc}

將資源檔新增至新的翻譯軟體組或更新要翻譯的現有資源檔時，我接收到錯誤。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} 只接受下列類型的資源檔：Java™ .properties、JSON 和 AMD I18N。
{: tsCauses}

請確定正在上傳的資源檔為下列其中一種類型。
{: tsResolve}
* Java .properties
* JSON
* AMD I18N



## 資源檔太大，因此無法上傳
{: #problem3}

不接受我正在嘗試上傳的資源檔。
{:shortdesc}

將資源檔新增或更新至翻譯專案時，因為檔案的某個部分太大，所以發生錯誤。
{: tsSymptoms}

{{site.data.keyword.GlobalizationPipeline_short}} 只能接受符合特定大小需求的資源檔。
{: tsCauses}

請確定資源檔符合下列準則：
{: tsResolve}
* 每一個索引鍵最多可以有 256 個字元。
* 每一個值最多可以有 2048 個字元。
* 每一個翻譯專案最多可以包含 500 個鍵值組。
* 資源檔不可以超過 2 MB。




## 字串中所含變數周圍的間距不一致
{: #problem5}

變數周圍所使用的間距在翻譯之後不一定相同。
{:shortdesc}

字串內所含變數周圍所使用的間距，在翻譯成不同語言之後不一定會一致。
{: tsSymptoms}

機器翻譯引擎的設計是使用自然語言，而且不一定可辨識或知道如何處理程式設計語言所使用的特定語法。因此，混合使用純文字之語法的處理可能會不同。
{: tsCauses}

{{site.data.keyword.GlobalizationPipeline_short}} 目前可辨識常用來代表變數的型樣 "{}"，而且將保留其內所含內容的原始格式。
{: tsResolve}
