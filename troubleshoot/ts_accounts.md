---

copyright:
  years: 2015, 2017
  
lastupdated: "2017-06-01"

---

{:tsSymptoms: .tsSymptoms} 
{:tsCauses: .tsCauses} 
{:tsResolve: .tsResolve} 
{:new_window: target="_blank"}  
{:shortdesc: .shortdesc}
{:codeblock: .codeblock} 


# Troubleshooting for managing accounts
{: #managingaccounts}

General problems with managing your account might include different apps share the same domain name, or administrators can't view all organizations. In many cases, you can recover from these problems by following a few easy steps.
{:shortdesc}

## Unable to access a different {{site.data.keyword.Bluemix_notm}} region
{: #nosecondreg}

An error message is received when you try to create a new {{site.data.keyword.Bluemix_notm}} region. 
{: tsSymptoms}

This is likely because you are using a Standard account, which supports development in one public region only. You select the {{site.data.keyword.Bluemix_notm}} public region in which you want to work when the account is first set up. 
{: tsCauses}

If you have a Standard account, you can upgrade to a billable account to access additional regions. Go to the **Manage > Billing and Usage > Billing** page in the console, and click **Add Credit Card**. On the **Billing** page, you can also check if you have a Standard account.
{: tsResolve}

## Unable to create new organization
{: #nosecondorg}
 
An error message is received when you try to create a new organization. 
{: tsSymptoms}

This is likely because you are using a Standard account, which supports development in one organization only. You create the organization when your account is first set up. 
{: tsCauses}

If you have a Standard account, you can upgrade to a billable account to access additional organizations. Go to the **Manage > Billing and Usage > Billing** page in the console, and click **Add Credit Card**. On the **Billing** page, you can also check if you have a Standard account.
{: tsResolve}

## Unable to create new Lite plan instance
{: #nosecondlite}

The following error message is displayed when you try to create a new Lite plan instance:
{: tsSymptoms}

`Unable to provision new Lite instance`

There is a limit of one instance per Lite plan instance to allow us to keep these plans free. 
{: tsCauses}

You can create additional instances of the service by selecting one of the billable service plans, which are available in the billable accounts. To upgrade to a billable account from the console, go to the **Manage > Billing and Usage > Billing** page, and click **Add Credit Card**.
{: tsResolve}

If you do not want to upgrade from a Standard account and are no longer using your existing Lite service instance, you can delete the exisiting Lite plan instance from the Services dashboard and then create a new instance. 

## Exceeded the runtime memory allowance
{: #noruntimemem}

You are unable to deploy apps and get an error stating that you have exceeded your organization's memory limit.
{: tsSymptoms}

In a Standard account your Cloud Foundry apps can use up to 256 MB of instantaneous runtime memory. In billable accounts, there is a 2GB memory limit.
{: tsCauses}

If you are using a Standard account, you can get additional memory by upgrading to a billable account. Go to the **Manage > Billing and Usage > Billing** page in the console, and click **Add Credit Card**.
{: tsResolve}

If you do not want to upgrade from a Standard account but have some idle apps, you can delete the idle apps to free up some runtime memory. 

## Account is inactive
{: #ts_accnt_inactive}

You can't create an app in {{site.data.keyword.Bluemix_notm}} if your account is inactive. You must contact the support team to fix this problem.

When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms} 

`BXNUI0096E: The app wasn't created. Your account is inactive because it was canceled or suspended.`

The status of your {{site.data.keyword.Bluemix_notm}} account becomes inactive when the account is cancelled or suspended.
{: tsCauses}


To reactivate your account, contact [{{site.data.keyword.Bluemix_notm}} Support ![External link icon](../icons/launch-glyph.svg "External link icon")](http://ibm.biz/bluemixsupport.com){: new_window}. Include the following information in the email:
{: tsResolve}

  * The IBMid that you use to log in to {{site.data.keyword.Bluemix_notm}}.
  * The name of the organization in which your app is being created. This information can help the support team determine whether you are assigned the correct roles or membership in your organization.


## No space is associated with your current org
{: #ts_no_space}

You can't create an application if no space is associated with your current organization.

When you try to create an app in {{site.data.keyword.Bluemix_notm}}, you see the following error message:
{: tsSymptoms} 

`BXNUI0097E: Before you can add an app, at least one space must be associated with your organization and region. On the Dashboard, click Create a Space. When the space is created, try again.`

Apps in {{site.data.keyword.Bluemix_notm}} must be created in a space under your organization.
{: tsCauses} 

To create a space, use one of the following methods: 
{: tsResolve}
 
  * On the {{site.data.keyword.Bluemix_notm}} Dashboard, select the organization in which you want to create the space, then click **Create a Space**.
  * In the cf command line interface, type `cf create-space <space_name> -o <organization_name>`.

  
## Apps share the same domain name
{: #ts_domain_diff}

You might notice that several apps share the same URL in {{site.data.keyword.Bluemix_notm}}.

This problem might happen when you assign the same URL route for different apps in a space.
{: tsCauses}

For example, you push the myApp1 app to {{site.data.keyword.Bluemix_notm}} and set the domain to "mynewapp.stage1.mybluemix.net". Then, you push another myApp2 app to the same space and set one of its URL routes to "mynewapp.stage1.mybluemix.net". The route is now mapped to both apps.

This is supported behavior of the {{site.data.keyword.Bluemix_notm}} and you can use this practice to achieve zero downtime for your app upgrade. For more information, see [Using Blue-Green Deployment to Reduce Downtime and Risk ![External link icon](../icons/launch-glyph.svg "External link icon")](https://docs.cloudfoundry.org/devguide/deploy-apps/blue-green.html){: new_window}.
{: tsResolve}
  

## Administrators can't view all orgs by using the {{site.data.keyword.Bluemix_notm}} user interface
{: #ts_ui_org}

As an administrator, when you use the {{site.data.keyword.Bluemix_notm}} user interface, you can't display every organization to administer them. You can display and administer only those organizations to which you belong.

As an administrator, you can't see all the organizations by using the {{site.data.keyword.Bluemix_notm}} user interface.
{: tsSymptoms}

This is a limitation of the {{site.data.keyword.Bluemix_notm}} user interface.
{: tsCauses}

You can use commands such as `cf orgs`, `cf create-org`, and `cf delete-org` from the cf command line interface to manage all the organizations. For a full list of cf commands, enter `cf help`.
{: tsResolve}
	
## Credit card can't be added
{: #ts_addcc}

You can't submit your credit card information to convert your trial account to a Pay As You Go account.

The **Submit** button on the Add credit card page is disabled.
{: tsSymptoms}

This problem happens when your information isn't filled in correctly in the Add credit card page.
{: tsCauses}


Complete the following steps:
{: tsResolve}

  1. On the Add credit card page, fill in all the required fields in the contact information, contact address, and billing address sections.
  2. Select **I have read and agree to IBM's Terms and Conditions**, then click **Submit**. The **Select a payment method** section is displayed.
  3. Enter your credit card number, the expiry date of your card, and the security code on your card. Then click **Submit**.
