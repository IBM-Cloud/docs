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

# Terraform 플러그인 제공자용 리소스
{: #terraform-resources}

{{site.data.keyword.IBM}} 클라우드 리소스는 Terraform 플러그인 제공자로 사용 가능합니다. 다양한 리소스를 결합하여 사용자 고유의 구성을 작성하고 이를 환경에 배치할 수 있습니다.
{: shortdesc}

GitHub의 <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">데이터 소스 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a> 및 <a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">리소스 문서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>에서 사용법 예제, 필수 인수, 내보내기 속성을 확인할 수 있습니다. 구성은 JSON 또는 <a href="https://www.terraform.io/docs/configuration/index.html">HCL(HashiCorp Configuration Language) <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>로 작성할 수 있습니다.

## 로컬에서 개발
{: #developing}

시스템에서 로컬로 개발하려면 다음 단계를 완료하십시오.

1. <a href="https://www.terraform.io/intro/getting-started/install.html">사용자의 시스템에 적합한 Terraform을 다운로드하고 설치하십시오. <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">{{site.data.keyword.IBM_notm}} 클라우드 제공자용 Terraform 바이너리를 다운로드하십시오. <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a>

3. Terraform 바이너리를 가리키는 `.terraformrc` 파일을 작성하십시오. 

  다음 예에서 `/opt/provider/terraform-provider-ibmcloud`는 디렉토리의 라우트입니다.

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. Terraform과 작동하도록 플러그인 제공자와 {{site.data.keyword.IBM_notm}} 신임 정보를 구성하십시오. 

  `.tf` 파일에서 다음 코드를 사용하여 신임 정보를 환경 변수로 제공할 수 있습니다.
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  그런 다음 터미널에서 신임 정보를 내보낼 수 있습니다.
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## 데이터 소스
{: #data}

사용 가능한 데이터 소스는 다음과 같으며 이를 사용하여 리소스에 대한 읽기 전용 정보를 추출할 수 있습니다. 

<table summary="Bluemix 데이터 소스">
<caption>표 1. 사용 가능한 플랫폼 데이터 소스.
</caption>
 <thead>
 <th colspan="5">Bluemix 데이터 소스</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix 계정 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix 조직 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix 영역 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry 서비스 인스턴스 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry 서비스 키 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry 서비스 플랜 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes 클러스터 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes 클러스터 구성 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes 작업자 노드 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix Infrastructure(SoftLayer) 데이터 소스">
<caption>표 2. 사용 가능한 인프라 데이터 소스.
</caption>
<thead>
<th colspan="4">Bluemix Infrastructure(SoftLayer) 데이터 소스</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS 도메인 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">이미지 템플리트 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH 키 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
 <t/r>
</tbody></table>


## 리소스
{: #resources}

사용 가능한 리소스는 다음과 같으며 이를 사용하여 인프라의 컴포넌트를 정의할 수 있습니다. 

 <table summary="Bluemix 리소스">
 <caption>표 3. 사용 가능한 플랫폼 리소스.
 </caption>
  <thead>
  <th colspan="5">Bluemix 리소스</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry 서비스 인스턴스 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry 서비스 키 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes 클러스터 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes 서비스 바인딩 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">사용자 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix Infrastructure(SoftLayer) 리소스">
<caption>표 4. 사용 가능한 인프라 리소스.
</caption>
 <thead>
 <th colspan="5">Bluemix Infrastructure(SoftLayer) 리소스</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">베어메탈 서버 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">기본 모니터 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">블록 스토리지 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS 도메인 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS 도메인 레코드 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">파일 스토리지 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">하드웨어 방화벽 전용 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">하드웨어 방화벽 전용 규칙 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">글로벌 IP <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">로드 밸런서 로컬 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">로드 밸런서 로컬 서비스 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">로드 밸런서 로컬 서비스 그룹 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">로드 밸런서 VPX <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">로드 밸런서 VPX HA <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">로드 밸런서 VPX 서비스 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">로드 밸런서 VPX 가상 IP <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">오브젝트 스토리지 계정 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">프로비저닝 훅 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">스케일링 그룹 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">스케일링 정책 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">보안 인증서 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH 키 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">사용자 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">가상 게스트 <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="외부 링크 아이콘"></a></td>
  <tr>
</tbody></table>
