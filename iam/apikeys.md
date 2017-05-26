---

copyright:

  years: 2015, 2017
lastupdated: "2017-05-25"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing API keys
{: #manapikey}

An application programming interface key (API key) is a code that is passed in by computer programs that call an application programming interface (API) to identify the calling program, its developer, or its user to the website. API keys are used to track and control how the API is being used, for example to prevent malicious use or abuse of the API (as defined perhaps by terms of service). The API key often acts as both a unique identifier and a secret token for authentication, and generally has a set of access rights on the API associated with it. API keys can be based on the universally unique identifier (UUID) system to ensure they are unique to each user.

As a {{site.data.keyword.Bluemix_notm}} user you might want to use an API key when you enable a program or script without distributing your password to the script. A benefit of using an API key can be that a user or organization can create several API Keys for different programs and the API keys can be deleted independently if compromised without interfering with other API keys or even the user. In addition, as a [federated user](/docs/admin/adminpublic.html#federatedid), you can use an API key to login by using the `BLUEMIX_API_KEY` environment variable. For more information about using an API key for logging in, see the documentation for the [{{site.data.keyword.Bluemix_notm}} CLI `bluemix login` command](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_login) and the [cf CLI `cf login` command](/docs/cli/reference/cfcommands/index.html#cf_login).

You can manage your {{site.data.keyword.Bluemix_notm}} API keys, from the Bluemix API Keys window. Go to **Manage** &gt; **Security** &gt; **Bluemix API keys** to see a list of your API Keys with descriptions and dates. You can create, edit or delete API keys from this page.

To create an API key:

1. Go to **Manage** &gt; **Security** &gt; **Bluemix API keys**.
2. Click **Create API key**.
3. Enter a name and description for your API key.
4. Click **Create API key**.
5. Then, click **Show** to display the API key to copy and save it for later, or click **Download API key**.

**Note**: The API key is only available to show or download at the time of creation. If the API key is lost, you must create a new API key.

To edit an API key:

1. Go to **Manage** &gt; **Security** &gt; **Bluemix API keys**.
2. From the **Actions** menu of an API key that is listed in the table, click **Edit the name & description** 
3. Update the information for your API key.
4. Click **Update API key**.

To delete an API key: 

1. Go to **Manage** &gt; **Security** &gt; **Bluemix API keys**.
2. From the **Actions** menu of an API key that is listed in the table, click to **Delete**.
3. Then, confirm the deletion by clicking **Delete key**.

You can also use the {{site.data.keyword.Bluemix_notm}} CLI to manage your API keys by listing your keys, creating keys, updating keys, or deleting keys. See the [`bluemix iam api-keys`](/docs/cli/reference/bluemix_cli/bx_cli.html#bluemix_iam) command section for more information.
