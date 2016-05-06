---

copyright:
  years: 2015, 2016

---

{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 使用測試版特性
{: #using_beta_features}

*前次更新：2016 年 3 月 23 日*

Liberty 測試版特性可讓您提早存取未來 Liberty 版本中可能包含的新功能及程式設計模型。大部分的測試版特性也可以用於已部署至 Bluemix 的應用程式。

**重要事項**：測試版特性僅針對開發及測試用途，可能無法用於正式作業。如需完整的使用條款，請參閱[測試版授權合約](http://public.dhe.ibm.com/ibmdl/export/pub/software/websphere/wasdev/downloads/wlp/beta/lafiles/en.html)。

Bluemix 中可用的 Liberty 測試版特性
<table>
<tr>
<th align="left">特性</th>
<th align="left">特性</th>
<th align="left">特性</th>
<th align="left">特性</th>
</tr>

<tr>
<td>cloudant-1.0</td>
<td>httpWhiteboard-1.0</td>
<td>osgiBundle-1.0</td>
<td>passwordUtilities-1.0</td>
</tr>
</table>

若要在 Bluemix 中使用 Liberty 測試版特性，您必須執行下列其中一項：

1. 在 server.xml 檔案中啟用一個以上的測試版特性，以[部署伺服器目錄或包裝伺服器](optionsForPushing.html)，如下列範例所示：
```
    <server>
        <featureManager>
            <feature>jsp-2.3</feature>
            <feature>passwordUtilities-1.0</feature>
        </featureManager>
    </server>
```
{: #codeblock}

2.  將 IBM_LIBERTY_BETA 環境變數設為 **true**。此變數會指示 Liberty 建置套件，為您的應用程式安裝並啟用測試版特性。請參閱下列範例：
  * 使用 cf 指令行工具：
```
       $ cf set-env <yourappname> IBM_LIBERTY_BETA true
```
{: #codeblock}

  * 或者，使用 manifest.yml 檔案：
```
      env:
          IBM_LIBERTY_BETA: "true"
```
{: #codeblock}

# 相關鏈結
## 一般
* [Liberty 執行時期](index.html)
* [Liberty 設定檔概觀](http://www-01.ibm.com/support/knowledgecenter/SSAW57_8.5.5/com.ibm.websphere.wlp.nd.doc/ae/cwlp_about.html)
