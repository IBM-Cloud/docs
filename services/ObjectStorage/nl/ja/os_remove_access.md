---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# アクセス権限の削除 

アクセス制御リストを使用して、コンテナーまたはオブジェクトのアクセス権限を削除できます。
{: shortdesc}

読み取り ACL をコンテナーから削除するには、以下のいずれかのコマンドを実行します。

* Swift コマンド:

```
  swift post <container_name> --read-acl “”
  ```
{: pre}

* cURL コマンド:

```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
{: pre}

書き込み ACL をコンテナーから削除するには、以下のいずれかのコマンドを実行します。

* Swift コマンド:

```
    swift post <container_name> --write-acl “”
    ```
{: pre}

* cURL コマンド:

```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
{: pre}

ACL が削除されたことを確認するには、以下のいずれかのコマンドを実行します。

* Swift コマンド:

```
    swift stat <container_name>
    ```
{: pre}

* 以下の出力例では、Read ACL と Write ACL の両方がブランクで示されています。これは、該当するアクセス権限が削除されたことを意味します。

```
           Account: AUTH_c727d7e248b448f6b268f31a1bd8691e
         Container: Test
           Objects: 1
             Bytes: 31512
          Read ACL:
         Write ACL:
           Sync To:
          Sync Key:
     Accept-Ranges: bytes
  X-Storage-Policy: standard
       X-Timestamp: 1462818314.11220
        X-Trans-Id: txf04968bc9ef8431982b77-005772e34b
      Content-Type: text/plain; charset=utf-8
  ```
{: screen}

* cURL コマンド:

```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
{: pre}
