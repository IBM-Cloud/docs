---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-23"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# GitHub 패키지 사용
{: #openwhisk_catalog_github}

`/whisk.system/github` 패키지는 [GitHub API](https://developer.github.com/)를 사용하는 편리한 방법을 제공합니다.

패키지에는 다음 피드가 포함됩니다.

| 엔티티 | 유형 | 매개변수 | 설명 |
| --- | --- | --- | --- |
| `/whisk.system/github` | 패키지 | username, repository, accessToken | GitHub API와 상호작용 |
| `/whisk.system/github/webhook` | 피드 | events, username, repository, accessToken | GitHub 활동 시 트리거 이벤트 실행 |

`username`, `repository`, `accessToken` 값을 사용하여 패키지 바인딩을 작성하도록 권장합니다. 바인딩을 사용하면, 패키지에서 피드를 사용할 때마다 값을 지정할 필요가 없습니다.

## GitHub 활동과 함께 트리거 이벤트 실행

`/whisk.system/github/webhook` 피드는 지정된 GitHub 저장소에 활동이 있을 때 트리거를 실행하는 서비스를 구성합니다. 매개변수는 다음과 같습니다.

- `username`: GitHub 저장소의 사용자 이름입니다. 
- `repository`: GitHub 저장소입니다.
- `accessToken`: GitHub 개인 액세스 토큰입니다. [토큰을 작성](https://github.com/settings/tokens)할 때, repo:status 및 public_repo 범위를 선택하십시오. 또한 저장소에 이미 정의된 웹훅이 없는지 확인하십시오. 
- `events`: 관심 있는 [GitHub 이벤트 유형](https://developer.github.com/v3/activity/events/types/)입니다.

다음은 GitHub 저장소에 대한 새 커미트가 있을 때마다 실행될 트리거를 작성하는 예입니다.

1. GitHub [개인 액세스 토큰](https://github.com/settings/tokens)을 생성하십시오.
  
  액세스 토큰은 다음 단계에서 사용됩니다.
  
2. 액세스 토큰을 사용하여 GitHub 저장소에 대해 구성된 패키지 바인딩을 작성하십시오. 
  
  ```
  wsk package bind /whisk.system/github myGit \
    --param username myGitUser \
    --param repository myGitRepo \
    --param accessToken aaaaa1111a1a1a1a1a111111aaaaaa1111aa1a1a
  ```
  {: pre}
  
3. `myGit/webhook` 피드를 사용하여 GitHub `push` 이벤트 유형에 사용할 트리거를 작성하십시오. 
  
  ```
  wsk trigger create myGitTrigger --feed myGit/webhook --param events push
  ```
  {: pre}
  
  `git push`를 사용하여 GitHub 저장소에 커미트하면 웹훅에서 트리거를 실행합니다. 트리거와 일치하는 규칙이 있는 경우 연관된 조치가 호출됩니다.
조치는 GitHub 웹훅 페이로드를 입력 매개변수로 받습니다. 각 GitHub 웹훅 이벤트에는 비슷한 JSON 스키마가 있지만 각 이벤트는 해당 이벤트 유형으로 판별되는 고유 페이로드 오브젝트입니다.
페이로드 컨텐츠에 대한 자세한 정보는 [GitHub 이벤트 및 페이로드](https://developer.github.com/v3/activity/events/types/) API 문서를 참조하십시오. 
  
