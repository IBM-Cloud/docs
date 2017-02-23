---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# アクセスのタイプ 

{{site.data.keyword.objectstorageshort}} のユーザーは、管理ユーザーまたは非管理ユーザーのいずれかです。アクセス制御リストは、管理ユーザーによってコンテナー・レベルで有効にされます。
{: shortdesc}

<table>
<caption> 表 1. 定義済みのユーザー役割</caption>
  <tr>
    <th> 管理ユーザー (管理者) </th>
    <th> 非管理ユーザー (メンバー) </th>
  </tr>
  <tr>
    <td> アクセス制御を管理 </td>
    <td> デフォルトでは、サービスおよびコンテナーに対するアクセス権限がない </td>
  </tr>
  <tr>
    <td> コンテナーの作成および削除が可能 </td>
    <td> コンテナーの読み取り/書き込み ACL に基づいてアクションを実行可能 </td>
  </tr>
  <tr>
    <td> コンテナーの読み取りおよび書き込みが可能 </td>
    <td> 管理者の決定に従ってアクションを実行可能 </td>
  </tr>
</table>


{{site.data.keyword.Bluemix_notm}} ユーザー・インターフェース、Cloud Foundry API、または Cloud Foundry CLI を使用して、{{site.data.keyword.objectstorageshort}} ユーザーを管理できます。
