---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-25"

---

# Frequently Asked Questions

## OSI Model Layer
{: #osi}

### Question
What layer of the OSI model does the Secure Gateway service represent?

### Answer
The Secure Gateway service represents layer 4 of the OSI model.

## TLS Version Support
{: #tls}

### Question
What version of TLS does the Secure Gateway service support?

### Answer
The Secure Gateway service supports TLS version 1.2.

## Why would I disable my gateway or destination?
{: #disabled}

### Question

Why would you want to disable a gateway or destination?

### Answer
You might want to disable a destination or gateway for one of the following reasons:

- You create a destination, but you have not set up the security.  In this case, you might disable the destination until its security is set up.
- You do not want the service to be available to users because you are making some updates to the service.  In this case, you might temporarily disable the necessary gateways and wait for the service to be updated.
- You have set up all your gateways and destinations on the front end, but your backend is still building.  In this case, you would disable your gateways or destinations until the backend build is complete.

For more information on disabling a gateway or a destination, see [how to manage your Secure Gateway service instance](./securegateway_managing.html).

## What is the recommended approach to creation automation across multiple spaces?
{: #automation-spaces}

### Question
A customer environment has one org and three spaces.  One space is for development, another for staging, and the final one for production.  Should the customer create a single Secure Gateway instance or multiple (e.g., one for each space).  If the customer can create multiple gateways, are there any considerations for reusing a Node.js application to create a gateway and destination in each space?

### Answer

- You can create a single Secure Gateway instance for all three spaces.  However, you must remember the gateway and destination [limitations for your specific plan](./securegateway_plans.html).
- There are no additional considerations for reusing a Node.js application as no service bindings are required by Secure Gateway.


## What is the recommended approach to creation automation across multiple orgs?
{: #automation-orgs}

### Question
A customer environment has three orgs: one for development, one for staging, and one for production.  Is a Secure Gateway service instance required for each org and is the configuration available to all spaces within that org?

### Answer

- You are not required to have a Secure Gateway service instance in each org.  You could have an instance in one org and use the gateways within that instance from all of your other environments.  With this setup, you must remember the gateway and destination [limitations for your specific plan](./securegateway_plans.html).
- You can have a Secure Gateway service instance in each org and the configuration will be available to all your spaces.

## Does my app need to be in the same space?
{: #app-space}

### Question
Do you need to run the Node.js app in the same {{site.data.keyword.Bluemix_notm}} space as the Secure Gateway service?

### Answer
No, you do not need to run your app in the same {{site.data.keyword.Bluemix_notm}} space as the Secure Gateway service.

## Can I get the Secure Gateway server logs?
{: #server-logs}

### Question
Can you retrieve error logs for the Secure Gateway server?

### Answer
Error logs on the server cannot be retrieved.  Only errors that are made at the time of the request can be seen.

## What are the functional states of Secure Gateway?
{: #states}

### Question
What are the different lifecycle states of gateways and destinations?

### Answer

#### Non-functional State
The 1.7.0 release introduced a new tiered plan pricing model. With this model came the ability to mark both Gateways and Destinations as 'Active' or 'Inactive'. Part of the new plan billing structure charges the user for the number of Gateways and Destinations that they have.

- Inactive items are not billed
- Inactive Destinations do not have a provisioned cloud port.
- All Destinations within an inactive gateway will also be inactive and cannot be reactivated until their Gateway is also set Active.
- Inactive items are considered Non Functional. Inactive items cannot be in the any of the Functional states.

#### Functional States
When a gateway or destination is marked active it will be billed. Active states for Gateways and Destinations are below:

- Enabled - the gateway or destination is ready for use under normal circumstances.
- Disabled - the gateway or destination has been disabled.
    - Gateways - clients will be unable to flow data to the disabled gateway.
    - Destinations - clients will be unable to create connections to these disabled destinations.
