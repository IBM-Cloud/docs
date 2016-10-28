---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# {{site.data.keyword.Bluemix_notm}} 퍼블릭에서 도구 체인 사용
{: #toolchains-using}

*마지막 업데이트 날짜: 2016년 8월 12일*
{: .last-updated}

도구 체인을 사용하여 일상적인 개발, 배치 및 및 운영 작업의 생산성을 향상시킬 수 있습니다. 도구 체인을 설정한 후에는 도구 통합을 추가, 삭제 또는 구성하거나 도구 체인에 대한 액세스를 관리할 수 있습니다.
{: shortdesc}

**중요**: 이 기능은 시범 서비스입니다. 도구 체인은 안정적이지 않을 수 있으며 이전 버전과 호환되지 않는 방식으로 변경될 수 있습니다. 프로덕션 환경에서는 도구 체인을 사용하지 않는 것이 좋습니다. 도구 체인은 미국 남부 지역에서만 사용 가능합니다. 

## 도구 통합 구성
{: #configuring_a_tool_integration}

도구 체인을 작성할 때 도구 통합 구성을 연기한 경우 해당 타일에 **구성** 단추가 표시됩니다. 도구 체인을 작성할 때 도구 통합을 구성한 경우에는 구성 설정을 업데이트할 수 있습니다. 

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱의 개요 페이지에 있는 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 후 **도구 통합**을 클릭하십시오. 
1. 처음 도구 통합을 구성하는 경우, 해당 타일에서 **구성**을 클릭하십시오. 

  ![구성 단추](images/toolchain_tile_configure.png)

 도구 통합 구성을 완료했으면 **통합 저장**을 클릭하십시오. 
 
1. 도구 통합의 구성을 업데이트해야 하는 경우, 해당 타일에서 메뉴를 클릭하여 구성 옵션에 액세스하십시오. 

  ![구성 메뉴](images/toolchain_tile_menu.png)
 
 설정 업데이트를 완료했으면 **통합 저장**을 클릭하십시오. 

## 도구 통합 추가
{: #adding_a_tool_integration}

도구 체인에 도구 통합을 추가하고 적합하게 구성할 수 있습니다. 

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱의 개요 페이지에 있는 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 후 **도구 통합**을 클릭하십시오. 
1. 추가할 도구 통합 목록을 보려면 추가 단추(+)를 클릭하십시오. 
1. 추가할 도구 통합을 클릭하십시오. 
1. 도구 통합을 구성하는 데 필요한 정보를 입력하십시오.  
1. **통합 작성**을 클릭하여 도구 체인에 도구 통합을 추가하십시오. 

## 도구 통합 삭제
{: #deleting_a_tool_integration}

도구 체인에서 도구 통합을 삭제하는 경우 삭제를 실행 취소할 수 없습니다.  

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 해당 도구 통합 페이지를 여십시오. 또는 앱의 개요 페이지에 있는 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 후 **도구 통합**을 클릭하십시오. 
1. 삭제할 도구 통합의 타일에서 메뉴를 클릭하여 구성 옵션에 액세스하십시오. 
1. 도구 체인에서 도구 통합을 삭제하려면 **삭제**를 클릭하십시오. 
1. **삭제**를 클릭하여 확인하십시오.   

## 액세스 관리
{: #managing_access}

도구 체인이 연관된 조직에 사용자를 추가하여 사용자에게 도구 체인에 대한 액세스 권한을 부여할 수 있습니다. 각 도구 체인은 특정 조직과 연관되어 있으며 해당 조직의 구성원인 사용자는 누구나 연관된 도구 체인에 액세스할 수 있습니다. 메뉴 표시줄에서 **{{site.data.keyword.avatar}}** 아이콘 ![아바타 아이콘](../icons/i-avatar-icon.svg)을 클릭하여 계정 및 지원 위젯을 열고 현재 작업 중인 조직을 보십시오. 다른 도구 체인 세트에 액세스하려면 다른 조직으로 전환하십시오. 

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. DevOps 대시보드의 **도구 체인** 탭에서 관리할 도구 체인을 클릭한 후 **관리**를 클릭하십시오. 또는 앱의 개요 페이지에 있는 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 후 **관리**를 클릭하십시오.   
1. 조직에 대한 링크를 클릭하십시오.  
1. 조직 관리 페이지에서 **사용자 초대**를 클릭하고 사용자의 이메일 주소를 입력하십시오. 
1. {{site.data.keyword.Bluemix_notm}} 조직에서 사용자를 관리할 수 있는 고급 권한을 부여하려면 **관리자**, **청구 관리자** 및 **감사자** 선택란 중 하나 이상을 선택하십시오. 
1. **초대**를 클릭하십시오. 
1. **저장**을 클릭하십시오. 

## 도구 체인 삭제
{: #deleting_a_toolchain}

도구 체인을 삭제할 수 있으며 삭제할 연관된 도구 통합을 지정할 수 있습니다. 도구 체인을 삭제하는 경우 삭제를 실행 취소할 수 없습니다. 

1. DevOps 대시보드의 **도구 체인** 탭에서 삭제할 도구 체인을 클릭한 후 **관리**를 클릭하십시오. 또는 앱의 개요 페이지에 있는 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 후 **관리**를 클릭하십시오. 
1. **도구 체인 삭제**를 클릭하고 삭제할 도구 통합을 검토하거나 조정하십시오. 
1. 도구 체인의 이름을 입력하고 **삭제**를 클릭하여 삭제를 확인하십시오.   

 **팁**: GitHub 도구 통합을 삭제할 때 연관된 GitHub 저장소는 GitHub에서 삭제되지 않습니다. GitHub에서 저장소를 수동으로 제거해야 합니다. 
