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

# Terraform プラグイン・プロバイダーのリソース
{: #terraform-resources}

{{site.data.keyword.IBM}} Cloud リソースは Terraform プラグイン・プロバイダーとして使用できます。さまざまなリソースを組み合わせて独自の構成を作成し、その構成を環境にデプロイすることができます。
{: shortdesc}

使用例、必要な引数、エクスポートされる属性については、GitHub の<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d">データ・ソース・ドキュメント <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> および<a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r">リソース・ドキュメント <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> を参照してください。構成は JSON で記述するか、<a href="https://www.terraform.io/docs/configuration/index.html">HashiCorp Configuration Language (HCL) <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a> で記述することができます。

## ローカルでの開発
{: #developing}

使用するシステム上でローカルに開発する場合は、以下のステップを実行します。

1. <a href="https://www.terraform.io/intro/getting-started/install.html">使用するシステム用の Terraform をダウンロードしてインストールします。<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>

2. <a href="https://github.com/IBM-Bluemix/terraform/releases">{{site.data.keyword.IBM_notm}} Cloud プロバイダー用の Terraform バイナリーをダウンロードします。<img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a>

3. Terraform バイナリーを指す `.terraformrc` ファイルを作成します。 

  次の例では、`/opt/provider/terraform-provider-ibmcloud` がディレクトリーへの経路です。

  ```
  # ~/.terraformrc
providers {
    ibmcloud = "/opt/provider/terraform-provider-ibmcloud"
  }
  ```
  {:codeblock}
  
4. プラグイン・プロバイダーと {{site.data.keyword.IBM_notm}} 資格情報を、Terraform で使用できるように構成します。 

  資格情報を環境変数として提供するには、`.tf` ファイルで次のコードを使用します。
  ```
  provider "ibmcloud" {
    ibmid = "${var.ibmid}"
    ibmid_password = "${var.ibmidpw}"
  }
  ```
  {:codeblock}
  
  その後、使用する端末で資格情報をエクスポートできます。
  ```
  export ibmid="IBMid"
  export ibmid_password="IBMid password"
  ```
  {:codeblock}


## データ・ソース
{: #data}

以下のデータ・ソースが使用可能です。これらを使用して、リソースに関する読み取り専用の情報を抽出できます。 

<table summary="Bluemix データ・ソース">
<caption>表 1. 使用可能なプラットフォーム・データ・ソース。
</caption>
 <thead>
 <th colspan="5">Bluemix データ・ソース</th>
 </thead>
 <tbody>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_account.html.markdown">Bluemix アカウント <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_org.html.markdown">Bluemix 組織 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_space.html.markdown ">Bluemix スペース <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_instance.html.markdown">Cloud Foundry サービス・インスタンス <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_key.html.markdown">Cloud Foundry サービス・キー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 </tr>
 <tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cf_service_plan.html.markdown">Cloud Foundry サービス・プラン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster.html.markdown">Kubernetes クラスター <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_cluster_config.html.markdown">Kubernetes クラスター構成 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/cs_worker.html.markdown">Kubernetes ワーカー・ノード <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <tr>
 </tbody></table>
 
<table summary="Bluemix インフラストラクチャー (SoftLayer) データ・ソース">
<caption>表 2. 使用可能なインフラストラクチャー・データ・ソース
</caption>
<thead>
<th colspan="4">Bluemix インフラストラクチャー (SoftLayer) データ・ソース</th>
</thead>
<tbody>
<tr>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_dns_domain.html.markdown">DNS ドメイン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_image_template.html.markdown">イメージ・テンプレート <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_ssh_key.html.markdown">SSH 鍵 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/d/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
 <t/r>
</tbody></table>


## リソース
{: #resources}

以下のリソースが使用可能です。これらを使用して、インフラストラクチャーのコンポーネントを定義できます。 

 <table summary="Bluemix リソース">
 <caption>表 3. 使用可能なプラットフォーム・リソース。
</caption>
  <thead>
  <th colspan="5">Bluemix リソース</th>
  </thead>
  <tbody>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_instance.html.markdown">Cloud Foundry サービス・インスタンス <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/blob/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cf_service_key.html.markdown">Cloud Foundry サービス・キー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster.html.markdown">Kubernetes クラスター <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/cs_cluster_bind_service.html.markdown">Kubernetes サービス・バインディング <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">ユーザー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  </tr>
</tbody></table>

<table summary="Bluemix インフラストラクチャー (SoftLayer) リソース">
<caption>表 4. 使用可能なインフラストラクチャー・リソース。
</caption>
 <thead>
 <th colspan="5">Bluemix インフラストラクチャー (SoftLayer) リソース</th>
 </thead>
 <tbody>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_bare_metal.html.markdown">ベア・メタル・サーバー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_basic_monitor.html.markdown">基本モニター <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_block_storage.html.markdown">ブロック・ストレージ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain.html.markdown">DNS ドメイン <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_dns_domain_record.html.markdown">DNS ドメイン・レコード <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_file_storage.html.markdown">ファイル・ストレージ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated.html.markdown">専用ハードウェア・ファイアウォール <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_fw_hardware_dedicated_rules.html.markdown">専用ハードウェア・ファイアウォールのルール <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_global_ip.html.markdown">グローバル IP <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local.html.markdown">ロード・バランサー・ローカル <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service.html.markdown">ロード・バランサー・ローカル・サービス <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_local_service_group.html.markdown">ロード・バランサー・ローカル・サービス・グループ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx.html.markdown">ロード・バランサー VPX <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_ha.html.markdown">ロード・バランサー VPX HA <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_service.html.markdown">ロード・バランサー VPX サービス <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_lb_vpx_vip.html.markdown">ロード・バランサー VPX 仮想 IP <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_objectstorage_account.html.markdown">オブジェクト・ストレージ・アカウント <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_provisioning_hook.html.markdown">プロビジョニング・フック <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_group.html.markdown">スケーリング・グループ <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_scale_policy.html.markdown">スケーリング・ポリシー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  </tr>
  <tr>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_security_certificate.html.markdown">セキュリティー証明書 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_ssh_key.html.markdown">SSH 鍵 <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_user.html.markdown">ユーザー <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_virtual_guest.html.markdown">仮想ゲスト <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <td><a href="https://github.com/IBM-Bluemix/terraform/tree/provider/ibm-cloud/website/source/docs/providers/ibmcloud/r/infra_vlan.html.markdown">VLAN <img src="../../icons/launch-glyph.svg" alt="外部リンク・アイコン"></a></td>
  <tr>
</tbody></table>
