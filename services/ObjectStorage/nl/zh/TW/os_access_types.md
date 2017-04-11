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


# 存取類型 

{{site.data.keyword.objectstorageshort}} 使用者可以是管理使用者或非管理使用者。存取控制清單是由管理使用者在容器層次上啟用。
{: shortdesc}

<table>
<caption> 表 1. 定義的使用者角色</caption>
  <tr>
    <th> 管理使用者（管理者）</th>
    <th> 非管理使用者（成員）</th>
  </tr>
  <tr>
    <td> 管理存取控制</td>
    <td> 依預設，對服務及其容器沒有存取權</td>
  </tr>
  <tr>
    <td> 可以建立及刪除容器</td>
    <td> 可以根據容器的讀寫 ACL 執行動作</td>
  </tr>
  <tr>
    <td> 可以讀取容器並寫入其中</td>
    <td> 可以執行由管理者決定的動作</td>
  </tr>
</table>


您可以透過 {{site.data.keyword.Bluemix_notm}} 使用者介面、Cloud Foundry API 或 Cloud Foundry CLI 管理 {{site.data.keyword.objectstorageshort}} 使用者。
