---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 儲存大型物件 {: #large-files}

上傳作業受限於 5 GB 的單次上傳大小上限。不過，您可以將較大的物件分解成較小的區段，並使用資訊清單檔來連結區段。一旦連結物件，便沒有大小上限。
{: shortdesc}

大型物件可以是動態或靜態。使用靜態大型物件 (SLO)，區段不需要在相同的容器中；每一個區段都可以儲存在任何容器中，並指定任何名稱。使用動態大型物件，Swift 用戶端會建立容器，而且編號的區段會平行上傳至容器。


## 動態大型物件：{: #dynamic}

您有兩種方式，上傳動態大型物件：
  * 讓 Swift 用戶端自動處理所有項目
  * 您可以使用 Swift API 自行處理

#### 使用 Swift 用戶端處理動態大型物件

Swift 用戶端使用 `-segment-size` 參數，將您的物件細分成較小的部分。用戶端會使用您要將檔案上傳至其中的容器名稱來建立新容器，並新增具有區段號碼的字尾 (`<container_name>_segments`)。區段會平行上傳。區段全部上傳之後，即會以一個連結物件的形式下載至具有原始檔名的資訊清單檔。

1. 登入 {{site.data.keyword.Bluemix_notm}} 並準備好上傳之後，請執行下列指令將您的檔案分段。
    ```
    swift upload <container_name> <file_name> --segment-size <size_in_bytes>
    ```
    {: pre}

#### 使用 Swift API 處理動態大型物件

您可以自行將物件分段成等於或小於 5 GB，然後透過 Swift API 進行上傳。

**附註**：上傳時，必須在資訊清單檔之前上傳所有區段。如果在上傳所有區段之前下載物件，則下載的物件無法一致地連結。

您可以完成下列步驟，來上傳大型檔案。

1. 依據形成原始物件時區段所需的連結順序，並依名稱來排序區段。
2. 將區段上傳至某個與保留資訊清單檔之容器不同的容器中。上傳的節流控制是在上傳第 10 個區段之後開始，並會大幅增加上傳時間。  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000001
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_name>/<object_name>/000002
    ```
    {: pre}

3. 上傳 `X-Object-Manifest` 標頭設為對應之 `<container>/prefix>` 值的空資訊清單檔。

    ```
    curl -i -X PUT -H "X-Auth-Token: <token>" -H "X-Object-Manifest: <container_name>/<object_name>/" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}

    **附註**：資訊清單檔必須是空的。否則，會將檔案的內容視為一個區段，並破壞依排序名稱指出的連結順序。
4. 下載物件。因此，您會收到整個物件。您可以新增或移除區段，而不需要更新資訊清單檔。具有正確字首的區段會保持為物件的一部分。刪除資訊清單並不會刪除區段。

    ```
    curl -i -O -H "X-Auth-Token: <token>" https://<object-storage_url>/<manifest_container_name>/<object_name>
    ```
    {: pre}


## 儲存大型物件 {: #static}

靜態大型物件會使用區段及資訊清單檔，但是您可以進一步地控制。使用 SLO，區段不需要在相同的容器中；每一個區段都可以儲存在任何容器中，並指定任何名稱。不過，區段必須至少為 1 MB。您不需要設定資訊清單檔的標頭，然而在上傳正確的資訊清單之後，即會自動新增標頭 "X-Static-Large-Object" 並將其設為 true。
{: shortdesc}

資訊清單檔是提供區段詳細資料的 JSON 文件，必須在上傳所有區段之後予以上傳。會將資訊清單中針對每一個區段所提供的資料，與實際區段的 meta 資料進行比較。如果有任何不相符，則不會上傳資訊清單。

<table>
<caption> 表.1 資訊清單檔中的 JSON 屬性</caption>
  <tr>
    <th> 屬性</th>
    <th> 說明</th>
  </tr>
  <tr>
    <td> <i> path </i> </td>
    <td> 區段的位置及名稱。指定為 container_name/object_name。</td>
  </tr>
  <tr>
    <td> <i> etag </i> </td>
    <td> PUT 要求在上傳物件時所提供。對物件執行 HEAD，也可以找到該項目。</td>
  </tr>
  <tr>
    <td> <i> size_bytes </i> </td>
    <td> 物件大小（以位元組為單位）。</td>
  </tr>
</table>



#### 上傳大型檔案

1. 執行下列指令，以上傳區段。上傳的節流控制是在上傳第 10 個區段之後開始，並會大幅增加上傳時間。  

    ```
    curl -i -X PUT --data-binary @segment1 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    curl -i -X PUT --data-binary @segment2 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<segment>
    curl -i -X PUT --data-binary @segment3 -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_one>/<segment>
    ```
    {: pre}

2. 建置資訊清單：

    ```
    [
        {
            "path": "<container_one>/<segment>",
            "etag": "e0ed3b751eb8d4b2c648d2dd78576e36",
            "size_bytes": 801882690
        },
        {
            "path": "container_two/<segment>",
            "etag": "65a301e71c82cbd325a5efe5877e1a24",
            "size_bytes": 1048576
        },
        {
            "path": "<container_one>/<segment>",
            "etag": "aea8b7462d527ad5ed0cfc22ea161062",
            "size_bytes": 138257
        }
    ]
    ```
    {: pre}

3. 將查詢 `multipart-manifest=put` 新增至資訊清單的名稱來上傳資訊清單檔。

    ```
    curl -i -X PUT --data-binary @object_name -H "X-Auth-Token: <token>" https://<object-storage_url>/container_two/<object_name>?multipart-manifest=put
    ```
    {: pre}

4. 下載物件。

    ```
    curl -O -X GET -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}


#### 使用靜態大型物件

您可以使用下列指令管理您的檔案。

**附註**：若要將區段新增至物件，或從中移除區段，請上傳具有新區段清單的新資訊清單檔。資訊清單名稱可以保持相同。

* 若要下載資訊清單檔的內容，您必須將查詢 `multipart-manifest=get` 新增至指令。您接收的內容不會與上傳的內容相同。

    ```
    curl -O -X GET -H "X-Auth-Token:<token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=get
    ```
    {: pre}

* 若要刪除資訊清單，請執行下列指令：

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>
    ```
    {: pre}

* 若要刪除資訊清單及所有區段，請在資訊清單名稱後面加上查詢 `multipart-manifest=delete`：

    ```
    curl -i -X DELETE -H "X-Auth-Token: <token>" https://<object-storage_url>/<container_two>/<object_name>?multipart-manifest=delete
    ```
    {: pre}
