---

copyright:
  years: 2015, 2017
lastupdated: "2017-5-10"

---

{:shortdesc: .shortdesc}
{:new_window: target="_blank"}

# Upgrade your {{site.data.keyword.jazzhub_short}} project to a toolchain
{: #upgrade_projects}

{{site.data.keyword.jazzhub}} is evolving into {{site.data.keyword.contdelivery_full}}. As part of that change, projects will be upgraded to toolchains.

You can upgrade your project or wait for it to be automatically upgraded. For the best experience, make sure that you meet the [prerequisites](#upgrade_prereqs) and upgrade your project as soon as possible so that you can control what your toolchain's name is and which organization it is created in.
{: shortdesc}

## Toolchains
{: #compare_toolchains}

Toolchains are like projects, with a few important differences:

- Projects can have only one repository (repo) and pipeline. Toolchains can have as many repos and pipelines as you need.
- Toolchains can include tools that aren't available in projects, such as Slack, Sauce Labs, PagerDuty, and {{site.data.keyword.DRA_full}}.
- Access to toolchains is managed through standard {{site.data.keyword.Bluemix_notm}} organizations. Membership is maintained at the organization level, unlike projects, where membership was maintained at the project level.

You can learn about toolchains on [YouTube ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://youtu.be/2SIPE1e7NJ4){: new_window} or from [Getting started with {{site.data.keyword.contdelivery_short}}](/docs/services/ContinuousDelivery/index.html).
[![External link to YouTube](images/CD_video.png)](https://youtu.be/2SIPE1e7NJ4){: new_window}

## Prerequisites
{: #upgrade_prereqs}

- To access your upgraded project's toolchain, you need a {{site.data.keyword.Bluemix_notm}} ID. Before you upgrade, you must verify that you have an active {{site.data.keyword.Bluemix_notm}} ID. If you don't have one, [sign up](https://console.ng.bluemix.net/registration/).
- Make sure that your {{site.data.keyword.jazzhub_short}} project owner is correct. The toolchain that is created from your project will be part of that owner's {{site.data.keyword.Bluemix_notm}} organization.
- If you're planning to start the upgrade, make sure that you're a member of every org and space that the pipeline deploys to. Any project admin can start the upgrade. However, if the admin who starts the upgrade is not a member of every org and space that the pipeline deploys to, the pipeline cannot be created. The person who starts the upgrade becomes the owner of the repo in the toolchain.
- The Eclipse Orion {{site.data.keyword.webide}} in the toolchain is separate from the {{site.data.keyword.webide}} that is associated with your project. If you use the {{site.data.keyword.webide}} and you have uncommitted changes, commit them before you upgrade.


## Upgrading from a project to a toolchain
{: #project_to_toolchain}

**Important:** Projects at hub.jazz.net and toolchains are both hosted in the US South region. If your project was configured to deploy apps to a different region, it will still deploy apps to that region after it is upgraded to a toolchain.

When your project is ready to be upgraded, a message is displayed on the project's card and Overview page.

![Image of card with the Ready To Upgrade label](images/card-project-to-upgrade.png)

![Time to Upgrade message](images/banner-ready-to-upgrade.png)

**Tip:** You can find projects that are ready to upgrade from the menu on the My Projects page:

![Image of the Projects To Upgrade menu item](images/menu-projects-to-upgrade.png)

When you start the upgrade, the pipeline stages in your project are locked. You won't be able to run or modify them. If you revert the upgrade by deleting the toolchain, the pipeline is unlocked.

If your project uses a Git repo that is hosted on JazzHub, after you start the upgrade, the repo is locked to ensure the integrity of the data that is moved to the toolchain. If you revert the upgrade by deleting the toolchain, the repo on JazzHub is unlocked.

## Starting the upgrade process
{: #start_upgrade}

Before you start the upgrade process, you can watch it in action on [YouTube ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://youtu.be/LSr2e3uvyLs){: new_window}.
[![External link to YouTube](images/migration-video2.png)](https://youtu.be/LSr2e3uvyLs){: new_window}

To upgrade your project to a toolchain, follow these steps:

1. To start the upgrade process, on the banner message, click **upgrade now**. The "Project upgrade toolchain" page opens.

   ![Example of an upgrade page](images/project-upgrade-toolchain.png)

   For an overview of the upgrade process, read the description on that page. The toolchain will include a new pipeline that contains the same stages and jobs as the project's pipeline. In addition, the toolchain will contain a pointer to the Eclipse Orion {{site.data.keyword.webide}} that runs in {{site.data.keyword.contdelivery_short}}.

   In this example, because the project uses a public repo on github.com, the toolchain will be connected to the same GitHub repo. If your project uses a Git repo that is hosted on JazzHub, the contents of that repo will be cloned to a new repo in {{site.data.keyword.gitrepos}}, which is part of {{site.data.keyword.contdelivery_short}}. For full details about how each type of repo is treated, see the following table.

|Project repo |Project type	|Toolchain repo |
|:----------|:------------------------------|:------------------|
|github.com 		|Private or public 		|The same github.com repo with {{site.data.keyword.Bluemix_notm}} Public.	|
|hub.jazz.net/git		|Private or public 		|A new repo in {{site.data.keyword.gitrepos}} with {{site.data.keyword.Bluemix_notm}} Public.	|
{: caption="Table 1. Project repos mapped to toolchain repos" caption-side="top"}

2. To customize the toolchain, you can configure a few settings:

   - To change the name of the toolchain, edit the **Name** field.

      ![Name field](images/name-change.png)

   - To change which {{site.data.keyword.Bluemix_notm}} organization to create the toolchain in, select the organization from your account menu:

      ![Bluemix Organization chooser](images/bluemix-organization-chooser.png)

   Because toolchains are managed at the organization level, be sure to select an organization where the project members that need to access the toolchain already exist, or can be added.

3. If you used Track & Plan in your project, you can transfer your Track & Plan data to GitHub Issues.

   ![Track and Plan options](images/upgrade-tutorial-track-and-plan.png)

   - Indicate whether you want to migrate your Track & Plan data.
   - By default, all of your Track & Plan data is migrated. If you prefer to migrate only the work items that are part of a specific query, specify that query.
   - Select any work item attributes that you want to map to labels in GitHub Issues.

4. Click **Create**. The new toolchain is created, and its Overview page is displayed.

   ![Overview of the upgraded toolchain](images/new-toolchain-page.png)

   - To access your GitHub repo or the associated issue tracker, click **GitHub** or **Issues**.
   - To access your pipeline, click **Delivery Pipeline**.
   - To access the {{site.data.keyword.webide}}, which contains the contents of your repo that were checked out into the workspace, click **Eclipse Orion {{site.data.keyword.webide}}**.

   If you return to your project during the upgrade, the banner message might state that the upgrade is in progress, especially if the upgrade process involves importing source code to a new repo or importing Track &amp; Plan work items as issues.

   ![Message about project being upgraded to a toolchain](images/project-being-upgraded-banner.png)

## Revisiting your project
{: #revisit_projects}

You are ready to use your new toolchain. Your project is now labeled as "Upgraded," and on the Overview page, a confirmation message is displayed.

![Image of project card with the Upgraded label](images/card-upgraded-project.png)

![Upgraded project](images/banner-upgraded.png)

You can see which projects are upgraded by selecting **Upgraded Projects** from the menu on the My Projects page:

![Image of the Upgraded Projects menu item](images/menu-upgraded-projects.png)

If you need to revert the upgrade, delete your toolchain. You can delete your toolchain from the **More Actions** menu on the toolchain's Overview page:

![image of Delete action in More Actions menu](images/upgrade-tutorial-delete-toolchain.png)

When you return to your project, the upgrade message is displayed again, and you can upgrade again when you are ready.

## Next steps
{: #upgrade_next_steps}

1. Confirm that the upgrade is complete by refreshing your browser and checking for the message that your project was "upgraded to this toolchain" on the project Overview page:

   ![Message in banner indicating the project was upgraded](images/banner-upgraded.png)

   **Note:** If the message says "upgrade now," your upgrade failed. Click the **upgrade now** link to try again.

   ![Message in banner indicating the project is ready to upgrade](images/banner-ready-to-upgrade.png)

2. Give your team members access to the toolchain.
    - Each team member must have a valid {{site.data.keyword.Bluemix_notm}} account. Team members who don't have accounts must [sign up ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://console.ng.bluemix.net/registration){:new_window}.
    - Grant organization (org) members access to the toolchain from the toolchain Manage page. For more information about access control for toolchains, see [Managing access ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/services/ContinuousDelivery/toolchains_using.html#managing_access){:new_window}.
    - If a user is not a member of the org that the toolchain belongs to, add them to the org from the Manage Organizations page.
      For more information about managing organizations, see [Managing organizations and spaces ![External link icon](../../icons/launch-glyph.svg "External link icon")](/docs/admin/orgs_spaces.html#orgsspacesusers){:new_window}.

3. Use the tools from your toolchain instead of the tools from your {{site.data.keyword.jazzhub_short}} project. For example, to edit code from a browser, use the Web IDE from your toolchain.

4. If you are using {{site.data.keyword.gitrepos}}, authenticate by using a personal access token or an SSH key. For more information about SSH keys, see [Creating a personal access token or SSH key for authentication](/docs/services/ContinuousDelivery/git_working.html#git_authentication). To authenticate from an external Git client through https, follow these steps:
    1. Go to the [Access Tokens page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/profile/personal_access_tokens){:new_window} of your {{site.data.keyword.gitrepos}} user settings.
    2. Create a personal access token that uses **api** as the scope.
    3. Go to the [Account page ![External link icon](../../icons/launch-glyph.svg "External link icon")](https://git.ng.bluemix.net/profile/account){:new_window} and find your username for {{site.data.keyword.gitrepos}}. Your username is listed in the "Change username" section and it is shown as the first part of the URL for any personal repo that you create.
    4. To authenticate with {{site.data.keyword.gitrepos}} from an external Git client through https, use your username and your personal access token.
    5. If you want to reuse the local repo of your JazzHub Git repo, point the repo to the new repo in {{site.data.keyword.gitrepos}}. From a shell in a terminal, change to the directory where the JazzHub Git repo is cloned. Enter the `git remote set-url` command: `git remote set-url origin https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

        **Tip:** To check which remote URLs are set to which remote names, use the `git remote -v` command. The default remote name is `origin`. If you have a more advanced setup, the form of the command is as follows: `git remote set-url <remote-name-that-uses-jazzhub-repo> https://git.ng.bluemix.net/<userid>/<name-of-new-repo>`

5. When your toolchain is set up and you have started to use it, consider taking all or any of these steps to ensure that no one uses your project:
    - Add a suffix to your project name to indicate that it must not be used. You might add `_DO_NOT_USE` to the end of the project name.
    - Update the project's description to mention that it is no longer used, and add a pointer to the toolchain.
    - Remove the members from the project.
    - When you no longer need the project, delete it.

6. Optional: To explore your project's development maturity, your team's practices, and the quality of your code base, add IBM Cloud {{site.data.keyword.DRA_short}} to your toolchain. {{site.data.keyword.DRA_short}} applies developer, team, and deployment analytics to DevOps projects. For more information, see [Getting started with {{site.data.keyword.DRA_short}}](/docs/services/DevOpsInsights/index.html).


## Troubleshooting
{: #upgrade_troubleshoot}

If you have questions or problems, go to the [support forum](https://developer.ibm.com/answers/questions/ask/?smartspace=devops-services). In your forum post, include the URLs to your {{site.data.keyword.jazzhub_short}} project and your {{site.data.keyword.contdelivery_short}} toolchain, and tag your post with the `devops-services` tag.
