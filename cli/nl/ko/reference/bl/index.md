# bl 명령

*마지막 업데이트 날짜:* 2015년 11월 13일

Node.js 애플리케이션을 빌드하는 경우 Bluemix™ Live Sync를 사용하여 재배치 없이 데스크탑에서처럼 Bluemix에서 실행되는 애플리케이션 인스턴스를 신속하게 업데이트하고 개발할 수 있습니다. 변경할 경우 실행 중인 Bluemix 애플리케이션에서 변경사항을 즉시 확인할 수 있습니다. Bluemix Live Sync 명령행 인터페이스를 *bl*이라고 합니다.

**bl** 명령행 인터페이스 명령을 사용하여 다음과 같은 태스크를
완료할 수 있습니다. 

* Bluemix에서 실행 중인 애플리케이션을 시작하고 중지합니다.
* 데스크탑에서 새 클라우드 기반 프로젝트를 작성합니다.
* 데스크탑의 변경사항을 클라우드 기반 프로젝트 작업공간과 Bluemix에서 실행되는 애플리케이션에 동기화합니다.
* 동기화할 수 있는 프로젝트 목록을 확인합니다.
* 실행 중인 애플리케이션의 상태를 확인합니다.

bl 명령 다운로드 및 사용에 대한 자세한 정보는 [Bluemix Live Sync](https://www.ng.bluemix.net/docs/manageapps/bluemixlive.html#bluemixlive)를 참조하십시오.

## bl 명령

Bluemix Live Sync 명령행인 **bl**은 다음과 같은 구문을 사용합니다. 

``` bl command [arguments][options] [--help]```

### 명령
<dl>
<dt>login, l</dt>
<dd>Bluemix에 로그인합니다.</dd>
<dt>logout, lo</dt>
<dd>사용자가 로그아웃됩니다. </dd>
<dt>sync, s</dt>
<dd>데스크탑과 서버 간 동기화 프로세스를 시작합니다. </dd>
<dt>create, c</dt>
<dd>개인용 프로젝트를 작성하여 이 디렉토리의 Git repo에 링크한 다음 컨텐츠를 Bluemix에 배치합니다.</dd>
<dt>projects, p</dt>
<dd>동기화할 수 있는 모든 프로젝트를 나열합니다. </dd>
<dt>start, st</dt>
<dd>Bluemix에서 애플리케이션 인스턴스를 시작합니다.</dd>
<dt>stop, sp</dt>
<dd>Bluemix에서 애플리케이션 인스턴스를 중지합니다.</dd>
<dt>status, ss</dt>
<dd>Bluemix에서 실행 중인 애플리케이션 인스턴스의 상태 목록을 표시합니다.</dd>
</dl>

### 인수
<dl>
<dd>명령에 대한 인수입니다. </dd>
</dl>

### 옵션
<dl>
<dd>명령에 대한 옵션입니다. </dd>
</dl>

### 글로벌 옵션
<dl>
<dt>--help</dt>
<dd>지정된 명령의 도움말 페이지를 표시합니다. </dd>
<dt>--verbose</dt>
<dd>상세 로깅을 설정합니다. </dd>
</dl>

**참고:** 인수 또는 옵션에 공백이 포함되어 있으면 값을 큰따옴표로 묶으십시오.
