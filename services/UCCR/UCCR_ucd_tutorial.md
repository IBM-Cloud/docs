---

copyright:
 years: 2017
lastupdated: "2017-6-21"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


# Running UrbanCode Deploy applications with Continuous Release

{: #tut_ucdOverview}

The {{site.data.keyword.uccr_full}} service on IBM {{site.data.keyword.Bluemix_short}} is a comprehensive release management solution. With {{site.data.keyword.uccr_short}}, you can run releases and deployments for all software applications in your development lifecycle.
{:shortdesc}

[After you create an instance](https://console.ng.bluemix.net/catalog/services/continuous-release/){:new_window} ![External link icon](../../icons/launch-glyph.svg "External link icon") of {{site.data.keyword.uccr_short}}, choose how you want to get started.

* Begin with **[creating a release and running a deployment](#gs_create_plan)** if you want to plunge in and start creating deployment plans.

* Begin with **[installing and configuring DevOps Connect](#gs_install_dc)** if you want to integrate {{site.data.keyword.uccr_short}} with your on-premises IBM UrbanCode&trade; Deploy instance. After you configure an integration, you can use Continuous Release tasks to manage UrbanCode Deploy applications.


## Integrating with DevOps Connect
{: #tut_ucdDC}

1. [Create a release](/docs/services/UCCR/UCCR_releases.html##releases_create) and assign it to one of your teams. Any team member can create deployment plans for the release and run deployments.

1. Add a deployment plan to the release.

  * [Create the plan](/docs/services/UCCR/UCCR_releases.html#releases_planAdd) and assign it to the release. 

  * [Add tasks to the deployment plan](/docs/services/UCCR/UCCR_tasks.html#tasks_create). Each task is listed on a separate row in the deployment plan. Try adding different types of tasks: manual, UrbanCode Deploy, Continuous Delivery pipeline, delay, Email, and Slack.

  * You can modify the list of tasks in the plan in various ways. You can reposition tasks, copy tasks, and delete them. 

4. When your deployment plan is ready, run a deployment by using the deployment plan that you created in the previous step.

  * [You run a deployment by resolving the tasks in a deployment plan](/docs/services/UCCR/UCCR_deployRun.html). Resolve tasks by starting them and then changing their status to `Complete`, `Fail`, or `Skipped`. After all the tasks in a deployment plan are resolved, the deployment has a status of Done.

  * Tasks can be started when they are eligible to start. Eligibility is determined by the plan's execution pattern. By default, a plan's execution pattern is sequential. Initially, the first, or topmost, task is eligible to start. You can modify the execution pattern by grouping tasks. A task group can have a parallel execution pattern, which means that the group's tasks can be started in any order and can run simultaneously. A deployment plan can have multiple groups and groups nested within other groups.

  * Some tasks, called auto tasks, start automatically as soon as they are eligible to run. UrbanCode Deploy and Continuous Delivery pipeline type tasks start as soon as they are eligible, without manual intervention. Auto tasks also update their status without manual intervention.  


