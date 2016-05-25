---

 

copyright:

  years: 2016

 

---

{:shortdesc: .shortdesc}

#  Bluemix 인프라 계층

*마지막 업데이트 날짜: 2016년 3월 15일*

{{site.data.keyword.Bluemix_notm}}는 관리할 필요가 없도록 운영 체제 및 인프라 계층을 추상화하고 숨깁니다. 그러나 때때로 사용자 앱의 운영 체제와 미들웨어에 대한 정보가 필요할 수 있습니다.
{:shortdesc}

## Bluemix 인프라 계층 보기
{:viewinfra}

cf stacks 명령을 실행하여 앱을 배치할 사용 가능한 스택 또는 루트 파일 시스템을 표시할 수 있습니다. cf push 명령에 *-s* 옵션과 *stack_name*을 사용하여 스택을 지정할 수도 있습니다. 여기서 stack_name은 루트 파일 시스템(예: `lucid64` 또는 `cflinuxfs2`)입니다.
```
cf push appName -s stack_name
```
`cf buildpacks` 명령을 사용하여 앱을 실행할 런타임으로 사용 가능한 미들웨어 컴포넌트(예: WebSphere Liberty 프로파일 및 SDK for Node.js)를 표시할 수 있습니다. 또한 다음 명령을 사용하여 앱의 런타임 환경을 지정할 수 있습니다.
```
cf push appName -b buildpackname
```
