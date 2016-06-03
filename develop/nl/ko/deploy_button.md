---

 

copyright:

  years: 2015, 2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}


#{{site.data.keyword.Bluemix_notm}}에 배치 단추 작성 {: #deploy-button} 

*마지막 업데이트 날짜: 2016년 3월 2일* 

{{site.data.keyword.Bluemix}}에 배치 단추는 다른 사람들이 코드를 사용해 보고 IBM {{site.data.keyword.Bluemix_notm}}에 배치할 수 있도록 공용 Git 소스 앱을 공유하는 효과적인 방법입니다. 이 단추를 사용하려면 최소한의 구성이 필요하며 마크업을 지원하는 모든 위치에 이 단추를 삽입할 수 있습니다. 사용자가 이 단추를 클릭하면 원래 앱이 영향을 받지 않도록 새 Git 저장소에 복제된 코드 사본이 작성됩니다. 
{: shortdesc} 

**팁:** 회사 브랜드가 중요할 경우, 단추를 삽입하는 대신 컨텐츠에
[{{site.data.keyword.Bluemix_notm}} iFrame에 배치 플로우를 임베드](../develop/deploy_button_embed.html)할 수 있습니다. 사용자가 공용 Git 소스 앱의
복제본을 작성할 경우, bluemix.net 웹 사이트로 경로 재지정되는 대신에 사용자 컨텐츠에
남게 됩니다. 

사용자가 단추를 클릭하면
다음과 같은 조치가 수행됩니다. 

1. 활성 {{site.data.keyword.Bluemix}} 계정이 없는 경우
평가판 계정을 작성해야 합니다. 

2. 사용자는 지역, 조직, 영역 및 앱 이름을 선택할 수 있습니다. 제시된 앱 이름은 이전 앱 이름, 사용자 이름 및 시간을 바탕으로
구성됩니다. 

3. 원래 공용 Git 저장소의 마스터 분기가 새 전용 {{site.data.keyword.jazzhub_title}}
프로젝트에 새 Git 저장소로 복제됩니다. 

4. 앱에 빌드 파일이 필요한 경우 빌드 파일이 자동으로 검색되어 앱이
빌드됩니다. 

5. 빌드 및 배치 프로세스에 대해 파이프라인이 구성되어 있으면 `pipeline.yml` 파일이 앱을 배치하는 데 사용됩니다.

6. 앱에 컨테이너가 필요한 경우, **IBM Containers** 서비스를 정의하는 `pipeline.yml`과 이미지를 정의하는 Dockerfile이 앱을 {{site.data.keyword.Bluemix_notm}} 컨테이너에 배치하는 데 사용됩니다. 

7. 앱이 사용자의 {{site.data.keyword.Bluemix_notm}} 조직에 배치됩니다. 

##단추 예 {: #button-examples} 

공용 {{site.data.keyword.jazzhub_short}} 저장소의
앱 단추 예를 참조하십시오.

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://hub.jazz.net/git/idsorg/sample-java-cloudant" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix에 배치" /></a>
</p> 

공용 GitHub 저장소의
앱 단추 예를 참조하십시오. 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/ibmjstart/bluemix-node-mysql-uploader" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix에 배치" /></a>
</p> 

{{site.data.keyword.Bluemix_notm}} 컨테이너에
배치되는 앱에 대한 단추 예를 참조하십시오. 

<p>
<a class="xref" href="https://bluemix.net/deploy?repository=https://github.com/Puquios/hello-containers" target="_blank" title="(새 탭 또는 창에서 열림)"><img class="image" src="images/deploy_buttonx2.png" alt="Bluemix에 배치" /></a>
</p> 

##단추 작성 {: #create-button}

{{site.data.keyword.Bluemix_notm}}에 배치 단추를 작성하려면 다음을 수행하십시오. 

<ol>
<li> 다음 스니펫 템플리트 중 하나를 복사하여 수정한 다음 올바른 공용 Git 저장소를 포함시키십시오.

<p></p>
<p>
<strong>팁</strong>: DevOps 서비스 프로젝트에 대한 빌드 입력 항목을 지정하려는 경우, 분기 매개변수를 Git URL에 추가하십시오. 분기 매개변수를 추가하면 모든 분기를 포함하여 원래 공용 Git 저장소가 새 개인용 DevOps 서비스 오브젝트에 새 Git 저장소로 복제됩니다. 지정된 Git 분기가 빌드 작업을 위한 입력 항목으로 설정됩니다. 분기를 지정하지 않으면 빌드 작업의 입력 항목이 기본적으로 마스터 분기로 설정됩니다.
</p>
<ul>
<li>HTML:
<p>
기본 마스터 분기:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
<p>
지정된 Git 분기:
</p>
<pre class="codeblock">
&lt;a href="https://bluemix.net/deploy?repository=&lt;git_repository_URL&gt;&branch=&lt;git_branch>" # [required]&gt;&lt;img src="https://bluemix.net/deploy/button.png" alt="Deploy to Bluemix"&gt;&lt;/a&gt;
</pre>
</li>
<li>마크다운:
<p>
기본 마스터 분기:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> # [required]&#41;
</pre>
<p>지정된 Git 분기:
</p>
<pre class="codeblock">
[&#33;[Deploy to Bluemix]&#40;https://bluemix.net/deploy/button.png&#41;]&#40;https://bluemix.net/deploy?repository=&lt;git_repository_URL> &branch=&lt;git_branch&gt; # [required]&#41;
</pre>
</li>
</ul>
</li>
<li>블로그, 기사, 위키, readme 파일 또는 앱 승격을 원하는 위치에 스니펫을 삽입하십시오.
</li>
</ol>

##단추에 대한 스니펫 고려사항 {: #button-snippet}

Bluemix에 배치 단추에 대한 스니펫을 사용자 정의하는 경우, 다음 고려사항을 검토하십시오. 

* 두 템플리트 모두에서 외부 단추 이미지의 기본 경로가 PNG 형식과 영어를 사용합니다. 

    * 단추에 대해 PNG 대신 SVG 이미지를 사용하려는 경우 SVG 버전이 사용 가능합니다. 스니펫에 사용된 외부 단추 이미지의 경로를 `https://bluemix.net/deploy/button.svg`로 변경할 수 있습니다.
	
	* 더 큰 단추 이미지를 사용하고 싶으면 원본 크기보다 두 배 큰
PNG 이미지가 있습니다. 스니펫에
사용된 외부 단추 이미지의 경로를
`https://bluemix.net/deploy/button_x2.png`로 변경할 수 있습니다. 
	
	* 이미지를 로컬에 저장하려는 경우 이미지를 다운로드하고 Git 저장소에
저장할 수 있습니다. 이미지의 상대 위치를 사용하도록 경로를 조정하십시오. 
	
	* 단추의 번역된 버전을 사용하려는 경우 이 버전을 원격으로 참조하거나
[ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button](ftp://public.dhe.ibm.com/cloud/bluemix/deploy_button)에서
다운로드할 수 있습니다. 
	
##단추에 대한 저장소 고려사항 {: #button-repo} 

Bluemix에 배치 단추에서 사용할 프로젝트 저장소에 대한 고려사항을 검토하십시오. 

<ul>
<li><code>manifest.yml</code>은 저장소에 없어도 됩니다. 그러나 앱에서 다른 서비스를 실행해야 하는 경우 해당 서비스를 선언하는
Manifest 파일을 제공해야 합니다.  

Manifest 파일을 사용하여 다음을
지정할 수 있습니다. 
    <ul>
    <li>고유한 앱 이름</li>  
    <li>선언된 서비스: 앱 배치 전에 설정해야 하는 필수 또는 선택적 서비스(예: 데이터 캐시 서비스)를 작성하거나 찾는 Manifest 확장입니다. <a href="https://github.com/cloudfoundry/cli/releases">CF 명령행 인터페이스</a>를 사용하여 <code>cf marketplace</code> 명령을 실행하거나 <a href="https://console.ng.bluemix.net/?ssoLogout=true&cm_mmc=developerWorks-*-dWdevcenter-*-devops-services-_-lp#/store">{{site.data.keyword.Bluemix_notm}} 카탈로그</a>를 찾아보는 방식으로 적합한 {{site.data.keyword.Bluemix_notm}} 서비스, 레이블 및 플랜 목록을 찾을 수 있습니다.
    
    <strong>참고:</strong> 선언된 서비스는 표준 Cloud Foundry Manifest 형식의 IBM 확장입니다. 기능이 진화하고 향상되면 이후 릴리스에서
이 확장을 수정할 수 있습니다.
	
	<a href="http://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#minimal-manifest" target="_blank"><code>manifest.yml</code> 파일 작성 방법을 알아보십시오.</a>  
<pre class="codeblock">
	---
    #Template manifest.yml

  declared-services:
    &lt;`arbitrary_service_instance_name`&gt;:  # [required] 
      label: &lt;`actual_service_name`&gt; # [required] The actual service name from market place 
      plan: Shared # [optional] If provided, used to fetch the declared service. Otherwise, defaults to 'Free' or 'free'.
  applications:
  - services
    - &lt;`arbitrary_service_instance_name`&gt;
    name: &lt;`appname`&gt;
    host: &lt;`apphostname`&gt;
</pre>

<pre class="codeblock">
	---
    #Example manifest.yml

  declared-services: 
      sample-java-cloudant-cloudantNoSQLDB: 
        label: cloudantNoSQLDB 
        plan: Shared 
  applications:
  - services
    - sample-java-cloudant-cloudantNoSQLDB
    name: My app
    host: myapp
</pre>
   </li>
   </ul>
	<li> 앱이 배치되기 전에 저장소를 빌드해야 하는 경우 저장소에 있는 코드의 자동 빌드가
배치 전에 트리거됩니다. 빌드 스크립트 파일이 저장소의 루트 디렉토리에 있는 경우
자동 빌드가 수행됩니다. 
	
	지원되는 빌더는 다음과 같습니다. 
	    <ul>
		<li> <a href="http://ant.apache.org/manual/using.html" target="_blank">Ant:</a> /<code>build.xml</code> - 출력을 <code>./output/</code> 폴더에 빌드합니다. </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#gradle" target="_blank">Gradle:</a> <code>/build.gradle</code> - 출력을 <code>.</code> 폴더에 빌드합니다. </i>
		<li> <a href="http://gruntjs.com/getting-started#the-gruntfile" target="_blank">Grunt:</a> <code>/Gruntfile.js</code> - 출력을 <code>.</code> 폴더에 빌드합니다. </li>
		<li> <a href="http://docs.cloudfoundry.org/buildpacks/java/build-tool-int.html#maven" target="_blank">Maven:</a> <code>/pom.xml</code> - 출력을 <code>./target/</code> 폴더에 빌드합니다.</li>
	   </ul>
	</li>	
	<li>프로젝트의 파이프라인을 구성하려면 <code>.bluemix</code> 디렉토리에 <code>pipeline.yml</code> 파일을 포함시키십시오. <code>pipeline.yml</code> 파일을 수동으로 작성하거나 기존 DevOps Services 프로젝트에서 하나를 생성할 수 있습니다. {{site.data.keyword.jazzhub_short}} 프로젝트로부터 pipeline.yml 파일을 작성하고 이를 저장소에 추가하려면 다음 단계를 완료하십시오.
<ol>
<li>브라우저에서 DevOps Services 프로젝트를 열고 <b>빌드 및 배치</b>를 클릭하십시오.</li>
<li>빌드 및 배치 작업과 함께 파이프라인을 구성하십시오.</li>
<li>브라우저에서 <code>/yaml</code>을 프로젝트 파이프라인 URL에 추가하고 Enter를 누르십시오. 
<br>예: <code>https://hub.jazz.net/pipeline/<owner>/<project_name>/yaml</code></li>
<li>결과 <code>pipeline.yml</code> 파일을 저장하십시오.</li>
<li>프로젝트의 루트 디렉토리에서 <code>.bluemix</code> 디렉토리를 작성하십시오.</li>
<li><code>pipeline.yml</code> 파일을 <code>.bluemix</code> 저장소에 업로드하십시오.</li>
</ol> </li>
	<li><stong>IBM Containers</strong>를 사용하여 컨테이너에 앱을 배치하는 경우, 저장소의 루트 디렉토리에 Dockerfile을 포함시키고 <code>.bluemix</code> 디렉토리에 <code>pipeline.yml</code> 파일을 포함시켜야 합니다.
	<ul>
	    <li> Dockerfile 작성에 대해 자세히 알아보려면 <a href="https://docs.docker.com/reference/builder/" target="_blank">Docker 문서를 참조</a>하십시오.</li>
	    <li><code>pipeline.yml</code> 파일을 수동으로 작성하거나 기존 DevOps Services 프로젝트에서 하나를 생성할 수 있습니다. 특히 컨테이너에 대한 <code>pipeline.yml</code>을 수동으로 작성하려면 <a href="https://github.com/Puquios/" target="_blank">GitHub의 예를 참조</a>하십시오.</li>
        </ul>

 </li>
 </ul>
</ul>

문제점 해결 도움말은
[Bluemix에
배치 단추로 앱이 배치되지 않는 경우](../troubleshoot/index.html#deploytobluemixbuttondoesntdeployanapp){:new_window}를 참조하십시오.	
