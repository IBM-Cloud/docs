---

copyright:
  years: 2015, 2017
lastupdated: "2017-02-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

<!-- Acrolinx: 2017-02-23 -->

# Authorization

After you [authenticate](authentication.html),
the next test is to decide whether you can do certain tasks.
This process is called authorization.
{:shortdesc}

## Roles

Role          | Description
--------------|------------
`_reader`     | Gives the user permission to read documents from the database.
`_writer`     | Gives the user permission to create, update, and delete documents (except design documents) in the database.
`_admin`      | Gives the user the ability to change security settings, including adding roles.
`_replicator` | Gives the user permission to replicate a database, including creating checkpoints.
`_db_updates` | Gives the user permission to use the global changes feed.
`_design`     | Gives the user permission to read design documents.
`_shards`     | Gives the user access to the `/$DATABASE/_shards` endpoint.
`_security`   | Gives the user permission to read from the `/_api/v2/db/$DATABASE/_security` endpoint

The credentials that you use to log in to the dashboard automatically have `_admin` permissions to all databases you create.
Everyone and everything else,
including users you share databases with and API keys you create,
must be given a permission level explicitly.

## Viewing Permissions

To see who has permissions to read,
write,
and manage the database,
send a `GET` request to `https://$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security`.

_Example of using an HTTP request to determine permissions:_

```http
GET /_api/v2/db/$DATABASE/_security HTTP/1.1
```
{:codeblock}

_Example of using the command line to determine permissions:_

```sh
curl https://$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security
```
{:codeblock}

<!--

_Example of using JavaScript to determine permissions,:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
account.request({
	db: $DATABASE,
	path: '_security'
	},
	function (err, body, headers) {
		if (!err) {
			console.log(body);
		}
	}
});
```
{:codeblock}

-->

The `cloudant` field in the response object contains an object with keys that are the user names
that have permission to interact with the database.
The `nobody` user name indicates what permissions are available to unauthenticated users,
that is,
any request made without authentication credentials.

In the following example response,
the `nobody` user name has `_reader` permissions.
The effect is that the database is publicly readable.

_Example response to request for permissions:_

```json
{
	"cloudant": {
		"antsellseadespecteposene": [
			"_reader",
			"_writer",
			"_admin"
		],
		"garbados": [
			"_reader",
			"_writer",
			"_admin"
		],
		"nobody": [
			"_reader"
		]
	},
	"_id": "_security"
}
```
{:codeblock}

## Modifying Permissions

To modify who has permissions to read,
write,
or manage a database,
send a `PUT` request to `https://$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security`.
To see what roles you can assign,
see [Roles](#roles).

_Example of using HTTP to send an authorization modification request:_

```http
PUT /_api/v2/db/$DATABASE/_security HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to send an authorization modification request:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security \
	-X PUT \
	-H "Content-Type: application/json" \
	-d "$JSON"
```
{:codeblock}

<!--

_Example of using JavaScript to send an authorization modification request:_

```javascript
var nano = require('nano');
var account = nano("https://"+$USERNAME+":"+$PASSWORD+"@"+$USERNAME+".cloudant.com");
account.request(
	{
		db: $DATABASE,
		path: '_security',
		method: 'PUT',
		body: '$JSON'
	},
	function (err, body, headers) {
		if (!err) {
			console.log(body);
		}
	}
);
```
{:codeblock}

-->

The request must provide a document in JSON format,
describing a `cloudant` field.
The field contains an object with keys that are the user names that have permission to interact with the database.
The `nobody` user name indicates what permissions are available to unauthenticated users,
that is, anybody.

In the following example request,
the `nobody` user name is given `_reader` permissions.
This authorization makes the database publicly readable.

_Example of an authorization modification request document:_

```json
{
	"cloudant": {
		"antsellseadespecteposene": [
			"_reader",
			"_writer",
			"_admin"
		],
		"garbados": [
			"_reader",
			"_writer",
			"_admin"
		],
		"nobody": [
			"_reader"
		]
	}
}
```
{:codeblock}

The response indicates whether the update was successful.

_Example response after a successful authorization modification request:_

```json
{
	"ok" : true
}
```
{:codeblock}

You must run the `GET` command first to retrieve the security object.
Then,
you can modify that security object with new permissions.
If you do not run the `GET` command and retrieve the security object before you run an API call,
the result might disrupt your environment.
For example,
if you want to add a `nobody` user with read-only access,
the  following _incorrect_ request removes _all_ the other users with access to the database.

_Example of an incorrect authorization modification request document:_

```json
{
    "cloudant": {
        "nobody": [
            "_reader"
        ]
    }
}
```
{:codeblock}

## Creating API Keys

>	**Note**: An earlier method of generating API keys by `POST`ing to
the `https://cloudant.com/api/generate_api_key` endpoint is deprecated.

Use API keys to give access to a person or application without creating a new Cloudant account for that person or application.
An API key consists of a randomly generated user name and password.
The key is given the wanted access permissions.

When generated,
the API key can be used in the same way as a normal user account,
for example by granting read,
write,
or admin access permissions.

API keys are not the same as normal user accounts.
In particular,
an API key does not have access to the dashboard.

An API key is primarily used to enable applications to access a database,
with a determined level of access control.

>	**Note**: If you choose to generate an API key through the dashboard,
remember to record the key name and password.
These values are both randomly generated,
and cannot be retrieved if lost or forgotten.

>	**Note**: [IBM Cloudant Data Layer Local Edition ("Cloudant Local") ![External link icon](../images/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSTPQH_1.0.0/com.ibm.cloudant.local.doc/SSTPQH_1.0.0_welcome.html){:new_window}
does not support API Keys.
For a similar capability,
create "CouchDB" style users,
as described in the [IBM Knowledge Center ![External link icon](../images/launch-glyph.svg "External link icon")](http://www-01.ibm.com/support/knowledgecenter/SSTPQH_1.0.0/com.ibm.cloudant.local.install.doc/topics/clinstall_db_security.html){:new_window}.

_Example of using an HTTP request to create an API key:_

```http
POST https://<username>.cloudant.com/_api/v2/api_keys HTTP/1.1
```
{:codeblock}

_Example of using the command line to create an API key:_

```sh
curl -X POST https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/_api/v2/api_keys
```
{:codeblock}

<!--

_Example of using JavaScript to create an API key:_

```javascript
var nano = require('nano');
var account = nano("https://$USERNAME:$PASSWORD@cloudant.com");
account.request(
	{
		db: '_api',
		path: 'v2/api_keys',
		method: 'POST'
	},
	function (err, body) {
		if (!err) {
			console.log(body);
		}
	}
);
```
{:codeblock}

-->

The response contains the generated key and password.

_Example response to request for an API key:_

```json
{
	"password": "YPNCaIX1sJRX5upaL3eqvTfi",
	"ok": true,
	"key": "blentfortedsionstrindigl"
}
```
{:codeblock}

## Using API keys

API keys are typically generated by using an account that has at least one database.

However,
when generated,
it is possible to use the API key with other databases,
or even with other accounts.

By default,
an API key has no permissions for anything.
It must be given permissions explicitly.

After you generate the API key,
grant the key access-specific permissions for a specific database by sending a `PUT` request to 
`https://<username>.cloudant.com/_api/v2/db/<database>/_security`,
as described in [modifying permissions](#modifying-permissions).

The database does not have to be in the same account as the account used for generating the API key initially.

To give an existing API key permissions to access a database in another account,
do the following steps:

1.  Retrieve the existing security permissions for the database, as described [here](#viewing-permissions).
2.  [Add](#modifying-permissions) the details of the API key to the database security permissions, along with the [roles](#roles) required.

For an example of this process,
see the blog article:
[Using a Cloudant API Key with Multiple Cloudant Databases and Accounts ![External link icon](../images/launch-glyph.svg "External link icon")](https://dx13.co.uk/articles/2016/4/11/using-a-cloudant-api-key-with-multiple-cloudant-databases-and-accounts.html){:new_window}.

## Deleting API keys

### To remove an API key by using the Dashboard

1.	Click `Databases` -> `Permissions`.
2.	Hover over the API key you would like to delete.
3.	Click the '`X`' that appears when you hover over the API key.

### To remove an API key by using the Cloudant API

Use the [modifying permissions](#modifying-permissions) technique to remove the API key from the list of users with access permission.

This technique works because an API key is similar to a user,
and is granted access permissions.
By removing the API key from the list of users that have access permissions,
the effect is to delete the API key.

To remove the API key,
send an HTTP `PUT` request to the same `_security` API endpoint you used to [create the API key](#creating-api-keys).
Provide an updated list of the user names that have access permission.
The updated list _must omit_ the API key.

## Enabling the `_users` database with Cloudant

You can use the
[_users database ![External link icon](../images/launch-glyph.svg "External link icon")](http://docs.couchdb.org/en/1.6.1/intro/security.html#authentication-database){:new_window}
to manage roles in Cloudant.
However,
you must turn off Cloudant security for those roles first,
by sending a JSON document to the `_security` endpoint of the database.
For example, `https://<username>.cloudant.com/<database>/_security`.

_Example of using HTTP to submit a modification request:_

```http
PUT /$DATABASE/_security HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of using the command line to submit a modification request:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/$DATABASE/_security \
	-X PUT \
	-H "Content-Type: application/json" \
	-d @request-body.json
```
{:codeblock}

_Example modification request, in JSON format:_

```json
{
	"couchdb_auth_only": true,
	"members": {
		"names": ["member"],"roles":[]
	},
	"admins": {
		"names": ["admin"],"roles":[]
	}
}
```
{:codeblock}

_Example response:_

```json
{
	"ok" : true
}
```
{:codeblock}
