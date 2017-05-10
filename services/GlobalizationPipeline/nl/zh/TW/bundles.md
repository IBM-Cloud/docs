---

copyright:
  years: 2015, 2017
lastupdated: "2016-08-30"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# 使用軟體組
{: #globalizationpipeline_workingwithbundles}


您建立的每一個軟體組都會包含資源檔中的鍵值組，以及一組已產生的完整翻譯。
{:shortdesc}

您上傳的資源檔可以是下列任何格式，而且必須包含代表應用程式中使用者介面字串之鍵值組形式的內容。


* 檔案類型：*Java™ Properties 檔案 (.properties)*<br>
範例：
```js
logout=Logout 
back=Back 
examples=Menu 
home=Home 
web=Web 
enterprise=Enterprise 
extra=Resources 
about=About 
settings=Settings 
help=Help 
support=Support 
topics=Topics 
appExitMsg=Are you sure you want to quit the application?
```
* 檔案類型：*AMD I18N (.js)*<br>
範例：
```js
define({
    "root": {
       logout: "Logout",
       back: "Back",
       examples: "Menu",
       home: "Home",
       web: "Web",
       enterprise: "Enterprise",
       extra: "Resources",
       about: "About",
       settings: "Settings",
       help: "Help",
       support: "Support",
       topics: "Topics",
       appExitMsg: "Are you sure you want to quit the application?"
    }
});
``` 
* 檔案類型：*JSON (.json)*<br>
範例：
```js
{
  "logout": "Logout",
  "back": "Back",
  "examples": "Menu",
  "home": "Home",
  "web": "Web",
  "enterprise": "Enterprise",
  "extra": "Resources",
  "about": "About",
  "settings": "Settings",
  "help": "Help",
  "support": "Support",
  "topics": "Topics",
  "appExitMsg": "Are you sure you want to quit the application?"
}
``` 

此外，資源檔也必須遵循下列準則：
* 每一個索引鍵最多可以有 255 個字元。
* 每一個值最多可以有 8191 個字元。
* 每一個軟體組最多可以包含 500 個鍵值組。


## 翻譯軟體組
{: #globalizationpipeline_translatingabundle}

只會翻譯已上傳的資源檔。您可以在[建立軟體組](index.html#globalizationpipeline_creatingbundles)或[修改軟體組詳細資料](bundles.html#globalizationpipeline_modifyingbundles)時上傳資源檔。

上傳資源檔之後，即可將其內容翻譯成預設機器翻譯引擎所提供的任何語言。您可以選擇性地選擇替代機器翻譯引擎（如[機器翻譯配置](managing_translations.html#globalizationpipeline_service_to_service)小節中所述）。預設引擎支援下列目標語言：

<table>
<thead>
<tr>
<th>目標語言</th>
</tr>
</thead>
<tbody>
<tr>
<td>簡體中文</td>
</tr>
<tr>
<td>繁體中文</td>
</tr>
<tr>
<td>法文</td>
</tr>
<tr>
<td>德文</td>
</tr>
<tr>
<td>義大利文</td>
</tr>
<tr>
<td>日文</td>
</tr>
<tr>
<td>韓文</td>
</tr>
<tr>
<td>葡萄牙文 (巴西)</td>
</tr>
<tr>
<td>西班牙文</td>
</tr>
</tbody>
</table>

**附註：**{{site.data.keyword.GlobalizationPipeline_short}} 的預設機器翻譯引擎只提供以英文作為原始語言的支援。不過，可在 {{site.data.keyword.GlobalizationPipeline_short}} 內配置替代機器翻譯引擎，這些引擎支援翻譯非英文的原始語言/語言配對。

軟體組在建立之後，會新增至**軟體組**標籤，讓它們更容易存取。您可以在這裡對您的翻譯執行其他作業。


## 選取要使用的軟體組
{: #globalizationpipeline_selectingabundle}

1. 按一下**軟體組**標籤，以檢視所有已建立的軟體組。
2. 按一下清單中的**軟體組 ID** 以查看軟體組的其他詳細資料，或按一下「動作」直欄中的**檢視軟體組詳細資料**圖示 ![選取「檢視軟體組詳細資料」圖示以開啟軟體組，並使用其翻譯](images/viewProjectDetailIcon.png)。

![檢視「軟體組」標籤中的所有可用軟體組。](images/translationBundles.png)

選取要使用的軟體組之後，您即可檢視其翻譯的狀態、新增或移除語言、編輯翻譯，或提供資源檔的更新。

如果您不再需要某軟體組，則可以從**軟體組**標籤中將它刪除。這會一併刪除與軟體組相關聯的所有翻譯。

## 修改軟體組詳細資料
{: #globalizationpipeline_modifyingbundles}

當您開啟軟體組時，可以檢視其所有詳細資料。會列出軟體組中的所有目標語言，以及其現行翻譯狀態。

![「軟體組詳細資料」頁面顯示軟體組及其翻譯的相關資訊。](images/bundleDetails.png)

軟體組中每一種語言的狀態可以是「進行中」、「失敗」或「已翻譯」：

| 狀態 | 說明 |
|--------|-------------|
| 進行中 | 仍在進行機器翻譯。 |
| 失敗 | 將資源檔翻譯成目標語言時發生錯誤。 |
| 已翻譯 | 已完成翻譯成目標語言。 |

您可以更新軟體組所使用的資源檔、將目標語言新增至軟體組、刪除軟體組中的目標語言，以及下載針對目標語言所產生的翻譯。

### 更新軟體組所使用的資源檔

1. 在來源語言旁邊，按一下「動作」直欄中的**上傳資源**圖示 ![選取此圖示以上傳新的資源檔](images/uploadIcon.png)。
2. 按一下**瀏覽**，然後選取要上傳的新資源檔。
3. 選取您所上傳之資源檔的類型
 * Java Properties 檔案
 * AMD I18N
 * JSON
4. 按一下**更新**以上傳新的資源檔。

新增或已更新資源檔中的鍵值組會與已上傳的值同步。只會翻譯新增或已變更的內容。

### 將目標語言新增至軟體組

1. 按一下**新增語言**按鈕。
2. 即會顯示所有可用的目標語言。選取要新增至軟體組的語言。

將立即開始所選取語言的翻譯。

### 刪除軟體組中的目標語言

當您刪除軟體組中的目標語言時，會移除專案中的目標語言和所有關聯的翻譯。在要移除之目標語言的「動作」直欄中，按一下**移除此目標語言**圖示 ![選取「移除此目標語言」的垃圾筒圖示](images/trashIcon.png)。

### 下載目標語言的已產生翻譯

{{site.data.keyword.GlobalizationPipeline_short}} 提供數種方法，將目標語言的翻譯併入應用程式中。您可以將翻譯下載為資源檔，並將它併入應用程式建置中。您也可以使用其中一個開放程式碼 [SDK](https://github.com/IBM-Bluemix/gp-common)，從 {{site.data.keyword.GlobalizationPipeline_short}} 動態參照翻譯。 

<!-- For information on {{site.data.keyword.GlobalizationPipeline_full}} SDKs, see <link>. -->

若要將翻譯下載為資源檔，請執行下列動作： 

1. 在要下載之目標或來源語言的**動作**直欄中，按一下**下載翻譯**圖示 ![選取「下載」圖示來下載目標語言的來源索引鍵或翻譯](images/downloadIcon.png)。
2. 選取檔案格式。
3. 按一下**下載**。
