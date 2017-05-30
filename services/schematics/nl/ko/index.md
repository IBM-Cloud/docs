---

copyright:
  years: 2017
lastupdated: "2017-05-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# {{site.data.keyword.bpfull_notm}}(베타) 시작하기
{: #gettingstarted}

{{site.data.keyword.bplong}}는 클라우드 인프라를 단일 단위로 정의하여 배치하고 여러 환경에서 해당 클라우드 리소스 정의를 재사용하는 데 사용할 수 있는 자동화 도구입니다.
{:shortdesc}

{{site.data.keyword.bpshort}}에서는 HashiCorp의 Terraform을 사용하여 인프라를 코드화합니다. 인프라의 컴포넌트는 개별 리소스로 구분되며, 여기에는 실제 하드웨어에서 사용자 계정까지 포함됩니다. 상위 레벨 및 하위 레벨 리소스를 추상화하여 소프트웨어처럼 인프라를 코드로 처리할 수 있습니다. 

{{site.data.keyword.bpshort}}에 대해 작업할 때는 선언 구문으로 환경의 구성을 작성합니다. 사용자는 원하는 환경을 명시할 수 있습니다. 예를 들어, 프로덕션 상태에서 10개의 {{site.data.keyword.virtualmachinesshort}}를 보유하도록 명시할 수 있습니다. 이 서비스는 사용자의 구성과 Terraform에서 이전에 작성한 내용을 비교하고 필요한 대로 리소스를 추가하거나 제거합니다.

{{site.data.keyword.bpshort}}는 인프라의 SSOT(Single Source of Truth)를 제공하는 협업 DevOps 도구입니다. 소스 제어에 환경 구성을 저장하므로 팀이 더 쉽게 코드 검토를 수행하고 인프라를 버전화하며 커미트 히스토리를 통해 변경 내용을 추적하고 변경을 되돌릴 수 있습니다.

{{site.data.keyword.bpshort}}는 {{site.data.keyword.Bluemix_notm}} 계정의 모든 사용자가 자동으로 사용할 수 있습니다.


## 구성 작성
{: #configuration}

구성을 작성할 때는 환경을 구성하는 클라우드 리소스를 코드화합니다.
{:shortdesc}


{{site.data.keyword.bpshort}}의 샘플 구성을 시도해 보려면 다음 단계를 완료하십시오. 이 샘플에서는 {{site.data.keyword.BluSoftlayer}}에서 사용하는 SSH 키를 프로비저닝할 수 있습니다. 

**참고:** 샘플 구성에는 {{site.data.keyword.BluSoftlayer}} 계정이 필요합니다. 기존 계정이 있을 경우 [{{site.data.keyword.Bluemix_notm}} 및 SoftLayer 계정 연결 문서](../../pricing/linking_accounts.html#unifyingaccounts)를 참조할 수 있으며, 계정이 없을 경우에는 [계정을 등록](https://console.ng.bluemix.net/docs/pricing/index.html#pay-accounts)할 수 있습니다.

1. 로컬에 SSH 키 쌍을 생성하십시오.
  ```
  ssh-keygen -t rsa
  ```
  {:codeblock}

2. <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key" target="_blank">GitHub <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 샘플 구성을 분기(fork)하십시오. 

  다음 예에서는 샘플 구성에 있는 여러 다른 유형의 블록을 보여줍니다. GitHub 저장소의 `main.tf` 파일에서 전체 구성을 볼 수 있습니다.
  
  * 제공자 블록에서 {{site.data.keyword.IBM_notm}} 클라우드 제공자 및 로그인 신임 정보를 설정합니다.

    ```
    provider "ibmcloud" {
      ibmid                    = "${var.ibmid}"
      ibmid_password           = "${var.ibmidpw}"
      softlayer_account_number = "${var.slaccountnum}"
    }
    ```
    {:screen}
  
  * 리소스 블록에서 인프라의 컴포넌트를 정의합니다. 이 샘플에서는 SSH 키입니다.
  
    ```
    resource "ibmcloud_infra_ssh_key" "ssh_key" {
      label = "${var.key_label}"
      notes = "${var.key_note}"
      public_key = "${var.public_key}"
    }
    ```
    {:screen}
  
  * 변수 블록에서 변수를 정의합니다. 이 샘플에서는 {{site.data.keyword.bpshort}} GUI에 변수를 입력할 수 있습니다.
  
    ```
    variable ibmid {
      type = "string"
      description = "Your IBM-ID."
    }
    ```
    {:screen}
  
  * 출력 블록은 구성을 사용하여 환경을 작성하고 리소스(SSH 키)를 작성한 후에 Terraform 출력에 표시되는 내용을 정의합니다.
  
    ```
    output "ssh_key_id" {
      value = "${ibmcloud_infra_ssh_key.ssh_key.id}"
    }
    ```
    {:screen}
  
이제 구성에서 환경을 작성할 수 있습니다. 

{:codeblock}

## 환경 작성
{: #environment}

환경을 작성할 때는 서비스가 구성을 가리키도록 지정하여 서비스가 최신 코드 변경사항을 추출할 수 있게 합니다.
{:shortdesc}

샘플 구성을 사용하여 다음 단계를 완료하고 환경을 작성할 수 있습니다.

1. 메뉴에서 **서비스**를 선택한 다음 **{{site.data.keyword.bpshort}}**를 선택합니다. 그러면 {{site.data.keyword.bpshort}} 대시보드로 이동합니다.

2. 왼쪽 탐색 메뉴에서 **환경**을 선택하고 **환경 작성**을 클릭하여 구성에 대한 특성을 설명하십시오. 환경을 작성하면 {{site.data.keyword.bpshort}}에서 클라우드 리소스를 프로비저닝하고 업데이트하는 방법을 정의하지만, 아직 리소스를 작성하지는 않습니다.

3. 환경에 대한 세부사항을 입력하십시오. 샘플 구성에서는 다음 표에 나열된 값이 필요합니다.

  <table summary="샘플 구성을 환경의 소스로 사용하기 위해 필요한 값.">
  <caption>표 1. 샘플 구성을 환경의 소스로 사용하기 위해 필요한 값.
  </caption>
  <thead>
  <th colspan="1">설정</th>
  <th colspan="1">설명</th>
  </thead>
  <tbody>
  <tr>
  <td>소스 제어 URL</td>
  <td>샘플 구성을 분기(fork)한 GitHub URL을 입력하십시오.</td>
  </tr>
  <tr>
  <td>이름</td>
  <td>환경에 지정할 고유한 이름을 입력하십시오.</td>
  </tr>
  <td>Terraform 버전</td>
  <td>환경에서 호환 가능한 Terraform 버전을 실행하도록 Terraform의 버전을 입력하십시오. 샘플 구성에서는 <code>0.9.1</code> 버전을 사용하십시오.</td>
  </tr>
  <tr>
  <td>변수</td>
  <td>서비스에 변수를 정의하거나 <code>.tf</code> 파일에 있는 환경 변수를 대체할 수 있습니다. 잠금 아이콘을 클릭하여 민감한 변수를 마스킹할 수 있습니다. 변수를 마스킹하면 다른 사용자가 환경 세부사항 페이지에서 숨겨진 값을 보지 못합니다.
  <p>
  <p>샘플 구성 작업을 위해 다음 변수와 값을 추가하십시오.
  <ul>
  <li><code>ibmid</code> - 전체 {{site.data.keyword.ibmid}}를 값으로 입력하십시오.</li>
  <li><code>ibmidpw</code> - {{site.data.keyword.ibmid}}와 연관된 비밀번호를 입력하고 잠금 아이콘을 클릭하여 값을 마스킹하십시오.</li>
  <li><code>slaccountnum</code> - {{site.data.keyword.BluSoftlayer}} 계정 번호를 입력하십시오.
   <li><code>datacenter</code> - SSH 키 리소스를 배치하려는 데이터 센터를 입력하십시오. 사용 가능한 전체 값 목록은 <a href="https://github.com/IBM-Bluemix/tf-bluemix-ssh-key/blob/master/README.md" target="_blank">readme 파일 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>을 참조하십시오.</li> 
   <li><code>public_key</code> - 공개 SSH 키를 입력하십시오. <code>pbcopy < ~/.ssh/id_rsa.pub</code> 명령을 실행하여 공개 키를 클립보드에 복사할 수 있습니다.
   <li><code>key_label</code> - 고유 이름으로 키를 식별하십시오.
   <li><code>key_note</code> - 선택사항: SSH 키에 대한 설명적 텍스트를 추가하십시오.</ul></td>
   </tr></tbody></table>

4. 환경의 세부사항을 모두 채우고 나면 **작성**을 클릭하십시오. 새로 작성한 환경이 표시됩니다. 
5. 환경을 배치할 때 프로비저닝 또는 제거되는 리소스의 미리보기를 보려면 **플랜**을 클릭하십시오. 
6. 출력에서 오류를 검사하려면 플랜 로그를 보십시오. 
7. 환경을 배치할 준비가 되면 **적용**을 클릭하십시오. 키가 성공적으로 배치되었는지 확인하기 위해 적용 로그를 모니터할 수 있습니다. 배치에 성공하면 출력의 끝에 다음 행이 표시됩니다.

  ```
  Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
  ```
  {: screen}

  [{{site.data.keyword.slportal}}](https://control.bluemix.net/devices/sshkeys)에서도 SSH 키를 볼 수 있습니다.
8. 선택사항: SSH 키를 제거하고 {{site.data.keyword.Bluemix_notm}}에서 환경을 제거하려면 조치 메뉴에서 **리소스 영구 삭제**를 선택하십시오.

### 다음에 수행할 작업
{: #next}

* 프로그래밍 방식으로 환경을 배치하는 방법은 [CLI 또는 API를 확인](schematics_deploying.html)하십시오.
* 사용자 고유의 구성을 처음부터 새로 작성하려는 경우 <a href="https://ibm-bluemix.github.io/tf-ibm-docs/">{{site.data.keyword.IBM_notm}} 클라우드 리소스 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>를 확인하십시오. {{site.data.keyword.IBM_notm}} 클라우드 리소스는 Terraform 플러그인 제공자로 사용 가능합니다. 
