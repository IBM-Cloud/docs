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

# Account

Your account is your entry point for the {{site.data.keyword.cloudant}} API.
You access your account using the address prefix
`https://$ACCOUNT.cloudant.com`.
Your Cloudant dashboard is always
`https://$ACCOUNT.cloudant.com/dashboard.html`.
{:shortdesc}

If you don't yet have an account, [sign up ![External link icon](../images/launch-glyph.svg "External link icon")](https://cloudant.com/sign-up/){:new_window}.

## Ping

To see if your Cloudant account is accessible,
make a `GET` against `https://$ACCOUNT.cloudant.com`.
If you misspelled your account name,
you might get a [503 'service unavailable' error](http.html#503).

_Example of connecting to your Cloudant account, using HTTP:_

```HTTP
GET / HTTP/1.1
HOST: $ACCOUNT.cloudant.com
```
{:codeblock}

_Example of connecting to your Cloudant account, using the command line:_

```sh
curl -u $ACCOUNT https://$ACCOUNT.cloudant.com
```
{:codeblock}

<!--

_Example of connecting to your Cloudant account, using Javascript:_

```javascript
var nano = require('nano');
var account = nano("https://$ACCOUNT:$PASSWORD@$ACCOUNT.cloudant.com");
account.request(function (err, body) {
	if (!err) {
		console.log(body);
	}
});
```
{:codeblock}

-->

_Example of connecting to your Cloudant account, using Python:_

```python
import cloudant
account = cloudant.Account(USERNAME)
ping = account.get()
print ping.status_code
# Expected return code: 200
```
{:codeblock}

## CORS

[Cross-origin resource sharing (CORS) ![External link icon](../images/launch-glyph.svg "External link icon")](http://www.w3.org/TR/cors/){:new_window} is a
mechanism that allows Javascript from another domain to interact with data in
your Cloudant account.

More information about CORS and Cloudant is available [here](cors.html).
