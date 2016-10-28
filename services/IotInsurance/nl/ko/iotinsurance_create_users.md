---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# 사용자 및 실드 연관 작성
{: #gettingstartedtemplate}
마지막 업데이트 날짜: 2016년 9월 15일
{: .last-updated}

{{site.data.keyword.iotinsurance_short}} 서비스를 작성하고 필수 지원 서비스와 앱을 배치한 후 권한이 부여된 사용자와 실드 연관을 작성하여 서비스를 테스트할 수 있습니다.
{:shortdesc}

**전제조건** 시작하기 전에 다음 전제조건에 부합하는지 확인하십시오. 

- 컴퓨터에 설치된 [Node.js](https://nodejs.org/en/).   
- Eclipse와 같은 Node.js 사용 런타임 환경. 
- Git 소프트웨어와 [API 예제의 GitHub 소스 코드 저장소](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)에 대한 액세스 권한.
 또는 [소스 코드 파일로 아카이브](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip)를 다운로드할 수 있습니다. 
- 준비된 소스 코드. 소스 코드를 준비하려면 다음 단계를 완료하십시오. 
  1. [GitHub 소스 코드 저장소](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs)를 컴퓨터에 복제하거나 다운로드하십시오. 
  2. 복사된 소스 코드 파일을 포함하는 폴더로 이동하는 명령 프롬프트를 사용하고 `npm install` 명령을 실행하여 프로젝트의 오픈 소스 필수 소프트웨어를 설치하십시오. 

샘플 모바일 앱과 대시보드의 기능을 테스트하는 데 사용할 수 있는 사용자를 작성하십시오. 

1. {{site.data.keyword.iotinsurance_short}} 시스템에서 사용자를 작성하십시오. 
  1. createUser.js 파일을 편집하여 **user** 변수의 값을 고유 사용자 정보로 대체하십시오. 
  2. 파일을 저장하십시오. 
  3. `node createUser.js`를 실행하십시오. 프로세스를 완료하는 데 시간이 약간 걸립니다. 
  4. 다음 단계에서 필요하므로 사용자 이름을 기록해두십시오. 
2. 사용자의 실드 연관을 작성하십시오. 
  1. createUserShieldAssociation.js 파일을 편집하여 이전 단계에서 기록해둔 사용자 이름을 **username** 변수에 추가하십시오. 
  2. 파일을 저장하십시오. 
  3. `node createUserShieldAssociation.js`를 실행하십시오. 실드에 대한 자세한 정보는 [컴포넌트](iotinsurance_overview.html#components})의 내용을 참조하십시오. 
3. (선택사항) 분석 엔진은 자동으로 업데이트됩니다. 그러나 올바른 데이터가 표시되지 않는 경우 `node updateAnalyticsEngine.js`를 실행하여 분석 엔진을 새로 고칠 수 있습니다. 
4. (선택사항) 사용자와 관련된 위험 이벤트를 시뮬레이션하십시오. 
  1. simulateHazard.js 파일을 편집하여 이전 단계에서 기록해둔 사용자 이름을 **usr** 변수에 추가하십시오. 
  2. 파일을 저장하십시오. 
  3. `node simulateHazard.js`를 실행하십시오. 
5. (선택사항) `node createHistoricalData.js`를 실행하여 시뮬레이션된 히스토리 데이터의 세트를 작성하십시오. 


# 관련 링크
{: #rellinks}

## API 참조
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API 예](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## 관련 링크
{: #general}
* [개발자 지원 포럼](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [스택 오버플로우 지원 포럼](http://stackoverflow.com/questions/tagged/ibm-bluemix)
