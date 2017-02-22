---

copyright:
  years: 2016, 2017
lastupdated: "2017-02-17"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Managing user access

From the access dashboard, you can control and manage access to your {{site.data.keyword.iot_full}} organization. You can add users by adding, inviting, registering, or importing them. You can also give different levels of access to your users by assiging roles.
{:shortdesc}

- [Adding new users](#adding-new-users)
- [Editing users](#editing-users)
- [Blocking user access](#blocking-users)
- [Removing users](#removing-users)

## Adding new users
{: #adding-new-users}

From the **Access** tab of the dashboard, you can add individual members by using the Add, Invite, or Register functions. You can also add, invite, or register multiple members simultaneously by using the Import function.

By default, members accounts do not expire. When you add users to your {{site.data.keyword.iot_short_notm}} organization, you can optionally set an expiry date for their account.

### Adding members to your {{site.data.keyword.iot_short_notm}} organization

To add a member to your organization, you will need the IBMid of the member. To add a member, you do not need confirmation from the member.

To add a single member to your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Add**.
3. Enter the IBMid of the member.
4. Select a role for the member.
5. Optional: Set an expiry date for the member.
6. Click **Add Member**.

To add multiple members simultaneously, you must upload a `.csv` file that contains the IBMid, the role, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Add**.
4. Select a default role and ensure that the column numbers on your `.csv file` match the column numbers in the CSV settings.
5. Ensure that the column separator in your `.csv` file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the `.csv` file into the **Upload CSV** window.

### Inviting members to your {{site.data.keyword.iot_short_notm}} organization

When you invite a user to become a member of your {{site.data.keyword.iot_short_notm}} organization, the user receives an email that contains an invitation link. Invitation links expire 48 hours after they are sent. If an invitation link is not used within 48 hours, the user must be invited again to receive a new invitation link.

To invite a member to your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Optional: Set an expiry date for the member.
6. Click **Invite Member**.

To invite multiple members simultaneously, you must upload a `.csv` file that contains the email address, role and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Invite**.
4. Select a default role and ensure that the column numbers on your `.csv` file match the column numbers in the CSV settings.
5. Ensure the column separator in your `.csv` file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the `.csv` file into the **Upload CSV** window.

### Registering a member with your {{site.data.keyword.iot_short_notm}} organization

If your organization isn't using {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.ssoshort}}, you can add individual members to your organization by registering them, which does not require an IBMid.

To register a member with your {{site.data.keyword.iot_short_notm}} organization:
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Invite**.
3. Enter the email address of the member.
4. Select a role for this member.
5. Enter the subject, realm name, and issuer.
   **Important:** Ensure that the `Subject`, `Realm Name`, and `Issuer` fields comply with the OpenID Connect recommendations and standards. For more information, see the [OpenID Connect ![External link icon](../../icons/launch-glyph.svg)](http://openid.net/connect/){: new_window} website.
6. Optional: Set an expiry date for the member.
7. Click **Register Member**.

To register multiple members simultaneously, you must upload a CSV (`.csv`) file that contains the email address, role, subject, realm name, issuer, and the optional expiry date of each member.
1. In the {{site.data.keyword.iot_short_notm}} dashboard, go to **Access**.
2. Click **Add Member** and select **Import**.
3. Click **Bulk Register**.
4. Select a default role and ensure that the column numbers on your CSV file match the column numbers in the CSV settings.
5. Ensure the column separator in your CSV file matches the column separator in the CSV settings.
6. Click **Browse your files** or drag the CSV file into the **Upload CSV** window.

### Constructing your CSV file

When you construct a CSV file to import members into your organization, ensure that you include the required information for the method that you are using. Use either commas or semi-colons to separate columns. When you upload the CSV file, under **CSV settings**, ensure that you select the correct column separator.

## Editing users
{: #editing-users}

Users can be edited to change their role, add, remove, or change an access expiration date, or add or remove access to the organization.

1. From your {{site.data.keyword.iot_short_notm}} dashboard, click **Members** from the navigation bar on the left.
2. Click the **Edit** icon ![Edit](/docs/images/edit_32.svg) next to the user you wish to edit.
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
2. Click the **Delete** icon ![Delete](/docs/images/trash_32.svg) next to the user to be removed.
3. Click **Delete** in the confirmation dialog.
