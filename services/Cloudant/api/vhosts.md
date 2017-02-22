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

# Virtual hosts

Virtual hosts (vhosts) are a way to make Cloudant serve data from a different domain
than the one normally associated with your Cloudant account.
{:shortdesc}

You can create as many vhosts as needed
and point them to any endpoint in your Cloudant account.
Vhosts are often used to point to a `_rewrite` endpoint of a design document
in order to use Cloudant as a web server.
You need to have the admin role in order to use any of the vhost endpoints.

## Listing virtual hosts

To list all virtual hosts in your account,
send a `GET` request to `/_api/v2/user/virtual_hosts`.

The JSON response details all of the virtual hosts,
and any virtual path associated with each host.

_Example request to list all vhosts, using HTTP:_

```http
GET /_api/v2/user/virtual_hosts HTTP/1.1
Host: $ACCOUNT.cloudant.com
```
{:codeblock}

_Example request to list all vhosts, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/_api/v2/user/virtual_hosts"
```
{:codeblock}

_Example response, list all vhosts:_

```json
{
    "virtual_hosts": [
        [
            "system1.business.org", 
            ""
        ], 
        [
            "system2.business.org", 
            "/specificpath"
        ]
    ]
}
```
{:codeblock}

## Creating a virtual host

To create a virtual host,
send a `POST` request to the `/_api/v2/user/virtual_hosts` endpoint,
with a description of the vhost as a JSON object within the request body.
The JSON document contains these fields:

Field  | Purpose
-------|--------
`host` | The domain name you want to use for the vhost.
`path` | An (optional) endpoint in your Cloudant account the vhost should point to.

_Example request for creating a vhost, using HTTP:_

```http
POST /_api/v2/user/virtual_hosts HTTP/1.1
Host: $ACCOUNT.cloudant.com
Content-Type: application/json
```
{:codeblock}

_Example request for creating a vhost, using the command line:_

```sh
curl "https://$ACCOUNT.cloudant.com/_api/v2/user/virtual_hosts" -X POST -d '@vhost.json' -H 'Content-Type: application/json'
```
{:codeblock}

_Example JSON describing the required vhost:_

```json
{
    "host": "www.example.com",
    "path": "/_api/v2/user/virtual_hosts"
}
```
{:codeblock}

_Example response to request for a vhost:_

```json
{
  "ok": true
}
```
{:codeblock}

## Deleting a virtual host

To delete a vhost,
send a `DELETE` request to `/_api/v2/user/virtual_hosts`.

Specify the host to delete within the request body,
as shown in the following example.

_Example request for deleting a vhost, using HTTP:_

```http
DELETE /_api/v2/user/virtual_hosts HTTP/1.1
Host: $ACCOUNT.cloudant.com
Content-Type: application/json
```
{:codeblock}

_Example request for deleting a vhost, using the command line:_

```sh
curl "https://account.cloudant.com/_api/v2/user/virtual_hosts" -X DELETE -d '@vhost.json' -H 'Content-Type: application/json'
```
{:codeblock}

_Example JSON describing the vhost to delete:_

```json
{
  "host": "www.example.com"
}
```
{:codeblock}

_Example response to vhost delete request:_

```json
{
  "ok": true
}
```
{:codeblock}
