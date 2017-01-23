---

copyright:
  years: 2017
  last-updated: "2017-01-23"

---


<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Managing deployment plans
{: #plan_overview}

A deployment plan is container for tasks. The tasks define the activities that you complete to run a software deployment.

{:shortdesc}

You define a deployment plan by adding tasks to it. You can create new tasks or copy tasks from other deployment plans. When you are satisfied with the plan, you can schedule a deployment, or you can run a deployment by starting one of the plan's tasks.

The tasks in a deployment plan are displayed on individual rows. Each row contains information that identifies the task and provides its status. Each row also contains action icons that are used during deployments, such as `Start` task or `Skip` task

By default, tasks run sequentially beginning with the first task, or topmost task, in the plan. After the first task finishes, the second task is eligible to run, and so forth. The order in which tasks are eligible to run is called the execution order.

The execution order can be modified by combining tasks into groups. When you create a group, you set the group's execution pattern. A group's execution pattern can be sequential or parallel. If a group has a sequential execution pattern, its tasks run sequentially starting with the first task. A deployment plan's default execution pattern is sequential. If a group has a parallel execution pattern, tasks in the group can be started in any order and they can run simultaneously. If a plan consists entirely of parallel tasks, you can start any task regardless of its position in the list.

Eligible tasks display a **Start Task** button. To start a deployment, you start one of a plan's eligible tasks. A deployment cannot start until you manually start an eligible task. This requirement is true even if all the eligible tasks are of types that can otherwise run automatically.

Some tasks start automatically as soon as they are eligible to run, while other tasks are started manually. Whether a task starts automatically or not depends on its type. Manual tasks, as the name implies, are started manually. For example, if a group has the sequential execution pattern, only the first task eligible to start is the first one. After the first task finishes, the second task becomes eligible to run. If the second task is a manual task, it can be started as soon as it becomes eligible to run. If the second task is a type that starts automatically, it starts as soon as the first task finishes.

When all tasks are resolved, the deployment is finished.

## Filtering deployment plans
{: #plan_filter}
By default, the Deployment Plans page displays all unarchived plans managed by your teams. You can filter the display in several ways.

<ul>
<li>To display the plans managed by specific teams, click the **Filter** icon, select **Show Plans for Selected Teams**, and then select the teams. All teams to which you belong are available. You can select multiple teams.
</li>
<li>To display all unarchived plans managed for the selected teams, select **All**. This option is the defulat setting.
</li>
<li>To display only plans that have deployments in progress, select **In Progress**.
</li>
<li>To display only plans that do not have scheduled or completed deployments, select **Drafts**.
</li>
<li>To display only plans that have deployments scheduled, select **Scheduled**.
</li>
<li>To display only plans that are saved as templates, select **Templates**.
</li>
<li>To display only plans that have completed deployments, select **Done**.
</li>
<li>To display only archived plans, select **Trash**. Archived plans can restored.
</li>
</ul>

## Creating deployment plans
{: #plan_create}
After you name a plan, you assign a team to manage it and, optionally, schedule a deployment for it. You can start with a blank plan that has no defined tasks, or you can copy an existing plan. You can also start with a plan template.  When you copy a plan or use a template, many tasks are already defined.

Complete the following steps to create a deployment plan.

1. Start by completing one of the following activities:
  <ul>
  <li>On the Deployment Plan page, click **Create New Plan**. The Deployment Plan Details page is displayed.
  </li>
  <li>On the Getting Started page, click **Get Started with Deployment Plans**.
  </li>
  </ul>

2. On the Deployment Plan Details page, edit the plan name.

3. In the **Team** list, select a team to manage the plan.

4. To schedule a deployment for the plan, click **Scheduled Start**, and then select a date and time for the deployment. You can schedule a deployment at any time.

6. Click **Save**. After the plan is saved, click **Edit** to edit plan details.

After you save the plan, add tasks to it. See xxx for information about creating manual tasks; see xxx for information about UrbanCode Deploy tasks. You can any number of tasks to a deployment plan.

## Promoting and archiving plans
{: #plan_promArch}

<!-- for example, Finding the password -->


<!-- Include a sentence describing why this task is needed.  For example: -->
To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
**Tip:** blah blah

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed info
```
{: screen

## Managing plan templates
{: #plan_templates}

  <!-- for example, Finding the password -->


  <!-- Include a sentence describing why this task is needed.  For example: -->
  To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

  <!-- Include a sentence to briefly introduce the steps. For example:-->

  To find the `biblumix` user password, follow these steps:

  <!-- Use ordered list markup for the step section. Include code examples as needed. -->

  1. Step 1
  **Tip:** blah blah

  2. Step 2. For example input:
  3. ```
  copyable code
  ```
  {: codeblock}

  3. Step 3. For example output:



## Copying deployment plans
    {: #plan_copy}

      <!-- for example, Finding the password -->

>Use the **Copy this plan** action for an existing plan. A new plan that is named 'Copy of ...' is inserted into the Deployment Plans page. The copied plan contains the tasks that are defined in the original plan. To edit the copied plan, click the plan to open the Deployment Plan Detail page. **Tip:** You can copy a template or any existing plan.
      <!-- Include a sentence describing why this task is needed.  For example: -->
      To access the HDFS file system, you must connect as the `biblumix` user, so that you can access the `/user/biblumix` directory in HDFS.

      <!-- Include a sentence to briefly introduce the steps. For example:-->

      To find the `biblumix` user password, follow these steps:

      <!-- Use ordered list markup for the step section. Include code examples as needed. -->

      1. Step 1
      **Tip:** blah blah

      2. Step 2. For example input:
      3. ```
      copyable code
      ```
      {: codeblock}

      3. Step 3. For example output:
      ```
      displayed info
      ```
      {: screen  
