---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

# Managing your {{site.data.keyword.SecureGateway}} Service

## {{site.data.keyword.SecureGateway}} Dashboard
From your {{site.data.keyword.SecureGateway}} dashboard, you can quickly see the following details:

- The current number of connections to your destinations across all of your gateways.
- The inbound data flow across all your gateways in the past 12 hours.
- The outbound data flow across all your gateways in the past 12 hours.
- A graph displaying the past 12 hours of usage on a per gateway basis.
- Your existing gateways, their current status, and the number of destinations they contain.

![{{site.data.keyword.SecureGateway}} Dashboard with Usage](./images/dashboardUsage.png?raw=true "{{site.data.keyword.SecureGateway}} Dashboard with Usage")

### Service Profile
By clicking the Profile button, you can see:

Field | Description
-- | --
Plan Level | Your currently selected service plan.
Gateway Limit | The number of gateways you can have before being charged for extra gateways.
Client Limit | The number of clients you can connect to any single gateway.
Destination Limit | The number of destinations any single gateway can contain.
Data Limit | The amount of data transfer (in GB) that your plan supports before being charged for a data overage.
Gateway Overages | The current number of gateway overages you are being charged for.
Data Overages | The number of data overages incurred for the current month's billing cycle.

### Gateway Info Panel
By clicking the Settings button on any of the gateway tiles, you can see:

- The security token required to use the API or to connect a client, depending on whether the token is being enforced on client connections.
- The gateway ID required to use the API or to connect a client.
- The node your gateway has been created on.  This is the server your client will connect to.
- When the gateway was created and the user who it was created by.
- When the gateway was last modified and the user who it was modified by.
- A link to regenerate the certificate and key associated with the gateway.  These files are only used with legacy destinations that do not contain their own certificate/key pair for mutual authentication on the client.

The following tasks can also be completed from the Gateway Info panel:

- Edit or view more information about your gateway and security token.  A new panel is displayed when you select this option.
- Disable or enable the gateway.
- Delete the gateway.

## Dashboard for a particular gateway
By clicking on one of the gateway tiles, the dashboard for that particular gateway is displayed.  Similar to the main {{site.data.keyword.SecureGateway}} dashboard, you can quickly see the following details:

- The current number of connections to the destinations on this gateway.
- The inbound data flow across this gateway in the past 12 hours.
- The outbound data flow across this gateway in the past 12 hours.
- A graph displaying the past 12 hours of usage on a per destination basis.
- Your existing destinations, their current status, and their current number of active connections.

![Dashboard for a particular gateway](./images/viewGateway.png?raw=true "Dashboard for a particular gateway")

### Destination Info Panel
By clicking the Settings button on any of the destination tiles, you can see:

- The destination ID required to use the API.
- On-premises destinations will have a cloud host and port.  This information is required by your application in order to connect to your on-premises resource.
- Cloud destinations will have a client port.  This is the port the {{site.data.keyword.SecureGateway}} Client will be listening on in order to connect your on-premises application to your cloud resource.
- The resource host and port this destination is pointed to.
- When the destination was created as well as the user it was created by.
- When the destination was last modified as well as the user it was modified by.

The following tasks can also be completed from the Destination Info panel:

- Edit or view more information about the destination.  A new panel is displayed when you select this option.
- Disable or enable the destination.
- Delete the destination.
