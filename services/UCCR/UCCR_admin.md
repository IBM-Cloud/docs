---

copyright:
 years: 2017
lastupdated: "2017-6-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Administering
{: #admin_overview}

Functional security
{:shortdesc}

Users are authenticated to Bluemix with their IBM web identity. For Bluemix Dedicated and Local, LDAP authentication is supported by default. [Overview of Bluemix security services](https://console.bluemix.net/docs/security/index.html)

In {{site.data.keyword.uccr_short}}, you use organizations to enable collaboration among users and to facilitate the logical grouping of project resources. User security is managed on the Bluemix organization level.

You can group a set of spaces, applications, services, domains, routes, and users together in organizations.
You can manage the access to the spaces and organizations on a per-user basis.
When you create an organization, the organization name must be unique in Bluemix. If the organization name is already in use by another Bluemix Public, Dedicated, or Local user, then you must specify a new name. After you create the organization, you will be automatically assigned the Organization Manager permission, which enables you to edit the organization name, add users, and create or delete spaces in the organization.

Domains

Spaces

Within an organization, you can use spaces to group a set of applications, services, and users. Spaces are tied to a specific region in Bluemix.

After you add users to an organization, you can grant them permissions to the spaces. Similar to organizations, spaces also have a set of user roles with specific permissions that are assigned to team members:

admins
control the security system and UCD protected environments. No UCD protected environments can be used until a user is added to UCD admin role for the protected resource (effetcs UCD only, not Bluemix).

Control is on the org level--org manager. Can see users in the org. If the org admin is admin in more than pone org, he can include users from all his orgs.  


# Managing user Security
{: #admin_security}

To create a a team, on the Manage teams page, click **New Team**, and enter name for the team. After you save the team, add users and user groups to it.

1. On the Manage teams page, click **New Team**. If this is your first time creating a release event, click **Define a release to coordinate work**.

1. In the Create Release Event window, in the **Name** field, enter a name for the release.

3. In the **Team** list, select a team to manage the release. You can add deployment plans oowned by other teams to the release event, not just those owned by the team selected to manage the release. All the teams that you belong to are available.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select an ending date and time.

3. In the **Tags** list, select a calendar event. You can select multiple calendar events. To create a tag instead, type the tag name in list field. Tags that you create with the Create Release Event window are not displayed on the calendar, which can help prevent calendar clutter. If you want your event to appear on the calendar, [select an event that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

5. Click **Save**.

The release event is displayed in the Activities list. After the release is created, you can add deployment plans to it.

## Creating teams
{: admin_securityCreateTeams}

To create a release event, complete the following steps:

1. On the Releases page, click **Create release event**. If this is your first time creating a release event, click **Define a release to coordinate work**.

1. In the Create Release Event window, in the **Name** field, enter a name for the release.

3. In the **Team** list, select a team to manage the release. You can add deployment plans oowned by other teams to the release event, not just those owned by the team selected to manage the release. All the teams that you belong to are available.

3. In the **Start Time** field, select a starting date and time. Starting times are required for all releases.

3. In the **End Time** field, select an ending date and time.

3. In the **Tags** list, select a calendar event. You can select multiple calendar events. To create a tag instead, type the tag name in list field. Tags that you create with the Create Release Event window are not displayed on the calendar, which can help prevent calendar clutter. If you want your event to appear on the calendar, [select an event that is created on the Configure Calendar page](UCCR_events.html#events_tagCreate).

5. Click **Save**.

The release event is displayed in the Activities list. After the release is created, you can add deployment plans to it.
