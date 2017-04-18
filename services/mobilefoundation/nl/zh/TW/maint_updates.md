---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# 維護及更新
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} 佈建一個 {{site.data.keyword.mfserver_short_notm}}<!-- on {{site.data.keyword.containerlong}} as a container group-->。{{site.data.keyword.mobilefoundation_short}} 伺服器的更新會通知使用者。您可以選擇在您方便的時候更新 {{site.data.keyword.mobilefoundation_short}} 伺服器。
{:shortdesc}

## 維護策略
{: #maintupdate_strategy_mf}

當 {{site.data.keyword.mobilefoundation_short}} 有更新時，使用者會收到更新可用性的通知。通知將顯示於服務實例儀表板中。使用者可以選擇在他所決定的維護時間範圍內，將更新套用至 {{site.data.keyword.mobilefoundation_short}}。

{{site.data.keyword.mobilefoundation_short}} 服務更新將在下列其中一個元件更新時提供。

* {{site.data.keyword.mfserver_short_notm}}.
* 基礎 Liberty 版本。
* 基礎 Java 開發者套件版本。


## 套用更新
{: #apply_update_mf}

{{site.data.keyword.mobilefoundation_short}} 的更新可以藉由按一下**重建**來套用。

套用更新時，伺服器版本（如 {{site.data.keyword.mfp_oc_short_notm}} 中所見）將修改為指出伺服器更新版本。

### 附註：
{: #note notoc}

* 使用者將無法套用自己的修正程式和更新至 {{site.data.keyword.mobilefoundation_short}} 服務實例。
* 請參閱[在 Developer 方案中重建伺服器](c_using_mfs_p1.html#recreate_mobilefoundation_p1)和[在 Professional 1 Application 方案中重建伺服器](c_using_mfs_p2.html#recreate_mobilefoundation_p2)，以瞭解按一下**重建**時，方案之間的行為差異。
