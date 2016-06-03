---

 

copyright:

  years: 2015，2016

 

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# 커뮤니티 빌드팩 사용
*마지막 업데이트 날짜: 2016년 3월 15일*

원하는 런타임을 제공하는 스타터가 {{site.data.keyword.Bluemix}} 카탈로그에 없는 경우, 외부 빌드팩을 {{site.data.keyword.Bluemix_notm}}로 가져올 수 있습니다. cf push 명령을 사용하여 앱을 배치하는 경우, 사용자 정의 Cloud Foundry 호환 가능 빌드팩을 지정할 수 있습니다.
{:shortdesc}

사용자 자신의 빌드팩으로 사용할 수 있도록 Cloud Foundry 커뮤니티에서 외부 빌드팩을 제공합니다. {{site.data.keyword.Bluemix_notm}}에 앱을 배치하기 전에 cf 명령행 인터페이스를 설치했는지 확인하십시오.

**참고:** 외부 빌드팩은 IBM에서 제공하지 않으므로 Cloud Foundry 커뮤니티에 지원을 요청해야 합니다.

## 기본 제공 커뮤니티 빌드팩

{{site.data.keyword.Bluemix_notm}}에서는 Cloud Foundry 커뮤니티에서 제공하는 기본 제공 빌드팩을 사용할 수 있습니다. 기본 제공 커뮤니티 빌드팩을 표시하려면 cf buildpacks 명령을 실행하십시오.

```
cf buildpacks
Getting buildpacks...

buildpack      position   enabled   locked   filename
...
java_buildpack     7      true      false    buildpack_java_v2.0.2.zip
ruby_buildpack     8      true      false    buildpack_ruby_v46-245-g2fc4ad8.zip
nodejs_buildpack   9      true      false    buildpack_nodejs_v8-177-g2b0a5cf.zip
```
{:screen}

<ul>

<li>
동일한 런타임 또는 프레임워크의 경우, IBM에서 작성된 빌드팩이 커뮤니티 빌드팩에 우선합니다. 커뮤니티 빌드팩으로 IBM에서 작성된 빌드팩을 겹쳐쓰려면 cf push 명령과 함께 -b 옵션을 사용하여 빌드팩을 지정해야 합니다.
<p>예를 들어, Java™ 웹 앱에 대해 커뮤니티 빌드팩을 사용할 수 있습니다.</p>
<pre class="pre"><code>cf push app_name -b java_buildpack -p app_path</code></pre>
<p>또한 Node.js 앱에 대해서도 커뮤니티 빌드팩을 사용할 수 있습니다.</p>
<pre class="pre"><code>cf push app_name -b nodejs_buildpack -p app_path</code></pre>
</li>

<li>
<p>IBM에서 작성된 빌드팩에서는 지원되지 않으나 기본 제공 커뮤니티 빌드팩에서는 지원되는 런타임 또는 프레임워크의 경우, cf push 명령과 함께 -b 옵션을 사용할 필요가 없습니다.</p><p>예를 들어, Ruby 앱의 경우 IBM에서 작성된 빌드팩이 없습니다. 다음 명령을 입력하여 기본 제공 커뮤니티 빌드팩을 사용할 수 있습니다.</p>
<pre class="pre"><code>cf push app_name -p app_path</code></pre>
</li>
</ul>

## 외부 빌드팩

{{site.data.keyword.Bluemix_notm}}에서는 외부 빌드팩 또는 사용자 정의 빌드팩을 사용할 수 있습니다. **cf push** 명령에서 -b 옵션을 사용하여 빌드팩의 URL을 지정하고 ```-s``` 옵션을 사용하여 스택을 지정하십시오. 예를 들어, 정적 파일에 대한 외부 커뮤니티 빌드팩을 사용하려면 다음 명령을 실행하십시오.

```
cf push app_name -p app_path -b https://github.com/cloudfoundry-incubator/staticfile-buildpack.git -s cflinuxfs2
```
{:pre}

또 다른 예로, 기본 제공 커뮤니티 빌드팩을 Ruby 앱에 사용하지 않으려는 경우 다음 명령을 입력하여 외부 빌드팩을 사용할 수 있습니다.

```
cf push app_name -p app_path -b https://github.com/cloudfoundry/heroku-buildpack-ruby -s cflinuxfs2
```
{:pre}

자신의 애플리케이션에 사용자 정의 빌드팩을 사용할 수도 있습니다. 예를 들어, Cloud Foundry 커뮤니티에서 제공하는 오픈 소스 PHP 빌드팩을 사용하려면 Bluemix에 PHP 앱을 배치할 때 다음 명령을 입력하여 빌드팩의 Git 저장소 URL을 지정하십시오.

```
cf push app_name -p app_path -b https://github.com/dmikusa-pivotal/cf-php-build-pack -s cflinuxfs2
```
{:pre}

## Java 빌드팩 버전 지정

<ul>
<li>
<strong>cf set-env</strong> 명령을 사용하십시오. 예를 들어 다음 명령을 입력하여 Java 버전을 1.7.0으로 설정하십시오.
<pre class="pre"><code>cf set-env app_name JBP_CONFIG_OPEN_JDK_JRE &#39;{jre: { version: 1.7.0_+ }}&#39;</code></pre>
<p>그런 다음 앱을 다시 스테이징하여 변경사항을 적용하십시오.</p>
<pre class="pre"><code>cf restage app_name</code></pre>
</li>
<li>
<code>manifest.yml</code> 파일을 사용하십시오. 파일에 직접 지정할 환경 변수와 값을 추가할 수 있습니다. 자세한 정보는 <a href="https://docs.cloudfoundry.org/devguide/deploy-apps/manifest.html#env-block">환경 변수</a>를 참조하십시오.</li></ul>
  

