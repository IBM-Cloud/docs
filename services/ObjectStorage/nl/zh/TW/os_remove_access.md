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


# 移除存取權 

您可以利用存取控制清單，移除容器或物件的存取權。
{: shortdesc}

若要從容器中移除讀取 ACL，請執行下列其中一個指令。

* Swift 指令：

```
  swift post <container_name> --read-acl ""
  ```
{: pre}

* cURL 指令：

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

若要從容器中移除寫入 ACL，請執行下列其中一個指令。

* Swift 指令：

```
    swift post <container_name> --write-acl ""
    ```
{: pre}

* cURL 指令：

```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
{: pre}

若要驗證您已移除 ACL，請執行下列其中一個指令。

* Swift 指令：

```
    swift stat <container_name>
    ```
{: pre}

* 下列範例輸出將「讀取 ACL」及「寫入 ACL」顯示為空白，這表示已移除存取權。

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

* cURL 指令：

```
    curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
{: pre}
