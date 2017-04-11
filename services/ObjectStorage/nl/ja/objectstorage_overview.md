---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-31"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# {{site.data.keyword.objectstorageshort}} の概要 {: #about-object-storage}


{{site.data.keyword.objectstorageshort}} では、ストレージ内のオブジェクトをメタデータで識別することで、大容量のデータ間でもそれらを簡単に検索し、迅速にアクセスできるようにします。
{: shortdesc}


## {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} の仕組み {: #public}

Public {{site.data.keyword.objectstorageshort}} では、アカウントをプロビジョンするときに使用できるルートが 2 つあります。専用プライベート・ネットワーク内で開始するか、あるいは、{{site.data.keyword.Bluemix_notm}} アプリで {{site.data.keyword.objectstorageshort}} にアクセスすることが可能です。以下の図のように、管理者と開発者の両方が、オブジェクトを保管およびアクセスすることができます。

<dl>
  <dt><dfn> {{site.data.keyword.Bluemix_notm}} アプリ </dfn></dt>
    <dd> {{site.data.keyword.objectstorageshort}} サービスを {{site.data.keyword.Bluemix_notm}} アプリにバインドできます。</dd>
  <dt><dfn> クライアント・アプリ </dfn></dt>
    <dd> プライベート・ネットワーク上のファイアウォールを介したアプリケーションから直接、{{site.data.keyword.objectstorageshort}} にアクセスできます。</dd>
  <dt><dfn> Keystone </dfn></dt>
    <dd> {{site.data.keyword.objectstorageshort}} サービスで提供された資格情報を使用して、Keystone から許可トークンを取得します。</dd>
  <dt><dfn> OpenStack の Swift API</dfn></dt>
    <dd> インスタンスを認証したら、Swift API を使用して、保管されたオブジェクトに対する読み取りおよび書き込みを行えます。</dd>
  <dt><dfn> ストレージ・ノード </dfn></dt>
    <dd> サービスでは、<a href="http://docs.openstack.org/developer/swift/overview_replication.html">複数のストレージ・ノードに複製した</a> 3 つのデータ・コピーを保持します。</dd>
</dl>

![上記に記述された {{site.data.keyword.objectstorageshort}} の仕組みが、図示されています。](images/OS_howitworks.png)

図 1. {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} の仕組み

**注意**: プロバイダー・サイドの暗号化は提供されていません。アップロードの前にデータを暗号化するのは、クライアント・アプリケーションの責任です。ディスク・レベルの暗号化は、現在 {{site.data.keyword.Bluemix_notm}} Public {{site.data.keyword.objectstorageshort}} に使用可能ではありません。
