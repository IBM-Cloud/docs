---

copyright:
  years: 2016

---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 管理管線
{: #deliverypipeline_managing}
前次更新：2016 年 11 月 17 日
{: .last-updated}

您可以管理、配置及延伸 IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 整合。
{:shortdesc}

請完成下列作業來管理、配置及延伸管線。

## 環境內容及資源
{: #deliverypipeline_envprop}

您可以使用環境內容及預先安裝的資源，以與 {{site.data.keyword.deliverypipeline}} 服務互動。例如，您可以將它們併入工作 Script 或測試指令中。如需相關資訊，請參閱 [{{site.data.keyword.deliverypipeline}} 服務的環境內容及資源](./deploy_var.html)。

您可以從階段的**環境內容**標籤中，將專屬環境內容新增至階段。階段中的每個工作都會有環境內容。

您可以從「環境內容」標籤中新增四種類型的內容：
* **文字**：具有單行值的內容索引鍵。
* **文字區**：具有多行值的內容索引鍵。
* **安全**：具有單行值的內容索引鍵。值會顯示為星號。
* **內容**：專案儲存庫中的檔案。此檔案可以包含多個內容。每一個內容都必須在其專屬行上。若要區隔索引鍵值組，請使用等號 (=)。

## 延伸管線的功能
{: #deliverypipeline_extend}

將工作配置成使用支援的服務，即可延伸管線的功能。例如，測試工作可以執行靜態程式碼掃描，建置工作則可以將字串進行全球化。


如需延伸管線功能的相關資訊，請參閱[延伸 {{site.data.keyword.deliverypipeline}} 服務的功能](./deliverypipeline_extension.html)。

