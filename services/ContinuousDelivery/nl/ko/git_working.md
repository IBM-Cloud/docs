---

copyright:
  years: 2015, 2017
lastupdated: "2017-4-11"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Git Repos and Issue Tracking 관련 작업(시범)
{: #git_working}

IBM에서 호스팅하고 [GitLab Community Edition ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://about.gitlab.com/){:new_window}에서 빌드된 Git 저장소(repo) 및 문제 트래커를 사용하여 사용자의 팀과 협업하고 소스 코드를 관리합니다.
{: shortdesc}

Git Repos and Issue Tracking 도구 통합은 코드를 관리하고 다양한 방법으로 협업할 수 있도록 팀을 지원합니다. 
   * 코드의 보안을 유지하는 미세 조정된 액세스 제어를 통해 Git 저장소를 관리함
   * 코드를 검토하고 병합 요청을 통해 협업을 개선함
   * 문제 트래커를 통해 문제를 추적하고 아이디어를 공유함
   * 위키 시스템에서 프로젝트를 문서화함

**참고:** 이 도구 통합이 GitLab Community Edition에서 빌드되며 Bluemix에서 IBM에 의해 호스팅되므로 일부 GitLab 옵션은 사용이 불가능합니다. 예를 들어, Delivery Pipeline이 Bluemix에 대해 지속적 통합 및 지속적 딜리버리를 제공하므로 GitLab의 지속적 통합 기능은 지원되지 않습니다. 또한 IBM에서 관리하므로 관리자 기능은 사용할 수 없습니다. 

## 파일 및 저장소 크기 한계
{: #git_limits}

파일 크기는 100MB로 엄격히 제한됩니다. 권장되는 저장소 크기 한계는 1GB입니다. 저장소가 1GB를 초과하면 저장소 크기를 줄여달라는 요청 이메일을 받을 수 있습니다. 

## 인증을 위한 개인 액세스 토큰 또는 SSH 키 작성    
{: #git_authentication}

`clone` 또는 `push` 등의 원격 Git 조작을 완료하려면, 로컬 Git 저장소에서 개인 액세스 토큰 또는 SSH 키를 사용하여 GitLab을 인증해야 합니다. 

* 개인 액세스 토큰을 설정하려면 [Personal Access Tokens ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}을 참조하십시오. 
* SSH 키를 설정하려면 [SSH ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/help/ssh/README){:new_window} 또는 [How to create your SSH Keys ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}을 참조하십시오. SSH 인증으로 저장소에 액세스하려면 프록시 및 방화벽에 대한 추가 구성이 필요할 수 있습니다. 

**참고:** 인증에 개인 액세스 토큰 또는 SSH 키를 사용하려면 로컬로 Git를 설정해야 합니다. 지시사항은 [Start using Git on the command line ![외부 링크 아이콘](../../icons/launch-glyph.svg "외부 링크 아이콘")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}을 참조하십시오. 
