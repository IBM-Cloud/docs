---

copyright:
  years: 2016

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# 도구 체인 사용
{: #toolchains-using}

*마지막 업데이트 날짜: 2016년 5월 4일*
{: .last-updated}

매일의 개발, 배치 및 운영 작업이 생산적이도록 도구 체인을 사용할 수 있습니다. 도구 체인을 설정하고 나면 도구 통합을 추가, 삭제 또는 구성하고 도구 체인에 대한 액세스를 관리할 수 있습니다.
{: shortdesc}

**중요**: 이 기능은 실험적으로 사용됩니다. 도구 체인이 안정적이지 않거나 이전 버전과 호환되지 않는 방식으로 변경될 수 있습니다. 프로덕션 환경에서는 사용하지 않는 것이 좋습니다. 도구 체인을 사용하려면 일회성 [액세스 요청](https://new-console.ng.bluemix.net/devops?cm_mmc=IBMBluemixGarageMethod-_-MethodSite-_-10-19-15::12-31-18-_-toolchains-welcome-page){: new_window}을 수행해야 합니다. 도구 체인은 미국 남부 지역에서만 사용할 수 있습니다.

## 도구 통합 구성
{: #configuring_a_tool_integration}

도구 통합을 처음으로 구성하거나 이미 도구 체인의 일부인 도구 통합의 구성 설정을 업데이트할 수 있습니다.

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **도구 통합**을 클릭하십시오.
1. 도구 통합을 처음으로 구성해야 하는 경우 해당 타일에서 **구성**을 클릭하십시오.

  ![구성 버튼](images/toolchain_tile_configure.png)

 도구 통합 구성을 완료하면 **통합 저장**을 클릭하십시오.
 
1. 도구 통합 구성을 업데이트해야 하는 경우 해당 타일에서 메뉴를 클릭하여 구성 옵션에 액세스하십시오.

  ![구성 메뉴](images/toolchain_tile_menu.png)
 
 설정 업데이트를 완료하고 나면 **통합 저장**을 클릭하십시오.

 **참고**: GitHub 도구 통합의 저장소를 구성하고 나면 저장소의 url을 업데이트할 수 있지만, 저장소 자체는 변경할 수 없습니다. 다른 저장소를 사용하려면 도구 체인에서 현재 GitHub 도구 통합을 삭제하고 GitHub 도구 통합을 도구 체인에 추가한 다음 새 저장소를 사용하도록 해당 도구 통합을 구성하십시오.

## 도구 통합 추가
{: #adding_a_tool_integration}

도구 체인의 도구 통합을 추가하고 구성할 수 있습니다.

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **도구 통합**을 클릭하십시오.
1. 추가할 도구 통합 목록을 보려면 추가 버튼(+)을 클릭하십시오.
1. 추가할 도구 통합을 클릭하십시오.
1. 도구 통합을 구성하는 데 필요한 정보를 입력하십시오. 
1. **통합 작성**을 클릭하여 도구 체인에 도구 통합을 추가하십시오.

## 도구 통합 삭제
{: #deleting_a_tool_integration}

도구 체인에서 도구 통합을 삭제할 수 있습니다. 

1. DevOps 대시보드의 **도구 체인** 탭에서 도구 체인을 클릭하여 도구 통합 페이지를 여십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **도구 통합**을 클릭하십시오.
1. 삭제할 도구 통합 타일에서 메뉴를 클릭하여 구성 옵션에 액세스하십시오.
1. 도구 체인에서 도구 통합을 삭제하려면 **삭제**를 클릭하십시오.
1. **삭제**를 클릭하여 확인하십시오.

## 액세스 관리
{: #managing_access}

도구 체인이 연관된 조직(org)에 추가하여 사용자에게 도구 체인에 대한 액세스 권한을 부여할 수 있습니다. 각 도구 체인은 특정 조직과 연관되며 해당 조직의 구성원인 사용자가 연관된 도구 체인에 액세스할 수 있습니다. 다른 조직으로 전환하면 다른 도구 체인 세트에 액세스할 수 있습니다.

<!--CA: Commenting out the content on authentication for Interconnect since it applies to GitHub Enterprise. This content can be exposed again when GHE is supported for the Dedicated Beta 2.-->

<!--You have three authentication options for your Bluemix dedicated environment: LDAP, SAML, or Web ID. 

**Important:** For this beta, Web ID authentication requires additional user management on GitHub Enterprise.

If you use LDAP or SAML authentication in your Bluemix dedicated environment, when you add users to your Bluemix org and spaces, the users can log in to GitHub Enterprise by using their Bluemix ID and password, and accounts are created for them. When you add users to your Bluemix org and spaces, they are not automatically added to the GitHub Enterprise repo. Someone who has admin privileges for the repo must add them.  

If you use Web ID authentication, when you add users to your Bluemix org and spaces, a GitHub Enterprise site administrator must set up a GitHub Enterprise account for those users. Alternatively, new users can create a toolchain, in which case a GitHub Enterprise account is created for them. However, if those users want to access repos that are associated with toolchains besides their own, they must be granted access to those repos.

To add a user: -->

1. DevOps 대시보드의 **도구 체인** 탭에서 관리할 도구 체인을 클릭한 다음 **관리**를 클릭하십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **관리**를 클릭하십시오.  
1. 조직의 링크를 클릭하십시오. 
1. 조직 관리 페이지에서 **사용자 초대**를 클릭하고 사용자 이메일 주소를 입력하십시오.
1. 사용자에게 고급 권한을 제공하려면 하나 이상의 **관리자**, **비용 청구 관리자** 또는 **감사자** 선택란을 선택하십시오. 
1. **초대**를 클릭하십시오.
1. **저장**을 클릭하십시오. 

## 도구 체인 삭제
{: #deleting_a_toolchain}

도구 체인을 삭제하고 삭제할 연관된 도구 통합을 지정할 수 있습니다.

1. DevOps 대시보드의 **도구 체인** 탭에서 삭제할 도구 체인을 클릭한 다음 **관리**를 클릭하십시오. 또는 앱 개요 페이지의 Continuous Delivery 타일에서 **도구 체인 보기**를 클릭한 다음 **관리**를 클릭하십시오.
1. **도구 체인 삭제**를 클릭하고 삭제할 도구 통합을 검토하십시오.
1. 도구 체인의 이름을 입력하고 **삭제**를 클릭하여 삭제를 확인하십시오.

 **팁**: GitHub 도구 통합을 삭제해도 연관된 GitHub 저장소는 GitHub에서 삭제되지 않습니다. GitHub에서 수동으로 저장소를 제거해야 합니다.
