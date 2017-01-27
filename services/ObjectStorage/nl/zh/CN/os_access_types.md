---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# 访问权类型 

{{site.data.keyword.objectstorageshort}} 用户可以是管理用户，也可以是非管理用户。访问控制表由管理用户在容器级别启用。
{: shortdesc}

<table>
<caption> 表 1. 定义的用户角色</caption>
  <tr>
    <th> 管理用户 (admin)</th>
    <th> 非管理用户 (member)</th>
  </tr>
  <tr>
    <td> 管理访问控制</td>
    <td> 缺省情况下，无权访问服务或其容器</td>
  </tr>
  <tr>
    <td> 可以创建和删除容器</td>
    <td> 可以基于容器读/写 ACL 执行操作</td>
  </tr>
  <tr>
    <td> 可以读取和写入容器</td>
    <td> 可以执行由 admin 确定的操作</td>
  </tr>
</table>


您可以通过 {{site.data.keyword.Bluemix_notm}} 用户界面、Cloud Foundry API 或 Cloud Foundry CLI 来管理 {{site.data.keyword.objectstorageshort}} 用户。
