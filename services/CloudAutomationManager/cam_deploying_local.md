---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-19"

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

# Deploying a template
<!-- for example, Uploading your data -->
{: #cam_deploying}
<!-- Provide an appropriate ID above -->

<!-- The short description section should include a sentence describing why this task is needed. For search engine optimization, include the service long name and "Bluemix". For example: -->

Deploy a template in your Cloud Automation Manager Local environment.
{:shortdesc}

To deploy a template, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. In the left-side navigation bar, click **Library > Templates**. The template library is displayed.
2. Click the template that you want to deploy.
3. Read the information about the template and click **Deploy Template**.
    You can see the template source code in the **Template Source** tab.
4. Specify the instance name and enter the required deployment parameters as, for example, the connection to the cloud provider where you want to deploy the template.

    The cloud connection list only contains the connections defined for the type of cloud provider where you can deploy the template. For information about cloud connections, see [Managing connections](/docs/services/CloudAutomationManager/cam_managing_connections.html).

    If you specify an SSH key, ensure that the key format is correct. The SSH key must start with the <code>ssh-rsa</code> string and the crypted string cannot contain any space. For example:
    ```
    ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAkZ5wvjWedYOYnkx2Mp2lnXgTxLKnvSYkvfb36P6JQFPhLY0cmgqY9Vi7XP/LsOFeLk6+7qSsInIILQ5iZ8   /uKsNxAOo2gZdyh5FKzaMDTsBbZggwqayjplADQ1C+QbHbprJLKSFRx98+ROb19u+CUIFL0FSmO03m1ZzZB3cYrEIiXql0vJp3DeSUSq/xCQ76qrXT7qzMUTfJdi3hPjtfTh1UIzC5buyR7jhe8FocDf5dn3KRCMzIUUrvd3zvyYHmcer0InmtK3e2OTvu8V4Xw2Mx4BrbpjBcDAmBShaHOhKq7IqT8qPWek46UxY9vUmnBbB9hP5jOn+ip3HSBJc3BQ==
    ```

    If you are deploying an Amazon EC2 template, ensure that the image that you specify supports the T2 instance type. For more information, see [T2 Instances](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/t2-instances.html){:new_window}.
<!-- This topic is pointed to by the CAM Content deploy topics, so adding CAM Content requirement here -->
5. If you are deploying advanced content from the Enterprise Middleware Repository, select the target environment.
6. Click **Deploy**. The template instance window is displayed.

    In the template instance window, you can see the instance status, the instance information, and the related resource details. You can view or copy the instance logs and you can also access the template from which the instance was deployed.
