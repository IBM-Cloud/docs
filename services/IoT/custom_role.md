---

copyright:
  years: 2016, 2017
lastupdated: "2016-11-10"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# About custom roles
{: #custom_roles}

In addition to the predefined roles that are detailed in the [user, application, and gateway role documentation](roles_index.html), users can create custom roles that have unique combinations of permissions. Roles represent access to specific operations, and, by creating a custom role, you can combine any of the permissions that are available to the predefined roles.
{:shortdesc}

For more information on the API operations that are available to user roles, see the [user, application, and gateway role documentation](roles_index.html).

## Creating a custom role
{: #custom-role-create}

To create a custom role:

1. In the {{site.data.keyword.iot_short_notm}} dashboard, open the **Members** pane from the navigation bar.
2. Select the **Roles** tab and click **New Role**.
3. Enter a name for your custom role.
4. Optional: Enter a description for your custom role.
5. Optional: Custom roles can use an existing role as a template. To base the custom role on an existing user role, select the role from the list.
6. Click **Next**.
7. From the permissions list, expand the permission categories and select the operations that the custom role should include.
8. Click **Add Role**.

The custom role is included in the list of available roles.

## Editing or deleting a custom role
{: #custom-role-edit}

To edit or delete a custom role:

1. In the {{site.data.keyword.iot_short_notm}} dashboard, open the **Members** pane from the navigation bar.
2. Select the **Roles** tab.
3. Locate the column that corresponds to the custom role that you want to edit.
3. Click the edit icon for the custom role name.
4. Make any required changes to the role description and to the permissions.
5. To delete the role, scoll to the bottom of the permission categories list, and click **Delete Role**.
5. If you have made any changes, click **Save** to update the role.

The role is updated.
