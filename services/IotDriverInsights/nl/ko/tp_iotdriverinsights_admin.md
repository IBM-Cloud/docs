---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Trajectory Pattern Analysis 관리
{: #tp_iotdriverinsights_admin}

마지막 업데이트 날짜: 2016년 7월 22일
{: .last-updated}

Trajectory Pattern Analysis 서비스를 관리하려면 {{site.data.keyword.Bluemix_notm}} 대시보드의 관리 콘솔을 사용하십시오. 관리 콘솔에서, Trajectory Pattern Analysis의 매개변수를 구성하고 서비스에 저장된 데이터를 관리할 수 있습니다. 또한 테넌트 정보를 보고 테넌트 비밀번호를 재설정할 수 있습니다.

{:shortdesc}

## 관리 콘솔 시작
{: #start-admin-console}

{{site.data.keyword.iotdriverinsights_full}}의 Trajectory Pattern Analysis 서비스의 관리 콘솔에 액세스하려면 다음을 수행하십시오.

1. {{site.data.keyword.Bluemix_notm}} 대시보드에서 {{site.data.keyword.iotdriverinsights_short}} 서비스 타일을 클릭하십시오.
2. 서비스 인스턴스의 **관리** 보기를 선택하십시오.
나중에 필요하므로 사용자 이름 및 비밀번호 신임 정보를 기록해 두십시오. 관리 콘솔에 액세스하려면 IBM ID가 필요하며, 이는 {{site.data.keyword.Bluemix_notm}} 신임 정보와 동일하지 않을 수 있습니다.
3. **실행**을 클릭하고 프롬프트가 표시되면 IBM ID 신임 정보를 입력하십시오.
4. **로그인**을 클릭하십시오. **관리 콘솔** 창이 열립니다.


## 테넌트 정보 관리
{: #viewtenantinfo}

테넌트 정보를 보려면 **Tenant Information**을 클릭하십시오.

### 테넌트 비밀번호 재설정
{: #resettenantpassword}

테넌트 비밀번호를 재설정하려면 다음을 수행하십시오.

1. **Tenant Information** 창에서 **RESET**을 클릭하십시오.
2. 확인 대화 상자에서 **OK**를 클릭하십시오.
새 비밀번호가 생성되어 **Tenant Information** 보기에 표시됩니다.
**중요:** {{site.data.keyword.iotdriverinsights_short}} API에 액세스하는 모든 애플리케이션에서 비밀번호를 업데이트해야 합니다.

## 서비스 매개변수 구성
{: #configureparameters}

서비스 매개변수는 운행 데이터가 분석되는 방식을 제어합니다. Trajectory Pattern Analysis 서비스 매개변수를 수정하려면 다음을 수행하십시오.

1. **Parameters** 보기를 여십시오.
2. **Parameters of Trajectory Pattern** 탭을 클릭하고 사용자의 요구사항에 맞게 [궤적 패턴 분석 매개변수](#tp_parameters)를 업데이트하십시오.
3. **SAVE**를 클릭하십시오.
4. **OK**를 클릭하십시오.

업데이트된 매개변수 값은 다음으로 제출되는 작업에 적용됩니다.

### 지원 임계값 매개변수

다음 표에서는 **Parameters of Trajectory Pattern** 탭에서 구성할 수 있는 지원 임계값 매개변수를 설명합니다.

|매개변수 이름|설명|기본값|
|:--------|:--------|:-------|
|Minimal support of trip numbers for an O/D|O/D(기점/종점) 패턴에 필요한 최소 절대 지원 운행 수|4(0보다 커야 함)|
|Minimal support of trip numbers for a route|경로 패턴에 필요한 최소 절대 지원 운행 수|2(0보다 커야 함)|

## 결과 데이터 관리
{: #managedata}

Trajectory Pattern Analysis 서비스의 분석에서 생성되는 결과 데이터는 사용자가 이를 삭제할 때까지 시스템에 저장됩니다.

결과 데이터를 삭제하려면 다음을 수행하십시오.

1. **Data Management** > **Result of Trajectory Pattern**을 클릭하십시오. 결과 데이터가 표시됩니다.
2. 레코드를 선택한 다음 **DELETE**를 클릭하십시오.
