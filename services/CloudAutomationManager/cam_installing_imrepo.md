---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-07"

---
<!-- Copyright info and last updated date at top of file: REQUIRED
    The copyright and lastupdated info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be --- surrounded by 3 dashes ---
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    The value "lastupdated" must be followed by a machine date in quotes in the following format: "YYYY-MM-DD"
    The value for "years" must be indented 2 spaces under "copyright", followed by "lastupdated" which should start on its own non-indented line.

-->

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Installing and configuring the Installation Manager repository
<!-- for example, Uploading your data -->
{: #cam_installing_imrepo}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

The Installation Manager repository is served by the local software repository HTTP Server and must be manually installed. The following steps must be completed on the software repository before installation.
{:shortdesc}

## About this task

Complete these steps to build Installation Manager repositories by using the IBM External Installation Manager repositories. This method assumes that the IBM product binary files are available in an IBM Public Installation Manager repository.

## Procedure
1. Download the Installation Manager 1.8.6 Linux X86-64 offering to a local machine. For more information about downloading these files, see [Installation Manager and Packaging Utility download documents](http://www.ibm.com/support/docview.wss?uid=swg27025142){: new_window}
2. Transfer the Installation Manager 1.8.6 toolkit to the `/opt/ibm/docker/software-repo/var/swRepo/im/v1x/base` directory. If this directory structure does not exist, you must create it.
3. Log in to the console that has the mounted software repository NFS file system.
4. Change to the `/opt/ibm/docker/software-repo/var/swRepo/private` directory by using the `cd /opt/ibm/docker/software-repo/var/swRepo/private` command.
5. Make a directory named `IMTemp` by using the `mkdir IMTemp` command.
6. Change to the `IMTemp` directory by using the `cd IMTemp` command.
7. Copy the installer file to the `IMTemp` directory by using the following command:

  ```copy /opt/ibm/docker/software-repo/var/swRepo/private/im/v1x/base/agent.installer.linux.gtk.x86_64_1.8.6000.20161118_1611.zip to /opt/ibm/docker/software-repo/var/swRepo/private/IMTemp```

    **Note:** The name of the `.zip` file (agent.installer.linux.gtk.x86_64_1.8.5000.20160506_1125.zip) might vary depending on the version that you downloaded. Use the file name that you downloaded in the command.
8. Extract the files from the `.zip` file by using the following command: `unzip agent.installer.linux.gtk.x86_64_1.8.5000.20160506_1125.zip -d imtoolkit`.
9. Change to the `/opt/ibm/docker/software-repo/var/swRepo/private/IMTemp/imtoolkit/tools` directory.
10. Install the package utility from the Package Utility remote repository by using the following command:

  ```./imcl install com.ibm.cic.packagingUtility_1.8.6000.20161118_1701 -repositories http://www.ibm.com/software/repositorymanager/com.ibm.cic.packagingUtility  -installationDirectory /opt/ibm/docker/software-repo/var/swRepo/private/IMProducts/PUCL -dataLocation /opt/ibm/docker/software-repo/var/swRepo/private/IMProducts/datalocation -sharedResourcesDirectory /opt/ibm/docker/software-repo/var/swRepo/private/IMProducts/IMshared -log /opt/ibm/docker/software-repo/var/swRepo/private/IMProducts/IMlogs -Prompt -acceptLicense```

## What to do next

Set up your composite repository: [Setting up a composite repository](cam_setup_compositerepo.html){: new_window}
