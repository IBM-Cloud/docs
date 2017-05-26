---

copyright:
  years: 2015, 2017

lastupdated: "2017-02-01"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}


# 예: Cloud Foundry 애플리케이션 로그를 Splunk에 스트리밍
{: #splunk}

이 예에서, 이름이 Jane인 개발자는 IBM Virtual Servers Beta 및 Ubuntu 이미지를 사용하여 가상 서버를 작성합니다. Jane은 {{site.data.keyword.Bluemix_notm}}에서 Splunk로 Cloud Foundry 앱 로그의 스트리밍을 시도합니다. {:shortdesc}

  1. 우선 Jane은 Splunk를 설정합니다. 

     a. Jane은 [Splunk Light 다운로드 사이트 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://www.splunk.com/en_us/download/splunk-light.html){:new_window}에서 Splunk Light를 다운로드한 후 다음 명령을 사용하여 설치합니다. 소프트웨어는 */opt/splunk*에 설치됩니다. 

	    ```
dpkg -i  ~/splunklight-6.3.0-aa7d4b1ccb80-linux-2.6-amd64.deb
        ```

     b. Jane은 {{site.data.keyword.Bluemix_notm}}와의 통합을 위해 RFC5424 syslog 기술 추가 기능을 설치하고 패치합니다. 추가 기능 설치 지시사항에 대한 자세한 정보는 [Cloud Foundry 가이드라인 ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://docs.cloudfoundry.org/devguide/services/integrate-splunk.html){:new_window}을 참조하십시오.

	    Jane은 다음 명령을 사용하여 추가 기능을 설치합니다. 

	    ```
cd /opt/splunk/etc/apps
        tar xvfz ~/rfc5424-syslog_11.tgz
        ```

        그리고 Jane은 */opt/splunk/etc/apps/rfc5424/default/transforms.conf*를 다음 텍스트로 구성된 새 *transforms.conf* 파일로 대체하여 추가 기능을 패치합니다. 

	    ```
[rfc5424_host]
        DEST_KEY = MetaData:Host
        REGEX = <\d+>\d{1}\s{1}\S+\s{1}(\S+)
        FORMAT = host::$1[rfc5424_header]
        REGEX = <(\d+)>\d{1}\s{1}\S+\s{1}\S+\s{1}(\S+)\s{1}(\S+)\s{1}(\S+)
        FORMAT = prival::$1 appname::$2 procid::$3 msgid::$4
        MV_ADD = true
        ```
        {:screen}

     c. Splunk가 설정되면, Jane은 Ubuntu 시스템의 일부 포트를 열어서 수신 syslog 드레인(포트 5140) 및 Splunk 웹 UI(포트 8000)를 허용해야 합니다. {{site.data.keyword.Bluemix_notm}} 가상 서버에 방화벽이 기본적으로 설정되어 있기 때문입니다. 

	    **참고:** iptable 구성은 Jane의 평가 용도로 여기서 수행되며, 이는 임시적입니다. 프로덕션에서 Bluemix 가상 서버의 방화벽 설정을 구성하려면 [Network Security Groups ![외부 링크 아이콘](../icons/launch-glyph.svg "외부 링크 아이콘")](https://new-console.ng.bluemix.net/docs/services/networksecuritygroups/index.html){:new_window} 문서를 참조하십시오.

	   ```
	   iptables -A INPUT -p tcp --dport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --sport 5140 -j ACCEPT
       iptables -A INPUT -p tcp --dport 8000 -j ACCEPT
       iptables -A INPUT -p tcp --sport 8000 -j ACCEPT
	   ```
	   {:screen}

	   그리고 Jane은 다음 명령을 사용하여 Splunk를 실행합니다. 

       ```
	   /opt/splunk/bin/splunk start --accept-license
       ```

  2. Jane은 {{site.data.keyword.Bluemix_notm}}에서 syslog 드레인을 허용하도록 Splunk 설정을 구성합니다. Jane은 syslog 드레인에 대한 데이터 입력을 작성해야 합니다. 

     a. Splunk 웹 인터페이스에서 Jane은 **데이터 > 데이터 입력**을 클릭합니다. Splunk에서 지원하는 입력 유형의 목록이 표시됩니다. 

     b. syslog 드레인이 TCP 프로토콜을 사용하므로, Jane은 **TCP**를 선택합니다. 

     c. **TCP** 분할창에서, Jane은 **포트** 필드에 **5140**을 입력하고 나머지 필드는 공백으로 남겨둔 후에 **다음**을 클릭합니다. 

     d. **소스 유형** 목록에서 Jane은 **미분류 > rfc5424_syslog**를 선택합니다. 

     e. **메소드** 유형에 대해 Jane은 **IP**를 선택합니다. 

     f. **색인** 필드에서 Jane은 **색인 새로 작성**을 클릭합니다. 그리고 새 색인의 이름을 "bluemix"로 지정한 후에 **저장**을 클릭합니다. 

     g. 마지막으로 **검토** 창에서 Jane은 설정이 올바른지 확인한 후에 **제출**을 클릭하여 이 데이터 입력을 사용 가능하게 설정합니다. 

  3. {{site.data.keyword.Bluemix_notm}}에서, Jane은 syslog 드레인 서비스를 작성하고 이 서비스를 앱에 바인드합니다. 

     a. Jane은 cf cli에서 다음 명령을 사용하여 syslog 드레인 서비스를 작성합니다. 

     ```
cf cups splunk -l syslog://dummyhost:5140
     ```

     **참고:** *dummyhost*는 실제 이름이 아닙니다. 이는 실제 호스트 이름을 숨기는 데 사용됩니다. 

     b. Jane은 syslog 드레인 서비스를 자체 영역의 앱에 바인드한 후에 앱을 다시 스테이징합니다. 

	 ```
cf bind-service myapp splunk
     cf restage myapp
     ```


Jane은 자신의 앱을 사용해 본 후에 Splunk 웹 인터페이스에서 다음의 조회 문자열을 입력합니다. 

```
source="tcp:5140" index="bluemix" sourcetype="rfc5424_syslog"
```

Jane은 Splunk 웹 인터페이스에서 로그의 스트림을 봅니다. 설치하는 Splunk가 Splunk Light이지만, Jane은 매일 500MB 로그를 계속 보유할 수 있습니다. 

