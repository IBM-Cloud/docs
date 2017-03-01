---

copyright:
  years: 2016, 2017
lastupdated:  "2016-08-03"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Maintenance and updates
{: #maintupdates_mf}

{{site.data.keyword.mobilefoundation_short}} provisions a {{site.data.keyword.mfserver_short_notm}}<!-- on {{site.data.keyword.containerlong}} as a container group-->. The updates to the {{site.data.keyword.mobilefoundation_short}} server are notified to the users. You can choose to update the {{site.data.keyword.mobilefoundation_short}} server when it is convenient for you.
{:shortdesc}

## Maintenance strategy
{: #maintupdate_strategy_mf}

When there is an update to  {{site.data.keyword.mobilefoundation_short}}, the user will be notified about the availability of the update.  A notification will be shown in the service instance dashboard. The user can choose to apply the update to {{site.data.keyword.mobilefoundation_short}} during a maintenance window that is decided by him.

{{site.data.keyword.mobilefoundation_short}} service update will be made available when one of the following components are updated.

* {{site.data.keyword.mfserver_short_notm}}.
* Underlying Liberty version.
* Underlying Java Developer Kit version.


## Applying the updates
{: #apply_update_mf}

The update to {{site.data.keyword.mobilefoundation_short}} can be applied by clicking **Recreate**.

On applying the update, the version of the server, as seen in the {{site.data.keyword.mfp_oc_short_notm}}, will be modified to indicate the server update version.

### Note:
{: #note notoc}

* Users will not be able to apply their own fixes and updates to their  {{site.data.keyword.mobilefoundation_short}} service instance.
* See [Re-creating server in Developer plan](c_using_mfs_p1.html#recreate_mobilefoundation_p1) and [Re-creating server in Professional 1 Application plan](c_using_mfs_p2.html#recreate_mobilefoundation_p2) to understand the difference in behavior across the plans  when **Recreate** is clicked.
