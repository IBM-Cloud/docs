---

copyright:
  years: 2017
  last-updated: "2017-01-05"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Running deployments
{: #deployment_run}

You run a deployment by completing the tasks in a deployment plan.
{:shortdesc}

You start a deployment by running one of the eligible tasks in a deployment plan. If a deployment plan has several eligible tasks, you can start any of them. You must deliberately start the first task even if all eligible tasks are UrbanCode Deploy type tasks that normally start automatically as soon as they are eligible.  

The deployment plan's execution pattern determines when a task is eligible to run. If all tasks have the sequential execution pattern, which is the default pattern, tasks become eligible in the order in which they are listed in the plan, starting with the first, or top, task.

The tasks in a group with a parallel execution pattern become eligible simultaneously as soon as the group itself becomes eligible. Tasks in a group with a parallel pattern can be started in any order. Nested groups and tasks with ad hoc dependencies can affect the execution pattern.

You can start a deployment at any time. You can modify a deployment plan after you start a deployment. You can add, delete, and modify tasks. You can reopen a finished task.

<!-- scheduled deployments-->

After all tasks are resolved, the deployment is complete. A task is resolved if it has a status of `Complete` or `Skipped`.

## Starting deployments
{: #deployment_start}

To start a deployment, complete these steps.

<!-- Include a sentence to briefly introduce the steps. For example:-->

1. Step 1.
On the `Deployment Plans` page, click the deployment plan that you want to use for the deployment. The deployment detail page is displayed. You can filter the list of plans by team.

2. Step 2. Click `Start` for one of the eligible tasks. The deployment begins. Task and plan durations are calculated based on when the deployment started.

3. Step 3. For example output:
```
displayed information
```
{: screen}


## Completing tasks
{: #deployment_taskStart}

<!-- Include a sentence describing why this task is needed.  For example: -->
To start a task,.

<!-- Include a sentence to briefly introduce the steps. For example:-->

To find the `biblumix` user password, follow these steps:

<!-- Use ordered list markup for the step section. Include code examples as needed. -->

1. Step 1
Click `Start`. The deployment begins if the task is the first task started.  

2. Step 2. For example input:
3. ```
copyable code
```
{: codeblock}

3. Step 3. For example output:
```
displayed information
```
{: screen}
