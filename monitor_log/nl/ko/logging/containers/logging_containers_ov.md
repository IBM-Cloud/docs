---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# IBM Bluemix 컨테이너 서비스에 대한 로깅
{: #logging_containers_ov}

{{site.data.keyword.Bluemix}}에서 {{site.data.keyword.Bluemix_notm}} 대시보드, Kibana 및 명령행 인터페이스를 통해 컨테이너 로그를 보고 필터링하고 분석할 수 있습니다.
{:shortdesc}

크롤러를 사용하여 컨테이너 외부에서 컨테이너 로그를 모니터하고 전달합니다. 데이터는 크롤러가
{{site.data.keyword.Bluemix_notm}}의 다중 테넌트 Elasticsearch에 전달합니다.

다음 그림은 {{site.data.keyword.containershort}} 로깅의 상위 레벨 보기를 보여줍니다.

![컨테이너의 상위 레벨 컴포넌트 개요](images/logging_containers_ov.jpg "컨테이너의 상위 레벨 컴포넌트 개요")

{{site.data.keyword.Bluemix_notm}}에서 컨테이너를 배치할 때 해당 컨테이너의 로깅이 자동으로 사용됩니다.

## 컨테이너에 대해 수집된 로그
{: #logging_containers_ov_logs_collected}

기본적으로 다음 로그가 수집됩니다.

<table>
  <tbody>
    <tr>
      <th align="center">로그</th>
      <th align="center">설명</th>
    </tr>
    <tr>
      <td align="left" width="30%">/var/log/messages</td>
      <td align="left" width="70%"> 기본적으로 Docker 메시지는 컨테이너의 /var/log/messages 폴더에 저장됩니다. 이 로그에는 시스템 메시지가 들어 있습니다.
      </td>
    </tr>
    <tr>
      <td align="left">./docker.log</td>
      <td align="left">이 로그는 Docker 로그입니다. <br> Docker 로그 파일은 컨테이너 내의 파일로서 저장되지는 않지만, 그래도 이 파일은 수집됩니다. 컨테이너의 stdout(표준 출력)과 stderr(표준 오류) 정보를 노출하는 표준 Docker 규칙이므로 이 로그 파일이 기본적으로 수집됩니다. 컨테이너 프로세스가 stdout 또는 stderr에 인쇄되는 경우 해당 정보가 수집됩니다.
      </td>
     </tr>
  </tbody>
</table>

추가 로그를 수집하려면 컨테이너를 작성할 때 로그 파일의 경로와 함께 **LOG_LOCATIONS** 환경 변수를 추가하십시오. 여러 로그 파일을 쉼표로 구분하여 추가할 수 있습니다. 자세한 정보는 [컨테이너에서 기본이 아닌 로그 데이터 수집](logging_containers_other_logs.html#logging_containers_collect_data)을 참조하십시오.


## 컨테이너 로그를 분석하는 방법
{: #logging_containers_ov_methods}
 
다음 방법 중 하나를 선택하여 컨테이너의 로그를 분석할 수 있습니다.

* {{site.data.keyword.Bluemix_notm}}에서 로그를 분석하고 컨테이너의 최근 활동을 보십시오.
    
    각 컨테이너에 사용 가능한 **모니터링 및 로그** 탭을 통해 로그를 보고 필터링하며 분석할 수 있습니다. 자세한 정보는 [Bluemix 대시보드에서 로그 분석](../logging_view_dashboard.html#analyzing_logs_bmx_ui)을 참조하십시오.
    
* Kibana에서 로그를 분석하여 고급 분석 태스크를 수행하십시오.
    
    오픈 소스 분석 및 시각화 플랫폼인 Kibana를 사용하여 데이터를 모니터링하고 검색하고 분석하고 다양한 그래프(예: 차트와 테이블)로 시각화할 수 있습니다. 자세한 정보는 [Kibana에서 로그 분석](../kibana4/logging_analyzing_logs_Kibana.html#analyzing_logs_Kibana)을 참조하십시오.

* CLI를 통해 로그를 분석하여 명령을 통해 프로그래밍 방식으로 로그를 관리하십시오.
    
    **cf ic logs** 명령을 사용하여 명령행 인터페이스를 통해 로그를 보고 필터링하고 분석할 수 있습니다. 자세한 정보는 [명령행 인터페이스에서 로그 분석](../logging_view_cli.html#analyzing_logs_cli)을 참조하십시오.


## 로그 보유
{: #logging_containers_ov_log_retention}

로그 보존에 대한 다음 정보를 고려하십시오.

* 데이터 영역당 최대 1GB가 매일 저장됩니다. 1GB 상한을 초과하는 로그는 버립니다. 상한 할당은 협정 세계시(UTC)로 매일 오전 12:30에
재설정됩니다. 

    지원 센터에 문의하여 상한을 늘릴 수 있습니다. 지원 티켓에 상한 증가 요청을 할 영역 ID, 새로운 상한 크기 및 요청 이유를 포함시키십시오.

* 최대 7일 동안 최대 7GB의 데이터를 검색할 수 있습니다. 7GB의 데이터에 도달하거나 7일이 지나면 로그 데이터가 롤오버됩니다(선입선출).

