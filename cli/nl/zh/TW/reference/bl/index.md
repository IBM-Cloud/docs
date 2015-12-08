# bl 指令

*前次更新：*2015 年 11 月 13 日

如果您要建置 Node.js 應用程式，可以使用 Bluemix™ Live Sync 快速更新 Bluemix 上執行的應用程式實例，並像在桌面上那樣地開發應用程式而不必重新部署。當您進行變更時，可以立即在執行中的 Bluemix 應用程式看到該變更。Bluemix Live Sync 指令行介面稱為 *bl*。

您可以使用 **bl** 指令行介面指令來完成下列作業：

* 啟動及停止在 Bluemix 上執行的應用程式。
* 從您的桌面建立新的雲端型專案。
* 將桌面的變更同步至雲端型專案工作區，以及在 Bluemix 上執行的應用程式。
* 查看可以同步化的專案清單。
* 查看執行中應用程式的狀態。

如需下載及使用 bl 指令的相關資訊，請參閱 [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive)。

## bl 指令

Bluemix Live Sync 指令行 (**bl**) 的語法如下：

``` bl command [arguments][options] [--help]```

### 指令
<dl>
<dt>login、l</dt>
<dd>登入 Bluemix。</dd>
<dt>logout、lo</dt>
<dd>將使用者登出。</dd>
<dt>sync、s</dt>
<dd>啟動桌上型電腦與伺服器之間的同步化處理程序。</dd>
<dt>create、c</dt>
<dd>建立專用專案、將它鏈結至此目錄中的 Git 儲存庫，然後將內容部署至 Bluemix。</dd>
<dt>projects、p</dt>
<dd>列出可用於同步化的所有專案。</dd>
<dt>start、st</dt>
<dd>在 Bluemix 中啟動應用程式實例。</dd>
<dt>stop、sp</dt>
<dd>在 Bluemix 中停止應用程式實例。</dd>
<dt>status、ss</dt>
<dd>列出 Bluemix 中的執行中應用程式實例狀態。</dd>
</dl>

### 引數
<dl>
<dd>指令的引數。</dd>
</dl>

### 選項
<dl>
<dd>指令的選項。</dd>
</dl>

### 廣域選項
<dl>
<dt>--help</dt>
<dd>顯示所指定指令的說明頁面</dd>
<dt>--verbose</dt>
<dd>啟用詳細記載。</dd>
</dl>

**附註：**如果您的任何引數或選項包含空格，請將值含括在雙引號中。
