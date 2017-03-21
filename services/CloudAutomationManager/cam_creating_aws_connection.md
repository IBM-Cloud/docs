---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

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

<!-- Additional task topic: OPTIONAL
This is the template for additional task topics that are needed beyond the basic tasks in the getting started index.md.  As needed, other task topics can be included, with titles such as "Configuring x", "Administering y", "Managing z", etc. This topic is a peer of the getting started index.md in the <servicename>.ditamap. This topic can have one level of children and they also can be referenced in <servicename>.ditamap -->

# Configuring an Amazon EC2 connection
<!-- for example, Uploading your data -->
{: #cam_creating_aws_connection}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

In order for Cloud Automation Manager to access your Amazon Web Services (AWS) account, an access key and the secret access key to your account are required. 
{:shortdesc}

The access key and the secret access key are not your AWS user name and password, but they are special tokens that allow Cloud Automation Manager to communicate with your AWS account via secure API calls. 

For more information about creating AWS access keys, see [Creating, Modifying, and Viewing Access Keys (AWS Management Console)](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_access-keys.html#Using_CreateAccessKey){:new_window}.

