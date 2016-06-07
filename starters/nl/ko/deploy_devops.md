---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:download: .download}

# Git를 사용하여 코딩 시작
*마지막 업데이트 날짜: 2016년 3월 2일*  

{{site.data.keyword.Bluemix}}에 자동으로 배치되는 호스팅되는 Git 저장소를 작성할 수 있습니다. 그런 다음 변경사항을 Git 저장소에 푸시하여 사용자의 앱에서 실행되는 코드를 수정할 수 있습니다.
{:shortdesc}

1. 시작하려면 앱의 개요 페이지에서 **Git 저장소 및 파이프라인 추가**를 클릭하거나 {{site.data.keyword.Bluemix_notm}} Classic Experience에서 **GIT 추가**를 클릭하십시오. 
2. 열린 창에서 **스타터 앱 패키지로 저장소 채우기 및 파이프라인 빌드 및 배치 사용** 선택란이 선택되어 있는지 확인하십시오. Git 저장소가 작성됩니다. 스타터 코드가 사용 가능하면 저장소에 로드됩니다. 또한 {{site.data.keyword.jazzhub}}에서 실행 중인 Delivery Pipeline 서비스에 의해 애플리케이션이 배치됩니다.  
3. 앱을 업데이트하려면 명령행 또는 Web IDE를 사용할 수 있습니다.
   **명령행을 사용하는 경우:**
   a. 앱의 개요 페이지의 Git URL에서 Git 저장소를 복제하십시오.
   b. 즐겨찾기 편집기에서 코드를 업데이트하십시오.
   c. Git 명령행 인터페이스에서 변경사항을 푸시하십시오.  
	    
   **Web IDE를 사용하는 경우:**  
   a. 앱의 개요 페이지에서 **코드 편집**을 클릭하십시오. 프로젝트가 Web IDE에서 열립니다.  
   b. 필요에 따라 변경하고 기본 제공 Git 지원을 사용하여 푸시하십시오.  
		
업데이트된 앱이 {{site.data.keyword.Bluemix_notm}}에 다시 배치됩니다.  

단계별 지시사항을 보려면 [DevOps Services에서 Git 통합 및 자동 배치 설정](https://hub.jazz.net/tutorials/jazzeditor/#git_integration_and_autodeployment)을 참조하십시오.  

## Git가 추가되었습니까? {{site.data.keyword.Bluemix_notm}} Live Sync를 시도해 보십시오.  

Node.js 앱을 빌드 중인 경우, {{site.data.keyword.Bluemix_notm}} Live Sync를 사용하면 데스크탑에서와 같이 {{site.data.keyword.Bluemix_notm}}에서 앱 인스턴스를 신속하게 업데이트하고 개발할 수 있습니다.  

{{site.data.keyword.Bluemix_notm}} Live Sync에 대한 자세한 정보는 [{{site.data.keyword.Bluemix_notm}} Live Sync](../develop/bluemixlive.html)를 참조하십시오. 명령에 대한 세부사항은 [{{site.data.keyword.Bluemix_notm}} Live Sync CLI 문서](../cli/reference/bl/index.html)를 참조하십시오. {{site.data.keyword.Bluemix_notm}} Live Sync를 Web IDE와 함께 사용하려면 [Live Edit](../develop/bluemixlive.html)를 참조하십시오.  

1. {{site.data.keyword.Bluemix_notm}} Live Sync bl 명령행을 다운로드하고 설치하십시오. 

<p>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/blive_setup.msi" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/bl_gs_icons_windows_b.svg" alt="Windows bl 명령행 다운로드 단추" /> </a>
<a class="xref" href="http://livesyncdownload.ng.bluemix.net/downloads/BluemixLive.pkg" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/bl_gs_icons_mac-osx_b.svg" alt="Mac bl 명령행 다운로드 단추" /> </a>
</p>

**중요:** bl 명령행 도구는 Windows 7 및 8과 Mac OS X 버전 10.9 이상에서만 사용할 수 있습니다. 

2. 명령행에서 다음 명령을 사용하여 로그인하십시오. IBM® ID와 비밀번호를 입력하도록 프롬프트됩니다.
```
bl login
```

3. 다음 명령을 입력하여 {{site.data.keyword.Bluemix_notm}} Live Sync 동기화에 사용할 수 있는 프로젝트 목록을 표시하십시오.
```
bl projects
```
목록에서 애플리케이션과 일치하는 프로젝트 이름을 찾으십시오. 프로젝트 이름은 *별명* | *애플리케이션 이름* 형식입니다. 

4. 다음 명령을 입력하여 로컬 환경을 {{site.data.keyword.Bluemix_notm}}에 있는 프로젝트와 동기화하십시오. 프로젝트 소유자인 경우에는 projectName으로 your-application-name만 지정하면 됩니다. 
<!--- this command needs italicized parameters projectName localDirectory and yellow on 'local' -->
```
bl sync projectName -d localDirectory --verbose
```
이 명령은 사용자가 "q"를 입력할 때까지 계속 실행되고 동기화도 계속됩니다. --verbose 옵션은 로깅 및 상태 정보를 표시합니다. 인수에 공백이 포함된 경우 이름을 따옴표로 묶어야 합니다.

5. 다른 명령행 창의 로컬 디렉토리에 다음 명령을 입력하여 애플리케이션을 {{site.data.keyword.Bluemix_notm}}에 Live Edit 모드로 배치하십시오.
```
bl start
```  

로컬 디렉토리에서 파일을 변경하면 {{site.data.keyword.Bluemix_notm}}에서 실행 중인 애플리케이션 및 프로젝트 클라우드 작업공간 둘 다에 변경사항이 자동으로 전파됩니다. Node 애플리케이션을 다시 시작해야 하는 경우에는 다음 명령을 사용할 수 있습니다.
```
bl start --restart
```
