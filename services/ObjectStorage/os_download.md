---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-23"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Downloading objects

You can download your stored objects for review or editing through the UI or the CLI.
{: shortdesc}


## Downloading objects from the UI {: #downloading-ui}

1. To prevent data destruction by unintentional over-writes, [set up object versioning](/docs/services/ObjectStorage/os_versioning.html). If you don't want object versioning, rename the directory or the files before you download, if necessary.
2. In your service instance dashboard, select the container with the file you want to download.
3. Select the file.
4. In the **Actions** drop-down menu, select **Download File**.


## Downloading objects with the Swift CLI {: #downloading-cli}

1.  If you are not logged in to {{site.data.keyword.Bluemix_notm}}, log in to the org and space that contains your instance of {{site.data.keyword.objectstorageshort}}.

    ```
    cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
    ```
    {: pre}

2. To prevent data destruction by unintentional over-writes, [set up object versioning](/docs/services/ObjectStorage/os_versioning.html). If you do not want object versioning, list your existing files in the store, and if necessary, rename the directory or the files before you download.

3. Download a file by running the following command:

    ```
    swift download <container_name> <file_name>
    ```
    {: pre}
