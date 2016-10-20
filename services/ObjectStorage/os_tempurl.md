---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Creating a temporary URL {: #create-temporary-url}

*Last updated: 19 October 2016*
{: .last-updated}

A temporary URL is a long, difficult-to-guess URL that can be used for a specified period to download objects without requiring further authentication.
{: shortdesc}


1. Identify your authentication information by printing your account information with the following command:

    ```
    swift stat
    ```
    {: pre}
    
    **Note**: Locate the Account field and note the full string behind *Account*: including `AUTH_`.
2. Set a secret key. This key can be anything that you select, but best practice is that you select a long, random, and hard to guess string. To set the key, run the following command:

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
      <tr>
        <th> Argument </th>
        <th> Description </th>
      </tr>
      <tr>
        <td> [method] </td>
        <td> GET to allow download. PUT to allow upload. </td>
      </tr>
      <tr>
        <td> [seconds] </td>
        <td> Time in seconds that the temporary URL will be available. </td>
      </tr>
      <tr>
        <td> [path] </td>
        <td> The full path of the object expressed as `/v1/<auth_account>/<container_name>/<object_name>`. For more information, see the [{{site.data.keyword.objectstorageshort}} URL documentation](/os_api.html#access-points). </td>
      </tr>
      <tr>
        <td> [key] </td>
        <td> The secret key that you set in step 2. </td>
      </tr>
    </table>
    *Table 2: tempurl positional arguments*
5. (*Optional*): Append the returned URL to your cluster name to get a full URL. You can then use the full URL to download objects with any compatible HTTP client such as cURL, wget, or Firefox.
