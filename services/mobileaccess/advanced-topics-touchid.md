---

copyright:
  years: 2015, 2016
lastupdated: "2016-10-27" 

---

# Authorizating access with Touch ID
{: #before-you-begin}

Touch ID is a fingerprint recognition feature for iOS devices. You can use Touch ID wth the {{site.data.keyword.amafull}} service to automatically secure authorization information for future use. 

**Note:** Touch ID is available only from the  {{site.data.keyword.amashort}} Objective-C SDK.

To configure security strength, set one of the following persistence polices with the `IMFAuthorizationManager.setAuthorizationPersistencePolicy()` method.

* **IMFAuthorizationPersistencePolicyNever** (Most secure): Never persist authorization information on the device. An authorization header is valid during a single application session. Authorization information is persisted in the iOS keychain.

* **IMFAuthorizationPersistencePolicyAlways** (Least secure): Always persist authorization information on the device, regardless of whether Touch ID is present, supported, or enabled. Touch ID and device passcode authentication are never required.

* **IMFAuthorizationPersistencePolicyWithTouchBiometrics**: Use Touch ID to fetch the authorization information from the iOS keychain. This option balances security and ease of use. The authorization information is persisted only if Touch ID is present, supported, and enabled. Touch ID or device passcode authentication is required to access the persisted authorization information one time per application session. When this policy has been set, but there is no access to Touch ID, for example, because the necessary hardware is not present or has been disabled, the fallback is the **IMFAuthorizationPersistancePolicyNever** policy.
