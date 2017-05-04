---



copyright:

  years: 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Managing usage for {{site.data.keyword.Bluemix_notm}} linked accounts 
{: #linked_usage}

If you have a linked {{site.data.keyword.Bluemix_notm}} and SoftLayer account, you can use the Control Portal to make a one-off payment, change your payment card details, view your billing items, and view your involices.

**Note:** The billing and usage options that are displayed in the {{site.data.keyword.Bluemix}} console can be different if you have a free account or you do not have a linked {{site.data.keyword.Bluemix_notm}} and SoftLayer account.

## Making a payment
{: #managemakeapayment}

You can make a one-off payment at any time. The payment can be for the full balance or a partial amount and the details that you enter for the payment are not recorded. In the {{site.data.keyword.Bluemix_notm}} console, complete the following steps to make a one-off payment.

1. Select one of the following options, depending on which dashboard you are using:   
 * From the Apps or Services dashboard, click **Manage** &gt; **Billing and Usage** &gt; **Make a Payment**.  
 * From the Infrastructure dashboard, click **Account** &gt; **Make a Payment**.
3. In the **Payment Amount** field, enter the amount you want to pay.
4. Select your payment method:
 * Paying with a credit card. Enter your card details and the card billing address. Then, click **Make Credit Card Payment**. 
 * Paying with PayPal. Enter your details when prompted to complete the payment. 

Resolve any reported problems with the payment. The Account Balance is updated after the payment is accepted. You can contact the 
support team by clicking **Support** &gt; **Add Ticket**.

## Changing your payment method
{: #managepaymentmethod}

Each billable account must have a registered credit card that is valid. Every month, the credit card is charged with the usage amount that is accumulated during that month. In the {{site.data.keyword.Bluemix_notm}} console, complete the following steps to add or change  your payment details. 

1. Select one of the following options, depending on which dashboard you are using:  
 * From the Apps or Services dashboard, click **Manage** &gt; **Billing and Usage** &gt; **Modify Payment Method**.  
 * From the Infrastructure dashboard, click **Account** &gt; **Billing** &gt; **Payment Method**.
2. In the Add Payment Method section, enter your credit card details and the card billing address. Then, click **Add Credit Card**. 

Your card details are validated and then your card is available to use in your account within 24 hours. A confirmation email is 
sent to contact entered in the card billing address section.

## Viewing your billing items
{: #managebillingitems}

You can associate billing items to specific devices and also disassociate those billing items. By default, the 
Billing Items page displays associated billing items. You can change the view by selecting an option from 
the display menu. Association and disassociation can occur for one item, or for more than one item at a time by using the Bulk Actions operation. Individual billing items can be canceled at any time from the Billing Items page. In the {{site.data.keyword.Bluemix_notm}} console, complete the following steps to associate or disassociate your billing items.

1. Select one of the following options, depending on which dashboard you are using:   
 * From the Apps or Services dashboard, click **Manage** &gt; **Billing and Usage** &gt; **Billing Items**.  
 * From the Infrastructure dashboard, click **Account** &gt; **Billing** &gt; **Billing Items**.
2. Select the billing item option that you want and complete the relevant fields. 

## Viewing your invoices
{: #manageinvoices}

Invoices can be be viewed or paid at any time. Each invoice is summarized by Invoice Number, Date, Invoice Type and various 
monetary balances. Invoice Types may fall into the following categories:

 *  New -- the first invoice in a series of recurring invoices.
 *  Recurring -- an invoice for recurring charges that have been active on the account for more than one month.
 *  One-Time-Charge -- a one-time charge for various expenses, which may include overages.
 *  Credit -- a credit from {{site.data.keyword.Bluemix_notm}} to the account balance.
 *  Refund -- a refund, or reversal, for either a one-time or recurring charge.

The Invoices page also displays a billing summary for the account, which includes the current and estimated next balance, 
the payment method, and the last and next recurring invoice dates. You can view an invoice in the Control Portal or download the invoice. 

In the {{site.data.keyword.Bluemix_notm}} console, complete the following steps to view an invoice:

1. Select one of the following options, depending on which dashboard you are using:  
 * From the Apps or Services dashboard, click **Manage** &gt; **Billing and Usage** &gt; **Invoices**.  
 * From the Infrastructure dashboard, click **Account** &gt; **Billing** &gt; **Invoices**.
2. You can view an invoice in the Control Portal or download the invoice. 

## Using {{site.data.keyword.Bluemix_notm}} services with SoftLayer assets
{: #bluemix_services}

You can easily use API-based public {{site.data.keyword.Bluemix_notm}} services with your SoftLayer assets. All APIs are secure and encrypted so that your data is protected.
{:shortdesc}

For example, have you ever wanted to add cognitive capabilities from Watson to your apps running on bare metal servers from SoftLayer? You can add a service such as {{site.data.keyword.personalityinsightsshort}} to help understand your app's user in four easy steps:

1. Find the service in the {{site.data.keyword.Bluemix_notm}} catalog.
2. Provision an instance of the service with just a few clicks.
3. Set up the service to run with your existing code by copying the service credentials and adding them to your application.
4. After the update to the app, deploy the new version on your SoftLayer infrastructure.

You can gain *Insights and Cognitive* knowledge by calling Watson APIs from your apps in SoftLayer to make them more personalized. Or, use *Data and Analytics* services to tap into high performance analytics for your apps. Or, choose database-as-a-service where you can leave the management to {{site.data.keyword.Bluemix_notm}}.

Modernize your application development by using containers with services like {{site.data.keyword.activedeployshort}} and {{site.data.keyword.deliverypipeline}}. You can then use the {{site.data.keyword.vpn_short}} service to communicate with SoftLayer to connect your container in a private network to the SoftLayer private network. All of the usage charges of the compute resources and services are reflected in your {{site.data.keyword.Bluemix_notm}} bill.
