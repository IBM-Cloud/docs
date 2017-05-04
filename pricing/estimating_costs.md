---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Estimating your costs
{: #cost}

You can use different methods to know how much you need to pay for using {{site.data.keyword.Bluemix_notm}} to build and host your app.

* The cost estimators on the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}
provide a rough estimation of the cost based on the size of your app.
* The cost calculator on the {{site.data.keyword.Bluemix_notm}} Pricing page provides accurate app prices based on your input of runtime and service usages.
* You can also calculate your cost manually.

## Using the cost calculators
{: #calculator}

You can quickly price your app by using the cost calculators that are provided by {{site.data.keyword.Bluemix_notm}}.

1. Go to the {{site.data.keyword.Bluemix_notm}} {{site.data.keyword.pricing_sheet}}.
2. Use one of the Infrastructure widgets, or click **Pricing calculator**.

To use the calculator, type your projected monthly usage of the listed resources; for example, number of instances or push notifications. Click inside the **Monthly Usage** field for hints about the units that are expected in the field. The calculator displays the price for your input immediately. You can also adjust the calculator to display yearly costs instead of monthly costs.

## Calculating your costs manually
{: #manual}

You might want to estimate your {{site.data.keyword.Bluemix_notm}} costs yourself, to better understand how {{site.data.keyword.Bluemix_notm}} costs are calculated. You can calculate the total price of using {{site.data.keyword.Bluemix_notm}} to build and host your app by considering the prices of the runtime and the services it uses. The prices of runtimes and services sometimes change, so you must refer to the latest information on the {{site.data.keyword.Bluemix_notm}} pricing sheet when you calculate the total price.

## Example: Pricing a sample app
{: #sample}

Assume that you have a Node.js web app with scalability capabilities, and that the app uses several services that are provided by {{site.data.keyword.Bluemix_notm}}. You can learn how the actual cost of your app is calculated in this example. The web app uses the following {{site.data.keyword.Bluemix_notm}} services and items:

* Four 256 MB Node.js runtime instances
* Two {{site.data.keyword.autoscaling}} policies, processor and memory
* 2 GB per month {{site.data.keyword.datacshort}}
* 150 GB per month NoSQL database, 100,000 heavy API calls, and 500,000 light API calls
* 20 GB inbound or outbound network traffic

## Prices for Bluemix resources
{: #sample_resources}

To keep the example simple, assume that the prices in the following table do not fluctuate within or between a time frame, for example, a month. All pricing in this example is in US currency.

|Service |	Features |	Price |
|--------|-----------|--------|
|SDK for Node.js |	375 GB-hours free per month (shared across all runtimes) |	$0.07 USD/GB-hour|
|Auto-Scaling |	Free service plan for the Auto-Scaling service |	Free|
|Data Cache - Starter |	1 GB of cache space and a replica |	$55.00 USD/instance |
|Data Cache - Standard |	5 GB of cache space and a replica |	$155.00 USD/instance |
|Data Cache - Premium |	25 GB of cache space and a replica |	$505.00 USD/instance|
|IBM Cloudant® NoSQL DB for {{site.data.keyword.Bluemix_notm}} |	2 GB of free data storage<br/>50,000 light API calls free per month<br/>10,000 heavy API calls free per month | $1.00 USD/GB<br/>$0.03 USD/1000 light API calls<br/>$0.15 USD/1000 heavy API calls |
{:caption="Table 1. Pricing sheet" caption-side="top"}

## Calculating the app price

The price of the app can be calculated in the following way:

<dl>
<dt>Four 256 MB Node.js runtime instances</dt>
<dd>Bluemix charges for a runtime by GB-hours. The number of GB used per month is <code>4 x 256 = 1024 MB or 1 GB per month</code>. Assume that there are <code>24 x 30 = 720 hours in a month</code>, so the application is charged for <code>1 x 720 = 720 GB-hours</code>.
<p>
375 GB-hours are included in a free allowance per month, shared across all {{site.data.keyword.Bluemix_notm}} runtimes. So the total cost for the runtime is <code>$0.07 x (720-375) = $24.15</code>.</p></dd>

<dt>Two Auto-Scaling policies (processor and memory)</dt>
<dd>The Auto-Scaling policies are free of charge.</dd>

<dt>2 GB per month Data Cache</dt>
<dd>The 50 MB plan that is provided by the Data Cache service is free of charge. However, the free plan would not cover your projected use of 2 GB per month. The three paid plans for Data Cache cost a set amount for a specific amount of space, regardless of how much space you actually use. Therefore, you want to choose the minimum plan that meets your projected use, which is the standard plan of 5 GB. The total cost is $155 per month.</dd>

<dt>150 GB per month NoSQL database</dt>
<dd>The IBM Cloudant NoSQL DB for {{site.data.keyword.Bluemix_notm}} service charges are based on data storage and the ability to access that data by different API methods. The <strong>PUT</strong> and <strong>POST</strong> commands are considered as heavy API calls, but <strong>GET</strong> commands are considered as light API calls.
<p>
Add up the number of GB and deduct a 2 GB free allowance. 148 GB is charged per month. Subtract the free allowance of 50,000 for light api calls and 10,000 for heavy api calls. The total storage price includes the following parts:</p>
<pre class="codeblock">
<codeblock>
    148 x 1 = $148
    (450,000 / 1000) x 0.03 = $13.5
    (90,000 / 1000) x 0.15 = $13.5
</codeblock>
</pre>
<p>
The total price is 148 + 13.5 + 13.5 = $175.</p></dd>

<dt>20 GB inbound or outbound network traffic</dt>
<dd>Inbound and outbound network traffic is free of charge.</dd>

</dl>

When all the items are added, the total price of the application is $354.15.

## Supported currencies

Although the United States dollar (USD) is used in the pricing examples, other currencies are also supported in {{site.data.keyword.Bluemix_notm}}. The following table lists the different currencies that are supported.

|ISO 4217 code| Currency|
|-------------|---------|
|AUD |	  Australian dollar|
|BRL |	  Brazilian real|
|CAD |	  Canadian dollar|
|CHF |	  Swiss franc|
|DKK |	  Danish krone|
|EUR |	  Euro|
|GBP |	  Pound sterling|
|INR |	  Indian rupee|
|JPY |	  Japanese yen|
|KRW |	  South Korean won|
|NOK |	  Norwegian krone|
|NZD |	  New Zealand dollar|
|SEK |	  Swedish krona|
|USD |    United States dollar|
|ZAR |	  South African rand|
{:caption="Table 2. Supported currencies" caption-side="top"}

**Note:** If you have linked your {{site.data.keyword.Bluemix_notm}} and SoftLayer accounts, the single invoice you receive is in United States dollars (USD) only.
