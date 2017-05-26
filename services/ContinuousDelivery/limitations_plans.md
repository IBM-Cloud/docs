---

copyright:
  years: 2016, 2017
lastupdated: "2017-5-17"
---
<!-- Copyright info at top of file: REQUIRED
    The copyright info is YAML content that must occur at the top of the MD file, before attributes are listed.
    It must be surrounded by 3 dashes.
    The value "years" can contain just one year or a two years separated by a comma. (years: 2014, 2016)
    Indentation as per the previous template must be preserved.
-->

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Plan limitations and usage
{: #deliverypipeline_plans}
{: #free_deprecation}

The use of {{site.data.keyword.contdelivery_full}} is limited to the building, deploying, testing, and ongoing operations of applications on the {{site.data.keyword.Bluemix_notm}} platform or other compatible platform-as-a-service or infrastructure-as-a-service offerings.

The acceptable usage behaviors include, but are not limited to, these behaviors:

* The compilation and assembly of artifacts for supported programming languages
* The automated deployment of application artifacts, configurations, and supporting resources or services
* Testing, validation, and other development event-generated behavior that is triggered as the result of a development process

The usage behaviors that are not permitted include, but are not limited to, these behaviors:

* The use of pipeline jobs or workers for general compute behaviors, such as Bitcoin mining, distributed denial-of-service attacks, and malicious or offensive behavior to other clients or users within the IBM Cloud platform or general Internet users
* The use in the normal development process for sites or services that promote hate speech, or other activities that violate the IBM Business Conduct Guidelines
* The use of event-generated behavior for malicious intrusion or attacks against {{site.data.keyword.Bluemix_notm}} or other sites

At the discretion of IBM, users who violate the acceptable usage behaviors of the {{site.data.keyword.contdelivery_short}} services or the [IBM Business Conduct Guidelines ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/investor/governance/business-conduct-guidelines.html){: new_window} may be disabled without notice. At the discretion of IBM, some services may be restored if users correct their usage behaviors after they are notified of the offensive action. Otherwise, accounts may be suspended or terminated.

## Git Repos and Issue Tracking limitations
{: #git_limitations}

{{site.data.keyword.gitrepos}} is built on GitLab Community Edition and hosted by IBM on {{site.data.keyword.Bluemix_notm}}, however, a few GitLab options are not available:

 * Because {{site.data.keyword.deliverypipeline}} provides continuous integration and continuous delivery for {{site.data.keyword.Bluemix_notm}}, the continuous integration features in GitLab are not supported.
 * GitLab admin functions are not available because they are managed by IBM.
 * {{site.data.keyword.gitrepos}} might not be fully accessible.


## Git Repos and Issue Tracking user information and content
{: #git_projects}

Three types of {{site.data.keyword.gitrepos}} projects are available:

  1. Public projects are visible to all site visitors. The content in a public project is visible to everyone who accesses {{site.data.keyword.contdelivery_short}}, even if they are not invited to the project.
  2. Private projects are visible to only select users. For details about granting users access to a project, see [Project users ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/workflow/add-user/add-user.md){: new_window}.
  3. Internal projects are visible to all logged-in users. Any user who has a {{site.data.keyword.Bluemix_notm}} account can view these projects.

You can modify the project type in the project's settings. For more information, see [How to change project visibility ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/public_access/public_access#how-to-change-project-visibility){: new_window}.

When you use {{site.data.keyword.gitrepos}}, the content that you contribute to a project is licensed under any terms that are specified in that project. When you create a project, include a file that describes the license that applies to the content. When you contribute to a project, your name and the email address that is associated with your commits might be visible to the public. The email address that is associated with your {{site.data.keyword.Bluemix_notm}} account is used when you create commits through the {{site.data.keyword.gitrepos}} web interface.

<!-- ###Privacy with Git Repos and Issue Tracking profiles -->

<!-- A few features of {{site.data.keyword.gitrepos}} require the use of a profile page that publicly displays information that you provide. You give IBM the following permissions: -->

  <!-- a. Make the information in your profile&mdash;such as your name, email, picture, bio, social media links, and user activity&mdash;visible to other users of the service. -->

  <!-- b. Publicly disclose your name and other public information and activities that are associated with your use of the service, or otherwise publicize the fact that you are a user of the service, without any further notice to you. -->

<!-- The email address that is associated with your profile page is derived from your {{site.data.keyword.Bluemix_notm}} account details. To modify the email address that is displayed on your profile page, modify your {{site.data.keyword.Bluemix_notm}} account. -->

## Deprecated services
{: #deprecated_services}

{{site.data.keyword.trackplan}} and {{site.data.keyword.deliverypipeline}} Classic, which are part of IBM Bluemix {{site.data.keyword.jazzhub_short}} (JazzHub), are being retired. For more information, see [Track & Plan Retirement ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/04/track-plan-retirement/){: new_window} and [Delivery Pipeline Retirement ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/blogs/bluemix/2017/04/delivery-pipeline-retirement/){: new_window}.

Starting on May 25, no new JazzHub projects can be created. Through automatic rolling upgrades, JazzHub projects will be upgraded to {{site.data.keyword.contdelivery_short}} toolchains. The JazzHub site will be removed from service in early July. For more information about the upgrade, see [Upgrading JazzHub project to Bluemix Continuous Delivery toolchains ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://developer.ibm.com/devops-services/2017/4/18/upgrading-jazzhub-projects-bluemix-continuous-delivery-toolchains/){: new_window}
