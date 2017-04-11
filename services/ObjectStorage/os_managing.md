---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Managing objects

You can use the Swift CLI, API, or Bluemix UI to manage your objects and containers.
{: shortdesc}

Before you can manage objects, be sure that you have [authenticated](/docs/services/ObjectStorage/os_authenticate.html) your service instance, [generated](/docs/services/ObjectStorage/os_credentials.html) service credentials, and [configured](/docs/services/ObjectStorage/os_configuring.html) the Swift CLI.

Keep the following points in mind when you are managing objects:
  * There is no limit to the amount of data that you can store, but each upload can be no more than 5 GB. If you need to upload files larger than 5 GB follow the steps that are found in [storing large objects](/docs/services/ObjectStorage/os_large_files.html).
  * Swift does not have a true directory structure, but you can add an [existing directory](/docs/services/ObjectStorage/os_directories.html) to your commands.
  * To avoid unintentionally overwriting a file, [set up object versioning](/docs/services/ObjectStorage/os_versioning.html).
  * You can [schedule a time](/docs/services/ObjectStorage/os_deletion.html) for your objects to be deleted.
