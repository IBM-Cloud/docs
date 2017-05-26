---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI 是外掛程式，可讓您管理組織中的登錄資源，例如名稱空間及映像檔。
{: shortdesc}

**必要條件**
* 在執行登錄指令之前，請先使用 `bx login` 指令來登入 {{site.data.keyword.Bluemix_short}}，以產生 {{site.data.keyword.Bluemix_short}} 存取記號，並鑑別您的階段作業。

<table summary="管理容器登錄">
<caption>表 1. 用來在 {{site.data.keyword.Bluemix_short}} 上管理 {{site.data.keyword.registryshort}} 的指令</caption>
 <thead>
 <th colspan="5">用來管理登錄的指令</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
傳回執行指令所針對之登錄 API 端點的詳細資料。

```
bx cr api
```
{: codeblock}


## bx cr info
顯示所登入之登錄的名稱及組織。

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
檢視特定映像檔的詳細資料。

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**參數**
<dl>
<dt>--format FORMAT</dt>
<dd>（選用）使用 Go 範本將輸出元素格式化。</dd>
<dt>IMAGE</dt>
<dd>您要檢查之映像檔的完整 {{site.data.keyword.Bluemix_short}} 登錄路徑，格式為 namespace/image:tag。如果映像檔路徑中未指定標籤，則會檢查以 `latest` 標記的映像檔。若要檢查多個映像檔，您可以在指令中列出每一個專用 {{site.data.keyword.Bluemix_short}} 登錄路徑，每一個路徑之間以空格隔開。</dd>
</dl>


## bx cr image-list
檢視 {{site.data.keyword.Bluemix_short}} 組織中的所有映像檔。

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**參數**
<dl>
<dt>--no-trunc</dt>
<dd>（選用）不要截斷輸出。</dd>
<dt>-q、--quiet</dt>
<dd>（選用）以下列格式顯示映像檔的唯一 ID：'repository:tag'。</dd>
<dt>--include-ibm</dt>
<dd>（選用）將 IBM 提供的公用映像檔包含在輸出中。若不使用此選項，則只會列出專用映像檔。</dd>
<dt>--format FORMAT</dt>
<dd>（選用）使用 Go 範本將輸出元素格式化。</dd>
</dl>


## bx cr image-rm
從登錄刪除指定的映像檔。

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**參數**
<dl>
<dt>IMAGE</dt>
<dd>您要移除之映像檔的完整 {{site.data.keyword.Bluemix_short}} 登錄路徑，格式為 namespace/image:tag。如果映像檔路徑中未指定標籤，則依預設會刪除以 `latest` 標記的映像檔。若要刪除多個映像檔，您可以在指令中列出每一個專用 {{site.data.keyword.Bluemix_short}} 登錄路徑，每一個路徑之間以空格隔開。</dd>
</dl>


## bx cr login
如果已安裝 Docker，此指令會針對登錄執行 `docker login` 指令。必須執行 `docker login` 指令，才能針對登錄執行 `docker push` 或 `docker pull` 指令。若要執行其他 `bx cr` 指令，則不需要執行此指令。如果未安裝 Docker，則此指令會傳回錯誤訊息。

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
將名稱空間新增至 Bluemix 組織。 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**參數**
<dl>
<dt>NAMESPACE</dt>
<dd>您要新增的名稱空間。此名稱空間在所有 {{site.data.keyword.Bluemix_short}} 組織中必須是唯一的。</dd>
</dl>


## bx cr namespace-list
檢視 {{site.data.keyword.Bluemix_short}} 組織的所有名稱空間。

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
從 {{site.data.keyword.Bluemix_short}} 組織移除名稱空間。移除名稱空間時，也會刪除此名稱空間中的映像檔。

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**參數**
<dl>
<dt>NAMESPACE</dt>
<dd>您要移除的名稱空間。</dd>
</dl>
