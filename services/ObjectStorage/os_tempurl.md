---

copyright:
  years: 2014, 2017
lastupdated: "2017-02-10"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Creating a temporary URL {: #create-temporary-url}

A temporary URL is a long, difficult-to-guess URL that can be used for a specified period of time to download objects without requiring further authentication or giving full access to the storage account.
{: shortdesc}


1. Identify your authentication information by printing your account information with the following command:

  ```
  swift stat
  ```
  {: pre}
  **Note**: Take note of the full string behind *Account*, including `AUTH_`.

2. Set a secret key. Choose a long, random, and hard to guess string. To set the key, run the following command:

  ```
  swift post -m "Temp-URL-Key:<key>"
  ```
  {: pre}

3. Verify that the `Temp-URL-Key` was set successfully by running the following command.

  ```
  swift stat
  ```
  {: pre}

4. Create a temporary URL by running the following command:

  ```
  swift tempurl GET <seconds> <path> <key>
  ```
  {: pre}

  The following table explains the positional arguments that the Swift `tempurl` command takes.
  <table>
  <caption> Table 1. Temporary URL positional arguments </caption>
    <tr>
      <th> Argument </th>
      <th> Description </th>
    </tr>
    <tr>
      <td> <i> method </i> </td>
      <td> GET to allow download. PUT to allow upload. </td>
    </tr>
    <tr>
      <td> <i> seconds </i> </td>
      <td> Time that the temporary URL is available, expressed in seconds. </td>
    </tr>
    <tr>
      <td> <i> path </i> </td>
      <td> The full path of the object expressed as <code>/v1/<i>auth_account</i>/<i>container_name</i>/<i>object_name</i></code>. </td>
    </tr>
    <tr>
      <td> <i> key </i> </td>
      <td> The secret key that you set in step 2. </td>
    </tr>
  </table>

5. Optional: Append the returned URL to your cluster name to get a full URL. You can then use the full URL to download objects with any compatible HTTP client such as cURL, wget, or Firefox.
