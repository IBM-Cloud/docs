---

copyright:
  years: 2015, 2016
lastupdated: "2017-02-24"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}

# 维护和 VM 更新
{: #maintenance_and_vm_updates}

## 维护策略
{: #maintenance_strategy}

IBM WebSphere Application Server in Bluemix 会定期更新，以确保使用当前修订包和补丁来创建新的服务实例。云能够简单快捷地为中间件管理供应新服务实例。预计有许多使用者在想要应用维护时都会升级到新的服务实例。对于那些想要保留长期运行的服务实例的使用者，可以使用为中
间和底层操作访客提供的维护存储库。通过这些存储库，用户可以像在内部部署环境中那样维护自己的环境。

## VM 更新

以下部分说明如何应用虚拟机系统的更改。

您可以像更新其他任何正常 RHEL 系统那样来更新 VM。通过使用 Red Hat 软件包管理器“Yum”，您能够对软件包进行安装、更新、卸载和执行其他各种操作。

您的系统已设置为从 IBM 的 Red Hat Satellite Server 接收这些更新。此 Satellite Server 通过 Yum 软件包管理器从 Red Hat 网络为您提供安全的软件包。

Satellite Server 是由 IBM 管理的，不能从您的系统进行修改。

有关更多信息，请参阅 [Applying package updates on Red Hat Enterprise
Linux](https://access.redhat.com/articles/11258#rhel6){: new_window} 和 [Yum（Red Hat 软件包管理器）](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/6/html/Deployment_Guide/ch-yum.html){: new_window}。
