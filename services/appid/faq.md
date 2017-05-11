---

copyright:
  years: 2017
lastupdated: "2017-05-08"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}


# FAQ {: #faq}

This FAQ provides answers to common questions about the {{site.data.keyword.appid_full}} service.
{: shortdesc}


## How does {{site.data.keyword.appid_short_notm}} calculate pricing? {: #pricing}

With {{site.data.keyword.appid_short_notm}}, you pay less as you use more resources.
{: shortdesc}

The graduated tier plan consists of two parts: the number of authentication events and the number of authorized users. You are charged each month, based on the summary of the two parts. The total price is the cumulative charge for each level of usage, consisting of your quantity multiplied by the unit price at that tier.

### Authentication events

An authentication event occurs when a new {{site.data.keyword.appid_short_notm}} token is issued. For identified users, each new token is valid for one hour. Tokens are valid for one month for anonymous users. After the token expires, you must create a new token to access protected resources. When you use app ID for mobile authentication, user tokens are stored in `key-store/key-chain` and are added to every future request. The tokens are accessible by using the {{site.data.keyword.appid_short_notm}} Android or iOS Swift SDK. When you use the service for web authentication, <a href="https://github.com/ibm-cloud-security/appid-serversdk-nodejs" target="_blank">store the user token <img src="../../icons/launch-glyph.svg" alt="External link icon"></a> in the session cookies.

### Authorized users

An authorized user is a unique user that logs in with your service whether directly or indirectly. You are charged for one authorized user every time a new user logs in from each identity provider, including anonymous users. For example, if a user logs in with Facebook, and later logs in by using Google, they are considered two separate authorized users.


For more information on graduated tier pricing, see the [{{site.data.keyword.Bluemix_notm}} pricing docs](/docs/pricing/index.html#pricing).
