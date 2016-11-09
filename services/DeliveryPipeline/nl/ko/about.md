---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}


# {{site.data.keyword.deliverypipeline}} 정보
{: #deliverypipeline_about}
마지막 업데이트 날짜: 2016년 8월 29일
{: .last-updated}

IBM&reg; Bluemix&reg; {{site.data.keyword.deliverypipeline}} 서비스(파이프라인이라고도 함)는 Bluemix 프로젝트의 연속 배치를 자동화합니다. 파이프라인에서는 일련의 단계에서 입력을 검색하고 작업(예: 빌드, 테스트 및 배치)을 실행합니다.
{:shortdesc}

다음 절에서는 파이프라인의 기반이 되는 개념적 세부사항을 설명합니다. 

## 단계
{: #deliverypipeline_stages}

단계는 코드가 빌드, 배치 및 테스트됨에 따라 입력 및 작업을 구성합니다. 단계는 소스 제어 저장소 또는 다른 단계의 빌드 작업으로부터의 입력을 승인합니다. 첫 번째 단계를 작성하면 **입력** 탭에 기본 설정이 자동으로 설정됩니다.

단계의 입력은 해당 단계에 포함된 작업에 전달되며, 각 작업에는 실행 장소인 클린 컨테이너가 제공됩니다. 하나의 단계에 있는 작업은 서로 아티팩트를 전달할 수 없습니다.

모든 작업에서 사용할 수 있는 단계 환경 특성을 정의할 수 있습니다. 예를 들어, 하나의 단계에서 배치 및 테스트 작업에 단일 URL을 전달하는 `TEST_URL` 특성을 정의할 수 있습니다. 배치 작업은 해당 URL에 배치하고 테스트 작업은 해당 URL에서 실행 앱을 테스트합니다.

기본적으로 단계에서 빌드 및 배치는 프로젝트의 소스 제어 저장소에 변경사항이 전달될 때마다 자동으로 트리거됩니다. 단계 및 작업은 직렬로 실행되므로 작업 플로우를 제어할 수 있습니다. 예를 들어, 배치 단계 앞에 테스트 단계를 놓을 수 있습니다. 테스트 단계의 테스트가 실패하면 배치 단계가 실행되지 않습니다.

특정 단계를 면밀히 제어할 수 있습니다. 해당 입력에서 변경이 발생할 때마다 단계가 실행되도록 하지 않으려면 해당 기능을 사용 불가능하게 설정하십시오. **입력** 탭의 단계 트리거 섹션에서 **이 단계를 수동으로 실행할 때만 작업 실행**을 클릭하십시오.

![입력 탭](./images/input_tab_only_execute.png)

## 작업
{: #deliverypipeline_jobs}

작업은 단계 내의 실행 단위입니다. 단계에는 여러 작업이 포함될 수 있으며, 단계 내의 작업은 순차적으로 실행됩니다. 기본적으로 하나의 작업이 실패하면 단계 내의 후속 작업이 실행되지 않습니다.

![단계 내의 빌드 및 테스트 작업](./images/jobs.png)

작업은 각 파이프라인 실행을 위해 작성된 Docker 컨테이너 내의 개별 작업 디렉토리에서 실행됩니다. 작업이 실행되기 전에 해당 작업 디렉토리는 단계 레벨에서 정의된 입력으로 채워집니다. 예를 들어, 하나의 테스트 작업과 하나의 배치 작업을 포함하는 단계가 있을 수 있습니다. 하나의 작업에 종속 항목을 설치하는 경우 다른 작업에서는 이를 사용할 수 없습니다. 그러나 단계의 입력에서 종속 항목을 사용 가능하게 설정하면 두 작업 모두 해당 종속 항목을 사용할 수 있습니다.

단순 유형 빌드 작업을 제외하곤, 작업을 구성할 때 빌드, 테스트 또는 배치 명령이 포함된 UNIX 쉘 스크립트를 포함시킬 수 있습니다. 작업은 임시 컨테이너에서 실행되므로 작업이 같은 단계에 속하는 경우에도 한 작업의 조치는 다른 작업의 실행 환경에 영향을 미칠 수 없습니다.

작업이 실행된 후에는 그 작업을 위해 작성된 컨테이너가 버려집니다. 작업 실행의 결과는 유지될 수 있지만 작업이 실행된 환경은 유지되지 않습니다.

**참고**: 작업은 최대 60분 동안 실행될 수 있습니다. 작업이 이 한계를 초과하면 작업이 실패합니다. 하나의 작업이 이 한계를 초과하는 경우에는 작업을 여러 개의 작업으로 나누십시오. 예를 들어, 작업이 세 개의 태스크를 수행하는 경우 이 작업을 세 개의 작업(태스크당 하나의 작업)으로 나눌 수 있습니다.

단계에 작업을 추가하는 방법을 학습하려면 [단계에 작업 추가를 참조하십시오](./build_deploy.html#deliverypipeline_add_job).

### 빌드 작업

빌드 작업은 배치를 준비하기 위해 프로젝트를 컴파일합니다. 빌드 작업은 빌드 아카이브 디렉토리로 전송할 수 있는 아티팩트(기본적으로 프로젝트의 루트 디렉토리에 배치됨)를 생성합니다.

빌드 작업에서 입력되는 작업은 빌드 아티팩트를 작성 시와 동일한 구조로 참조해야 합니다. 예를 들어, 빌드 작업이 빌드 아티팩트를 `output` 디렉토리에 아카이브하는 경우 배치 스크립트는 프로젝트 루트 디렉토리가 아니라 `output` 디렉토리를 참조하여 컴파일된 프로젝트를 배치합니다.

**참고**: 빌드 작업에 **단순** 빌더 유형을 선택하는 경우 빌드 프로세스를 건너뜁니다. 이 경우에는 코드가 컴파일되지 않지만 있는 그대로 배치 단계에 전송됩니다. 빌드 및 배치 모두에 대해 **단순** 이외의 빌더 유형을 선택하십시오.

#### 빌드 스크립트의 환경 특성
빌드 작업의 빌드 쉘 명령 내에 환경 특성을 포함시킬 수 있습니다. 이러한 특성을 통해 작업 실행 환경에 대한 정보에 액세스할 수 있습니다. 자세한 정보는 [{{site.data.keyword.deliverypipeline}} 서비스의 환경 특성 및 리소스를 참조하십시오](./deploy_var.html).

### 배치 작업

배치 작업은 프로젝트를 하나의 앱으로 Bluemix에 업로드하며 URL에서 액세스할 수 있습니다. 프로젝트가 배치되면 Bluemix 대시보드에서 배치된 앱을 찾을 수 있습니다. 빌드 및 배치 작업을 개별 단계로 구성하거나 동일한 단계에 추가하여 자동으로 실행할 수 있습니다.

배치 작업은 새 앱을 배치하거나 기존 앱을 업데이트할 수 있습니다. 처음에 다른 방법(예: Cloud Foundry 명령 인터페이스 또는 Web IDE의 run bar)을 사용하여 앱을 배치한 경우에도 배치 작업을 사용하여 앱을 업데이트할 수 있습니다. 앱을 업데이트하려면 배치 작업에서 해당 앱의 이름을 사용하십시오.

하나 또는 다수의 지역과 서비스에 배치할 수 있습니다. 예를 들면, 개발 아티팩트가 IBM Containers를 사용하고 한 지역에서 테스트되며 여러 지역의 프로덕션에 배치되도록 {{site.data.keyword.deliverypipeline}} 서비스를 설정할 수 있습니다. 자세한 정보는
				[지역](../../overview/index.html#ov_intro__reg)을 참조하십시오.

#### 배치 스크립트의 환경 특성

배치 작업의 배치 스크립트 내에 환경 특성을 포함시킬 수 있습니다. 이러한 특성을 통해 작업 실행 환경에 대한 정보에 액세스할 수 있습니다. 자세한 정보는 [{{site.data.keyword.deliverypipeline}} 서비스의 환경 특성 및 리소스를 참조하십시오](./deploy_var.html).

### 테스트 작업
조건이 충족되도록 하려면 빌드 및 배치 작업의 앞이나 뒤에 테스트 작업을 포함시키십시오. 필요에 따라 단순하거나 복잡하도록 테스트 작업을 사용자 정의할 수 있습니다. 예를 들어, cURL 명령을 실행하고 특정 응답을 예상할 수 있습니다. 또한 단위 테스트 스위트를 실행하거나 써드파티 서비스(예: Sauce Labs)를 사용하여 기능 테스트를 트리거할 수도 있습니다.

테스트로 인해 JUnit XML 형식의 결과 파일이 생성되는 경우, 결과 파일에 기반한 보고서가 각 테스트 결과 페이지의 **테스트** 탭에 표시됩니다. 테스트가 실패하면 작업도 실패합니다.

#### 테스트 스크립트의 환경 특성

테스트 작업의 스크립트에 환경 특성을 포함시킬 수 있습니다. 이러한 특성을 통해 작업 실행 환경에 대한 정보에 액세스할 수 있습니다. 자세한 정보는 [{{site.data.keyword.deliverypipeline}} 서비스의 환경 특성 및 리소스를 참조하십시오](./deploy_var.html).

## Manifest 파일
{: #deliverypipeline_manifest}

이름이 `manifest.yml`이고 프로젝트의 루트 디렉토리에 저장되는 Manifest 파일은 프로젝트가 Bluemix에 배치되는 방법을 제어합니다. 프로젝트의 Manifest 파일 작성에 대한 정보는 [애플리케이션 Manifest에 대한 Bluemix 문서를 참조하십시오](https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest). Bluemix와 통합하려면 프로젝트의 루트 디렉토리에 Manifest 파일이 있어야 합니다. 그러나 이 파일의 정보를 기반으로 배치하지 않아도 됩니다.

파이프라인에서는 `cf push` 명령 인수를 사용하여 Manifest 파일이 할 수 있는 모든 것을 지정할 수 있습니다. `cf push` 명령 인수는 배치 대상이 여러 개인 프로젝트에서 유용합니다. 여러 배치 작업이 모두 프로젝트 Manifest 파일에 지정된 라우트를 사용하려 하면 충돌이 발생합니다.

충돌을 피하려면 `cf push`와 그 뒤에 호스트 이름 인수 `-n` 및 라우트 이름을 사용하여 라우트를 지정하면 됩니다. 개별 단계의 배치 스크립트를 수정하면 여러 대상에 배치할 때 라우트 충돌을 피할 수 있습니다.

`cf push` 명령 인수를 사용하려면 배치 작업의 구성 설정을 열어 **배치 스크립트** 필드를 수정하십시오. 자세한 정보는 [Cloud Foundry 푸시 문서를 참조하십시오](http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push).

## 파이프라인 예
{: #deliverypipeline_example}

단순 파이프라인에는 세 개의 단계가 포함될 수 있습니다. 

1. 앱에서 빌드 프로세스를 컴파일하고 실행하는 빌드 단계
2. 앱의 인스턴스를 배치한 후 거기서 테스트를 실행하는 테스트 단계
3. 테스트한 앱의 프로덕션 인스턴스를 배치하는 프로덕션 단계

다음 개념 다이어그램에 이 파이프라인이 표시되어 있습니다. 

![파이프라인에 단계 및 작업이 포함된 개념 다이어그램](./images/diagram.jpg)

*3단계 파이프라인의 개념 모델*

단계는 저장소와 빌드 작업에서 입력을 받으며 단계 내의 작업은 순차적으로, 그리고 서로 독립적으로 실행됩니다. 파이프라인 예에서, 테스트 및 프로덕션 단계가 모두 빌드 단계의 출력을 입력으로 받지만 단계는 순차적으로 실행됩니다.

<!--
[1]: https://www.ng.bluemix.net/docs/manageapps/deployingapps.html#appmanifest
[2]: https://www.ng.bluemix.net/docs/#services/DeliveryPipeline/index.html#getstartwithCD
[3]: http://docs.cloudfoundry.org/devguide/installcf/whats-new-v6.html#push
[4]: https://console.ng.bluemix.net/?ace_base=true/#/pricing/cloudOEPaneId=pricing
[5]: ./images/open_logs.png
[6]: #manifests
[7]: ./images/runbar-annotated-dark.png
[8]: ./images/input_tab_only_execute.png
[9]: ./images/deploy_to.png
[10]: ./images/view_logs_and_history.png
[11]: ./images/play_button.png
[12]: ./images/basicAnimate.gif
[13]: ./images/AddStage.png
[14]: ./images/AddJob.png
[15]: ./images/jobs.png
[16]: ./images/RunStage.png
[17]: https://www.ng.bluemix.net/docs/starters/container_pipeline.html#container_pipeline
[18]: ../../../tutorials/basicbuild
[19]: #add_stage
[20]: #add_job
[21]: ../deploy_ext
[22]: ./images/pipeline_settings_icon.png
[23]: https://www.ng.bluemix.net/docs/services/reqnsi.html#add_service
[24]: ../deploy_var
[25]: ./images/click_stage_run_number.png
[26]: ./images/diagram.jpg
-->
