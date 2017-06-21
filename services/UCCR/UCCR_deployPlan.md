---

copyright:
 years: 2017
lastupdated: "2017-6-19"

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing deployment plans
{: #plan_overview}

A deployment plan is a container for tasks. Tasks define the activities that your team runs to complete a software deployment.

{:shortdesc}

You create a deployment plan by assigning a team to manage it and then adding tasks to the plan. Team members add tasks to the plan and run the tasks during deployments. The managing team also determines which IBM UrbanCode Deploy applications are available. After an integration is configured with DevOps Connect, all applications that are managed by the team in IBM UrbanCode Deploy are available in {{site.data.keyword.uccr_short}}.  

The tasks define the activities that the team performs to complete a deployment. You can create new tasks, copy tasks from other deployment plans or import tasks from CSV files. When you are satisfied with the plan, you can schedule a deployment. You can also run a deployment at any time by starting one of the plan's tasks.

Tasks are displayed on individual rows in deployment plans. Each row contains information that identifies the task and provides its status. Each row also contains action icons that are used during deployments, such as **Start** task or **Skip** task

By default, tasks run sequentially beginning with the first task, or topmost task, in the plan. After the first task finishes, the second task is eligible to run, and so forth. The order in which tasks are eligible to run is called the execution order.

The execution order can be modified by combining tasks into groups. [When you create a group](/docs/services/UCCR/UCCR_tasks.html#tasks_groups), you set the group's execution pattern, which can be sequential or parallel. If a group has a sequential execution pattern, its tasks run sequentially starting with the first task. A deployment plan's default execution pattern is sequential. If a group has a parallel execution pattern, tasks in the group can be started in any order and they can run simultaneously. If a plan consists entirely of parallel tasks, you can start any task regardless of its position in the list.

Task eligibility can also be effected by task dependencies. [If a task has any prerequisites](/docs/services/UCCR/UCCR_tasks.html#tasks_dependencies), it cannot start, even if it is otherwise eligible, until all prerequisite tasks are resolved.

Some tasks start automatically as soon as they are eligible to run, while other tasks are started manually. Whether a task starts automatically or not depends on its type. Manual tasks, as the name implies, are started manually. UrbanCode Deploy and Delayed-type tasks automatically start as soon as they are eligible.

Eligible tasks display a **Start Task** button. To start a deployment, you start one of a plan's eligible tasks. Scheduled deployments start automatically at the scheduled time if an eligible task is of a type that can start automatically, such as UrbanCode Deploy.

## Creating deployment plans
{: #plan_create}
You can start with a blank plan that has no defined tasks, or you can copy an existing plan. You can also start with a plan template.  When you copy a plan or use a template, many tasks are already defined.

Complete the following steps to create a deployment plan:

1. On the Releases page or on the Release Detail page, click **Create Deployment Plan**.

2. On the Create Deployment Plan window, in the **Template** list, specify the template that you want to base the plan on. The default value is **None**.

2. In the **Plan name** field, enter the plan name.

3. In the **Team** list, select a team to manage the plan. All teams that you are a member of are available. Team members can modify the plan and manage tasks. The UrbanCode Deploy applications that are managed by the team in UrbanCode Deploy are available to assign to UrbanCode Deploy type tasks.

4. To schedule a deployment for the plan, click **Start time**, and then select a date and time for the deployment. Scheduled deployments automatically start at the scheduled time if the plan contains eligible auto tasks. You can schedule a deployment for any future time.

5. In the **Release** list, select the release that you want to add the plan to. Releases that belong to one of your teams are available. If you select a release, the deployment plan is displayed on the Release Detail page.

6. Click **Save**. If you created the plan on a Release Detail page, the plan is part of the selected release.

After you save the plan, click **Edit** to modify plan details.

## Importing tasks into deployment plans
{: #plan_importTasks}

You can import tasks that are defined in comma-separated values (CSV) files into a deployment plan. You can use CSV files that are exported from IBM UrbanCode Release or another application capable of creating CSV files.

**Important:** When you import tasks, tasks that are already defined in the deployment plan are overwritten and replaced by the tasks in the CSV file.

Complete the following steps to import tasks into a deployment plan.

1. On the Deployment Plan Details page, click **Import Tasks**.

3. In the Import Tasks dialog, click **Choose File**, and then select the CSV file. You can also drag a file onto the **Choose File** field.

6. Click **Import**. The tasks are added to the deployment plan. If the import process is unsuccessful, click **View Report** to display the error log.

When you import a deployment plan from IBM UrbanCode Release, segments are converted into groups with the same execution pattern as the original segments. Segment tasks are bracketed by note-type Start Segment and End Segment tasks. Task dependencies are preserved during import. Segment dependencies are represented by dependencies to End Segment tasks.

The following table contains the fields that define a task in an IBM UrbanCode Release deployment plan. The first row in the CSV file contains the column headers, which correspond to the table's **Field** column. The rows after the first row contain task data, one task per row. The order of the columns does not matter.

To learn about deployment plans exported from IBM UrbanCode Release, download the `SamplePlan.csv` file from the Import Tasks dialog.

If you are creating tasks in a CSV file, you must include the required fields that are identified by the asterisk character (*) in the following table.

| Field  | Description  |
| ------------------ |------------------|
|segmentName*                 |The name segment. Required field.|                                                    
|name*                        |The name of the deployment task. Required field.|                                                                
|type*                        |Task type. Possible values are `note`, `waitfortimetask`, `ucdtask`, or `manual`. During import, if the field contains an unrecognized value, the task is assigned the `manual type.|
|description                 |Description of the deployment plan.|                                                                                                    
|property:processId           |The process ID in IBM UrbanCode Deploy that corresponds to the task.|
|property:task-environments   |Application environments available to the task.|
|property:mailRecipients|Email addresses of users who receive email messages when notifications are sent.|
|taskTagNames                 |The names of the tags that are associated with the task.|
|taskPrequisiteIds         |A comma-separated list of IDs for tasks that must complete before this task can start.|
|segmentPrerequisitelds       |A comma-separated list of IDs for segments with which the current segment has  dependencies.|
|taskPrequisiteNames         |A comma-separated list of names for tasks that must complete before this task can start.|
|segmentPrerequisiteNames       |A comma-separated list of names for segments with which the current segment has  dependencies.|
|assignedUserEmail                |Email address of the user who is assigned to the current task.|
|executorGroup                |User group assigned to the current task.|
|segmentPattern                |Execution pattern of the selected segment.|

{: caption="Table 1. IBM UrbanCode Release deployment plan fields" caption-side="top"}

## Copying and promoting deployment plans
{: #plan_copyPromote}

You can duplicate deployment plans by promoting and copying them. The status of a copied or promoted plan is `draft` even if the original plan has a status of `done` or `in progress`.

To copy a plan, use the **Copy this plan** action On the Deployment Plan page. When you copy a plan, a new plan with the name "Copy of `plan_name`" is inserted into the Deployment Plan page. The copied plan contains all the tasks that are defined in the original plan. If UrbanCode Deploy tasks are in the plan, the applications, versions, and environments that are slected in the original are also selected in the copied plan. Applications, versions, and environments are displayed on the **Versions** tab on the Deployment Plan Detail page.

To promote a plan, use the **Promote this plan** action On the Deployment Plan page. When you promote a plan, a new plan with the name "Promotion of `plan_name`" is inserted into the Deployment Plan page. The promoted plan contains all the tasks that are defined in the original plan. If UrbanCode Deploy tasks are in the plan, the applications and versions that are slected in the original are also selected in the promoted plan. The difference between copied and promoted plans is that application versions are not set in promoted plans.

## Managing plan templates
{: #plan_templates}

You can convert deployment plans to create deployment plan templates.

To create a template, use the **Template this plan** action On the Deployment Plan page. When you create a template, a new plan with the name "Copy of plan_name' is inserted into the Deployment Plan page. The status of a template is `template` even if the original plan has a status of `done` or `in progress`. The template contains all the tasks that are defined in the original plan. If UrbanCode Deploy tasks are in the plan, the applications selected in the original are also selected in the template.

You cannot run deployments with templates. To use a template for a deployment, first copy or promote it and then use the copied or promoted plan.

## Archiving deployment plans
{: #plan_arch}

When you put a deployment plan in the archive, the plan has a status of `Archived` and it not displayed in the Deployment Plan page unless you use the **Archive** filter.

Deployment plans that are in the archive can be restored to `draft` status. You cannot permanently delete a deployment plan.

## Reverting and restoring
{: #plan_history}

A history of changes and revisions is maintained for every deployment plan. You can display revisions on the **Change History** tab on the Deployment Plan Detail page.

To revert to a previous plan version, use the **Restore** action <img class="inline" src="images/restore-icon.png"  alt="restore action"> for the version that you want to restore. The plan is restored to the selected version.  

## Estimating deployment times
{: #plan_durationEst}

Before you start a deployment, you can estimate its expected duration. To estimate duration times, use the **Estimate Task Times** action on the Deployment Plan Detail page. The displayed time represents the time that the deployment ends if you start the deployment now.
