---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

# Adding a Gateway

A gateway can be thought of as a way to identify a particular network or environment.  It is what a Secure Gateway Client will use to establish connectivity with the Secure Gateway servers and can contain multiple resource definitions, or destinations.

![Secure Gateway Dashboard](./images/newDashboard.png?raw=true "Secure Gateway Dashboard")

From the Secure Gateway Dashboard, click the Add Gateway button to open the Add Gateway panel.

![Add Gateway](./images/addGateway.png?raw=true "Add Gateway")

The only required input on this panel is your Gateway Name.  By default, both `Require security token` and `Token Expiration` are selected.

By requiring the security token to connect clients, each time you start a Secure Gateway client, you will have to provide both the Gateway ID and the Security Token.  If you uncheck the `Require security token` box, you will only have to provide the Gateway ID for the client to connect.

The default expiration date for the Security Token is 90 days from when it is created.  To change the expiration date, keep the `Token Expiration` box checked and edit the text field with the number of days you would like the token to expire in (minimum 1, maximum 365).  To create a token that does not expire, uncheck the `Token Expiration` box.  

To finish the creation of your gateway, click Add Gateway.  Once the gateway is created, the page will automatically navigate into your new gateway.

![New Gateway](./images/newGateway.png?raw=true "New Gateway")

Now that you have your newly created gateway, you can [connect your first client](./securegateway_client.html).
