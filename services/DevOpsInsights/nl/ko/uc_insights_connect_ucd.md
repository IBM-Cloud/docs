---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IBM UrbanCode Deploy 서버를 Delivery Insights에 연결
{: #connect_ucd}

Delivery Insights에서 IBM UrbanCode Deploy 서버의 데이터를 보려면 서버에 패치를 설치한 다음 해당 서버를 DevOps Connect에 연결해야 합니다.
{:shortdesc}

## 시작하기 전에

- DevOps Connect의 인스턴스 설정을 포함하여 [전제조건](uc_insights_prereqs.html)을 참조하십시오.
- IBM UrbanCode Deploy 서버가 버전 6.2 이상이어야 합니다.

## 프로시저

1. IBM UrbanCode Deploy 서버에 패치를 설치하십시오. DevOps Connect와 통신하려면 모든 버전의 IBM UrbanCode Deploy에 패치가 필요합니다. 
  1. 다음 페이지로 이동하고 올바른 패치를 다운로드하여 IBM UrbanCode Deploy 버전의 올바른 패치를 다운로드하십시오.
  [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/)

  1. 파일을 추출하십시오. 서버에 추가해야 하는 하나 이상의 패치 파일을 포함합니다.

  1. 서버를 중지하십시오. [서버 시작 및 중지](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.install.doc/topics/run_server.html)를 참조하십시오.

  1. <code><em>application_data</em>/patches</code> 폴더에 배치 파일을 두십시오. 여기서 <code><em>application_data</em></code>는 서버 애플리케이션 데이터 폴더입니다. 기본 애플리케이션 데이터 폴더는 Linux에서는 `/opt/ibm-ucd/server/appdata`이며, Windows에서는 `C:\Program Files\ibm-ucd\server\appdata`입니다. 고가용성 시스템에서 애플리케이션 데이터 폴더는 항상 각 서버가 액세스할 수 있는 공유 네트워크 드라이브에 있습니다.

  1. 선택사항: 서버가 중지된 동안 이 서버에서 데이터 가져오기의 중요도를 높이려면 데이터베이스에서 다음 SQL 명령을 실행하십시오.  
  ```
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_app_process_request(submitted_time); 
  create index rt_cpr_submitted_time on MyUCDDatabase.rt_comp_process_request(component_id, submitted_time);
  ```
  `MyUCDDatabase`의 데이터베이스 이름을 사용하십시오.
  <!-- Ross says that this will not be necessary for versions 6.2.4.1 and later if he gets his code changes in. -->

  1. 서버를 시작하십시오. 

    **참고:** IBM UrbanCode Deploy 서버가 시작되기까지 평소보다 더 오랜 시간을 기다려야 할 수도 있습니다. 서버가 결국 시작되지 않거나 제대로 작동하지 않으면 패치 파일을 삭제하고 서버를 다시 시작하십시오. 패치 파일은 영구적으로 서버에 영향을 미치지 않습니다.

1. 서버가 DevOps Connect에 연결하려면 일부 IBM UrbanCode Deploy 버전에 추가 패치가 필요합니다. IBM UrbanCode Deploy 버전 6.2 - 6.2.1.2를 사용 중인 경우 서버에서 다음 추가 패치를 설치해야 합니다.
  1. 다음 패치를 다운로드하십시오. [http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar](http://public.dhe.ibm.com/software/products/UrbanCode/plugins/ucsync/patches/ibmucd/ucd-6.2.1.1-WI149200-CLI-Updates-for-UCSync.jar).
  1. 서버를 중지하십시오. 
  1. 패치 파일을 <code><em>application_data</em>/patches</code> 폴더에 두십시오.
  1. 서버를 시작하십시오.

1. DevOps Connect와 IBM UrbanCode Deploy 서버 사이에 통합을 작성하십시오.  
  **중요:** 통합을 처음 실행할 때 DevOps Connect에서 이전 90일 동안의 데이터를 검색합니다. 다량의 배치 데이터가 있으면 이 프로세스는 시간이 오래 걸릴 수 있습니다. 90일 미만 동안의 데이터를 검색하려면 [문제점 해결](uc_insights_connect_ucd.html#troubleshooting)을 참조하십시오.
  1. IBM UrbanCode Deploy에서 인증 토큰을 작성하십시오. [토큰](https://www.ibm.com/support/knowledgecenter/SS4GSP_6.2.3/com.ibm.udeploy.admin.doc/topics/security_token.html)을 참조하십시오.
  1. DevOps Connect에서 **통합**을 클릭한 다음 **새로 추가**를 클릭하십시오.
  1. 통합의 이름과 설명을 지정하십시오. DevOps Connect의 기본 위치는 `https://hostname:8443/`입니다. 여기서 `hostname`은 DevOps Connect를 호스트하는 시스템의 호스트 이름입니다.
  1. **통합 유형** 목록에서 **IBM UrbanCode Deploy for Cloud Reporting**을 선택하십시오.
  1. **서버 URI** 필드에 IBM UrbanCode Deploy 서버의 공용 URL(예: `https://my_UCD.example.com:8447`)을 입력하십시오.
  1. **인증 토큰** 필드 IBM UrbanCode Deploy를 통해 생성한 인증 토큰을 입력하거나 붙여넣으십시오.
  1. **관리 사용자** 필드에 쉼표로 구분된 IBM ID 목록을 입력하여 DevOps Connect 인터페이스에 대한 액세스 권한을 제공하십시오.
  1. 선택사항: **통합 실행**을 클릭하여 즉시 통합을 실행하십시오. 기본적으로 통합은 1분마다 실행됩니다.
  1. **저장**을 클릭하십시오. 

  ![DevOps Connect에서 통합 설정](images/uc_insights_dc_integration.gif)

이제 데이터가 Delivery Insights와 동기화됩니다. 이제 이 데이터를 기반으로 하는 보고서를 작성하고 볼 수 있습니다.

## 문제점 해결
{: #troubleshooting}

여러 애플리케이션과 컴포넌트 프로세스 요청이 IBM UrbanCode Deploy 서버 데이터베이스에 저장되어 있으면 검색 프로세스 중에 오류가 발생할 수 있습니다. 다음 텍스트와 비슷한 메시지가 서버 출력 로그에 기록됩니다.

`ORA-01652: 테이블스페이스 TEMP에서 임시 세그먼트를 128만큼 확장할 수 없음`

이 동작을 임시로 해결하려면 플러그인의 `plugin.properties` 파일을 편집하여 검색할 데이터 기간(일)을 줄이십시오. `plugin.properties` 파일은 DevOps Connect를 설치한 컴퓨터의 `~/.ibm/cloud-sync/plugins/settings/reporting-ucd-plugin/` 디렉토리에 있습니다. 다음 행을 편집하여 번호 부호(#)를 제거하고 기간(일)을 줄이십시오.

`#numDaysToRetrieve=90`

예를 들어, 행을 다음 텍스트로 변경하여 이전 30일 동안의 데이터만 검색하십시오.

`numDaysToRetrieve=30`

파일을 저장한 다음 통합을 다시 실행하십시오. 서버 로그를 확인하여 오류가 더 이상 발생하지 않는지 확인하십시오.
