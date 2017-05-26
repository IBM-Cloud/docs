---

copyright:
  years: 2017
lastupdated: "2017-05-23"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:pre: .pre}

# Access and identity tokens
{: #access-and-identity}

{{site.data.keyword.appid_short}} uses two types of tokens: access and identity. The tokens are formatted as <a href="https://jwt.io/introduction/" target="_blank">JSON Web Tokens <img src="../../icons/launch-glyph.svg" alt="External link icon"></a>.
{:shortdesc}


## Access token
{: #access-tokens}

The access token enables communication with [back-end resources](/docs/services/appid/protecting-resources.html) that are protected by {{site.data.keyword.appid_short_notm}} authorization filters. The token conforms to JavaScript Object Signing and Encryption (JOSE) specifications and has the following format:

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "exp": "1495562664",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "amr": "facebook",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "iat": "1495559064",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "scope": "appid_default appid_readprofile appid_readuserattr appid_writeuserattr",
}
```
{:screen}

<table>
<caption> Access token components explained </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> typ </i> </td>
    <td> The header type, specified as "JOSE". </td>
  </tr>
  <tr>
    <td> <i> alg </i> </td>
    <td> The algorithm used, specified as "RS256". </td>
  </tr>
  <tr>
    <td> <i> iss </i> </td>
    <td> The {{site.data.keyword.appid_short}} server that issued the token; specified as a string or URL. </td>
  </tr>
  <tr>
    <td> <i> sub </i> </td>
    <td> The ID of the user who the token was issued to. </td>
  </tr>
  <tr>
    <td> <i> aud </i> </td>
    <td> The OAuth2 client id of the person the token intended for. </td>
  </tr>
  <tr>
    <td> <i> exp </i> </td>
    <td> The time at which the timestamp expires, specified in epoch time. </td>
  </tr>
  <tr>
    <td> <i> iat </i> </td>
    <td> The time at which the timestamp was issued, specified in epoch time. </td>
  </tr>
  <tr>
    <td> <i> tenant </i> </td>
    <td> The {{site.data.keyword.appid_short}} tenant ID for which the token was issued. </td>
  </tr>
  <tr>
    <td> <i> amr </i> </td>
    <td> The identity provider used for authentication. This variable can be <i>appid_facebook</i> or <i>appid_google</i>. </td>
  </tr>
  <tr>
    <td> <i> scope </i> </td>
    <td> the scope[s] this token was issued for </td>
  </tr>
</table>


## Identity token
{: #identity-tokens}

The identity token contains information about the user, including name, email, gender, picture, and location.

```
Header: {
    "typ": "JOSE",
    "alg": "RS256",
}
Payload: {
    "iss": "appid-oauth.ng.bluemix.net",
    "aud": "a3b87400-f03b-4956-844e-a52103ef26ba",
    "exp: "1495562664",
    "tenant": "9781974b-6a1c-46c3-aebf-32b7e9bbbaee",
    "iat": "1495559064",
    "name": "John Smith",
    "email": "js@mail.com",
    "gender", "male",
    "locale": "en",
    "picture": "https://url.to.photo",
    "sub": "de6a17d2-693d-4a43-8ea2-2140afd56a22",
    "identities": [
        "provider": "facebook"
        "id": "377440159275659",
        "amr: "facebook",
    ],
    "oauth_client":{
      "name": "BluemixApp",
      "type": "serverapp",
      "software_id": "cb638f8f-e24b-41d3-b770-23be158dd8e6.2b94e6bb-bac4-4455-8712-a43fa804d5cc.a3b87400-f03b-4956-844e-a52103ef26ba",
      "software_version": "1.0.0",
    }
}
```
{:screen}


<table>
<caption> Identity token components explained </caption>
  <tr>
    <th> Component </th>
    <th> Description </th>
  </tr>
  <tr>
    <td> <i> name </i> </td>
    <td> The user's full name as reported by the identity provider. This must be returned. </td>
  </tr>
  <tr>
    <td> <i> email </i> </td>
    <td> The user's email as reported by the identity provider. Returned only when available. </td>
  </tr>
  <tr>
    <td> <i> gender </i> </td>
    <td> The user's gender as reported by the identity provider when available. </td>
  </tr>
  <tr>
    <td> <i> locale </i> </td>
    <td> The user's locale as reported by the identity provider. </td>
  </tr>
  <tr>
    <td> <i> picture </i> </td>
    <td> The URL to a user's picture, if available. </td>
  </tr>
  <tr>
    <td> <i> identities: </br> <ul><li> provider <li> id <li> amr </ul></i></td>
    <td> </br><ul><li> The identity provider used for authentication. This variable can be either <i>appid_facebook</i> or <i>appid_google</i>, and must be returned. <li> A unique user ID as reported by an identity provider. <li> A JSON object returned by that must be returned by the identity provider. </ul></i></td>
  </tr>
  <tr>
    <td> <i> oauth_client: </br> <ul><li> type <li> name <li> software_id <li> software_version</ul></i> </td>
    <td> </br><ul><li> The type of application determined during client registration. The variable can be <i>serverapp</i> or <i>mobileapp</i>. <li> The client name as reported during client registration. <li> The software id as reported during client registration. <li> The version of software used during client registration. </ul></td>
  </tr>
</table>
