---



copyright:

  years: 2015, 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# How you are charged
{: #charges}

Charges vary depending on the resources used by a particular service, runtime, container, or support option. The resources can be the number of API calls, the number of instances, memory, storage, and so on. {{site.data.keyword.Bluemix_notm}} also provides detailed cost estimators, and a down-to-the-penny cost calculator to help you plan for charges. You can check the actual cost after you build your apps on the Usage Dashboard page.

With a {{site.data.keyword.Bluemix_notm}} billable account, you are charged for the compute, containers, and services that are used in your organization. You might be invited by other {{site.data.keyword.Bluemix_notm}} users to participate in organizations under a different account. If you create apps or use services in the organizations that you are invited to, the usage incurred is charged to the account that contains those organizations. You can see more information about a specific charges on a resource details page from the {{site.data.keyword.Bluemix_notm}} Catalog, or on the price calculator from the {{site.data.keyword.Bluemix_notm}} Pricing page.

Different types of charges apply depending on the features of {{site.data.keyword.Bluemix_notm}} you are using. The following table provides a high-level overview:

| Type of charge | Description | {{site.data.keyword.Bluemix_notm}} features that use this type of charge | Example |
|------------------|------------------|--------------------------|--------------------------|
| Fixed | Fixed-rate pricing is based on an agreed upon monthly charge that is not adjusted. | Services  | Data Cache has a fixed plan that is charged at a fixed monthly rate. |
| Metered | Metered-usage pricing is based on the number of GB-hours consumed for runtimes, and on the number of GB-hours consumed and the number of IP addresses and storage for containers. | Services, Compute, and Containers | For the Push service, any usage over the free monthly allowance is charged. |
|  Tiered   |  Some pricing plans are based on a tiered pricing model, so you can get a volume-based discount according to your actual usage. Services might offer simple, graduated, or block tier pricing plans. | Services | Tiered pricing is typically used for charge metrics that are expected to have very high quantities per month, such as API calls. |
| Reserved | Reserved pricing is based on a long-term commitment for a service, so you can get a discounted price. With a reserved plan, you get a dedicated service instance that is easy to set up, deploy, and deliver in the public {{site.data.keyword.Bluemix_notm}} environment. | Services | DB2 on Cloud has reserved plans.|

## Charges for compute resources
{: #compute}

You are charged for the time that your apps run and the memory that is used, calculated as *GB-hours*. GB-hours is the calculation of the number of application instances, multiplied by the memory per instance, multiplied by the hours that the instances run. You can customize the number of instances and the amount of memory per instance based on your needs. You can also add memory or instances to scale for more users. The final charge is per GB-hour: your application instances, multiplied by memory per instance, multiplied by hours running.

For example, consider a runtime that costs $0.07 per GB-hour in two 512 MB instances, running for 30 days (720 hours). These resources would cost $24.15 USD, including a free allowance of 375 GB-hours, with the following calculations:

```
2 instances x 0.5 GB x 720 hours = 720 GB-hours.
(720 - 375) GB-hours x $0.07 per GB-hour = $24.15
```

## Charges for services
{: #services}

Many services include monthly free allowances. Usage of services that is not included as part of the free allowance is charged in one of the following ways:
<dl>
<dt>Fixed charges</dt>
    <dd>You select a plan and pay on a flat rate basis. For example, the Data Cache service is charged at a flat-rate.</dd>
<dt>Metered charges</dt>
    <dd>You pay based on your runtime and service consumption. For example, with the Push service, any usage over the free monthly allowance is charged.</dd>
<dt>Reserved charges</dt>
    <dd><p>As the account owner of a Pay As You Go account or a Subscription account, you can reserve a service instance, with a long-term commitment, for a discounted price. For example, you can reserve the standard large DB2 on Cloud offering for 12 months.</p>
    <p>Some {{site.data.keyword.Bluemix_notm}} services offer reserved plans. You can request a reserved plan from the {{site.data.keyword.Bluemix_notm}} <strong>Catalog</strong> by clicking the tile of the service. Then, select the service plan that best meets your needs. If a reserved plan is available, click <strong>Request</strong>, and follow the prompts to send your request. You will receive an email that contains the price information of the reserved plan. A {{site.data.keyword.Bluemix_notm}} sales representative will also contact you soon to complete the purchase.</p></dd>
<dt>Tiered charges</dt>
    <dd>Similar to metered charges, you pay based based on your runtime and service consumption. However, Tiered charges add additional pricing tiers, often offering discounted charges in tiers with larger consumption. Tiered pricing is offered in simple, graduated, or block.</dd>
</dl>

### Simple tier
{: #simple_tier}

In the simple tier model, the unit price is determined by the tier that the quantity of your usage falls into. The total price is your quantity multiplied by the unit price in that tier. For example:

| Quantity of items | Unit price for all items |
|-------------------|--------------------------|
| Tier 1: 1 - 1000  | $1 USD                   |
| Tier 2: 1001 - 2000    |    $0.90 USD                      |
| Tier 3: 2001 - 3000                  |   $0.75 USD                       |
| Tier 4: 3001 - 4000           |      $0.60 USD                    |
|Tier 5: &gt; 4000 | $0.40 USD |
{:caption="Table 1. Simple tier pricing table" caption-side="top"}

The following table illustrates how much you pay with a plan that is based on a simple tier pricing model:

| Quantity of items | Charge Calculation | Total Price |
|-------------------|--------------------|-------------|
|500 |	500 × 1 = 500 |	$500 USD|
|1500 |	1500 × 0.90 = 1350 |	$1350 USD|
|2500 |	2500 × 0.75 = 1875 |	$1875 USD|
|... |	... |	...|
|5200 |	5200 × 0.40 = 2080 |$2080 USD|
{:caption="Table 2. Charge calculation by using the simple tier pricing model" caption-side="top"}

### Graduated tier
{: #graduated_tier}

In the graduated tier model, the unit price per tier decreases as your level of usage increases. The total price is the cumulative charges for each level of usage, consisting of your quantity multiplied by the unit price at that tier. For example:

| Quantity of items |	Unit price for items in the tier|
|-------------------|------------------------------------|
|    Tier 1: 1 - 1000 |	$1 USD |
|   Tier 2: 1001 - 2000 |	$0.90 USD |
|    Tier 3: 2001 - 3000 |	$0.75 USD |
|    Tier 4: 3001 - 4000 |	$0.60 USD |
|    Tier 5: &gt; 4000 |	$0.40 USD |
{:caption="Table 3. Graduated tier pricing table" caption-side="top"}

The following table illustrates how much you pay with a plan that is based on a graduated tier pricing model:

|Quantity of items | Charge calculation | Total price|
|------------------|--------------------|------------|
|500 |	500 × 1 (unit price for Tier 1) = 500 |	$500 USD|
|1500 |	(1000 × 1 (unit price for Tier 1)) + (500 × 0.90 (unit price for Tier 2)) = 1450 |	$1450 USD|
|2500 |	(1000 × 1 (unit price for Tier 1)) + (1000 × 0.90 (unit price for Tier 2)) + (500 × 0.75 (unit price for Tier 3)) = 2275 |	$2275 USD |
|... |	... |	...|
|5200 |	(1000 × 1 (unit price for Tier 1)) + (1000 × 0.90 (unit price for Tier 2)) + (1000 × 0.75 (unit price for Tier 3)) + (1000 × 0.60 (unit price for Tier 4)) + (1200 × 0.40 (unit price for Tier 5)) = 3730 |	$3730 USD|
{:caption="Table 4. Charge calculation by using the graduated tier pricing model" caption-side="top"}

### Block tier
{: #block_tier}

In the block tier model, the price is a set charge for the quantity you use within a usage level. The total price is the charge for your level of usage, regardless of your actual usage. Each successive tier provides a lower price to quantity ratio. For example:

|Quantity of items |	Total price for all items|
|------------------|-----------------------------|
| Tier 1: &lt;= 1000 |	$1000 USD|
| Tier 2: &lt;= 2000 |	$1900 USD|
| Tier 3: &lt;= 3000 |	$2800 USD|
| Tier 4: &lt;= 4000 |	$3500 USD|
| Tier 5: &lt;= 10000 |	$5000 USD|
{:caption="Table 5. Block tier pricing table" caption-side="top"}

The following table illustrates how much you pay with a plan that is based on a block tier pricing model:

|Quantity of items |	Charge calculation |	Total price|
|------------------|-----------------------|---------------|
|500 |	The number of items falls into Tier 1, so the total price is $1000 USD. |	$1000 USD|
|1500 |	The number of items falls into Tier 2, so the total price is $1900 USD. |	$1900 USD|
|... |	... |	...|
|5200 |	The number of items falls into Tier 5, so the total price is $5000 USD. |	$5000 USD|
{:caption="Table 6. Charge calculation by using the block tier pricing model" caption-side="top"}
