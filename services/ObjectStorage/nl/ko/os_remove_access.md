---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 액세스 제거 

액세스 제어 목록을 사용하여 컨테이너나 오브젝트에 대한 액세스 권한을 제거할 수 있습니다.
{: shortdesc}

컨테이너에서 읽기 ACL을 제거하려면 다음 명령 중 하나를 실행하십시오. 

* Swift 명령:

```
swift post <container_name> --read-acl “”
```
{: pre}

* cURL 명령: 

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Read: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

컨테이너에서 쓰기 ACL을 제거하려면 다음 명령 중 하나를 실행하십시오. 

* Swift 명령:

```
swift post <container_name> --write-acl “”
```
{: pre}

* cURL 명령: 

```
curl -i <OS_STORAGE_URL> -X POST -H "Content-Length: 0" -H "X-Container-Write: " -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}

ACL이 제거되었는지 확인하려면 다음 명령 중 하나를 실행하십시오. 

* Swift 명령:

```
swift stat <container_name>
```
{: pre}

* 다음 예제 출력에서는 읽기 ACL과 쓰기 ACL 모두를 공백으로 표시하며, 이는 액세스 권한이 제거되었음을 의미합니다. 

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

* cURL 명령: 

```
curl -i <OS_STORAGE_URL> -I -H "X-Auth-Token: <OS_AUTH_TOKEN>"
```
{: pre}
