---

copyright:
  years: 2015, 2017
lastupdated: "2017-01-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Authorization

When you have [authenticated](authentication.html),
the next test is to decide whether you are permitted to perform certain tasks.
This is called authorization.
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

The credentials you use to log in to the dashboard automatically have `_admin` permissions to all databases you create.
Everyone and everything else,
including users you share databases with and API keys you create,
must be given a permission level explicitly.

## Viewing Permissions

To see who has permissions to read,
write,
and manage the database,
send a `GET` request to `https://$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security`.

_Example request to determine permissions, using HTTP:_

```http
GET /_api/v2/db/$DATABASE/_security HTTP/1.1
```
{:codeblock}

_Example request to determine permissions, using the command line:_

```sh
curl https://$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security
```
{:codeblock}

<!--

_Example request to determine permissions, using Javascript:_

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

The `cloudant` field in the response object contains an object with keys that are the usernames
that have permission to interact with the database.
The `nobody` username indicates what rights are available to unauthenticated users,
that is,
any request made without authentication credentials.

In the following example response,
the `nobody` username has `_reader` permissions.
This means that the database is publicly readable.

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

_Example of sending an authorization modification request, using HTTP:_

```http
PUT /_api/v2/db/$DATABASE/_security HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example of sending an authorization modification request, using the command line:_

```sh
curl https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/_api/v2/db/$DATABASE/_security \
	-X PUT \
	-H "Content-Type: application/json" \
	-d "$JSON"
```
{:codeblock}

<!--

_Example of sending an authorization modification request, using Javascript:_

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
The field contains an object with keys that are the usernames having permission to interact with the database.
The `nobody` username indicates what rights are available to unauthenticated users,
that is, anybody.

In the following example request,
the `nobody` username is given `_reader` permissions.
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

The response tells you whether the update has been successful.

_Example response following a successful authorization modification request:_

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
if you want to add a new `nobody` user with read-only access,
the  following incorrect request removes _all_ the other users with access to the database.

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

API keys allow you to give access to a person or application without having to create a new Cloudant account.
An API key consists of a randomly generated username and password.
The key is given the desired access permissions.

Once generated,
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
These are both randomly generated,
and cannot be retrieved if lost or forgotten.

>	**Note**: [IBM Cloudant Data Layer Local Edition ("Cloudant Local") ![External link icon](../images/launch-glyph.svg "External link icon")](https://www.ibm.com/support/knowledgecenter/SSTPQH_1.0.0/com.ibm.cloudant.local.doc/SSTPQH_1.0.0_welcome.html){:new_window}
does not support API Keys.
For a similar capability,
create "CouchDB" style users,
as described in the [IBM Knowledge Center ![External link icon](../images/launch-glyph.svg "External link icon")](http://www-01.ibm.com/support/knowledgecenter/SSTPQH_1.0.0/com.ibm.cloudant.local.install.doc/topics/clinstall_db_security.html){:new_window}.

_Example request to create an API key, using HTTP:_

```http
POST https://<username>.cloudant.com/_api/v2/api_keys HTTP/1.1
```
{:codeblock}

_Example request to create an API key, using the command line:_

```sh
curl -X POST https://$USERNAME:$PASSWORD@$USERNAME.cloudant.com/_api/v2/api_keys
```
{:codeblock}

<!--

_Example request to create an API key, using Javascript:_

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

When you have generated an API key,
you can assign the API key to a database by sending a `PUT` request to
`https://<username>.cloudant.com/_api/v2/db/<database>/_security`.
Once assigned to a database,
the key can be granted access permissions.
By default,
an API key has no permissions for anything,
and must be given permissions explicitly.

## Deleting API keys

### To remove an API key using the Dashboard

1.	Click on `Databases` -> `Permissions`.
2.	Hover over the API key you would like to delete.
3.	Click the '`X`' that appears when you hover over the API key.

### To remove an API key using the Cloudant API

Use the [modifying permissions](#modifying-permissions) technique to remove the API key from the list of users with access permission.

This works because an API key is similar to a user,
and has been granted access permissions.
By removing the API key from the list of users that have access permissions,
the effect is to delete the API key.

To remove the API key,
send an HTTP `PUT` request to the same `_security` API endpoint you used to [create the API key](#creating-api-keys).
Provide an updated list of the usernames that have access permission.
The updated list should _omit_ the API key.

## Enabling the `_users` database with Cloudant

You can use the
[_users database ![External link icon](../images/launch-glyph.svg "External link icon")](http://docs.couchdb.org/en/1.6.1/intro/security.html#authentication-database){:new_window}
to manage roles in Cloudant.
However,
you must turn off Cloudant security for those roles first.
To do this,
`PUT` a JSON document to the `_security` endpoint of the database.
For example, `https://<username>.cloudant.com/<database>/_security`.

_Example submission of a modification request, using HTTP:_

```http
PUT /$DATABASE/_security HTTP/1.1
Content-Type: application/json
```
{:codeblock}

_Example submission of a modification request, using the command line:_

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
