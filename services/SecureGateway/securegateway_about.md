---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---

# About {{site.data.keyword.SecureGateway}}

## How is it secure?
{{site.data.keyword.SecureGatewayfull}} maintains a single persistent encrypted (TLS v1.2) connection between the {{site.data.keyword.SecureGateway}} Client (in the on-prem network) and the {{site.data.keyword.SecureGateway}} Servers.  With this bidirectional connection, we're able to securely transmit data between your cloud resources and your on-prem resources.  For the connections on either end (between cloud resource and SG Servers and between on-prem resources and SG Client), the user defines the protocol (TCP, TLS, HTTP, HTTPS, UDP) and security measures (mutual authentication, iptables) placed on them.  

## Bidirectional Support
By combining the traditional on-premises destination with the new cloud destination, we achieve complete bidirectional support.  The new cloud destination allows an on-premises service/application to send information/requests to a cloud application via the {{site.data.keyword.SecureGateway}} Client.  When creating a new cloud destination, the destination will contain `resource host` (the hostname or IP of the cloud application), `resource port` (the port that the cloud application will be listening on), and `client port` (the port that the {{site.data.keyword.SecureGateway}} Client will be listening on).  Once this destination is established, the on-premises service can then connect to the client port and begin sending data which will be sent through the client, to the {{site.data.keyword.SecureGateway}} Server, and then to the specified cloud application.

The client port that is provided for a destination must be unique within the associated gateway.  E.g., a single gateway cannot have two reverse destinations listening on port 12000, but two gateways can each have their own destination listening on port 12000.  However, in the latter case, if both of the gateways are connected to the same client, only one of the destinations will be able to listen on port 12000.

### Cloud Destination
![Cloud Destination](./images/reverseDestination.png?raw=true "Cloud Destination")

### On Premises Destination
![On Premises destination](./images/onPremDestination.png?raw=true "On Premises Destination")

## High Availability
To achieve high availability, create multiple client connections to the same gateway ID.  This can be accomplished by connecting multiple single-gateway clients to the same gateway ID and/or by issuing multiple connections on a single multi-gateway client to the same gateway ID.  Connections will be distributed between all connected clients in a round-robin fashion.
