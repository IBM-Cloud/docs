---

copyright:
  years: 2016

---

<!-- Common attributes used in the template are defined as follows: -->
{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}


<!-- {{site.data.keyword.iotinsurance_full}}  {{site.data.keyword.iotinsurance_short}}  -->


# Creating users and shield associations
{: #gettingstartedtemplate}
Last updated: 15 September 2016
{: .last-updated}

After you create the {{site.data.keyword.iotinsurance_short}} service and deploy the required supporting services and apps, you can test the service by creating an authorized user and a shield association.
{:shortdesc}

**Prerequisites:** Before you begin, ensure that the following prerequisites are in place:

- [Node.js](https://nodejs.org/en/) installed on your computer.  
- A Node.js-enabled runtime environment such as Eclipse.
- Git software and access to the [GitHub source code repository for the API examples](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs).   Alternatively, you can download the [archive with the source code files](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs/archive/master.zip).
- Prepared source code.  
  To prepare the source code, complete these steps:
  1. Clone or download the [GitHub source code repository](https://github.com/IBM-Bluemix/iot4i-api-examples-nodejs) to your computer.
  2. Install the project's open source prerequisites by using a command prompt to go to the folder that contains the cloned source code files, and running `npm install` command.

Create a user that you can use to test the features of the dashboard and the sample mobile app.

1. Create a user in the {{site.data.keyword.iotinsurance_short}} system.
  1. Edit the createUser.js file to replace the values in the **user** variable with unique user information.
  2. Save the file.
  3. Run `node createUser.js`. The process takes a few moments to complete.
  4. Make a note of the user name; it is required in the next step.
2. Create a shield association for the user.
  1. Edit the createUserShieldAssociation.js file to add the user name from the previous step in the **username** variable.
  2. Save the file.
  3. Run `node createUserShieldAssociation.js`. For more information about shields, see [Components](iotinsurance_overview.html#components).
3. (optional) The analytics engine is updated automatically; however, if the correct data is not displayed, you can refresh the analytics engine by running `node updateAnalyticsEngine.js`.
4. (optional) Simulate a hazard event for the user.
  1. Edit the simulateHazard.js file to add the user name from the previous steps in the **usr** variable.
  2. Save the file.
  3. Run `node simulateHazard.js`.
5. (optional) Create a set of simulated historical data by running `node createHistoricalData.js`.


# Related Links
{: #rellinks}

## API Reference
{: #api}
* [{{site.data.keyword.iotinsurance_short}} API examples](https://iot4i-docs-api.mybluemix.net/dist/){:new_window}

## Related Links
{: #general}
* [Developer support forum](https://developer.ibm.com/answers/search.html?f=&type=question&redirect=search%2Fsearch&sort=relevance&q=%2B[iot]%20%2B[bluemix])
* [Stack overflow support forum](http://stackoverflow.com/questions/tagged/ibm-bluemix)
