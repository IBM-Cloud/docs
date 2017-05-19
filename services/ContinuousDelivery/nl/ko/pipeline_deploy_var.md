---

copyright:
  years: 2016
lastupdated: "2017-4-11"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 환경 특성 및 리소스
{: #deliverypipeline_environment}

환경 특성 및 사전 설치된 리소스를 사용하여 IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 서비스와 상호작용할 수 있습니다. 예를 들어, 이들을 작업 스크립트 또는 테스트 명령에 통합할 수 있습니다.
{:shortdesc}

해당 **환경 특성** 탭에서 단계에 고유의 환경 특성을 추가할 수 있습니다. 단계의 모든 작업에서 환경 특성을 사용할 수 있습니다. 

환경 특성 탭에서 다음 네 가지 유형의 특성을 추가할 수 있습니다. 
* **텍스트**: 단일 행 값을 갖는 특성 키입니다. 
* **텍스트 영역**: 다중 행 값을 갖는 특성 키입니다. 
* **소스**: 단일 행 값을 갖는 특성 키입니다. 이 값은 별표로 표시됩니다. 
* **특성**: 프로젝트의 저장소에 있는 파일입니다. 이 파일에는 여러 특성이 포함될 수 있습니다. 각 특성은 자체 고유의 행에 위치해야 합니다. 키-값 쌍을 구분하려면 등호 부호(=)를 사용하십시오. 


다음 특성과 리소스는 기본적으로 파이프라인 환경에서 사용할 수 있습니다. 

<!--##Contents
* [Environment properties](#env)
    * [General purpose properties](#gen)
    * [Runtime and tool properties](#runtime)
    * [Deployment properties](#deployment)
* [Pre-installed resources](#resources)
    * [Runtimes and tools](#tools)
    * [Node modules](#node)-->

## 환경 특성
{: #deliverypipeline_envprop}

### 범용 특성

| 환경 특성 | 설명 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ARCHIVE_DIR | 아카이브 대상 디렉토리 또는 아카이브를 다운로드하는 디렉토리입니다. |
| BUILD_ID | 현재 작업 실행의 고유 ID입니다.  |
| BUILD_DISPLAY_NAME | BUILD_ID 값이며 접두부 "#"가 있습니다. |
| BUILD_NUMBER | 파이프라인 UI에 표시되는 증분 단계 ID입니다.  |
| GIT_BRANCH | 작업에서 입력으로 사용하는 Git 분기입니다. 이 특성은 Git 저장소를 입력으로 사용하는 작업에서만 사용할 수 있습니다. |
| GIT_COMMIT | 작업에서 입력으로 사용하는 Git 커미트입니다. 이 특성은 Git 저장소를 입력으로 사용하는 작업에서만 사용할 수 있습니다. |
| GIT_PREVIOUS_COMMIT | 마지막 성공한 작업 실행의 Git 커미트 값입니다. 이 특성은 Git 저장소를 입력으로 사용하는 작업에서만 사용할 수 있습니다. |
| GIT_URL | 작업에서 입력으로 사용하는 Git 저장소 URL입니다. 이 특성은 Git 저장소를 입력으로 사용하는 작업에서만 사용할 수 있습니다. |
| IDS_JOB_ID | 작업 구성의 고유 ID입니다. |
| IDS_JOB_NAME | 작업 구성의 이름입니다. |
| IDS_OUTPUT_PROPS | 단계 환경 특성의 쉼표로 구분된 이름입니다.  |
| IDS_PROJECT_NAME | 프로젝트 이름입니다(예: <code>Owner - Project Name</code>). |
| IDS_STAGE_NAME | 현재 단계의 이름입니다. |
| IDS_URL | 현재 파이프라인의 URL입니다. |
| IDS_VERSION | 배치 중인 빌드 번호 또는 SCM ID입니다. 이 특성은 배치 작업에만 사용할 수 있습니다.
| JOB_NAME | 현재 파이프라인 컨텍스트의 고유 작업 ID입니다. |
| PIPELINE_STAGE_INPUT_JOB_ID | 현재 단계의 입력인 작업의 ID입니다. |
| PIPELINE_STAGE_INPUT_REV | 현재 단계의 입력 변경내용입니다. |
| PIPELINE_INITIAL_STAGE_EXECUTION_ID | 파이프라인 실행의 고유 ID입니다. |
| TASK_ID | 작업의 현재 실행 고유 ID입니다. |
| TMPDIR | 임시 파일을 저장하는 디렉토리 위치입니다. |
| WORKSPACE | 현재 작업 디렉토리의 경로입니다. |

### 런타임 및 도구 특성

| 환경 특성 | 설명 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| ANT_HOME | Apache Ant 1.9.2의 경로입니다. |
| GRADLE_HOME | Gradle 1.11의 경로입니다. |
| JAVA_HOME | IBM&reg; Java&trade; 7의 경로입니다. |
| JAVA7_HOME | IBM Java 7의 경로입니다. |
| JAVA8_HOME | IBM Java 8의 경로입니다. |
| MAVEN_HOME | Apache Maven 3.2.1의 경로입니다. |
| NODE_HOME | Node.js 0.10.29의 경로입니다. |

### 배치 특성

| 환경 특성 | 설명 |
|-------------------------------------|------------------------------------------------------------------------------------------------------------------------------|
| CF_APP | 배치 시 배치할 앱의 이름입니다. 이 특성은 배치에 필요하며 스크립트 자체, 배치 작업 구성 인터페이스 또는 프로젝트의 `manifest.yml` 파일에서 지정할 수 있습니다. |
| CF_ORG | 배치 시 사용할 배치 대상 조직의 이름입니다.  |
| CF_ORGANIZATION_ID |  배치 시 사용할 배치 대상 조직의 ID입니다.  |
| CF_SPACE | 배치 시 사용할 배치 대상 영역의 이름입니다.  |
| CF_SPACE_ID | 배치 시 사용할 배치 대상 영역의 ID입니다.  |
| CF_TARGET_URL | 배치 시 사용할 IBM Bluemix&reg; 또는 Cloud Foundry의 URL입니다. |
| IDS_VERSION | 배치 시 사용할 배치 중인 앱의 버전 또는 소스 ID입니다. |

## 사전 설치된 리소스
{: #deliverypipeline_resources}

각 파이프라인마다 여러 런타임, 도구, 노드 모듈이 사전 설치됩니다. 

### 런타임 및 도구

*참고:* 모든 링크는 홈 디렉토리에 있습니다. 

| 리소스 | 링크 이름 | 경로 |
|----------|-----------|-----------|
|Apache Ant 1.9.2|ant |/opt/IBM/ant |
|Cloud Foundry CLI 6.14 |cf | /opt/IBM/cf |
|Gradle 1.12|gradle |/opt/IBM/gradle |
|Gradle 2.9 |gradle2 |/opt/IBM/gradle2 |
|IBM Java (default)|java |/opt/IBM/java |
|IBM Java 7 x86_64-71 |java7 |/opt/IBM/java7 |
|IBM Java 8 x86_64-80|java8 |/opt/IBM/java8 |
|Apache Maven 3.2.1 |maven |/opt/IBM/maven |
|IBM Node |node |/opt/IBM/node |
|IBM Rational Team Concert&trade; SCM Tools |RTC-SCM-Tools |/opt/IBM/RTC-SCM-Tools |

파이프라인 환경에서 IBM Node 0.10, 0.10.48, 0.12, 0.12.17, 4.2, 4.4.5, 4.6.0, 6.2.2, 6.7.0의 64비트 버전을 사용할 수 있습니다. 버전을 선택하려면 내보내기 명령을 사용하십시오. 

예를 들어, Node 0.12.7을 사용하려면 다음 명령을 입력하십시오.
`export PATH=/opt/IBM/node-v0.12/bin:$PATH`

Node 4.2.2를 사용하려면 다음 명령을 입력하십시오.
`export PATH=/opt/IBM/node-v4.2/bin:$PATH`

### 노드 모듈

다음 노드 모듈은 파이프라인 환경에 글로벌로 설치됩니다. 

* grunt@0.4.5
* grunt-cli@0.1.13
* grunt-contrib-concat@0.4.0
* grunt-contrib-jshint@0.10.0
* grunt-contrib-nodeunit@0.4.1
* grunt-contrib-qunit@0.5.1
* grunt-contrib-uglify@0.5.0
* grunt-contrib-watch@0.6.1
* karma@0.12.23
* karma-cli@0.0.4
* karma-jasmine@0.1.5
* karma-phantomjs-launcher@0.1.4
* phantomjs@1.9.10
