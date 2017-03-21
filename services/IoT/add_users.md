---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing user access
{: #managing-user-access}

From the members dashboard, you can control and manage access to your {{site.data.keyword.iot_full}} organization. You can add users by adding, inviting<!--, registering-->, or importing them. You can also give different levels of access to your users by assigning roles.
{:shortdesc}

## Adding users
{: #adding-new-users}

From the **Members** tab of the dashboard, you can add individual members by using the <!--Add, Invite, or Register--> Add or Invite functions. You can also <!--add, invite, or register-->add or invite multiple members simultaneously by using the Import function.

By default, members accounts do not expire. When you add users to your {{site.data.keyword.iot_short_notm}} organization, you can optionally set an expiry date for their account.

### Adding members to your {{site.data.keyword.iot_short_notm}} organization

To add a member to your organization, you will need the IBMid of the member. To add a member, you do not need confirmation from the member.

To add a single member to your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Click **Add Members** and select the **Add** tab.
3. Enter the IBMid of the member.
4. Select a role for the member.
5. Optional: Set an expiry date for the member.
6. Click **Add**.

To add multiple members simultaneously, you must upload a `.csv` file that contains the IBMid, the role, and the optional expiry date of each member. For information, see [Constructing your CSV file](#constructing-your-csv).
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Click **Add Members** and select the **Import** tab.
3. Browse your files or drag the `.csv` file into the **Upload CSV** window.
4. Select a default role to use if a role specified in the CSV file is not recognized.
5. Map the column numbers in your CSV file to the corresponding IBMid, role, and (optional) expiry date entries.
6. Select the appropriate comma or semicolon column separator to match the separator used in your `.csv` file.
7. Click **Import** to import the IBMids and create the members.


### Inviting members to your {{site.data.keyword.iot_short_notm}} organization

When you invite a user to become a member of your {{site.data.keyword.iot_short_notm}} organization, the user receives an email that contains an invitation link. Invitation links expire 48 hours after they are sent. If an invitation link is not used within 48 hours, the user must be invited again to receive a new invitation link.

**Important:** The invite feature requires a configured mail service. For more information, see the Email section of the [External service integrations](reference/extensions/index.html#email) topic.

To invite a member to your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select the **Invite** tab.
3. Enter the email address of the member.
4. Select a role for this member.
5. Optional: Set an expiry date for the member.
6. Click **Invite Member**.

To invite multiple members simultaneously, you must upload a `.csv` file that contains the email address, role and the optional expiry date of each member. For information, see [Constructing your CSV file](#constructing-your-csv).
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select the **Import** tab.
3. Browse your files or drag the `.csv` file into the **Upload CSV** window.
4. Select a default role to use if a role specified in the CSV file is not recognized.
5. Map the column numbers in your CSV file to the corresponding email address, role, and (optional) expiry date entries.
6. Select the appropriate comma or semicolon column separator to match the separator used in your `.csv` file.
7. Click **Import** to send out the invitations.

<!-- ### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization is using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Members**.
2. Select the **Invitations** tab.
2. Click **Invite Members** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg "External link icon")](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window. -->

### Constructing your CSV file
{: #constructing-your-csv}

When you construct a CSV file to import members into your organization, ensure that you include the required information for the method that you are using. Use either commas or semi-colons to separate columns.  
**Important:** When you upload the CSV file, under **CSV settings**, ensure that you select the correct column separator.

Sample CSV file with comma delimitation:  
```
user1@sample.com,PD_DEVELOPER_USER,1489505652152
user2@sample.com,PD_OPERATOR_USER,1489505652152
user3@sample.com,PD_ADMIN_USER,1489505652152
```

Where the following column entries are used:  
- Column 1: The email address of the user.  
If you are adding members, make sure that you use the email address corresponding to a valid IBMid. If you are inviting members you can use any valid email address.
- Column 2: The role to be assigned to the user.  
Enter one of the following roles:
 - PD_ADMIN_USER
 - PD_OPERATOR_USER
 - PD_DEVELOPER_USER
 - PD_ANALYST_USER
 - PD_READER_USER  
 For more information about user roles, see [User, application, and gateway roles](roles_index.html#user_roles).
- Column 3: The Unix timestamp (in milliseconds since January 1, 1970 00:00 UTC) that corresponds to the user expiry date.

## Editing users
{: #editing-users}

Users can be edited to change their role, add, remove, or change an access expiration date, or add or remove access to the organization.

1. From your {{site.data.keyword.iot_short_notm}} dashboard, click **Members** from the navigation bar on the left.
2. Click the **Edit** icon next to the user you wish to edit.
3. Make the desired changes to the user.
4. Click **Save**.

## Blocking user access
{: #blocking-users}

Users can be blocked from accessing the {{site.data.keyword.iot_short_notm}} organization, while still maintaining organization membership.

1. From your {{site.data.keyword.iot_short_notm}} dashboard, click **Members** from the navigation bar on the left.
2. Click the toggle next to the user you wish to block from accessing the {{site.data.keyword.iot_short_notm}} organization.


## Removing users
{: #removing-users}

Users can be removed entirely from the {{site.data.keyword.iot_short_notm}} organization. Removing users cannot be undone, and users must be [added to the platform](#adding-new-users) to restore access.

1. From your {{site.data.keyword.iot_short_notm}} dashboard, click **Members** from the navigation bar on the left.
2. Click the **Delete** icon next to the user to be removed.
3. Click **Delete** in the confirmation dialog.
