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

# Storing objects

You can upload objects to storage by using the UI or CLI. Uploading objects is limited to a maximum size of 5 GB in a single upload. However, you can upload larger objects by segmenting them into smaller objects.
{: shortdesc}


## Storing objects in containers through the UI {: #storing-ui}

**Note**: When you upload a file with the same name, {{site.data.keyword.objectstorageshort}} replaces the stored file with the new file. If you download a file and make edits, be sure to give the file another name, or [set up object versioning](/docs/services/ObjectStorage/os_versioning.html) before you upload to keep both versions of the file.


1. From your service instance dashboard, add a container from the **Actions** drop-down menu.
2. Name your container and click **CREATE**.
3. From the **Actions** drop-down menu, select **Add Files**. A dialog box opens.
4. Select the file, or files you want to upload and click **Open**.



## Storing objects in containers through the CLI {: #storing-cli}

1. If you are not logged in to {{site.data.keyword.Bluemix_notm}}, log in to the org and space that contains your instance of {{site.data.keyword.objectstorageshort}}.

  ```
  cf login -a api.ng.bluemix.net -u <userid> -p <password> -o <organization> -s <space>
  ```
  {: pre}

2. Create an {{site.data.keyword.objectstorageshort}} container by running the following command. The *container_name* variable is set, by you, now.

  ```
  swift post <container_name>
  ```
  {: pre}

**Note**: If you receive an error message, confirm that the [the prerequisite software](/docs/services/ObjectStorage/os_configuring.html#install-swift-client) installed.

3. Optional: To verify that your container was created, run the following command to list your containers.

  ```
  swift list
  ```
  {: pre}

4. To prevent data destruction by unintentional over-writes, [set up object versioning](/docs/services/ObjectStorage/os_versioning.html). If you do not want object versioning, list your existing files in the store, and if necessary, rename the directory or the files before you upload.

5. Upload a file to your container by running the following command.

  ```
  swift upload <container_name> <file_name>
  ```
  {: pre}

  **Note**: To upload files larger than 5 GB [extra steps are needed](/docs/services/ObjectStorage/os_large_files.html).

6. Optional: To verify that upload was successful, view the content of your container by running the following command.

  ```
  swift list <container_name>
  ```
  {: pre}
