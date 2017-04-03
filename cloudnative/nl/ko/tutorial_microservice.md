---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# 마이크로서비스 기본 스타터의 엔드-투-엔드 튜토리얼
{: #tutorial}

다음 엔드-투-엔드 튜토리얼은 설치해야 하는 도구를 포함하여 마이크로서비스 기본 스타터에서 프로젝트를 작성하는 단계를 안내하고, 이어서 프로젝트 코드를 실행하는 단계를 안내합니다. 

## 개발자 도구 설치
{: #dev_tools}

[전제 조건 개발자 도구 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](get_code.html#prereq-dev-tools){: new_window}를 설치했는지 확인하십시오. 


## {{site.data.keyword.dev_console}}을 사용하여 프로젝트 작성
{: #create-devex}

1. {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}에서 프로젝트를 작성하십시오. 

	1. {{site.data.keyword.dev_console}}의 **시작하기** 페이지에서 **프로젝트 작성**을 클릭하십시오. 

		또는 **프로젝트** 페이지에서 **프로젝트 작성**을 클릭할 수 있습니다. 

	2. **마이크로서비스**를 선택하고 **다음**을 클릭하십시오. 

	3. **기본**을 선택하고 **다음**을 클릭하십시오. 

	4. 프로젝트 이름을 입력하십시오. 이 튜토리얼의 경우 `MicroserviceProject`를 사용하십시오.    

	5. 호스트 이름을 입력하십시오. 이 튜토리얼의 경우 `devhost`를 사용하십시오.  
   
	6. **작성**을 클릭하십시오.

2. 선택사항: 데이터 기능을 추가하십시오. 

	1. **프로젝트 개요** 페이지에서 **데이터**에 대한 **보기**를 클릭하십시오. 

      **기능 > 데이터** 페이지에서 **작성** 또는 **기존 추가**를 선택할 수도 있습니다. 

   2. 서비스 이름을 입력하고 **작성**을 클릭하십시오. 

3. 프로젝트 코드를 생성하십시오. 

	1. **프로젝트 개요** 페이지에서 **코드 가져오기**를 클릭하여 언어를 선택하십시오. 
   
		또는 **코드** 페이지를 클릭할 수 있습니다.
      
	2. **코드 생성**을 클릭하십시오. 
   
	3. 프로젝트 코드 생성이 완료되면 **코드 다운로드**를 클릭하여 프로젝트 아카이브를 다운로드하십시오.

4. 선택사항: 새 언어를 생성하도록 [프로젝트를 업데이트하십시오](project_overview_page.html#update_language). 


## {{site.data.keyword.dev_cli_notm}}을 사용하여 프로젝트 작성
{: #create-cli}

1. [{{site.data.keyword.dev_cli_short}}](dev_cli.html)을 설치했는지 확인하십시오. 

2. 터미널 프롬프트에서 원하는 로컬 디렉토리로 이동하여 다음 명령을 실행하십시오. 
  
	```
	bx dev create
	```
	{: codeblock}

3. 프롬프트가 표시되면 다음 값을 제공하십시오. 

	* 패턴 선택: 4(마이크로서비스)
	* 스타터 선택: 1(기본)
	* 플랫폼 선택: 3(Java)
	* 프로젝트의 이름 입력: `MicroserviceProjectCLI`

4. 프로젝트에 서비스를 추가하려면 질문 프롬프트에서 `y`를 입력하고 나머지 질문에 응답하십시오. 

5. `MicroserviceProjectCLI`가 저장되면 `MicroserviceProjectCLI` 폴더로 이동하십시오. 

6. 이 시점에서 고유 코드를 추가하거나, 프로젝트를 빌드하거나, 프로젝트를 실행할 수 있습니다. 
 
 
## {{site.data.keyword.dev_cli_notm}}을 사용하여 프로젝트 실행
{: #running-dev-plugin}

1. 현재 프로젝트 디렉토리에서 프로젝트를 빌드하려면 다음 명령을 입력하십시오. 

	```
	bx dev build
	```     
	{: codeblock}

2. 현재 프로젝트 디렉토리에서 프로젝트를 빌드하고 실행하려면 다음 명령을 입력하십시오. 

	```
	bx dev run
	```
	{: codeblock}	

3. 서버에서 curl을 사용하여 애플리케이션에 액세스할 수 있습니다. 

	```
	curl http://localhost:8080	
	```
	{: codeblock}
