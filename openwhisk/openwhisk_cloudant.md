---

copyright:
  years: 2016, 2017
lastupdated: "2017-06-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Using the Cloudant package
{: #openwhisk_catalog_cloudant}
The `/whisk.system/cloudant` package enables you to work with a Cloudant database. It includes the following actions and feeds.

| Entity | Type | Parameters | Description |
| --- | --- | --- | --- |
| `/whisk.system/cloudant` | package | dbname, host, username, password | Work with a Cloudant database |
| `/whisk.system/cloudant/read` | action | dbname, id | Read a document from a database |
| `/whisk.system/cloudant/write` | action | dbname, overwrite, doc | Write a document to a database |
| `/whisk.system/cloudant/changes` | feed | dbname, filter, query_params, maxTriggers | Fire trigger events on changes to a database |

The following topics walk through setting up a Cloudant database, configuring an associated package, and using the actions and feeds in the `/whisk.system/cloudant` package.

## Setting up a Cloudant database in Bluemix
{: #openwhisk_catalog_cloudant_in}

If you're using OpenWhisk from Bluemix, OpenWhisk automatically creates package bindings for your Bluemix Cloudant service instances. If you're not using OpenWhisk and Cloudant from Bluemix, skip to the next step.

1. Create a Cloudant service instance in your Bluemix [dashboard](http://console.ng.Bluemix.net).

  Be sure to remember the name of the service instance and the Bluemix organization and space you're in.

2. Make sure your OpenWhisk CLI is in the namespace corresponding to the Bluemix organization and space that you used in the previous step.

  ```
  wsk property set --namespace myBluemixOrg_myBluemixSpace
  ```
  {: pre}

  Alternatively, you can use `wsk property set --namespace` to set a namespace from a list of those accessible to you.

3. Refresh the packages in your namespace. The refresh automatically creates a package binding for the Cloudant service instance that you created.

  ```
  wsk package refresh
  ```
  {: pre}
  ```
  created bindings:
  Bluemix_testCloudant_Credentials-1
  ```

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 private binding
  ```

  You see the fully qualified name of the package binding that corresponds to your Bluemix Cloudant service instance.

4. Check to see that the package binding that was created previously is configured with your Cloudant Bluemix service instance host and credentials.

  ```
  wsk package get /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1 parameters
  ```
  {: pre}
  ```
  ok: got package /myBluemixOrg_myBluemixSpace/Bluemix_testCloudant_Credentials-1, displaying field parameters
  ```
  ```json
  [
      {
          "key": "username",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix"
      },
      {
          "key": "host",
          "value": "cdb18832-2bbb-4df2-b7b1-Bluemix.cloudant.com"
      },
      {
          "key": "password",
          "value": "c9088667484a9ac827daf8884972737"
      }
  ]
  ```

## Setting up a Cloudant database outside Bluemix
{: #openwhisk_catalog_cloudant_outside}

If you're not using OpenWhisk in Bluemix or if you want to set up your Cloudant database outside of Bluemix, you must manually create a package binding for your Cloudant account. You need the Cloudant account host name, user name, and password.

1. Create a package binding that is configured for your Cloudant account.

  ```
  wsk package bind /whisk.system/cloudant myCloudant -p username MYUSERNAME -p password MYPASSWORD -p host MYCLOUDANTACCOUNT.cloudant.com
  ```
  {: pre}
  

2. Verify that the package binding exists.

  ```
  wsk package list
  ```
  {: pre}
  ```
  packages
  /myNamespace/myCloudant private binding
  ```


## Listening for changes to a Cloudant database
{: #openwhisk_catalog_cloudant_listen}

### Filter database change events

You can define a filter function, to avoid having unnecessary change events firing your trigger.

To create a new filter function you can use an action.

Create a json document file `design_doc.json` with the following filter function
```json
{
  "doc": {
    "_id": "_design/mailbox",
    "filters": {
      "by_status": "function(doc, req){if (doc.status != req.query.status){return false;} return true;}"
    }
  }
}
```

Create a new design document on the database with the filter function

```
wsk action invoke /_/myCloudant/write -p dbname testdb -p overwrite true -P design_doc.json -r
```
The information for the new design document is printed on the screen.
```json
{
    "id": "_design/mailbox",
    "ok": true,
    "rev": "1-5c361ed5141bc7856d4d7c24e4daddfd"
}
```

### Create the trigger using the filter function

You can use the `changes` feed to configure a service to fire a trigger on every change to your Cloudant database. The parameters are as follows:

- `dbname`: Name of Cloudant database.
- `maxTriggers`: Stop firing triggers when this limit is reached. Defaults to infinite.
- `filter`: Filter function defined on a design document.
- `query_params`: Optional query parameters for the filter function.


1. Create a trigger with the `changes` feed in the package binding that you created previously including `filter` and `query_params` to only fire the trigger when a document is added or modified when the status is `new`.
Be sure to replace `/_/myCloudant` with your package name.

  ```
  wsk trigger create myCloudantTrigger --feed /_/myCloudant/changes \
  --param dbname testdb \
  --param filter "mailbox/by_status" \
  --param query_params '{"status":"new"}'
  ```
  {: pre}
  ```
  ok: created trigger feed myCloudantTrigger
  ```

2. Poll for activations.

  ```
  wsk activation poll
  ```
  {: pre}

3. In your Cloudant dashboard, either modify an existing document or create a new one.

4. Observe new activations for the `myCloudantTrigger` trigger for each document change only if the document status is `new` based on the filter function and query parameter.
  
  **Note**: If you are unable to observe new activations, see the subsequent sections on reading from and writing to a Cloudant database. Testing the following reading and writing steps will help verify that your Cloudant credentials are correct.
  
  You can now create rules and associate them to actions to react to the document updates.
  
  The content of the generated events has the following parameters:
  
  - `id`: The document ID.
  - `seq`: The sequence identifier that is generated by Cloudant.
  - `changes`: An array of objects, each of which has a `rev` field that contains the revision ID of the document.
  
  The JSON representation of the trigger event is as follows:
  
  ```json
  {
      "id": "6ca436c44074c4c2aa6a40c9a188b348",
      "seq": "2-g1AAAAL9aJyV-GJCaEuqx4-BktQkYp_dmIfC",
      "changes": [
          {
              "rev": "2-da3f80848a480379486fb4a2ad98fa16"
          }
      ]
  }
  ```
  
## Writing to a Cloudant database
{: #openwhisk_catalog_cloudant_write}

You can use an action to store a document in a Cloudant database called `testdb`. Make sure that this database exists in your Cloudant account.

1. Store a document by using the `write` action in the package binding you created previously. Be sure to replace `/_/myCloudant` with your package name.

  ```
  wsk action invoke /_/myCloudant/write --blocking --result --param dbname testdb --param doc "{\"_id\":\"heisenberg\",\"name\":\"Walter White\"}"
  ```
  ```
  ok: invoked /_/myCloudant/write with id 62bf696b38464fd1bcaff216a68b8287
  ```
  ```json
  {
    "id": "heisenberg",
    "ok": true,
    "rev": "1-9a94fb93abc88d8863781a248f63c8c3"
  }
  ```

2. Verify that the document exists by browsing for it in your Cloudant dashboard.

  The dashboard URL for the `testdb` database looks something like the following: `https://MYCLOUDANTACCOUNT.cloudant.com/dashboard.html#database/testdb/_all_docs?limit=100`.


## Reading from a Cloudant database
{: #openwhisk_catalog_cloudant_read}

You can use an action to fetch a document from a Cloudant database called `testdb`. Make sure that this database exists in your Cloudant account.

- Fetch a document by using the `read` action in the package binding that you created previously. Be sure to replace `/_/myCloudant` with your package name.

  ```
  wsk action invoke /_/myCloudant/read --blocking --result --param dbname testdb --param id heisenberg
  ```
  {: pre}
  ```json
  {
    "_id": "heisenberg",
    "_rev": "1-9a94fb93abc88d8863781a248f63c8c3",
    "name": "Walter White"
  }
  ```

## Using an action sequence and a change trigger to process a document from a Cloudant database
{: #openwhisk_catalog_cloudant_read_change notoc}

You can use an action sequence in a rule to fetch and process the document associated with a Cloudant change event.

Here is a sample code of an action that handles a document:
```javascript
function main(doc){
  return { "isWalter:" : doc.name === "Walter White"};
}
```

Create the action to process the document from Cloudant:
```
wsk action create myAction myAction.js
```
{: pre}

To read a document from the database, you can use the `read` action from the Cloudant package.
The `read` action may be composed with `myAction` to create an action sequence.
```
wsk action create sequenceAction --sequence /_/myCloudant/read,myAction
```
{: pre}

The action `sequenceAction` may be used in a rule that activates the action on new Cloudant trigger events.
```
wsk rule create myRule myCloudantTrigger sequenceAction
```
{: pre}

**Note** The Cloudant `changes` trigger used to support the parameter `includeDoc` which is not longer supported.
  You will need to recreate triggers previously created with `includeDoc`. Follow these steps to recreate the trigger:
  ```
  wsk trigger delete myCloudantTrigger
  ```
  {: pre}
  ```
  wsk trigger create myCloudantTrigger --feed /_/myCloudant/changes --param dbname testdb
  ```
  {: pre}

  The example illustrated above may be used to create an action sequence to read the changed document and call your existing actions.
  Remember to disable any rules that may no longer be valid and create new ones using the action sequence pattern.

