---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# 사용자 관리 {: #manage-users}

팁 협업을 위해 디자인된 {{site.data.keyword.iotrtinsights_short}}는 관리자가 더 많은 사용자를 추가하여 {{site.data.keyword.iotrtinsights_short}} 콘솔에 액세스할 수 있도록 합니다.
{: shortdesc}

역할 설명:
- 운영자
운영자는 직접 {{site.data.keyword.iotrtinsights_short}} 콘솔에 로그인하여 디바이스와 디바이스 그룹의 실시간 데이터 플로우를 모니터합니다. 운영자는 또한 규칙을 활성화 및 비활성화하고 편집 가능한 대시보드를 수정할 수 있습니다.  
- 관리자
운영자가 수행할 수 있는 태스크에 추가로, 관리자는 사용자를 추가, 대시보드 레이아웃을 관리, 데이터 소스를 추가, 디바이스 유형을 관리할 수 있습니다.   
- 소유자
소유자 역할은 Bluemix에서 {{site.data.keyword.iotrtinsights_short}} 서비스 인스턴스를 배치한 IBM ID에 지정됩니다. 소유자는 관리자와 동일한 권한을 갖지만 삭제될 수 없습니다. 

새 사용자를 추가하려면 다음을 수행하십시오.
1. {{site.data.keyword.iot_short}}에 사용자를 추가하십시오.   
>**중요:** 관리자 역할이 있는 사용자를 추가하는 경우, 해당 사용자를 {{site.data.keyword.iot_short}}에도 추가해야 합니다.  

  1. {{site.data.keyword.iotrtinsights_short}} 서비스에 대한 데이터 소스인 {{site.data.keyword.iot_short}} 서비스의 대시보드에 로그인하십시오.   
  2. **액세스 > 구성원**으로 이동하여 **구성원 추가**를 클릭하십시오.
  3. 추가하려는 사용자의 IBM ID를 입력하고 **구성원 추가**를 클릭하십시오. 
2. {{site.data.keyword.iotrtinsights_short}}에 사용자를 추가하십시오. 
  1. 관리자 역할 또는 소유자 역할이 있는 사용자로 {{site.data.keyword.iotrtinsights_short}} 콘솔에 로그인하십시오.
  2. **설정 > 사용자 관리**로 이동하십시오. 
  3. **새 사용자 추가**를 클릭하십시오.
  4. 초대하려는 사용자의 이메일 주소를 입력하고 사용자의 역할을 선택한 다음 ![작성 아이콘](images/create.png "작성 아이콘")을 클릭하십시오.
웹 콘솔 링크를 포함하는 이메일이 사용자에게 전송됩니다. 이메일 주소가 이미 IBM ID와 연관되어 있으면 사용자가 직접 콘솔에 로그인하여 액세스할 수 있습니다. 그렇지 않으면 콘솔에 액세스하기 전에 무료 IBM ID를 작성하도록 프롬프트가 표시됩니다.  
>**Real-Time Insights 인스턴스 선택:** 운영자 또는 관리자로 복수의 Real-Time Insights 인스턴스에 대한 액세스 권한을 갖는 사용자는 이러한 인스턴스 사이를 빠르게 전환할 수 있습니다. Real-Time Insights 콘솔에서 사용자 이름을 클릭하여 액세스하려는 인스턴스를 선택할 수 있습니다.   
