---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-14"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# 디바이스 유형 스키마 작성
{: #iotrtinsights_task}

규칙 및 조치와 같은 {{site.data.keyword.iot_short}} 기능을 사용하려면 스키마를 작성하여 디바이스 특성을 사용자에게 익숙한 특성 이름에 맵핑하고 특성의 데이터 단위를 설정하며 스키마와 함께 사용할 메시지 유형을 지정해야 합니다.
{: shortdesc}

**중요:** 스키마는 규칙과 조치를 사용하는 데 필요합니다. 자세한 정보는 [클라우드 분석](cloud_analytics.html#rules)을 참조하십시오.

**중요:** 분석 기능은 {{site.data.keyword.iotrtinsights_full}} 서비스에서 병합됩니다. {{site.data.keyword.iot_short_notm}} 조직이 기존 {{site.data.keyword.iotrtinsights_short}} 인스턴스의 데이터 소스로 사용되는 경우 {{site.data.keyword.iotrtinsights_short}} 인스턴스가 마이그레이션된 후에야 클라우드 및 에지 분석이 사용됩니다. 마이그레이션이 완료될 때까지 분석이 필요할 때는 계속 {{site.data.keyword.iotrtinsights_short}} 대시보드를 사용하십시오. 자세한 정보는 IBM developerWorks의 [IBM Watson IoT Platform 블로그 ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://developer.ibm.com/iotplatform/2016/04/28/iot-real-time-insights-and-watson-iot-platform-a-match-made-in-heaven/){: new_window} 및 기존 {{site.data.keyword.iotrtinsights_short}} 인스턴스 대시보드를 참조하십시오.   

## 디바이스 스키마 추가
{: #add_schema}

스키마를 추가하려면 다음을 수행하십시오.  
1. **디바이스 > 스키마 관리**로 이동하고 **스키마 추가**를 클릭합니다.  
2. 이 메시지 스키마와 연관될 디바이스 유형을 선택합니다. **중요:** 디바이스 유형마다 하나의 스키마만 정의할 수 있습니다.

3. 하나 이상의 특성을 추가합니다.  
연결된 디바이스에서 특성을 선택하거나, 기존 특성을 수정하거나 결합하는 가상 특성을 작성하거나, 수동으로 특성을 추가할 수 있습니다.  

    **팁:** 사용 가능한 특성은 디바이스에서 전송한 메시지의 페이로드에 정의됩니다. {{site.data.keyword.iot_short}} 페이로드 형식에 대한 정보는 [메시지 페이로드](reference/mqtt/index.html#message-payloadl "메시지 페이로드.") 주제를 참조하십시오.   
  <dl>
  <dt>수동으로 특성 추가</dt>
  <p><b>팁:</b> 중첩된 특성 구조를 작성하려면 먼저 데이터 유형이 Parent인 특성을 추가하십시오. 그런 다음 특성 테이블에서 ![하위 추가 아이콘](images/add_child.png "하위 추가")을 클릭하여 하나 이상의 하위 특성을 추가하십시오.</p>
  <dd>
  <ol>
    <li>**수동** 탭을 선택합니다.</li>
    <li>다음 특성 세부사항을 정의합니다.
    <ul>  
      <li>이름 - {{site.data.keyword.iot_short}} 대시보드, 메뉴 및 마법사에서 사용하는 특성의 설명적 이름입니다.</li>
      <li>데이터 유형 - 특성의 데이터 유형입니다.  
   `String`, `Integer`, `Float` 또는 `Parent`.</li>
   <!--<li>Event - A specific event to collect data for. Leave blank to collect for all events.</li>-->
   <li>특성 - ID의 특성입니다. 예를 들어 다음과 같습니다.  
 `temp` 또는 `speed`  </br> 디바이스 메시지에서 특성을 식별하는 방법에 대한 정보는 [디바이스의 특성 식별](#identify-datapoints "특성 식별.")을 참조하십시오.</li>
  <li>데이터 단위 - 선택사항: 특성의 데이터 단위입니다. 예를 들어 다음과 같습니다.  
     `C` 또는 `Mph`  </li>
     <li> 소수점 자리 - 선택사항으로, float 전용입니다. 디바이스 데이터에 포함할 10진수 수입니다.</li>
    </ul>
    </li>
    <li>**완료**를 클릭하여 특성을 작성합니다. </li>
  </ol>
  </dd>
  <dt>가상 특성 작성</dt>
  <dd> 예를 들어 디바이스 특성 temp에서 화씨로 온도 값을 리턴하지만 사용자는 섭씨를 사용하는 경우 *temp_c=(temp-32)/1.8* 함수가 있는 가상 특성 *temp_c*를 작성할 수 있습니다. 그런 다음 규칙 조건에서 실시간 *temp* 특성이 아니라 가상 *temp_c* 특성을 사용할 수 있습니다.  
  가상 특성을 작성하려면 다음을 수행하십시오.
  <ol>
    <li>**가상 특성** 탭을 선택합니다.</li>  
    <li>다음 특성 세부사항을 정의합니다.
    <ul>
    <li>이름 - {{site.data.keyword.iot_short}} 대시보드, 메뉴 및 마법사에서 사용하는 특성의 설명적 이름입니다.</li>
    <li>데이터 유형 - 특성의 데이터 유형입니다.  
 `Float` 또는 `Integer`.</li>
 <li>특성 - 가상 특성의 특성 ID입니다. 예를 들어 다음과 같습니다.  
`temp_virt`</li>
    <li>계산 - 올바른 함수를 정의하기 위해 하나 이상의 컴포넌트를 추가합니다. 특성, 숫자 값, 그리고  +, -, \*, /, ( 및 ) 등의 수학 연산자를 사용할 수 있습니다.   
    에지 디바이스의 데이터 점 시리즈에서 사용할 공식 세트에 대해 **고급**을 클릭하십시오. 고급 공식에 대한 자세한 정보는 [에지 가상 특성에 대한 고급 계산](im_vir_calculations.html)을 참조하십시오.  
    **중요:** 고급 공식을 기반으로 가상 특성을 비교하는 규칙 조건은 지원되지 않습니다. </li>
    <li>데이터 단위 - 선택사항: 특성의 데이터 단위입니다. 예를 들어 `C` 또는 `Mph`입니다.</li>
    <li> 소수점 자리 - 선택사항으로, float 전용입니다. 디바이스 데이터에 포함할 10진수 수입니다.</li>
   </ul>
   </li>
   <li>**완료**를 클릭하여 특성을 작성합니다.</li>
  </ol>
  </dd>
  <dt>연결된 디바이스에서 특성 선택</dt>
  <dd>
  <ol>
    <li>**연결에서** 탭을 선택합니다.</li>  
    <li>스키마에 추가할 하나 이상의 특성을 선택합니다. 이러한 특성은 이름 및 데이터 단위와 같은 속성을 설정하기 위해 나중에 편집할 수 있습니다.  
<!--**Important:** Each property must be unique for a schema. If you select multiple occurrences of the same property for different events, only one of the selected properties is added to the schema.</li>-->
  <li>**확인**을 클릭하여 특성을 작성합니다.</li>
  </ol>
  </dd>
    <dd>선택한 특성이 추가되고 설명이 특성의 이름으로 설정됩니다. 목록에서 특성을 클릭하여 편집하고 추가 속성(예: 센서 유형, 데이터 유형 및 소수점 자리 수)을 추가합니다.</dd>
  </dl>
8. **완료**를 클릭하여 메시지 스키마를 작성합니다.

## 디바이스의 특성 식별.
{: #identify-datapoints}
   디바이스의 특성은 {{site.data.keyword.iot_short}} 대시보드에 있습니다.

1. {{site.data.keyword.iot_short}} 대시보드에서 **디바이스**로 이동합니다.
2. 디바이스를 클릭하여 디바이스의 세부사항을 표시하는 페이지를 엽니다.
3. **센서 정보** 섹션까지 아래로 화면이동하여 연결된 디바이스에 사용 가능한 특성 목록을 확인합니다.
