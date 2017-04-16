---

copyright:
  years: 2015, 2016

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

# {{site.data.keyword.deliverypipeline}} 서비스 확장
{: #deliverypipeline_extending}
마지막 업데이트 날짜: 2016년 8월 29일
{: .last-updated}

지원되는 서비스를 사용하도록 작업을 구성하여 {{site.data.keyword.deliverypipeline}} 서비스의 기능을 확장할 수 있습니다. 예를 들어, 테스트 작업은 정적 코드 스캔을 실행할 수 있고 빌드 작업은 문자열을 글로벌화할 수 있습니다.
{:shortdesc}

<!-- Include a sentence to briefly introduce the steps/subtopics. Example: -->

다음 태스크는 선택된 도구를 Delivery Pipeline과 통합하는 방법에 대해 설명합니다.

## 파이프라인을 사용하여 정적 코드 스캔 실행

{: #deliverypipeline_scan}

코드를 배치하기 전에 코드에서 보안 문제를 찾고 싶습니까? IBM® Static Analyzer for Bluemix™를 파이프라인의 일부로 사용하면 Java™ 앱의 정적 `.war`, `.ear`, `.jar` 또는 `.class` 빌드 2진 파일에 대해 자동화된 검사를 실행할 수 있습니다.

Static Analyzer 서비스를 사용하는 파이프라인은 일반적으로 다음 단계를 포함합니다.

+ 소스 파일을 빌드하는 빌드 단계
+ 다음 작업을 포함하는 처리 단계
  + Static Analyzer 서비스를 실행하는 빌드 작업
  + 컨테이너 빌드를 실행하는 빌드 작업
+ 컨테이너를 배치하는 배치 단계


### 정적 코드 스캔 작성

시작하기 전에 [서비스의 이용 약관을 검토하십시오](http://www-03.ibm.com/software/sla/sladb.nsf/sla/bm-6814-01).

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. 처리 단계를 작성하십시오.

  a. **단계 추가**를 클릭하십시오. 

  b. 단계의 이름을 지정하십시오(예: `Processing`).

  c. 입력 유형으로 **빌드 아티팩트**를 선택하십시오.

  d. 단계 및 작업에 대해 값을 확인하고 필요한 경우 업데이트하십시오. 

2. 처리 단계에서 코드 스캔을 실행하는 빌드 작업을 추가하십시오.

  a. **작업** 탭에서 **작업 추가**를 클릭하십시오.

  b. 작업 유형으로 **테스트**를 선택하십시오.

  c. 테스터 유형으로 **IBM Security Static Analyzer**를 선택하십시오.

  d. 조직 및 영역에 대해 값을 확인하고 필요한 경우 업데이트하십시오.

  e. 필요에 따라 **서비스 및 영역 자동 설정** 선택란을 선택하거나 선택 취소하십시오.

    * 파이프라인이 Bluemix 영역에서 서비스와 이 서비스를 컨테이너에 바인드하는 앱이 있는지 확인하도록 하려면 이 선택란을 선택하십시오. 서비스 또는 바인드된 앱이 없는 경우 파이프라인은 서비스의 무료 사용제를 영역에 추가합니다. 작성되는 바인드된 앱은 `pipeline_bridge_app`이라는 이름이 지정됩니다. 파이프라인은 pipeline_bridge_app의 신임 정보를 사용하여 바인드된 서비스에 액세스합니다.

    * Bluemix 영역에 이미 서비스 및 바인드된 앱을 구성했거나 [이러한 요구사항을 수동으로 구성](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline)하려는 경우, 선택란을 선택 취소된 상태로 두십시오.

  f. **분석이 완료될 때까지의 대기 시간(분)** 필드에 0 - 59분 값을 입력하십시오. 기본값은 5분입니다. 작업 마지막에 Static Analyzer 대시보드로의 URL이 콘솔 로그에 표시됩니다.

     지정한 시간 전에 Static Analyzer 스캔이 완료되지 않으면 작업이 실패합니다. 그러나 스캔 분석은 계속 실행되며 Static Analyzer 대시보드에서 이를 볼 수 있습니다. Static Analyzer 스캔이 완료된 후 작업을 다시 실행하면 스캔 요청이 다시 제출되지 않으며 파이프라인 작업을 완료할 수 있습니다. 또는 스캔이 완료될 때 파이프라인이 차단되지 않도록 구성할 수 있습니다. 지시사항은 다음 단계를 참조하십시오.

  g. 현재 작업이 실패하거나 제한시간을 초과하는 경우에 원하는 결과에 따라 **현재 작업이 실패할 경우 현재 단계 실행 중지** 선택란을 선택하거나 선택 취소하십시오. 취약성이 높으면 작업이 실패할 수 있습니다.

    * 이 선택란을 선택한 상태에서 작업이 실패하면 해당 단계의 나중 작업과 나중 단계가 실행되지 않습니다.

    * 이 선택란을 선택 취소한 상태에서 작업이 실패하면 나중 작업 및 단계를 차단하지 않고 단계가 계속됩니다. 예를 들어, 보고서에 처리할 다수의 문제가 있음을 알고 있는 경우, 스캔에 오랜 시간이 소요될 수 있기 때문에 단계가 계속되도록 구성할 수 있습니다. 이러한 시나리오에서 스캔에 너무 오랜 시간이 소요된다는 이유만으로 나머지 작업 및 단계를 중지하고 싶지 않을 수도 있습니다. 

  h. **저장**을 클릭하십시오.

3. 작업이 완료되면 **로그 및 히스토리 보기**를 클릭하여 결과를 보십시오. 분석이 성공하거나 제한시간을 초과하면 스캔 결과에 URL이 표시됩니다. 스캔 상태가 보류 중인 경우, 전체 결과를 보려면 스캔이 완료될 때까지 기다리십시오.

4. 분석이 완료되기 전에 처리 단계를 다시 실행해야 하는 경우 이를 수행할 수 있습니다. 그러나 다음과 같은 상황에서는 새 분석이 다시 제출되지 않고 이전 결과가 사용됩니다.
  * 새 분석을 시작할 때 처리 단계가 계속 실행 중입니다.
  * 해당 빌드에 대한 스캔이 이미 제출되었습니다.
  * 새 소스 빌드가 아직 실행되지 않았습니다. 

5. 새 분석을 시작하려면 다음 단계 중 하나를 완료하십시오. 
  * 처리 단계에 입력을 제공하는 빌드 단계를 실행한 후 처리 단계를 다시 실행하십시오. 
  * 스캔 결과의 URL을 열고 **휴지통** 아이콘을 클릭하십시오. 그런 다음 처리 단계를 다시 실행하십시오. 

콘솔 출력 예: 

**성공적 스캔**
![성공적 스캔 예](images/analyzer_success.png)

**보류 중 스캔**
![보류 중 스캔 예](images/analyzer_pending.png)

Static Analyzer 서비스 사용에 대한 자세한 정보는 [Static Analyzer 서비스 문서를 참조하십시오](https://console.ng.bluemix.net/docs/services/ApplicationSecurityonCloud/index.html).

<!--

## Globalizing strings by using the pipeline
{: #deliverypipeline_globalize}

You can translate strings automatically into other languages when you use the IBM Globalization Pipeline service with your pipeline. IBM Globalization Pipeline uses machine translation to translate your source files as part of the pipeline's build and deployment process.

You can also update the machine-translated strings within the globalization project. A translator or native speaker of the language can then review the machine-translated strings to ensure that they are of a high quality.

To see an example of a typical pipeline that uses the Globalization Pipeline service, watch this video:

<iframe width="640" height="360" src="https://www.youtube.com/embed/UToj7FIomCg?feature=player_embedded" frameborder="0" allowfullscreen></iframe>

### Creating a globalization stage and job
Before you begin:

1. All English-translatable strings should be included in one or more `filename_en.properties` or `filename_en.json` files that all use the same name. For example: `messages_en.properties`.

2. If your messages are in `.json` files, remove the depth from the structure by removing any subkeys. To remove the subkeys, change instances of `{key: {subkey: value, subkey:value}}` to `{key:value, key:value}`.

To create the globalization stage and job:

1. Create a globalization stage.

  a. Click **ADD STAGE**.

  b. Name the stage; for example, `Globalization`.

  c. For the input type, select **SCM repository**.

2. In the globalization stage, add a job to translate the source files.

  a. On the **JOBS** tab, click **ADD JOB**.

  b. For the job type, select **Build**.

  c. For the builder type, select **IBM Globalization Pipeline**.

  d. For the organization and space, verify the values and update them if needed.

  e. In the **Source file name** field, type the name and extension of the `.properties` or `.json` input file. If you have files in different subdirectories, but they all have the same name, you need to type the file name once only. For example, if you have a `messages_en.properties` file in three directories, type `messages_en.properties` for the source file name, and all files with that name will be translated.

  f. Determine whether to select the **Set up service and space for me** check box.

    * If you want the pipeline to check your Bluemix space for the service and an app that binds the service to the container, select this check box. If the service or bound app does not exist, the pipeline adds the free plan of the service to your space for you. The bound app that is created is named `pipeline_bridge_app`. Then, the pipeline uses the credentials from pipeline_bridge_app to access the bound services.

    * If you configured the service and bound app in your Bluemix space already or if you want to [configure these requirements manually](https://www.ng.bluemix.net/docs/containers/container_group_pipeline_ov.html#container_binding_pipeline), leave this check box cleared.

  g. For the Globalization bundle prefix, enter a prefix for the bundle name, which is structured in this format: `<globalization_bundle_prefix>.path.to.source.file`. The pipeline job creates this Globalization bundle for you in the Globalization Pipeline service.

    **Tip:** Use the DevOps Services project name in the prefix so that the project can be identified easily in the Globalization Pipeline service.

  h. Click **SAVE**.

3. Create another stage to package your app. For the input of the job in this stage, use the IBM Globalization Pipeline job from the previous stage. Do not use the source as the input. The Globalization Pipeline job augments the source files with the machine-translated strings.

4. To ensure that the machine-translated content is included in the packaged app, create another stage to package the app in. For the input to that stage, include the Globalization Pipeline job.

The machine translated files are placed in the same directory as the source `.properties` or `.json` file. To view the files, click **Job > Artifacts**.

After the stage is completed, you can review the translated files from the console output. You can also direct translators to the files so that they can review the machine-translation output and provide revisions to improve quality. The revisions are stored in a Cloudant™ database and take precedence over any future machine translations of the same strings.

For more information about using the Globalization Pipeline service from the Bluemix Dashboard, [see the Globalization Pipeline service documentation](https://www.ng.bluemix.net/docs/services/GlobalizationPipeline/index.html).

-->

## 파이프라인에서 빌드에 대한 Slack 알림 작성
{: #deliverypipeline_slack}

Delivery Pipeline에서 Slack 채널로 IBM Container Service, IBM Security Static Analyzer 및 IBM Globalization 빌드 결과에 대한 알림을 전송할 수 있습니다.

시작하기 전에 Slack WebHook URL을 작성하거나 복사하십시오.

1. 팀의 Slack 통합 페이지를 여십시오(`https://_project_name_.slack.com/services`).
2. 통합 목록에서 **수신 WebHook**를 찾아 **추가**를 클릭하십시오.
3. 채널을 선택하고 **수신 WebHook 통합 추가**를 클릭하십시오.
4. **WebHook URL**을 추가하거나 기존 URL을 복사하십시오.

자세한 정보는 [Slack 문서에서 수신 WebHook를 참조하십시오](https://api.slack.com/incoming-webhooks).

Slack 알림을 작성하려면 다음을 수행하십시오.

1. 파이프라인에서 단계의 구성을 여십시오.
2. **환경 특성** 탭에서 **특성 추가**를 클릭하십시오.
3. **텍스트 특성**을 선택하십시오.
4. 환경 특성의 이름과 값을 입력하십시오. 여러 환경 특성을 작성하려면 단계를 반복하십시오.

  *표 1. Slack 알림 구성을 위한 환경 특성*

  <table>
  <tr>
  <th>이름</th>
  <th>값</th>
  <th>설명</th>
  <tr/>
  <tr>
    <td><code>SLACK_WEBHOOK_PATH</code></td>
    <td>URL</td>
    <td>필수. Slack 프로젝트의 설정에 저장되는 WebHook URL입니다.</td>
  </tr>
  <tr>
    <td><code>SLACK_COLOR</code></td>
    <td>다음 값 중 하나를 입력할 수 있습니다.
      <ul><li><code>good</code></li>
      <li><code>warning</code></li>
      <li><code>danger</code></li>
      <li>16진 색상(예: #439FEO)</li></ul></td>
    <td>선택사항. Slack에서 메시지의 측면을 따라 표시되는 경계의 색상입니다. 기본 색상은 좋은 메시지의 경우 초록색이고 나쁜 메시지의 경우 빨간색이며 정보 메시지의 경우 회색입니다. </td>
  </tr>
  <tr>
    <td><code>NOTIFY_FILTER</code></td>
    <td>메시지 유형 서브세트만 수신하려면 다음 값 중 하나를 입력하십시오.
      <ul>
      <li><code>good</code>: 알 수 없는 메시지, 좋은 메시지 및 정보 메시지만 가져옵니다. 나쁜 메시지는 전송되지 않습니다.</li>
      <li><code>bad</code>: 모든 메시지를 가져옵니다.</li>
      <li><code>info</code>: 정보 메시지만 가져옵니다. 좋은 메시지, 나쁜 메시지 및 알 수 없는 메시지는 전송되지 않습니다.</li>
      <li><code>unknown</code>: 모든 메시지를 가져옵니다. </li></ul>
      예: <code>NOTIFY_FILTER = bad</code>를 설정하면 Slack 채널에서 오류 알림만 표시됩니다. </td>
    <td>선택사항. 알림을 전송할 메시지 유형을 결정하십시오. 기본적으로 좋은 메시지와 나쁜 메시지가 전송되고 정보 메시지는 전송되지 않습니다.
      <ul><li><code>good</code>: 성공적 빌드 결과입니다. </li>
      <li><code>bad</code>: 비성공적 빌드 결과입니다.</li>
      <li><code>info</code>: 빌드 프로세스에 대한 정보 메시지입니다. </li>
      <li><code>unknown</code>: 알 수 없는 메시지에는 유형이 지정되지 않습니다.</li></ul></td>
   </table>

5. **저장**을 클릭하십시오.

6. IBM Container Service, IBM Security Analyzer 및 IBM Globalization 작업을 포함하는 다른 단계에 대한 Slack 알림을 전송하려면 이 단계를 반복하십시오. 

Slack에 표시되는 빌드 알림에는 DevOps Services 프로젝트에 대한 링크와 가끔 이 프로젝트의 대시보드에 대한 링크가 포함됩니다. Slack 사용자가 이러한 링크를 열려면 사용자가 DevOps Services에 등록되어 있고 파이프라인이 구성된 프로젝트의 멤버여야 합니다. 

## 파이프라인에서 빌드에 대한 HipChat 알림 작성
{: #deliverypipeline_hipchat}

Delivery Pipeline에서 HipChat 룸으로 IBM Container Service, IBM Security Static Analyzer 및 IBM Globalization 빌드 결과에 대한 알림을 전송할 수 있습니다.

시작하기 전에 HipChat 토큰을 작성하거나 기존 HipChat 토큰을 복사하십시오.

1. 팀의 HipChat 계정 페이지로 이동하십시오(`https://_project_name_.hipchat.com/account/api`).
2. 새 토큰을 작성하거나 기존 토큰을 사용하십시오. 

HipChat 알림을 작성하려면 다음을 수행하십시오. 

1. 파이프라인에서 단계의 구성을 여십시오.
2. **환경 특성** 탭에서 **특성 추가**를 클릭하십시오.
3. **텍스트 특성**을 선택하십시오.
4. 환경 특성의 이름과 값을 입력하십시오. 여러 환경 특성을 작성하려면 단계를 반복하십시오.

  *표 2. HipChat 알림 구성을 위한 환경 특성*

  <table>
  <tr>
  <th>이름</th>
  <th>값</th>
  <th>설명</th>
  </tr>
  <tr>
    <td><code>HIP_CHAT_TOKEN</code></td>
    <td>영숫자 문자열</td>
    <td>필수. HipChat 토큰 작성 또는 기존의 HipChat 토큰 복사에 대한 지시사항은 "시작하기 전에"를 참조하십시오.</td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_ROOM_NAME</code></td>
    <td>룸 이름</td>
    <td>필수. </td>
  </tr>
  <tr>
    <td><code>HIP_CHAT_COLOR</code></td>
    <td>다음 값 중 하나를 입력하십시오.
      <ul><li><code>yellow</code></li>
      <li><code>red</code></li>
      <li><code>green</code></li>
      <li><code>purple</code></li>
      <li><code>gray</code></li>
      <li><code>random</code></li></ul>
    </td>
    <td>선택사항: HipChat 알림의 배경색 및 경계색을 지정하십시오. <code>HIP_CHAT_COLOR</code>를 설정하는 경우, 스크립트를 호출할 때 색상을 지정하지 않아도 됩니다.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_COLOR</code></td>
    <td>다음 값 중 하나를 입력하십시오.
      <ul><li><code>good</code></li>
      <li><code>danger</code></li>
      <li><code>info</code></li></ul>
    이 변수는 HipChat 및 Clack 알림 색상 모두에 적용됩니다. <code>NOTIFICATION_COLOR</code>를 지정하는 경우 <code>HIP_CHAT_COLOR</code> 또는 <code>SLACK_COLOR</code>를 지정하지 않아도 됩니다. </td>
    <td>선택사항: HipChat 및 Slack 알림 둘 다의 배경색 및 경계색을 지정하십시오. <code>NOTIFICATION_COLOR</code>를 설정하는 경우, 스크립트를 호출할 때 색상을 지정하지 않아도 됩니다.
     <p><code>-l notification_level</code></p> </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_LEVEL</code></td>
    <td>다음 값 중 하나를 입력하십시오.
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul></td>
    <td>선택사항: 알림 레벨을 지정하십시오. 알림을 트리거하는 것에 대한 세부사항은 <code>NOTIFICATION_FILTER</code>를 참조하십시오. </td>
  </tr>
  <tr>
    <td><code>NOTIFICATION_FILTER</code></td>
    <td>다음 값 중 하나를 입력하십시오.
      <ul><li><code>good</code></li>
      <li><code>info</code></li>
      <li><code>bad</code></li></ul>
    <td>선택사항: 알림 필터 레벨을 지정하십시오. 다음 매개변수가 충족될 때 알림이 전송됩니다.
      <ul><li><code>NOTIFICATION_FILTER = good</code>이고 <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> 또는 <code>unknown</code>입니다.</li>
      <li><code>NOTIFICATION_FILTER = info</code>이고 <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code>, <code>info</code> 또는 <code>unknown</code>입니다.</li>
      <li><code>NOTIFICATION_FILTER = bad</code>이고 <code>NOTIFICATION_LEVEL = bad</code> 또는 <code>unknown</code>입니다.</li>
      <li><code>NOTIFICATION_FILTER = unknown</code>이고 <code>NOTIFICATION_LEVEL = bad</code>, <code>good</code> 또는 <code>unknown</code>입니다.</li></ul></td>
    </tr>
  </table>

5. **저장**을 클릭하십시오.

6. IBM Container Service, IBM Security Analyzer 및 IBM Globalization 작업을 포함하는 다른 단계에 대한 HipChat 알림을 전송하려면 이 단계를 반복하십시오. 

## 파이프라인에서 작동 중단 없는 배치를 위해 Active Deploy 사용
{: #deliverypipeline_activedeploy}

Bluemix® DevOps Services Delivery Pipeline에서 IBM® Active Deploy 서비스를 사용하여 앱 또는 컨테이너 그룹의 연속 배치를 자동화할 수 있습니다. 시작하기에 대한 자세한 정보는 [Active Deploy 문서를 참조하십시오](https://new-console.ng.bluemix.net/docs/services/ActiveDeploy/updatingapps.html#adpipeline).

## 파이프라인을 사용하여 컨테이너 이미지 빌드 및 배치
{: #deliverypipeline_containers}

IBM® Continuous Delivery Pipeline for Bluemix를 사용하여 앱 빌드와 Bluemix®로의 컨테이너 배치를 자동화할 수 있습니다. DevOps Services의 Delivery Pipeline 서비스는 다음을 지원합니다. 
  - Docker 이미지 빌드
  - Bluemix에 컨테이너의 이미지 배치

시작하기에 대한 자세한 정보는 [Delivery Pipeline 및 컨테이너 개요](https://new-console.ng.bluemix.net/docs/containers/container_pipeline_ov.html#container_pipeline_ov)를 참조하십시오. 
