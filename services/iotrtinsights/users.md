---

copyright:
  years: 2015,2016

---

{:shortdesc: .shortdesc}

# Managing users {: #manage-users}

Designed for team collaboration, {{site.data.keyword.iotrtinsights_short}} allows administrators to add more users to access the {{site.data.keyword.iotrtinsights_short}} console.
{: shortdesc}

Role descriptions:
- Operator  
Operators log in directly to the {{site.data.keyword.iotrtinsights_short}} console to monitor the real-time data flow of their devices and groups of devices. Operators can also activate and deactivate rules and modify editable dashboards.  
- Administrator  
In addition to the tasks that a operator can perform, administrators can add users, manage dashboard layouts, add data sources, and manage device types.  
- Owner  
The owner role is assigned to the IBM ID that deployed the {{site.data.keyword.iotrtinsights_short}} service instance in Bluemix. An owner has the same privileges as an administrator but cannot be deleted.

To add a new user:
1. Add the user to {{site.data.keyword.iot_short}}.  
**Important:** If you are adding a user with the administrator role you must also add that user to {{site.data.keyword.iot_short}}.  

  1. Log in to the dashboard of the {{site.data.keyword.iot_short}} service that is a data source for your {{site.data.keyword.iotrtinsights_short}} service.  
  2. Navigate to **Access > Members** and click **Add Members**.
  3. Enter the IBM ID for the user that you want to add and click **Add Members**.
2. Add the user to {{site.data.keyword.iotrtinsights_short}}.
  1. Log in to the {{site.data.keyword.iotrtinsights_short}} console as a user with the administrator role or the owner role.
  2. Go to **Set Up > Manage Users**.
  3. Click **Add new user**.
  4. Enter the email address of the user you want to invite, select a role for the user, and click ![Create icon.](images/create.png "Create icon").  
An email that contains the web console link is sent to the user. If the email address is already associated with an IBM ID, the user can log in and access the console directly. If not, the user is prompted to create a free IBM ID before accessing the console.  
**Selecting your Real-Time Insights instance:** Users that have access to multiple Real-Time Insights instances as operators or administrators can quickly switch between these instances. In the Real-Time Insights console, they can click their user name and select the instance that they want to access.  
