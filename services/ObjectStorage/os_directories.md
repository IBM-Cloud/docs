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

# Working with directories

Swift does not have a true directory structure, but uses naming to represent a directory layout. If you specify a directory name, it is attached to all file names as part of the relative path.
{: shortdesc}

## Adding a directory to a container with the Swift CLI

To add a directory to a container, you must have the directory structure in place on your local device.

1. Locally, create a directory and save your file.
2. Run the following command to upload a directory to your container.

    ```
    swift upload <container_name> <directory_name>
    ```
    {: pre}

## Downloading a directory with the CLI
To download a directory structure, use the `-prefix` parameter to indicate the directory or directory structure that you want to download.

1. Run the following command to download a directory.

    ```
    swift download <container_name> --prefix <directory>
    ```
    {: pre}
