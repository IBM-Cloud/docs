---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}



# 管理访问权

访问控制表可用于管理对服务的访问权。[Admin 用户](/docs/services/ObjectStorage/os_access_types.html)可以授予读和写访问权，也可以除去访问权。
{: shortdesc}

使用 UI 或 Swift CLI 管理访问权之前，请确保您已配置服务并开始存储对象。

使用访问控制表时，请记住以下几点：
  * 用户创建容器时，会自动授予其对该容器的 admin 特权。
  * 访问控制表不可用于服务实例或存储帐户，也不可在项目级别使用。访问权只能在容器或对象级别进行管理。
  * 确保验证对容器的访问权是否已[除去](/docs/services/ObjectStorage/os_remove_access.html)。
