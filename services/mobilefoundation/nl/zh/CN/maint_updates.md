---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 维护和更新
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} 会供应 {{site.data.keyword.mfserver_short_notm}}<!--on {{site.data.keyword.containerlong}} as a container group-->。当 {{site.data.keyword.mobilefoundation_short}} 服务器有更新时，用户会收到相应的通知。您可以选择在您方便的时间来更新 {{site.data.keyword.mobilefoundation_short}} 服务器。
{:shortdesc}

## 维护策略
{: #maintupdate_strategy_mf}

当 {{site.data.keyword.mobilefoundation_short}} 有更新时，用户会收到有关更新可用的通知。通知将显示在服务实例仪表板中。用户可以选择在自己决定的维护时段来应用 {{site.data.keyword.mobilefoundation_short}} 更新。

当以下某个组件更新后，即会有 {{site.data.keyword.mobilefoundation_short}} 服务更新可用。

* {{site.data.keyword.mfserver_short_notm}}.
* 底层 Liberty 版本。
* 底层 Java Developer Kit 版本。


## 应用更新
{: #apply_update_mf}

单击**重新创建**即可应用 {{site.data.keyword.mobilefoundation_short}} 更新。

应用更新后，服务器的版本（如 {{site.data.keyword.mfp_oc_short_notm}} 中所示）将会修改为服务器更新版本。

**注：**
* 用户将无法对其 {{site.data.keyword.mobilefoundation_short}} 服务实例应用自己的修订和更新。
* 请参阅 [Developer 套餐中的重新创建服务器](c_using_mfs_p1.html#recreate_mobilefoundation_p1)和 [Professional 1 Application 套餐中的重新创建服务器](c_using_mfs_p2.html#recreate_mobilefoundation_p2)，以了解单击**重新创建**后不同套餐之间的行为差异。
