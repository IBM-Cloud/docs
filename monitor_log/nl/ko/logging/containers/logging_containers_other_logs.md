---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-16"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 컨테이너에서 기본이 아닌 로그 데이터 수집
{: #logging_containers_collect_data}

컨테이너 내부의 기본이 아닌 로그 위치에서 데이터를 캡처하려면 컨테이너를 작성할 때 **LOG_LOCATIONS** 환경 변수를 설정하십시오.
{:shortdesc}

* 컨테이너를 작성할 때 로그 파일의 경로와 함께 **LOG_LOCATIONS** 환경 변수를 추가하십시오. 
* 여러 로그 파일을 쉼표로 구분하여 추가할 수 있습니다. 

## Bluemix 콘솔을 통해 기본이 아닌 로그 데이터 수집
{: #logging_containers_collect_data_ui}

콘솔을 통해 기본이 아닌 데이터를 수집하려면 다음 단계를 완료하십시오.

1. 카탈로그에서 **컨테이너**를 선택하고 이미지를 선택하십시오. 

    표시된 이미지 목록에는 {{site.data.keyword.IBM}}에서 제공한 이미지와 사설 {{site.data.keyword.Bluemix_notm}} 레지스트리에 저장된 이미지가 포함됩니다. 

2. 컨테이너를 정의하십시오. 유형을 선택하고 컨테이너의 이름을 입력하며 크기를 선택하고 IP 주소 세부사항 및 포트와 같은 기타 속성을 정의하십시오. 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} UI를 통한 단일 컨테이너 작성 및 배치](/docs/containers/container_single_ui.html#gui)를 참조하십시오. 

3. **고급 옵션** 섹션을 펼치고 **새로운 환경 변수 추가**를 선택하십시오.

4. **LOG_LOCATIONS** 변수를 추가하고 해당 값을 분석할 로그로 설정하십시오.

    예를 들어, 최신 Liberty 이미지를 기반으로 하는 컨테이너를 추가할 때 *dpkg.log* 로그 파일을 분석하려면 환경 변수를 다음 값으로 설정하십시오.
    
    <table>
      <caption>표 1. 로그 위치 샘플 값</caption>
      <tbody>
        <tr>
          <th align="center">변수 이름</th>
          <th align="center">값</th>
        </tr>
        <tr>
          <td align="left">LOG_LOCATIONS</td>
          <td align="left">/var/log/dpkg.log</td>
        </tr>
      </tbody>
    </table>

4. **작성**을 클릭하십시오.

컨테이너 대시보드가 열립니다. 컨테이너 상태가 *실행 중*인지 확인한 다음 **모니터링 및 로그** 탭에서 로그를 확인하십시오.


## CLI를 통해 기본이 아닌 로그 데이터 수집
{: #logging_containers_collect_data_cli}

CLI를 통해 기본이 아닌 데이터를 수집하려면 다음 단계를 완료하십시오.

1. {{site.data.keyword.containershort}} CLI를 사용하도록 터미널을 설정하십시오. 자세한 정보는 [IBM Bluemix 컨테이너 서비스 CLI 설정](/docs/containers/container_cli_cfic_install.html)을 참조하십시오.

2. `cf login` 명령을 사용하여 Cloud Foundry CLI에 로그인하십시오. 프롬프트되면 {{site.data.keyword.Bluemix_notm}} ID, 비밀번호, 조직 및 영역을 입력하십시오. 

    기본적으로 로그인한 마지막 영역 또는 미국 남부 지역에 로그인됩니다. 
    
    {{site.data.keyword.Bluemix_notm}}의 특정 지역에 로그인하려면 **–a** 옵션을 포함할 수 있습니다. 예를 들어 다음 표는 지역별 명령을 나열합니다.

    <table>
      <caption>표 2. 지역에 따른 명령</caption>
      <tbody>
        <tr>
          <th align="center">지역</th>
          <th align="center">명령</th>
        </tr>
        <tr>
          <td align="left">미국 남부</td>
          <td align="left"> cf login -a api.ng.bluemix.net</td>
        </tr>
        <tr>
          <td align="left">영국</td>
          <td align="left">cf login -a api.eu-gb.bluemix.net</td>
        </tr>
	 <tr>
          <td align="left">프랑크푸르트</td>
          <td align="left">cf login -a api.eu-de.bluemix.net</td>
        </tr>
       </tbody>
    </table>
    

3. `cf ic login` 명령을 사용하여 {{site.data.keyword.containershort}}에 로그인하십시오.

4. 이미지에서 단일 컨테이너를 작성하십시오. 기본이 아닌 로그 위치를 포함하도록 LOG_LOCATIONS 환경 변수를 포함하십시오.  

    Kibana에서 해당 정보를 볼 수 있도록 사용자 정의 위치를 추가하려면 컨테이너를 작성할 때 **LOG_LOCATIONS** 환경 변수를 추가하십시오. 다음 명령을 입력하십시오.
    
    `docker run -p portNumber -e "LOG_LOCATIONS=log1,log2" --name containerName registry.domain_name/imageName:imageTag`
    
    여기서,
    
     <table>
      <caption>표 3. 명령 옵션</caption>
      <tbody>
        <tr>
          <th align="center">옵션</th>
          <th align="center">설명</th>
        </tr>
        <tr>
          <td align="left">-p</td>
          <td align="left"> 인터넷에서 앱에 액세스할 수 있게 하려면 공용 포트를 노출해야 합니다. 사용 중인 이미지에 대해 Dockerfile에 지정된 포트를 포함합니다. <br> 사용할 IP 프로토콜을 표시하도록 UDP와 TCP 중에 선택할 수 있습니다. 프로토콜을 지정하지 않는 경우 포트가 TCP 트래픽에 자동으로 노출됩니다. <br> 공용 포트를 노출할 때 노출된 포트에서만 공용 데이터를 보내고 받을 수 있도록 컨테이너의 공용 네트워크 보안 그룹을 작성합니다. 다른 모든 공용 포트는 닫히고 인터넷에서 앱에 액세스하는 데 사용할 수 없습니다. <br> 여러 -p 옵션을 사용하여 여러 포트를 포함할 수 있습니다. </td>
        </tr>
        <tr>
          <td align="left">-e</td>
          <td align="left">환경 변수를 설정합니다. <br> 여러 키를 개별적으로 나열할 수 있습니다. 환경 변수 이름과 값 둘을 모두 따옴표로 묶으십시오. <br> 컨테이너에서 모니터링할 로그 파일을 추가하려면 LOG_LOCATIONS 환경 변수를 로그 파일의 경로와 함께 포함시키십시오. </td>
        </tr>
        <tr>
          <td align="left">--name</td>
          <td align="left">컨테이너의 이름을 정의합니다.</td>
        </tr>
	<tr>
          <td align="left">registry.domain_name</td>
          <td align="left">공용 영역의 레지스트리입니다. 예를 들어, 미국 남부 지역의 경우 기본 도메인 이름은 `ng.bluemix.net`이고, 영국의 경우 기본 도메인 이름은 `eu-gb.bluemix.net`입니다. </td>
        </tr>
        <tr>
          <td align="left">imageName</td>
          <td align="left">추가할 이미지의 이름입니다.</td>
        </tr>
	<tr>
          <td align="left">imageTag</td>
          <td align="left">추가할 이미지의 태그입니다.</td>
        </tr>
      </tbody>
    </table>
    
    예를 들어, 최신 Liberty 이미지를 기반으로 컨테이너를 작성하고 `/var/log/dpkg.log` 로그 파일을 포함하려면 다음 명령을 사용하십시오. 
    
    `docker run -p 9080 -e "LOG_LOCATIONS=/var/log/dpkg.log" --name MyContainer registry.ng.bluemix.net/ibmliberty:latest`
    
    dpkg.log 파일은 컨테이너 작성 중에 일반적으로 생성되는 표준 Ubuntu 로그 파일이지만, Kibana에 자동으로 푸시되지 않습니다.

컨테이너의 상태를 확인하려면 `docker ps` 명령을 실행하십시오. 상태가 *실행 중*이면 명령행 또는 Kibana를 통해 {{site.data.keyword.Bluemix_notm}} 콘솔의 로그를 확인하십시오.



