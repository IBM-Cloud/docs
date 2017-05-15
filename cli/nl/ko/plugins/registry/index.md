---



copyright:

  years: 2017

lastupdated: "2017-04-07"


---

{:codeblock: .codeblock}
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.registrylong_notm}} CLI
{: #containerregcli}

{{site.data.keyword.registrylong}} CLI는 조직 전체에서 네임스페이스와 이미지 등의 레지스트리 리소스를 관리할 수 있는 플러그인입니다.
{: shortdesc}

** 필수 소프트웨어**
* 레지스트리 명령을 실행하기 전에 `bx login` 명령으로
 {{site.data.keyword.Bluemix_short}}에 로그인하여 {{site.data.keyword.Bluemix_short}}
 액세스 토큰을 생성하고 세션을 인증하십시오.

<table summary="컨테이너 레지스트리 관리">
<caption>표 1. {{site.data.keyword.Bluemix_short}}의 {{site.data.keyword.registryshort}}를 관리하기 위한 명령
</caption>
 <thead>
 <th colspan="5">레지스트리 관리 명령</th>
 </thead>
 <tbody>
 <tr>
 <td>[bx cr api](#bx-cr-api)</td>
 <td>[bx cr info](#bx-cr-info)</td>
 <td>[bx cr image-inspect](#bx-cr-image-inspect)</td>
 <td>[bx cr image-list](#bx-cr-image-list)</td>
 <td>[bx cr image-rm](#bx-cr-image-rm)</td>
 </tr>
 <tr>
 <td>[bx cr login](#bx-cr-login)</td>
 <td>[bx cr namespace-add](#bx-cr-namespace-add)</td>
 <td>[bx cr namespace-list](#bx-cr-namespace-list)</td>
 <td>[bx cr namespace-rm](#bx-cr-namespace-rm)</td>
 </tr></tbody></table>


## bx cr api
명령을 실행할 레지스트리 API 엔드포인트에 대한 세부사항을 리턴합니다.

```
bx cr api
```
{: codeblock}


## bx cr info
로그인된 레지스트리의 이름과 조직을 표시합니다.

```
bx cr info
```
{: codeblock}


## bx cr image-inspect
특정 이미지에 대한 세부사항을 봅니다.

```
bx cr image-inspect [--format FORMAT] IMAGE [IMAGE]
```
{: codeblock}

**매개변수**
<dl>
<dt>--format FORMAT</dt>
<dd>(선택사항) Go 템플리트를 사용하여 출력 요소를 형식화합니다.</dd>
<dt>IMAGE</dt>
<dd>검사할 이미지에 대한 전체 {{site.data.keyword.Bluemix_short}} 레지스트리 경로이며, 형식은 namespace/image:tag입니다. 이미지 경로에 태그가 지정되지 않은 경우 `latest` 태그가 지정된 이미지를 검사합니다. 각 경로를 공백으로 구분하여 명령에 각 개인용 {{site.data.keyword.Bluemix_short}} 레지스트리 경로를 나열하여 여러 이미지를 검사할 수 있습니다. </dd>
</dl>


## bx cr image-list
{{site.data.keyword.Bluemix_short}} 조직의 모든 이미지를 표시합니다.

```
 bx cr image-list [--no-trunc] [-q, --quiet] [--include-ibm] [--format FORMAT]
```
{: codeblock}

**매개변수**
<dl>
<dt>--no-trunc</dt>
<dd>(선택사항) 출력을 자르지 않습니다.</dd>
<dt>-q, --quiet</dt>
<dd>(선택사항) 'repository:tag' 형식으로 이미지의 고유 ID를 표시합니다.</dd>
<dt>--include-ibm</dt>
<dd>(선택사항) 출력에 IBM 제공 공용 이미지를 포함합니다. 이 옵션을 사용하지 않으면 개인용 이미지만 표시됩니다.</dd>
<dt>--format FORMAT</dt>
<dd>(선택사항) Go 템플리트를 사용하여 출력 요소를 형식화합니다.</dd>
</dl>


## bx cr image-rm
레지스트리에서 지정된 이미지를 삭제합니다.

```
bx cr image-rm IMAGE [IMAGE]
```
{: codeblock}

**매개변수**
<dl>
<dt>IMAGE</dt>
<dd>제거할 이미지에 대한 전체 {{site.data.keyword.Bluemix_short}} 레지스트리 경로이며, 형식은 namespace/image:tag입니다. 이미지 경로에 태그가 지정되지 않은 경우 `latest` 태그가 지정된 이미지가 기본적으로 삭제됩니다. 각 경로를 공백으로 구분하여 명령에 각 개인용 {{site.data.keyword.Bluemix_short}} 레지스트리 경로를 나열하여 여러 이미지를 삭제할 수 있습니다. </dd>
</dl>


## bx cr login
Docker가 설치되어 있는 경우 이 명령은 레지스트리에 대해 `docker login` 명령을 실행합니다. 레지스트리에 대해 `docker push` 또는 `docker pull` 명령을 실행할 수 있으려면 `docker login` 명령이 필요합니다. 이 명령은 다른 `bx cr` 명령을 실행하는 데 필요하지 않습니다. Docker가 설치되지 않은 경우 이 명령은 오류 메시지를 리턴합니다.

```
bx cr login
```
{: codeblock}


## bx cr namespace-add
Bluemix 조직에 네임스페이스를 추가합니다. 

```
bx cr namespace-add NAMESPACE
```
{: codeblock}

**매개변수**
<dl>
<dt>NAMESPACE</dt>
<dd>추가하려는 네임스페이스입니다. 네임스페이스는 모든 {{site.data.keyword.Bluemix_short}} 조직에서 고유해야 합니다.</dd>
</dl>


## bx cr namespace-list
{{site.data.keyword.Bluemix_short}} 조직의 모든 네임스페이스를 표시합니다.

```
bx cr namespace-list
```
{: codeblock}


## bx cr namespace-rm
{{site.data.keyword.Bluemix_short}} 조직에서 네임스페이스를 제거합니다. 이 네임스페이스의 이미지는 네임스페이스를 제거하면 삭제됩니다.

```
bx cr namespace-rm NAMESPACE
```
{: codeblock}

**매개변수**
<dl>
<dt>NAMESPACE</dt>
<dd>제거하려는 네임스페이스입니다. </dd>
</dl>
