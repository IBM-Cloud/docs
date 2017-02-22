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

# 使用目录 

Swift 没有真正的目录结构，而是使用命名来表示目录布局。如果指定目录名称，那么会将该目录名称附加到所有文件名以作为相对路径的一部分。
{: shortdesc}

## 使用 Swift CLI 向容器添加目录

要向容器添加目录，必须在本地设备上具有目录结构。

1. 在本地创建目录，并保存文件。
2. 运行以下命令以向容器上传目录。

    ```
swift upload <container_name> <directory_name>
```
    {: pre}

## 使用 CLI 下载目录
要下载目录结构，请使用 `-prefix` 参数来指示要下载的目录或目录结构。

1. 运行以下命令以下载目录。

    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
