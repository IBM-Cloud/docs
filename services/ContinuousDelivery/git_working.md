---

copyright:
  years: 2015, 2017
lastupdated: "2017-3-28"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:screen:.screen}
{:codeblock:.codeblock}

# Working with Git Repos and Issue Tracking (Experimental)
{: #git_working}

Collaborate with your team and manage your source code with a Git repository (repo) and issue tracker that is hosted by IBM and built on [GitLab Community Edition![External link icon](../../icons/launch-glyph.svg "External link icon")](https://about.gitlab.com/){:new_window}. 
{: shortdesc}

The Git Repos and Issue Tracking tool integration supports teams to manage code and collaborate in many ways:
   * Manage Git repositories through fine-grained access controls that keep code secure
   * Review code and enhance collaboration through merge requests
   * Track issues and share ideas through the issue tracker
   * Document projects on the wiki system

**Note:** Because this tool integration is built on GitLab Community Edition and hosted by IBM on Bluemix, a few GitLab options are not available. For example, Delivery Pipeline provides continuous integration and continuous delivery for Bluemix; therefore, the continuous integration features in GitLab are not supported. In addition, the admin functions are not available because they are managed by IBM. 

## File and repo size limits
{: #git_limits}

Files are strictly limited to 100 MB. The suggested repo size limit is 1 GB. If your repo exceeds 1 GB, you might receive an email with a request to reduce the size of the repo. 

## Creating a personal access token or SSH key for authentication    
{: #git_authentication}

To complete remote Git operations, such as `clone` or `push`, from your local Git repo, you must use a personal access token or SSH key to authenticate with GitLab.

* To set up a personal access token, see [Personal access tokens ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/api/README.html#personal-access-tokens){:new_window}.
* To set up an SSH key, see [SSH ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/ssh/README){:new_window} or [How to create your SSH Keys ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/gitlab-basics/create-your-ssh-keys){:new_window}. Accessing your repositories with SSH authentication might require additional configuration for proxies and firewalls.

**Note:** To use a personal access token or SSH key for authentication, you must set up Git locally. For instructions, see [Start using Git on the command line ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help/gitlab-basics/start-using-git){:new_window}.


Related resources:
* [Git Repos and Issue Tracking help ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/help){:new_window}
* [Toolchain integrations: Configuring Git Repos and Issue Tracking (Experimental)](/docs/services/ContinuousDelivery/toolchains_integrations.html#gitbluemix)
* [Tutorial: Create a toolchain that uses Git Repos and Issue Tracking ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_cfv2){:new_window}
* [Tutorial: Create and use a microservices toolchain with DevOps Insights (v2) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://www.ibm.com/devops/method/tutorials/tutorial_toolchain_microservices_cd){:new_window}
