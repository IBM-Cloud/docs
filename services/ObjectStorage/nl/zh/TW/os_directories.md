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

# 使用目錄 

Swift 沒有真正的目錄結構，但會使用命名來代表目錄佈置。如果您指定目錄名稱，則會將它附加至所有檔名，作為相對路徑的一部分。
{: shortdesc}

## 使用 Swift CLI 將目錄新增至容器

若要將目錄新增至容器，您必須在本端裝置上有現成的目錄結構。

1. 在本端建立目錄，並儲存您的檔案。
2. 執行下列指令，以將目錄上傳至您的容器。

    ```
swift upload <container_name> <directory_name>
```
    {: pre}

## 使用 CLI 下載目錄
若要下載目錄結構，請使用 `-prefix` 參數來表示您要下載的目錄或目錄結構。

1. 執行下列指令，以下載目錄。

    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
