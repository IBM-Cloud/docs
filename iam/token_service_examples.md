---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-07-10"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Token Service examples
{: #token_service_examples}

The following is a list of the most common use cases in the Token Service. For additional details, see the [Token Service API](https://console.bluemix.net/apidocs/713-token-service-api?=undefined&language=node&env_id=ibm:yp:us-south#introduction).

**Note:** Access tokens are valid for roughly an hour, but they can be regenerated as needed, and refresh tokens are valid for 30 days.

To logout of IAM, navigate your browser to https://iam.ng.bluemix.net/oidc/logout. This will remove cookies that IAM keeps and remove cookies that BlueId potentially keeps, but it will not remove cookies from e.g. `w3id`. Make sure your service invalidates its session and cookies before calling IAM for logout.

<!---
* [Get an IAM token using an LTPA cookie](token_service_examples.html#iam_ltpa)
* [Get IAM or UAA tokens using an LTPA cookie](token_service_examples.html#iam_uaa_using_ltpa)
* [Get IAM or IMS tokens using an LTPA cookie](token_service_examples.html#iam_ims_using_ltpa)
* [Get an IAM or IMS token plus an IAM cookie using an LTPA cookie](token_service_examples.html#iam_ims_plus_iam_cookie_using_ltpa)
* [Get an IAM token using an IAM cookie](token_service_examples.html#iam_token_using_iam_cookie)
* [Refresh token](token_service_examples.html#refresh_token)
* [Get UAA and IMS tokens using IAM token](token_service_examples.html#uaa_ims_using_iam_token)
* [Get an IMS token with a new account using an IAM token](token_service_examples.html#ims_token_new_account_using_iam_token)
* [Get an IAM token using an IMS token](token_service_examples.html#iam_token_using_ims_token)
* [Get an IAM token using an API Key](token_service_examples.html#iam_token_using_api_key)
* [Recommended user authentication flow](token_service_examples.html#iam_auth)
-->


## 1. Get an IAM token using an LTPA cookie.
{: #iam_ltpa}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:identity-cookie
- response_type=cloud_iam
- cookie=*[LTPA cookie]*

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:identity-cookie&response_type=cloud_iam&cookie=<LTPA cookie value>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```


## 2. Get IAM or UAA tokens using an LTPA cookie.
{: #iam_uaa_using_ltpa}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:identity-cookie
- response_type=cloud_iam, uaa
- cookie=*[LTPA cookie]*
- uaa_client_id=*[your UAA client ID]*
- uaa_client_secret=*[your UAA client secret]*
- uaa_scope=openid

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:identity-cookie&response_type=cloud_iam,uaa&uaa_client_id=<clientID>&uaa_client_secret=<clientSecret>&uaa_scope=openid" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "uaa_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 3. Get IAM or IMS tokens using an LTPA cookie.
{: #iam_ims_using_ltpa}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:identity-cookie
- response_type=cloud_iam, ims_portal
- cookie=*[LTPA cookie]*
- ims_account=*[IMS account number]*

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:identity-cookie&response_type=cloud_iam,ims_portal&ims_account=<99999>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "ims_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "ims_user_id": 999999,
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 4. Get an IAM or IMS token plus an IAM cookie using an LTPA cookie.
{: #iam_ims_plus_iam_cookie_using_ltpa}

The IAM cookie preserves the account information and 2FA state of a `refreshToken`.

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:identity-cookie
- response_type=cloud_iam, ims_portal, iam_cookie
- cookie=*[LTPA cookie]*
- ims_account=*[IMS account number]*
- receiver_client_ids=*[comma_seperated_list_of_client_ids]* (e.g. *bitnNYn9AH,RENfci0FGJ*)

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:identity-cookie&response_type=cloud_iam,ims_portal,iam_cookie&ims_account=<99999>&receiver_client_ids=bitnNYn9AH,RENfci0FGJ" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "ims_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "iam_cookie": "...",
  "ims_user_id": 999999,
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 5. Get an IAM token using an IAM cookie.
{: #iam_token_using_iam_cookie}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:iam-cookie
- response_type=cloud_iam
- cookie=*[IAM cookie]*

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:iam-cookie&response_type=cloud_iam&cookie=<LTPA cookie value>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 6. Refresh token
{: #refresh_token}

Every IAM (Identity and Access Management) and UAA (User Account and Authentication) access token that is issued via the API expires after one hour. You must refresh your access tokens on a regular basis to assure access to the IBM Bluemix Container Service API. 

Before you begin, make sure that you have an IAM refresh token that you can use to request new access tokens. Use the following steps if you want to refresh your IAM, your UAA, or both tokens.

```
POST https://iam.ng.bluemix.net/oidc/token
```
{: codeblock}

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=refresh_token
- response_type=cloud_iam, uaa
- refresh_token=*[iam_refresh_token]*
- uaa_client_id=cf
- uaa_client_secret=

**Note** Add the uaa_client_secret key with no value specified.

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=refresh_token&response_type=cloud_iam&refreshed_token=SPrXw5tBE3......KBQ+luWQVY=" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "<iam_token>",
  "refresh_token": "<iam_refresh_token>",
  "uaa_token": "<uaa_token>",
  "uaa_refresh_token": "<uaa_refresh_token>",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1493747503
}
```
{: codeblock}


## 7. Get UAA and IMS tokens using IAM token
{: #uaa_ims_using_iam_token}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:derive
- response_type=uaa, ims_portal
- access_token=*[iam_token]*
- ims_account=*[IMS account number]*
- uaa_client_id=*[your UAA client ID]*
- uaa_client_secret=*[your UAA client secret]*
- uaa_scope=openid

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:derive&response_type=uaa,ims_portal&ims_account=<99999>&uaa_client_id=<clientID>&uaa_client_secret=<clientSecret>&uaa_scope=openid&access_token=<iamtoken>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "uaa_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "ims_token": "sdhSFLkkjsdiOi......asdajkhKJSs",
  "ims_user_id": 999999,
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 8. Get an IMS token with a new account using an IAM token.
{: #ims_token_new_account_using_iam_token}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:derive
- response_type=cloud_iam, ims_portal
- access_token=*[iam_token]*
- ims_account=*[IMS account number]*

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:derive&access_token=<iamtoken>&response_type=cloud_iam,ims_portal&ims_account<9999>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "access_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "ims_token": "sdhSFLkkjsdiOi......asdajkhKJSs",
  "ims_user_id": 999999,
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 9. Get an IAM token using an IMS token.
{: #iam_token_using_ims_token}

**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:ims-portal
- response_type=cloud_iam
- ims_portal_token=*[ims portal token]*
- ims_user_id=*[ims user id]*

```
curl -u "<clientid>:<secret>" -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:ims_portal&response_type=cloud_iam&ims_portal_token=<ims_token>&ims_user_id=<user id>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 10. Get an IAM token using an API Key.
{: #iam_token_using_api_key}

**POST** /oidc/token

headers:
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- grant_type=urn:ibm:params:oauth:grant-type:apikey
- response_type=cloud_iam
- apikey=*[Api key]*

```
curl -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "grant_type=urn:ibm:params:oauth:grant-type:apikey&response_type=cloud_iam&apikey=<api key>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJhbGciOiJIUz......sgrKIi8hdFs",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
{: codeblock}


## 11. Recommended User Authentication Flow
{: #iam_auth}

**Step 1:** Redirect browser to `https://<tokenservice-URL>/oidcauthorize?client_id=<your-client-id>&redirect_uri=<your-callback-uri>`

-> login prompt will show up

-> User enters credentials

-> browser callback to redirect uri providing a "code" response parameter


**Step 2:** Exchange the code for an access token calling
 
**POST** /oidc/token

headers:
- Authorization: Basic *[client id]:[client secret]*
- Content-Type: application/x-www-form-urlencoded
- Accept: application/json

with parameters:
- client_id=*[client id]*
- client_secret=*[client secret]*
- grant_type=authorization_code
- response_type=cloud_iam
- code=*[code from callback]*

```
curl -k -X POST --header "Content-Type: application/x-www-form-urlencoded" --header "Accept: application/json" 
-d "client_id=<your-client-id>&client_secret=<your-client-secret>&grant_type=authorization_code&response_type=cloud_iam&code=<code-from-the-callback>" "https://iam.stage1.ng.bluemix.net/oidc/token"
```
{: codeblock}

Response:

```
{
  "access_token": "eyJraWQiOiI......XmpBTIDdR5w",
  "refresh_token": "SPrXw5tBE3......KBQ+luWQVY=",
  "token_type": "Bearer",
  "expires_in": 3600,
  "expiration": 1473188353
}
```
