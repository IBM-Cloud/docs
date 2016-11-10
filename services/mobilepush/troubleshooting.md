---

copyright:
 years: 2015, 2016

---

# Troubleshooting
{: #errors}
Last updated: 08 November 2016
{: .last-updated}

Use this section as a guide to troubleshooting common {{site.data.keyword.mobilepushshort}} issues.


### Internal server error occurred. Please contact admin. (Internal error code: PUSHD102E)

####Explanation

**Explanation**: This error might occur if you have created a push instance before November 2015.  

####USER RESPONSE

**Action**:  To resolve this issue, delete the push instance and create a new one.

**Note**: When you delete the push instance, your tags are not be preserved.


### UnauthorizedRegistration

####Explanation

**Explanation**: Chrome Web Push does not work with Firebase Cloud Messaging (FCM) Keys. If you are unable to receive web push notifications on Chrome after moving to FCM from GCM, this is because the website was previously configured to work with GCM project and the new project is created in FCM. The generated tokens that identify the browser are cached by the Chrome browser.

**Action**: You can resolve this issue by removing the cookies and resetting the permissions of the browser. This would request for permissions to enable Push Notifications. 

