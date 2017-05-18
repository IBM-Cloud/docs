---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-25"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Eclipse Orion Web IDE를 사용하여 개발
{: #web_ide}

Eclipse Orion {{site.data.keyword.webide}}는 웹용으로 개발할 수 있는 브라우저 기반 개발 환경입니다. 컨텐츠 지원, 코드 자동 완성 및 오류 검사의 도움을 받아 JavaScript, HTML 및 CSS로 개발을 수행할 수 있습니다. {{site.data.keyword.webide}}는 거의 모든 언어에서 작동하며, 대부분의 파일 유형에 대해 구문 강조표시를 제공합니다. 소스 제어는 내장되어 있으며, 사용자는 로컬로 코드를 배치하여 앱을 테스트하고 디버그할 수 있습니다.
{:shortdesc}

특히 {{site.data.keyword.webide}}는 웹에서 구동됩니다. 설치, 관리 및 스케일링이 필요 없습니다. 인터넷이 연결되어 있으면 어디서든 개발할 수 있습니다. 

## IDE 설정
{: #editorsetup}

{{site.data.keyword.webide}}는 사용자 정의할 수 있으므로 개발 요구사항에 맞는 색상 구성표, 기술 도구 및 설정을 선택할 수 있습니다. 설정을 보고 수정하려면 왼쪽에 있는 메뉴에서 **설정** 아이콘 <img class="inline" src="images/webide_settings_icon_light_small.png"  alt="설정 아이콘">을 클릭하십시오. 

편집 중에 종종 특정 설정을 변경해야 하는 경우에는 **로컬 편집기 설정** 아이콘 <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="로컬 편집기 설정 아이콘">에서 해당 설정에 바로 액세스할 수 있습니다.  

![로컬 편집기 설정](images/webide_local_editor_settings_light.png)

기본적으로 편집기 스타일 및 글꼴 크기 설정은 항상 표시됩니다. 메뉴에 다른 편집기 설정을 포함시키려면 다음 단계를 따르십시오. 

1. **로컬 편집기 설정** 아이콘 <img class="inline" src="images/webide_local_settings_icon_light_small.png"  alt="로컬 편집기 설정 아이콘">을 클릭하십시오. 

2. **편집기 설정**을 클릭하십시오. 

3. **로컬 편집기 설정** 메뉴에서 설정을 포함하거나 제외하려면 각 설정 옆의 별표를 클릭하십시오. 

![편집기 설정 토글](images/webide_editor_settings_toggle_light.png)


## 코드 편집
{: #editcode}

{{site.data.keyword.webide}}에는 두 개의 기본 섹션이 있습니다. 첫 번째 섹션은 트리 구조로 프로젝트 파일을 표시하는 파일 네비게이터입니다. 파일 네비게이터에서 파일 및 폴더를 작성, 이름 바꾸기, 삭제 및 관리할 수 있습니다. 

**팁:** 파일 네비게이터에 파일을 업로드하려면 컴퓨터에서 파일 네비게이터로 파일을 끌어 오십시오. 

두 번째 섹션은 편집기 분할창입니다. 편집기는 컨텐츠 지원과 구문 유효성 검증을 포함하여 여러 코딩 기능을 제공합니다. 

![Web IDE](images/webide_light.png)

### 여러 파일에 대한 작업
1. 동시에 두 개의 파일로 작업하려면 **편집기 분할 모드 변경** 아이콘 <img class="inline" src="images/webide_split_editor_icon_light_small.png"  alt="편집기 분할 아이콘">을 클릭하십시오. 
2. 메뉴가 열리면 보기를 선택하십시오. 

 보기를 선택한 후 편집기에 파일이 이미 열려 있으면 해당 파일이 양쪽 편집기 보기에 표시됩니다. 

 편집기 보기 중 하나에 표시되는 파일을 열거나 변경하려면 다음을 수행하십시오. 
 1. 커서를 변경할 편집기 보기로 이동하십시오. 
 2. 파일 네비게이터에서 파일을 클릭하십시오. 

### 키보드 단축키
{{site.data.keyword.webide}}의 대부분의 명령은 키보드 단축키를 통해서만 액세스할 수 있습니다. 

편집기에서 키보드 단축키 목록을 보려면 Alt+Shift+?를 누르십시오. Mac OS를 사용 중인 경우에는 Ctrl+Shift+?를 누르십시오. 

## 소스 코드 관리
{: #sourcecontrol}

{{site.data.keyword.webide}}는 소스 코드 관리 도구와 통합됩니다. Git 저장소에 대해 작업하려면 **Git 저장소** 아이콘 <img class="inline" src="images/webide_git_icon_light_small.png"  alt="Git 저장소 아이콘">을 클릭하십시오.  

 **팁**: 오픈 도구 체인에서 {{site.data.keyword.webide}}를 사용 중이면 작업공간이 GitHub, {{site.data.keyword.ghe_short}} 또는 Git Repos and Issue Tracking 저장소로 미리 채워집니다. 현재 도구 체인과 연관된 저장소가 강조표시됩니다. 


## 작업공간에서 앱 배치
{: #deploy}

1. 앱을 배치하려면 실행 표시줄에서 실행 구성을 선택하거나 작성하십시오. 
1. 배치 아이콘 <img class="inline" src="images/webide_deploy_button_light_small.png"  alt="배치 아이콘">을 클릭하십시오. 작업공간의 현재 컨텐츠와 실행 구성에 정의된 환경을 사용하여 앱의 인스턴스가 배치됩니다.  
2. 앱이 배치되면 실행 표시줄을 사용하여 앱을 중지, 다시 시작 또는 디버그하고 로그를 보는 등의 작업을 수행할 수 있습니다.
![실행 표시줄](images/webide_runbar_light.png)    

<!-- 3/6/2016: bl commands don't work with V2/CD 
## Editing outside of the {{site.data.keyword.webide}}
{: #editlocal}

To use an editor besides the {{site.data.keyword.webide}}, set up {{site.data.keyword.Bluemix_live}} so that you can work directly with your project files in any tool. {{site.data.keyword.Bluemix_live_notm}} is a command-line application that synchronizes the changes in your local file system with your cloud workspace in {{site.data.keyword.jazzhub}}. 

### Before you begin 

Download and install the [{{site.data.keyword.Bluemix_live_notm}} command-line interface![External link icon](../../icons/launch-glyph.svg "External link icon")](http://livesyncdownload.ng.bluemix.net){: new_window}.

### Synchronizing your local environment with {{site.data.keyword.Bluemix_notm}}
{: #edit_local_download}

1. Open a command-line window.
2. Sign in to {{site.data.keyword.Bluemix_notm}}:

	```
	bl login
	```
	{: pre}

3. When you are prompted, enter your IBMid and password.
4. View a list of your {{site.data.keyword.Bluemix_notm}} projects: 

	```
	bl projects
	```
	{: pre}

4. Synchronize your local environment with your project on {{site.data.keyword.Bluemix_notm}}:

	```
	bl sync projectName
	```
	{: pre}

where `projectName` is your {{site.data.keyword.Bluemix_notm}} app's name.

When you are finished editing, enter `q` to end synchronization.

### Enabling the Desktop Sync feature to edit code locally

The Desktop Sync feature is like Live Edit mode for the command line. You need the Desktop Sync feature to debug on the command line.
1. In another command-line window, enable the Desktop Sync feature:

	```
	cd localDirectory
	bl start
	```
	{: codeblock}

2. Use the launch configuration that you created in the {{site.data.keyword.webide}}. After you select the launch configuration, the Desktop Sync feature is enabled in your local environment. In the command-line window that you just opened, you can view the app's URL, the debug URL, the manage URL, and view the {{site.data.keyword.Bluemix_live_notm}} state.

3. Refresh the browser and verify that you can see the changes that you saved to static files in the local workspace. 

### Disabling the Desktop Sync feature

1. In the second command-line window, enter `bl stop`.
2. In the first command-line window, enter `q`.

--> 
