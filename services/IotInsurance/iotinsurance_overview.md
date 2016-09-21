---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}


# About {{site.data.keyword.iotinsurance_short}}
{: #about_servicename}
Last updated: 15 September 2016
{: .last-updated}

{{site.data.keyword.iotinsurance_full}} is an integrated IoT production instance that collects and analyzes full-context data from policy holders to provide personalized risk assessments, real-time protection, and policy cost reductions.
{: shortdesc}

{{site.data.keyword.iotinsurance_short}} provides a full context view of the policy holder's assets and situation, including information such as location, weather, traffic, and overall wellness. In-depth analysis of this information allows the insurer to provide personalized risk assessment and real-time protection for the policy holder. Benefits for the policy holder include risk avoidance in the form of early alerts, personalized advice, and streamlined claims processing and settlement. Benefits for the insurer include customer satisfaction, customer loyalty, and expense reduction by using claims avoidance and processing automation.

## Process flow
{: #processFlow}
The insurance provider has an instance within the {{site.data.keyword.Bluemix_notm}} service broker. Customers of the insurer have sensors in their homes, which are connected to the sensor provider's cloud. From their mobile devices, homeowners authorize the {{site.data.keyword.iotinsurance_short}} service to receive sensor data from {{site.data.keyword.iotinsurance_short}}. The {{site.data.keyword.iotinsurance_short}} service connects to the sensor provider's cloud and pulls data for each user and sends it to the IoT server. If the sensor shows that the parameters that are specified in the insurer's shields are met in the customer's home, notifications are sent to the insurer's dashboard and to the customer's device.

## Components
{: #components}

### Insurance dashboard
{: #insurance_dashboard}
The Insurance Dashboard gives insurance company users, such as agents, a complete view of what is happening with their customers' insured assets. They can see the shields and events at a country, state, or account levels.

The sample insurance dashboard is loaded with simulated data to show you an example of the kind of information that you can collect and analyze.

### Mobile starter app
{: #mobileapp}
The mobile starter app is where insurance policy holders such, as homeowners, view and respond to the information that {{site.data.keyword.iotinsurance_short}} sends from the sensors in their homes.

Using a mobile device, homeowners authorize the service to connect to the sensor provider's cloud to send and receive data. For example, a homeowner might receive a notification in the mobile starter app when the sensor detects a water leak. For more information, see [Installing and connecting the mobile starter app](iotinsurance_mobile_app.html}).

### REST API
{: #rest_api}
The REST API is used by the mobile starter app, the insurance dashboard, the shield engine, and the hazard controller. It enables users to know the associations that exist between devices and shields and actions. By using this API, programmers can create new users, generate event data, create and register new shields, and fetch event data.

The API that you access from the service console is customized for your instance of  {{site.data.keyword.iotinsurance_short}}.

On the API page, you can  
  - View all available API calls and associated documentation.
  - Try individual API calls.  Select an API call to display all information, then click **Try it out!**.

API examples are available to help you get started with common scenarios. For more information, see [{{site.data.keyword.iotinsurance_short}} API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).

### Cloud provider
{: #cloudprovider}
Users must authorize the Transformer component to access sensor cloud data and process the recorded data. Authorization is granted by using the mobile starter app. Wink is the only cloud vendor that is supported at this time.

### Transformer
{: #transformer}
The Transformer requests new information from the cloud server API and transforms it to match the data in {{site.data.keyword.iotinsurance_short}}. The data is then published for the rest of the {{site.data.keyword.iotinsurance_short}} implementation to use.

### Analytics engine
{: #analytics_engine}
Based on the information that is stored in an event, the analytics engine determines if a hazard such as a water leak occurred. If a hazard is identified, it is passed to the hazard controller. The Action engine views the data in the database to determine the action to take based on the information that is specified in the shield.

You can create new shields in JavaScript by using the {{site.data.keyword.iotinsurance_short}} API.

### Shields
{: #shields}
A shield is a specific protection that a customer acquires from the insurance provider. For example, a homeowner purchases insurance on their home to shield it against fire, water damage, burglaries, and other hazards. The {{site.data.keyword.iotinsurance_short}} solution provides a built-in shield against water. Customers are alerted and can respond when an event that involves water threatens their home. Using the REST API, developers can add more shields.
Shields run in the {{site.data.keyword.iotinsurance_short}} analytics engine. The analytics engine identifies the type of hazard (for example, *Water is detected*), the user account of the sensor that sent the hazard, and the shields that are associated with the account. Action can be taken based on that information.
