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

# 디렉토리 관련 작업 

Swift에는 실제 디렉토리 구조가 없지만 이름을 지정하여 디렉토리 레이아웃을 표시합니다. 디렉토리 이름을 지정하면 상대 경로의 일부로 모든 파일 이름에 첨부됩니다.
{: shortdesc}

## Swift CLI를 사용하여 컨테이너에 디렉토리 추가

디렉토리를 컨테이너에 추가하려면 디렉토리 구조를 로컬 디바이스에 배치해야 합니다. 

1. 로컬로 디렉토리를 작성하고 파일을 저장하십시오. 
2. 다음 명령을 실행하여 디렉토리를 컨테이너에 업로드하십시오.

    ```
swift upload <container_name> <directory_name>
```
    {: pre}

## CLI로 디렉토리 다운로드
디렉토리 구조를 다운로드하려면 `-prefix` 매개변수를 사용하여 다운로드하려는 디렉토리 또는 디렉토리 구조를 표시하십시오. 

1. 다음 명령을 실행하여 디렉토리를 다운로드하십시오. 

    ```
swift download <container_name> --prefix <directory>
```
    {: pre}
