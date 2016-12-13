---

copyright:
 years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Troubleshooting
{: #errors}
Last updated: 12 December 2016
{: .last-updated}

Use this section as a guide to troubleshooting common {{site.data.keyword.mobilepushshort}} issues.


### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)

**Explanation**: This error might occur if you have created a push instance before November 2015.  

**User response**: To resolve the issue, delete the push instance and create a new one. Note that when you delete the push instance, your tags are not be preserved.


### UnauthorizedRegistration

**Explanation**: Chrome Web Push does not work with Firebase Cloud Messaging (FCM) Keys. If you are unable to receive web push notifications on Chrome after moving to FCM from GCM, this is because the website was previously configured to work with GCM project and the new project is created in FCM. The generated tokens that identify the browser are cached by the Chrome browser.

**User response**: You can resolve this issue by removing the cookies and resetting the permissions of the browser. This would request for permissions to enable Push Notifications. 


### Service workers are not supported in this browser

**Explanation**: The SDK that was included as a part of `BMSPushSDK.js` using the service worker is not available. 

**User response**: It is recommended that you switch to a browser that supports the service worker. The supported versions of the browsers are Firefox version 49 or later and Chrome version 53 (64 bit) or later.


### SecurityError: The operation is insecure

**Explanation**:  You might see the error when enabling the web console in Firefox. Web push support in Push Notification service requires the website to be accessed with the `https` protocol, rather than `http`.

**User response**: It is recommended that you try connecting to the website using `https`, from the browser.

