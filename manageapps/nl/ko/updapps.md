---

copyright:
  years: 2015, 2016

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

#앱 업데이트
{: #updatingapps}

*마지막 업데이트 날짜: 2016년 5월 9일*


cf push 명령 또는 {{site.data.keyword.Bluemix}} DevOps Services를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 애플리케이션을 업데이트할 수 있습니다. 대부분의 경우 심지어 Node.js와 같은 기본 제공 빌드팩의 경우에도 -c 매개변수를 제공하여 애플리케이션 시작에 사용할 명령을 지정해야 합니다.
{:shortdesc}

##사용자 정의 도메인 작성 및 사용
{: #domain}

애플리케이션의 URL에 기본 {{site.data.keyword.Bluemix_notm}} 시스템 도메인(mybluemix.net) 대신 사용자 정의 도메인을 사용할 수 있습니다.

도메인은 {{site.data.keyword.Bluemix_notm}}에서 조직에 할당되는 URL 라우트를 제공합니다. 사용자 정의 도메인을 사용하려면 공용 DNS 서버에 사용자 정의 도메인을 등록하고, {{site.data.keyword.Bluemix_notm}}에서 사용자 정의 도메인을 구성한 다음 해당 사용자 도메인을 공용 DNS 서버의 {{site.data.keyword.Bluemix_notm}} 시스템 도메인에 맵핑해야 합니다. 사용자 정의 도메인이 {{site.data.keyword.Bluemix_notm}} 시스템 도메인에 맵핑되면 사용자 정의 도메인에 대한 요청이 {{site.data.keyword.Bluemix_notm}}의 애플리케이션으로 라우팅됩니다.

{{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 또는 명령행 인터페이스를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 사용자 정의 도메인을 작성하고 사용할 수 있습니다.

* {{site.data.keyword.Bluemix_notm}} 사용자 인터페이스 사용:

  1. 조직의 사용자 정의 도메인을 작성하십시오.
    
	1. {{site.data.keyword.Bluemix_notm}} **대시보드**의 메뉴 표시줄에서 **조직 관리**를 클릭하십시오.
	
	2. **도메인** 탭에서 **도메인 추가**를 클릭하고 사용자 정의 도메인 이름을 입력한 다음 **저장**을 클릭하십시오.
    	
  2. 사용자 정의 도메인을 포함한 라우트를 애플리케이션에 추가하십시오.
  
    1. {{site.data.keyword.Bluemix_notm}} **대시보드**의 메뉴 표시줄에서 라우트를 추가할 애플리케이션의 타일을 클릭하십시오. **개요** 페이지가 표시됩니다.
	
	2. **개요** 페이지의 애플리케이션 메뉴에서 **라우트 및 앱 액세스 편집**을 클릭하십시오.
	
	3. **라우트 추가**를 클릭하고 애플리케이션에 사용할 라우트를 지정하십시오.
	
* cf 명령행 인터페이스 사용:
  
  1. 다음 명령을 입력하여 조직의 사용자 정의 도메인을 작성하십시오.
    
    ```
    cf create-domain <your org name> mydomain
    ```
    
    *organization_name*
  
        조직 이름입니다.
	  
    *mydomain*
    
        사용하려는 사용자 정의 도메인 이름입니다.
	  
  2. 다음 명령을 입력하여 사용자 정의 도메인을 포함한 라우트를 애플리케이션에 추가하십시오.
    
    ```
    cf map-route myapp mydomain -n host_name
    ```
    
    *myapp*
      
    	애플리케이션 이름입니다.
  	
    *mydomain*
      
    	사용자 정의 도메인의 이름입니다.
	
    *host_name*
    
        애플리케이션에 사용할 라우트의 호스트 이름입니다.
	
{{site.data.keyword.Bluemix_notm}}에서 사용자 정의 도메인을 구성한 후에는 사용자 정의 도메인을 등록된 DNS 서버의 {{site.data.keyword.Bluemix_notm}} 시스템 도메인으로 맵핑해야 합니다.

  1. DNS 서버에 사용자 정의 도메인 이름에 대한 'CNAME' 레코드를 설정하십시오.
  2. 애플리케이션이 실행 중인 {{site.data.keyword.Bluemix_notm}} 지역의 보안 엔드포인트에 사용자 정의 도메인 이름을 맵핑하십시오. 다음과 같은 지역 엔드포인트를 사용하여 {{site.data.keyword.Bluemix_notm}}에서 사용자 조직에 할당되는 URL 라우트를 제공하십시오.
  
    * US-SOUTH: `secure.us-south.bluemix.net`
    * EU-GB: `secure.eu-gb.bluemix.net`
    * AU-SYD: `secure.au-syd.bluemix.net`
  
브라우저 또는 명령행 인터페이스에서 myapp 애플리케이션에 액세스하는 데 필요한 다음 URL을 입력하십시오.

```
http://host_name.mydomain
```

**참고:** 분리된 라우트를 제거하려면 다음 명령을 사용하십시오.

```
cf delete-route domain -n hostname -f
```

*domain*은 도메인 이름이고, *hostname*은 애플리케이션에 대한 라우트의 호스트 이름입니다. **cf delete-route** 명령에 대한 자세한 정보를 보려면 `cf delete-route -h`를 입력하십시오.

##Blue-Green 배치
{: #blue_green}

{{site.data.keyword.Bluemix_notm}}에서는 Blue-Green 배치 기술을 사용하여 지속적 딜리버리 및 중단 시간 최소화 이벤트를 사용하도록 설정합니다.

*Blue-Green 배치*는 Blue 및 Green이라는 거의 동일한 두 개의 프로덕션 환경으로 구성된 무중단 배치 기술로서, 개발자가 보통 애플리케이션 버전을 통해 의도적으로 변경한 아티팩트별로 구별됩니다. 언제든지 적어도 하나의 환경은 활성 상태입니다. Blue-Green 배치 기술을 사용하면 다음과 같은 이점을 실현할 수 있습니다.

* 소프트웨어를 최종 테스트 단계에서 라이브 프로덕션으로 신속하게 전환할 수 있습니다.
* 애플리케이션에 대한 트래픽을 중단하지 않고도 새 애플리케이션 버전을 배치할 수 있습니다.
* 신속하게 롤백됩니다. 한 환경에 문제가 있을 경우 신속하게 다른 환경으로 전환할 수 있습니다.

{{site.data.keyword.Bluemix_notm}}에 이미 배치된 애플리케이션을 새 버전으로 업데이트하려는 경우 다음 두 가지 접근 방법으로 Blue-Green 배치를 보장할 수 있습니다.

###예: cf rename 명령 사용

이 예에서 애플리케이션의 이름은 Blue입니다. 이 예는 애플리케이션에 대한 트래픽을 중단하지 않고 **cf rename** 명령을 사용하여 *Blue*의 버전을 업데이트하는 방법을 보여줍니다. 업데이트된 버전이 적절히 갖춰져 있으면 선택적으로 *Blue*의 이전 버전을 삭제할 수 있습니다.

1. *Blue* 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
  
  ```
  cf push Blue
  ```
  
  **결과:** *Blue* 앱이 실행 중이며 URL `Blue.mybluemix.net`에 응답합니다.
  
2. 다음과 같이 **cf rename** 명령을 사용하여 *Blue* 앱의 이름을 *Green*으로 바꾸십시오.
  
  ```
  cf rename Blue Green
  ```
  
  **cf apps** 명령을 사용하여 현재 영역에 있는 애플리케이션을 나열하십시오.
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **결과:** *Green* 앱이 실행 중이며 URL `Blue.mybluemix.net`에 응답합니다.

3. 필요한 사항을 변경하고 업데이트된 *Blue* 버전을 준비 상태로 유지하십시오. 업데이트된 *Blue* 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
  
  ```
  cf push Blue
  ```
  
  **cf apps** 명령을 사용하여 현재 영역에 있는 애플리케이션을 나열하십시오.
  
  ```
  ...
  name             requested state   instances   memory   disk   urls
  Green            started           1/1         1G       1G	 Blue.mybluemix.net
  Blue             started           1/1         1G       1G	 Blue.mybluemix.net
  ...
  ```
  
  **결과:**
    * 애플리케이션의 두 인스턴스(*Blue* 및 *Green*)가 배치됩니다.
	* *Green* 앱이 실행 중이며 URL `Blue.mybluemix.net`에 응답합니다.
	
4. 선택사항: 앱의 이전 버전(*Green*)을 삭제하려는 경우, **cf delete** 명령을 사용하십시오.
  
  ```
  cf delete Green -f
  ```
  
  **cf route** 명령을 사용하여 영역에 있는 라우트를 나열하십시오.
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  ...
  ```
  
  **결과:** *Blue* 앱이 URL `Blue.mybluemix.net`에 응답합니다.
  
###예: cf map-route 명령 사용

이 예에서 *Blue*는 이전에 배치한 애플리케이션이고, *Green*은 업데이트된 버전입니다. 이 예는 애플리케이션에 대한 트래픽을 중단하지 않고 **cf map-route** 명령을 사용하여 *Blue*의 버전을 업데이트하는 방법을 보여줍니다. 업데이트된 버전이 적절히 갖춰져 있으면 선택적으로 *Blue*의 이전 버전을 삭제할 수 있습니다.

1. *Blue* 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
  
  ```
  cf push Blue
  ```
  
  **결과:** *Blue* 앱이 실행 중이며 URL `Blue.mybluemix.net`에 응답합니다.
  
2. 필요한 사항을 변경하고 *Green* 버전을 준비 상태로 유지하십시오. *Green* 앱을 {{site.data.keyword.Bluemix_notm}}에 푸시하십시오.
  
  ```
  cf push Green
  ```
  
  **cf route** 명령을 사용하여 현재 영역에 있는 애플리케이션을 나열하십시오.
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue
  Green            mybluemix.net    Green
  ...
  ```
  
  **결과:**
  
    * 앱의 두 인스턴스(*Blue* 및 *Green*)가 배치됩니다.
	* *Blue* 앱이 URL `Blue.mybluemix.net`에 응답합니다. *Green* 앱이 URL `Green.mybluemix.net`에 응답합니다.
	
3. `Blue.mybluemix.net`에 대한 모든 트래픽이 *Blue* 앱과 *Green* 앱에 라우트되도록 *Blue* 앱을 *Green* 앱에 맵핑하십시오.
  
  ```
  cf map-route Green mybluemix.net -n Blue
  ```
  
  cf routes 명령을 사용하여 영역에 있는 라우트를 나열하십시오.
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Blue, Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **결과:**

    * 이제 CF 라우터는 Blue.mybluemix.net에 대한 트래픽을 Blue 앱과 Green 앱에 전송합니다.
	* CF 라우터는 계속해서 Green.mybluemix.net에 대한 트래픽을 Green 앱에 전송합니다.
	
4. *Green*이 예상대로 실행되는 것이 확인되면, *Blue* 앱에서 `Blue.mybluemix.net` 라우트를 제거하십시오.
  
  ```
  cf unmap-route Blue mybluemix.net -n Blue
  ```
  
  cf routes 명령을 사용하여 영역에 있는 라우트를 나열하십시오.
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  Green            mybluemix.net    Green
  ...
  ```
  
  **결과:** CF 라우터가 *Blue* 앱에 대한 트래픽 전송을 중지합니다. *Green* 앱이 URL `Green.mybluemix.net` 및 `Blue.mybluemix.net`에 응답합니다.
  
5. *Green* 앱에 대한 `Green.mybluemix.net` 라우트를 제거하십시오.
  
  ```
  cf unmap-route Green mybluemix.net -n Green
  ```
  
  **결과:** CF 라우터가 *Blue* 앱에 대한 트래픽 전송을 중지합니다. *Green* 앱이 URL `Blue.mybluemix.net`에 응답합니다.
  
6. 선택사항: 애플리케이션의 이전 버전(*Blue*)을 삭제하려는 경우, `cf delete` 명령을 사용하십시오.
  
  ```
  cf delete Blue -f
  ```
  
  cf route 명령을 사용하여 영역에 있는 라우트를 나열하십시오.
  
  ```
  ...
  host             domain           apps
  Blue             mybluemix.net    Green
  ...
  ```
  
  **결과:** *초록색* 앱이 URL `Blue.mybluemix.net`에 응답합니다.


# 관련 링크
{: #rellinks}

## 관련 링크
{: #general}

* [Blue-Green 배치](http://martinfowler.com/bliki/BlueGreenDeployment.html){:new_window}
* [IBM {{site.data.keyword.Bluemix_notm}} DevOps Services](https://hub.jazz.net/){:new_window}
