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


# 除去访问权 

您可以使用访问控制表来除去对容器或对象的访问权。
{: shortdesc}

要从容器中除去读 ACL，请运行下列其中一个命令。

* Swift 命令：

```
  swift post <container_name> --read-acl “”
  ```
{: pre}

* cURL 命令：

```
    curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
    ```
{: pre}

要从容器中除去写 ACL，请运行下列其中一个命令。

* Swift 命令：

```
  swift post <container_name> --write-acl “”
  ```
{: pre}

* cURL 命令：

```
  curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
{: pre}

要验证是否已除去 ACL，请运行下列其中一个命令。

* Swift 命令：

```
  swift stat <container_name>
  ```
{: pre}

* 以下示例输出中显示的“读 ACL”和“写 ACL”均为空白，这表示访问权已除去。

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

* cURL 命令：

```
  curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
  ```
{: pre}
