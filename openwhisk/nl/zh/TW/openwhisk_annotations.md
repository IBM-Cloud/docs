---

copyright:
  years: 2016, 2017
lastupdated: "2016-02-21"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# OpenWhisk 資產的註釋

OpenWhisk 動作、觸發程式、規則及套件（通稱為資產）可以能會使用 `annotations` 進行裝飾。註釋會附加至資產，就像具有可定義名稱的 `key` 及可定義值的 `value` 的參數。從指令行介面 (CLI) 透過 `--annotation` 或 `-a`（簡稱）設定它們十分方便。
{: shortdesc}

基本原理：已將註釋新增至 OpenWhisk 來容許進行實驗，而不需要變更基礎資產綱目。截至撰寫本文件之前，我們故意不定義允許的 `annotations`。不過，在我們開始更頻繁地使用註釋來傳達語意變更時，最終一定要開始記錄它們。

到目前為止最常用的註釋是記載動作及套件。您將會在 OpenWhisk 型錄執行註釋中看到許多套件，例如其動作所提供功能的說明、套件連結期間所需的參數，以及哪些是呼叫期間參數，而不論參數是否為「機密」（例如密碼）。例如，我們已視需要創造這些項目來容許 UI 整合。

以下是 `echo` 動作的一組註釋範例，此動作會傳回其未經修改的輸入引數（例如，`function main(args) { return args }`）。例如，此動作可能適用於將輸入參數記載為某個系列或規則的一部分。

```
wsk action create echo echo.js \
    -a description 'An action which returns its input. Useful for logging input to enable debug/replay.' \
    -a parameters  '[{ "required":false, "description": "Any JSON entity" }]' \
    -a sampleInput  '{ "msg": "Five fuzzy felines"}' \
    -a sampleOutput '{ "msg": "Five fuzzy felines"}'
```
{: pre}

我們用於說明套件的註釋如下：

- `description`：套件的簡潔有力說明
- `parameters`：說明範圍設為套件的參數的陣列（下面會進一步說明）

同樣地，用於說明動作的註釋如下： 

- `description`：動作的簡潔有力說明
- `parameters`：說明執行動作所需動作的陣列
- `sampleInput`：顯示含一般值的輸入綱目的範例
- `sampleOutput`：顯示輸出綱目的範例，通常適用於 `sampleInput`

我們用於說明參數的註釋包括：

- `name`：參數的名稱
- `description`：參數的簡潔有力說明
- `doclink`：參數的進一步文件的鏈結（例如，適用於 OAuth 記號） 
- `required`：true 表示必要參數，false 則表示選用參數
- `bindTime`：如果應該在連結套件時指定參數，則為 true
- `type`：參數的類型，為 `password` 或 `array` 其中一個（但可能更廣泛使用）

註釋*不* 會進行檢查。因此，舉例來說，雖然可以想見可使用註釋來推斷將兩個動作合併至系列是否正當，但系統並未這麼做。

## 實驗性特性的註釋

我們最近使用了一些實驗性特性來擴充核心 API。為了啟用套件及動作來參與這些特性，我們已建立三個語意上有意義的新註釋。這些註釋必須明確地設為 `true` 才會作用。將值從 `true` 變更為 `false`，會從實驗性 API 中排除所附加的資產。註釋在系統中將沒有意義。註釋如下：

- `final`：僅套用至動作。它會將所有已定義的動作參數設為不可變。參數具有透過其含括套件或動作定義所定義的值之後，呼叫期間參數可能不會置換帶有註釋的動作的參數。
- `web-export`：僅套用至動作。如果存在，它可讓 REST 呼叫存取其對應的動作，而*不* 需要進行鑑別。我們將這些稱為 [*Web 動作*](openwhisk_webactions.html)，因為它們容許使用者從瀏覽器使用 OpenWhisk 動作（舉例來說）。請務必注意，Web 動作的*擁有者* 會引發在系統中執行它們的成本（亦即，動作的*擁有者* 同時擁有啟動記錄）。

