---

copyright:
  years: 2016, 2017
lastupdated: "2017-04-14"

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

Create and deploy a template from scratch or deploy one of the starter templates.
{:shortdesc}

To deploy a template, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

<ol><li>Click <strong>Template Library</strong>.</li>
<li>Click <strong>Bring Your Own Template</strong> if you want to create and deploy a template from scratch or click one of the starter  templates.
<p>For the starter templates, a tag identifies the type of provider to which you can deploy the template. You can also filter the starter templates by clicking <strong>Filter</strong> and selecting one or more cloud provider types.</p></li>
<li>Run one of the following procedures:
<ul><li>If you are creating a template from scratch, run the following steps:
 <ol><li>Specify the instance name, the template format (JSON or HCL), and the type of the cloud provider where you want to deploy the template.</li> 
 <li>Click <strong>Next</strong>.</li> 
 <li>Enter the template code or import it from a file or from a URL by clicking <strong>Import Source File</strong>. The template must be in HCL or JSON format depending on what you specified in the previous pane.</li>
 <li>Click <strong>Next</strong>.</li>
 <li>Enter the required deployment parameters as, for example, the connection to the cloud provider where you want to deploy the template.
 <p>The cloud connection list only contains the connections defined for the type of cloud provider where you can deploy the template. For information about cloud connections, see <a href="https://console.{DomainName}/docs/services/CloudAutomationManager/cam_managing_connections.html" target="_blank">Managing connections</a>.</p>
 <note>If you specify an SSH key, ensure that the key format is correct. The SSH key must start with the <code>ssh-rsa</code> string and the crypted string cannot contain any space. For example:
<pre><code>
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAkZ5wvjWedYOYnkx2Mp2lnXgTxLKnvSYkvfb36P6JQFPhLY0cmgqY9Vi7XP/LsOFeLk6+7qSsInIILQ5iZ8/uKsNxAOo2gZdyh5FKzaMDTsBbZggwqayjplADQ1C+QbHbprJLKSFRx98+ROb19u+CUIFL0FSmO03m1ZzZB3cYrEIiXql0vJp3DeSUSq/xCQ76qrXT7qzMUTfJdi3hPjtfTh1UIzC5buyR7jhe8FocDf5dn3KRCMzIUUrvd3zvyYHmcer0InmtK3e2OTvu8V4Xw2Mx4BrbpjBcDAmBShaHOhKq7IqT8qPWek46UxY9vUmnBbB9hP5jOn+ip3HSBJc3BQ==
</code></pre> 
</note>
 </li>
 <li>Click <strong>Deploy</strong>. The instance window is displayed.
 <p>In the instance window, you can see the instance status, the instance information, and the related resource details. You can view or download the instance logs and you can also access the template from which the instance was deployed.</p></li></ol></li>
<li>If you are deploying a starter template, run the following steps:
 <ol><li>Read the information about the template and click <strong>Deploy Template</strong>. 
 <p>You do not need to change the template code displayed in the <strong>Template Source</strong> tab.</p></li>
 <li>Specify the instance name and enter the required deployment parameters as, for example, the connection to the cloud provider where you want to deploy the template.
   <p>The cloud connection list only contains the connections defined for the type of cloud provider where you can deploy the template. For information about cloud connections, see <a href="https://console.{DomainName}/docs/services/CloudAutomationManager/cam_managing_connections.html" target="_blank">Managing connections</a>.</p>
 <note>If you specify an SSH key, ensure that the key format is correct. The SSH key must start with the <code>ssh-rsa</code> string and the crypted string cannot contain any space. For example:
<pre><code>
ssh-rsa AAAAB3NzaC1yc2EAAAABJQAAAQEAkZ5wvjWedYOYnkx2Mp2lnXgTxLKnvSYkvfb36P6JQFPhLY0cmgqY9Vi7XP/LsOFeLk6+7qSsInIILQ5iZ8/uKsNxAOo2gZdyh5FKzaMDTsBbZggwqayjplADQ1C+QbHbprJLKSFRx98+ROb19u+CUIFL0FSmO03m1ZzZB3cYrEIiXql0vJp3DeSUSq/xCQ76qrXT7qzMUTfJdi3hPjtfTh1UIzC5buyR7jhe8FocDf5dn3KRCMzIUUrvd3zvyYHmcer0InmtK3e2OTvu8V4Xw2Mx4BrbpjBcDAmBShaHOhKq7IqT8qPWek46UxY9vUmnBbB9hP5jOn+ip3HSBJc3BQ==
</code></pre> 
</note>
</li>
   <li>Click <strong>Deploy</strong>. The instance window is displayed.
   <p>In the instance window, you can see the instance status, the instance information, and the related resource details. You can view or download the instance logs and you can also access the template from which the instance was deployed.</p></li></ol></li></ul></li></ol>

