---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Jenkins와 {{site.data.keyword.DRA_short}} 통합
{: #toolchain_configure_jenkins}

모니터할 {{site.data.keyword.DRA_full}}의 정책을 정의한 후에는 그 다음 단계로 {{site.data.keyword.DRA_short}}를 도구 체인에 추가하고 Continuous Delivery Pipeline을 구성하십시오.
{:shortdesc}

<!--##Configuring a Jenkins project-->

{{site.data.keyword.DRA_short}}를 한 개의 Jenkins 프로젝트 또는 여러 관련 Jenkins 프로젝트에 통합할 수 있습니다. 그러면 {{site.data.keyword.DRA_short}} 대시보드에 빌드 품질 데이터를 수신할 뿐 아니라 품질 게이트를 설정할 수 있습니다. 

##전제조건    
{: #DI_jenkins_prereqs}

* 로컬 Jenkins 프로젝트나 Jenkins 프로젝트를 실행하는 서버에 액세스할 수 있어야 합니다. 

##{{site.data.keyword.DRA_short}} 플러그인 설치
{: #DI_jenkins_install}

Jenkins 프로젝트에 {{site.data.keyword.DRA_short}} 플러그인을 설치하려면 다음 단계를 수행하십시오. 

  1. 플러그인의 GitHub 저장소에서 [IBM DevOps Insight Plugin 설치 파일(.hpi)을 다운로드](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi)하십시오.
  2. Jenkins 설치에서 **Jenkins 관리**를 클릭하고 **플러그인 관리**를 선택한 다음 **고급** 탭을 클릭하십시오. 
  3. **파일 선택**을 클릭하고 DevOps Insight 플러그인 설치 파일을 선택하십시오. 
  4. **업로드**를 클릭하십시오. 
  5. Jenkins를 다시 시작하고 플러그인이 설치되었는지 확인하십시오.

##Jenkins와 {{site.data.keyword.DRA_short}} 통합    
{: #DI_jenkins_integrate}

플러그인을 설치한 후 {{site.data.keyword.DRA_short}}를 Jenkins 설치에 통합하기 전에 [제어 센터](https://control-center.stage1.ng.bluemix.net/)로 이동하여 정책을 한 개 이상 작성하십시오.

이미 소유한 개별 작업에 {{site.data.keyword.DRA_short}}를 사용하려면 다음 단계를 수행하십시오.

1. **빌드 정보를 {{site.data.keyword.DRA_short}}에 공개**, **배치 정보를 {{site.data.keyword.DRA_short}}에 공개** 또는 **테스트 결과를 {{site.data.keyword.DRA_short}}에 공개** 유형으로 사후 빌드 조치를 추가하십시오. 해당 유형은 작업 유형(빌드, 배치 또는 테스트)에 일치해야 합니다. 필수 필드를 완료하십시오. 
  * 신임 정보 필드에서 Bluemix ID와 비밀번호를 선택하십시오. Jenkins에서 저장하지 않은 경우 **추가** 단추를 클릭하여 추가하고 저장하십시오. 
  * 빌드 작업 이름 필드에서 Jenkins에 지정한 것과 동일하게 빌드 작업의 이름을 지정하십시오. 빌드가 테스트 작업과 함께 수행되는 경우 이 필드를 비워 두십시오. 빌드 작업이 Jenkins 외부에서 발생하는 경우 **빌드를 Jenkins 외부에서 수행함**을 선택하고 빌드 번호와 빌드 URL을 지정하십시오. 
  * 결과 파일 위치 필드에 결과 파일의 위치를 지정하십시오. 테스트에서 결과 파일을 생성하지 않으면 이 필드를 비워 두십시오. 이 플러그인은 현재 테스트 작업의 상태를 기반으로 기본 결과 파일을 업로드합니다. 
3. *선택사항*: 테스트 작업의 DRA 정책 게이트로 다운스트림 배치 작업을 제어하려면 **DevOps Risk Analytics 게이트** 유형으로 다른 사후 빌드 조치를 추가하고 필수 필드를 작성하십시오. 이 게이트를 사용하면 테스트 작업에서 연관 정책을 충족하지 못하는 경우 다운스트림 작업을 실행하지 않습니다. 
4. **적용**을 클릭한 후 **저장**을 클릭하십시오. 

프로젝트 페이지에서 **지금 빌드**를 클릭하여 프로젝트를 실행하십시오. 

빌드를 실행한 후에 [제어 센터](https://control-center.stage1.ng.bluemix.net/)로 이동하여 대시보드에서 빌드 상태를 확인하십시오. 정책 게이트를 구성한 경우, 현재 빌드의 상태 페이지에서도 {{site.data.keyword.DRA_short}} 결과를 볼 수 있습니다. 
