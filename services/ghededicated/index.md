---

copyright:
  years: 2016, 2017
lastupdated: "2017-4-10"

---
 
{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Getting started with Bluemix Dedicated for GitHub Enterprise
{: #gheded_getting_started}

{{site.data.keyword.ghe_long}} is the IBM Cloud-hosted and fully managed version of {{site.data.keyword.ghe_short}}, available for Dedicated {{site.data.keyword.Bluemix_notm}} environments. GitHub provides the social coding experience that developers love. [{{site.data.keyword.Bluemix_notm}} Dedicated ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/dedicated/index.html#dedicated){: new_window} provides a cloud computing environment on physically isolated hardware that is integrated into your network.

Dedicated {{site.data.keyword.ghe_short}} is for {{site.data.keyword.Bluemix_notm}} Dedicated customers only.

{: #ghe_setaccount}
## Setting up your account 

{{site.data.keyword.ghe_short}} includes single sign-on with {{site.data.keyword.Bluemix_notm}} Dedicated. To log in to {{site.data.keyword.ghe_short}}, paste the URL from your region administrator or welcome email into a browser. The URL will follow this pattern: `github.your-company-dedicated-name.bluemix.net`. Sign in with your {{site.data.keyword.Bluemix_notm}} Dedicated user ID and password. Your {{site.data.keyword.ghe_short}} account is created automatically.

**Note:** If a message states that your user ID doesn't exist, ask your region administrator to add your user ID to the {{site.data.keyword.Bluemix_notm}} Dedicated user registry. If you are the region administrator, see [Managing {{site.data.keyword.Bluemix_notm}} Dedicated users and permissions ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/admin/index.html#oc_useradmin){: new_window}.

In most cases, your GitHub user name is your email short name, unless your short name includes characters that GitHub does not support, such as periods. If your short name includes characters that GitHub does not support, the characters are replaced with dashes.     

{: #ghe_email}
## Adding an email address to your account

To receive notifications, you must add your email address to your {{site.data.keyword.ghe_short}} account settings. After you add your email address, you can take advantage of the social coding features of {{site.data.keyword.ghe_short}}.    
 
To add your email address to your Dedicated {{site.data.keyword.ghe_short}} account, follow these steps:    
1. On any GitHub page, click your profile icon and then click **Settings**.    
2. On the sidebar, click **Emails**.    
3. Add your email address and click **Add**.     
3. Add your email address and click **Add**.     

{: #ghe_auth}
## Creating a personal access token or SSH key for authentication

To perform remote Git operations, such as `clone` or `push`, from your local Git repository, you must use a personal access token or SSH key to authenticate with {{site.data.keyword.ghe_short}}. Authentication through HTTPS is supported by using an access token only; you cannot use your user ID and password to clone or push from a local repository. API requests also require a personal access token.

**Note:** To use a personal access token or SSH key for authentication, you must set up Git locally. For instructions, see [Setting up Git ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/user/articles/set-up-git/){: new_window}.    

To create a personal access token, follow these steps:    
   1. On any GitHub page, click your profile icon and then click **Settings**.    
   2. On the sidebar, click **Personal access tokens**.   
   3. Click **Generate new token**.
   4. Add a token description and click **Generate token**.
   5. Copy the token to a secure location or password management app.    
     **Note:** For security reasons, after you leave the page, you can no longer see the token again.    

Use your personal access token instead of a password for command line access over HTTPS. 


To create an SSH key, follow these steps:
   1. Open Git Bash (Windows) or a new Terminal window (Linux and Mac).    
   2. Paste the following text, substituting the email address that you added to your {{site.data.keyword.ghe_short}} account:
   
     ````
     ssh-keygen -t rsa -b 4096 -C "your_email@example.com"
     # Creates a new ssh key, using the provided email as a label
     Generating public/private rsa key pair.
     ````

   3. When you are prompted to specify a file to save the key in, press Enter to accept the default location.
   4. At the prompt, type a secure passphrase. For more information, see [Working with SSH key passphrases ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/user/articles/working-with-ssh-key-passphrases/){: new_window}.   

Add your SSH key to the ssh-agent:    
   1. Make sure that ssh-agent is enabled. By using Git Bash, enter this command to enable the ssh-agent: 
      ````
      # start the ssh-agent in the background
      $ eval "$(ssh-agent -s)"
      Agent pid 59566
      ````    
  
   2. Add your SSH key to the ssh-agent by entering this command:    
      ````
      $ ssh-add ~/.ssh/id_rsa
      ````    
   3. Add the SSH key to your GitHub account. For more information, see [Adding a new SSH key to your GitHub account ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/user/articles/adding-a-new-ssh-key-to-your-github-account/){: new_window}.    
   

{: #ghe_orgs}
## Setting up GitHub organizations, teams, and repos    

Setting up GitHub organizations is useful because you create distinct groups of users who work on similar projects or tasks. Organizing teams within an organization has the added benefit of controlling access to repositories. For more information, see [Organizations and teams ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/admin/guides/user-management/organizations-and-teams/){: new_window}.

**Note:** GitHub organizations are not the same as {{site.data.keyword.Bluemix_notm}} organizations.

Set up your team's project by completing these tasks:

   1. [Create an organization (org) ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/user/articles/creating-a-new-organization-account/){: new_window}.
   2. [Create a repo for your org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/enterprise/user/articles/create-a-repo/){: new_window}.
   3. [Invite users to join your org ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://help.github.com/articles/inviting-users-to-join-your-organization/){: new_window}.

  **Note:** Before you invite users to your org, they must log in to {{site.data.keyword.ghe_short}} at least once or their {{site.data.keyword.ghe_short}} accounts will not be available to invite.
   
<!-- ### Getting support 
To get answers now, submit questions to [Stack Overflow ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://stackoverflow.com/questions/ask?tags=ibm-bluemix_github-enterprise){: new_window}. 

For more support, use these resources:    
   1. Complete the form at https://ibm.biz/bluemixsupport.   
   2. Submit a new ticket through the Client Success Portal at https://support.ibmcloud.com/ics/support/mylogin.asp?login=bluemix. -->

