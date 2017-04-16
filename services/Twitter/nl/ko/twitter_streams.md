---

copyright:
  years: 2015, 2016
lastupdated: "2016-11-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Decahose 및 PowerTrack 스트림 {: #decahose_powertrack}

{{site.data.keyword.twittershort}}에서는 {{site.data.keyword.Bluemix_notm}} 계획 등록에 기반하여 Twitter Decahose 및 PowerTrack 스트림에 대한 액세스 권한을 제공합니다.
두 스트림 모두 사용자 요구에 맞게 실시간 피드 및 다른 특성을 전달합니다.
{:shortdesc}

Decahose 스트림은 Twitter Firehose의 10% 랜덤 샘플링입니다. 트윗은 실시간으로 Twitter에서 파생되며 Twitter의 샘플링 알고리즘에 의해 판별됩니다. 대부분의 통계 분석의 경우 10% 랜덤 샘플은 충분히 정확합니다. Decahose 데이터는 2년의 기간에 대해 색인화되므로 쿼리 응답에서 2년이 지난 트윗은 리턴되지 않을 수도 있습니다. Decahose에 대한 액세스 권한은 Free Plan 및 Entry Plan에서 사용 가능하고, PowerTrack 스트림에 대한 액세스 권한은 Entry Plan 사용자에게만 부여됩니다.

PowerTrack 스트림은 추적이라고 알려진 사용자 정의 규칙 기반 필터에 기반하여 수신 트윗을 필터링하는 이점을 추가합니다. Entry Plan 사용자는 계정당 최대 1,000개의 규칙을 작성할 수 있습니다. 고급 필터링의 경우 여러 추적을 결합하여 집계된 추적을 형성할 수 있습니다. 다음 섹션에서는 편집, 삭제 등 추적에서 수행할 수 있는 지원되는 조치와 특성, 추적 상태에 대해 설명합니다.

**참고**: PowerTrack 스트림의 색인화는 달력상 매월 1백만 트윗으로 제한됩니다. 한도에 도달하면 해당 월에 대해 색인 작성이 중지됩니다. 그 다음 월이 시작되면 추적을 다시 활성화할 수 있으며 자동으로 활성화되지는 않습니다. 스트림의 사용을 최대화하려면 추적을 적절히 관리해야 합니다. 예를 들어, 중복 추적은 비활성화될 수 있습니다. 

## 추적 유형 {: #track_types}

Entry Plan 사용자는 사용자 정의 가능한 추적을 작성하여 PowerTrack 데이터 스트림에 수집된 메시지를 필터링할 수 있습니다. {{site.data.keyword.twittershort}}에서는 다음 2개의 추적 유형을 지원합니다.

<dl>
<dt>Rule</dt>
<dd>이 추적에 수집된 모든 메시지는 추적과 연관된 하나 이상의 규칙과 일치합니다. 이 추적 유형 내에서 규칙을 추가, 편집 및 삭제할 수 있습니다.

전체 [GNIP PowerTrack 규칙 구문](http://support.gnip.com/apis/powertrack2.0/rules.html)이 규칙 기반 추적 내에서 지원됩니다. 모든 쿼리는 {{site.data.keyword.twittershort}} [쿼리 언어](twitter_rest_apis.html#querylanguage "쿼리 언어")에 부합해야 합니다.
</dd>

<dt>Aggregated</dt>
<dd>둘 이상의 규칙 또는 집계된 추적의 조합입니다. 집계된 추적은 여러 추적을 임의로 그룹화하는 데 사용됩니다. 집계된 추적 유형에서 개별 추적을 추가하고 삭제할 수 있습니다. 개별 규칙을 집계된 추적에 추가할 수 없습니다. 이 용도로 규칙 추적을 대신 사용하십시오. 집계된 추적은 stateless이지만, 해당 구성 성분 규칙 추적은 **활성** 또는 **비활성**입니다.</dd>
</dl>

## 추적 특성 {: #track_properties}
추적에는 다음 특성이 포함됩니다. 일부 특성은 규칙 기반 및 집계된 추적 둘 다에 적용되지 않습니다. 예를 들어 규칙 특성은 집계된 추적에 적용되지 않습니다.

<dl>
<dt>createdDate</dt>
<dd>추적이 작성된 시기를 `YYYYMMDDHHMM`로 지정하여 표시합니다. </dd>

<dt>endDate</dt>
<dd>추적이 메시지 수집을 중지하는 시기를 표시합니다. 지정된 값은 미래 값이어야 하고 `YYYY-MM-DD` 또는 `YYYY-MM-DDTHH:MM:SSZ` 형식 중 하나를 따라야 합니다. 과거의 날짜를 지정하면 HTTP 400 오류가 리턴됩니다.

이 특성은 집계된 추적에 적용되지 않습니다.</dd>

<dt>id</dt>
<dd>작성 시 추적에 지정되는 고유 ID 참조입니다. ID는 규칙 및 집계된 추적에 대해 GUID 문자열 형식(예: 3F2504E0-4F89-41D3-9A0C-0305E82C3301)으로 나타냅니다. </dd>

<dt>name</dt>
<dd>추적의 설명적 이름입니다. 이 특성의 고유성은 보장되지 않습니다.</dd>

<dt>rules</dt>
<dd>쿼리 키워드 및 기타 매개변수를 포함하여 추적 필터를 정의하는 규칙의 배열입니다. 이 특성은 규칙 기반 추적에 적용되지만 집계된 추적에 적용되지 않습니다.</dd>

<dt>state</dt>
<dd>**활성** 또는 **비활성**이어야 합니다. 활성 추적은 메시지를 수집하고 비활성 추적은 그렇지 않습니다. 추적 상태는 항상 변경할 수 있습니다.

이 특성은 집계된 추적에 적용되지 않습니다.</dd>

<dt>trackIds</dt>
<dd>추적 ID의 배열입니다. 이 특성은 집계된 추적에만 적용됩니다.</dd>

<dt>type</dt>
<dd>추적 유형이 **Rule** 또는 **Aggregated**인지 여부를 표시합니다.

추적 조작 및 모델 스키마를 포함하여 추적 특성에 대한 자세한 정보를 보려면 {{site.data.keyword.twittershort}} REST API 문서를 참조하십시오.</dd>
</dl>

