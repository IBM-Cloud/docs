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

# HTTP

This section provides details of the [HTTP Headers](#http-headers)
and [HTTP Status Codes](#http-status-codes) you need to know when using Cloudant.
{:shortdesc}

## HTTP Headers

Because Cloudant uses HTTP for all external communication,
you need to ensure that the correct HTTP request headers are supplied and processed on retrieval.
This is to ensure that you get the correct format and encoding.
Different environments and clients are more or less strict on the effect of these HTTP headers,
especially when they are not present.
To reduce the likelihood of problems or unexpected behavior,
you should be as specific as possible.

### Request headers

The supported HTTP request headers include:

*	[`Accept`](#accept)
*	[`Content-Type`](#content-type)
*	[`Content-Encoding`](#content-encoding)
*	[`If-None-Match`](#if-none-match)

#### Accept

The `Accept` header specifies the list of potential data types returned by the server that would be
accepted and understood by the client.
The format is a list of one or more MIME types,
separated by colons.

For the majority of requests,
the accepted list should include JSON data (`application/json`).

For attachments,
you can either specify the MIME type explicitly,
or use `*/*` to specify that all file types are supported.

If the `Accept` header is not supplied,
then the server assumes the`*/*` MIME type,
which means that the client accepts all formats.

_Example of sending a request without an explicit `Accept` header, or when specifying `*/*`:

```http
GET /recipes HTTP/1.1
Host: username.cloudant.com
Accept: */*
```
{:codeblock}

_Example of a returned header when the client is assumed to accept all formats:_

>	**Note**: The returned content type is `text/plain`
even though the information returned by the request is in JSON format.

```
Server: CouchDB/1.0.2 (Erlang OTP/R14B)
Date: Thu, 13 Jan 2011 13:39:34 GMT
Content-Type: text/plain;charset=utf-8
Content-Length: #7
Cache-Control: must-revalidate
```
{:codeblock}

The use of `Accept` in queries to Cloudant is not required,
but is highly recommended as it helps to ensure that the data returned can be processed by the client.

If you specify a data type using the `Accept` header,
Cloudant honors the specified type in the `Content-type` header field of responses.
For example,
if you explicitly request `application/json` in the `Accept` of a request,
the returned HTTP headers use this value in the returned `Content-type` field.

_Example request that explicitly specifies the `Accept` header:_

```http
GET /recipes HTTP/1.1
Host: username.cloudant.com
Accept: application/json
```
{:codeblock}

_Example of the headers returned in response, including the `application/json` content type:_

```
Server: CouchDB/1.0.2 (Erlang OTP/R14B)
Date: Thu, 13 Jan 2011 13:40:11 GMT
Content-Type: application/json
Content-Length: #7
Cache-Control: must-revalidate
```
{:codeblock}

#### Content-Type

The `Content-Type` header specifies the content type of the information being supplied within the request.
The specification uses MIME type specifications.
For the majority of requests,
the content type is JSON (`application/json`).

For some settings the MIME type is plain text.

In particular,
when uploading attachments the type should be the corresponding
MIME type for the attachment or binary (`application/octet-stream`).

The use of the `Content-type` on a request is highly recommended.

#### Content-Encoding

The `Content-Encoding` header specifies the encoding of the request body.
Supported values are `gzip` and `deflate`.
If the header is used,
the request body must be encoded using the corresponding format.

_Example of creating a gzipped request body:_

```sh
# create gzipped document
echo '{"foo":"bar"}' | gzip >doc.gzip
```
{:codeblock}

_Example of sending a gzip-encoded request body to create a document, using HTTP:_

```http
PUT /db/doc HTTP/1.1
HOST: example.cloudant.com
Content-Encoding: gzip
```
{:codeblock}

_Example of sending a gzip-encoded request body to create a document, using the command line:_

```sh
curl https://example.cloudant.com/db/doc \
	-X PUT \
	-T doc.gzip \
	-H 'Content-Encoding: gzip'
```
{:codeblock}

#### If-None-Match

The `If-None-Match` header is optional.
You might send it to determine whether a document has been modified since it was last read or updated.
The value of the `If-None-Match` header should match the last [`Etag`](#etag) value received.
If the value matches the current revision of the document,
the server sends a [`304 Not Modified`](#304) status code,
and the response itself has no body.

If the document has been modified,
you should get a normal [`200` response](#200),
provided the document still exists and no other errors occurred.

### Response Headers

Response headers are returned by the server when sending back content.
They include a number of different fields,
many of which are standard HTTP response headers and have no significance regarding how Cloudant operates.
The list of response headers important to Cloudant are as follows.

The supported HTTP response headers include:

*	[`Cache-Control`](#cache-control)
*	[`Content-Length`](#content-length)
*	[`Content-Type`](#content-type)
*	[`Etag`](#etag)

The Cloudant design document API and the functions when returning HTML (for example as part of a show or list)
enable you to include custom HTTP headers through the `headers` field of the return object.

#### Cache-Control

The `Cache-Control` HTTP response header provides a suggestion for client caching mechanisms
on how to treat the returned information.
Cloudant typically returns the `must-revalidate` value,
which indicates that the information should be revalidated if possible.
This is used to ensure that the dynamic nature of the content is correctly updated.

#### Content-Length

The `Content-Length` header reports the length in bytes of the returned content.

<div id="content-type-response"></div>

<div id="content-type-field"></div>

#### Content-Type

The `Content-Type` header specifies the MIME type of the returned data.
For most request,
the returned MIME type is `text/plain`.
All text is encoded in Unicode (UTF-8),
which is explicitly stated in the returned `Content-Type` as `text/plain;charset=utf-8`.

#### Etag

The `Etag` header is used to show the revision for a document,
or the response from a show function.
For documents,
the value is identical to the revision of the document.
The value can be used with an `If-None-Match` request header
to get a [`304 Not Modified`](#304) response if the revision is still current.

ETags cannot currently be used with views or lists,
since the ETags returned from those requests are just random numbers that change on every request.

## HTTP Status Codes

With the interface to Cloudant working through HTTP,
error codes and statuses are reported using a combination of the HTTP status code number,
and corresponding data in the body of the response data.

A list of the error codes returned by Cloudant and generic descriptions of the related errors are as follows.
The meaning of different status codes for specific request types are provided in the corresponding API call reference.

<div id="201"></div>

<div id="202"></div>

<div id="304"></div>

<div id="400"></div>

<div id="403"></div>

<div id="404"></div>

<div id="405"></div>

<div id="409"></div>

<div id="413"></div>

<div id="429"></div>

<div id="500"></div>

<div id="503"></div>


Code                                    | Meaning
----------------------------------------|--------
`200 - OK`                              | Request completed successfully.
`201 - Created`                         | Resource created or updated successfully. The resource could be a database or a document, for example.
`202 - Accepted`                        | Request has been accepted, but the [quorum](document.html#quorum) for the operation was not met.
`304 - Not Modified`                    | The content requested has not been modified. This is used with the [ETag](#etag) system to identify the version of information returned.
`400 - Bad Request`                     | Bad request structure. The error can indicate an error with the request URL, path or headers. Differences in the supplied MD5 hash and content also trigger this error, as this may indicate message corruption.
`401 - Unauthorized`                    | The item requested was not available using the supplied authorization, or authorization was not supplied.
`403 - Forbidden`                       | The requested item or operation is forbidden.
`404 - Not Found`                       | The requested resource could not be found. The content includes further information as a JSON object, if available. The structure contains two keys, `error` and `reason`, similar to the following example: `{ "error":"not_found", "reason":"no_db_file" }`
`405 - Resource Not Allowed`            | A request was made using an invalid HTTP request type for the URL requested. For example, you have requested a `PUT` when a `POST` is required. Errors of this type can also be triggered by invalid URL strings.
`406 - Not Acceptable`                  | The requested content type is not supported by the server.
`409 - Conflict`                        | Request resulted in an update conflict.
`412 - Precondition Failed`             | The request headers from the client and the capabilities of the server do not match.
`413 - Request Entity Too Large`        | The maximum request body size for an API request sent to Cloudant on IBM Bluemix is 1 MB.
`415 - Bad Content Type`                | The content types supported, and the content type of the information being requested or submitted indicate that the content type is not supported.
`416 - Requested Range Not Satisfiable` | The range specified in the request header cannot be satisfied by the server.
`417 - Expectation Failed`              | When sending documents in bulk, the bulk load operation failed.
`429 - Too Many Requests`               | The user has sent too many requests in a given amount of time. More information is available in the corresponding [RFC 6585 ![External link icon](../images/launch-glyph.svg "External link icon")](https://tools.ietf.org/html/rfc6585#page-3){:new_window}.
`500 - Internal Server Error`           | The request was invalid, either because the supplied JSON was invalid, or invalid information was supplied as part of the request. Alternatively, a replication was canceled while in progress.
`503 - Service Unavailable`             | The request could not be processed. Seeing this response following a Cloudant request might indicate an misspelled Cloudant account name.
