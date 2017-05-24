---

copyright:
  years: 2015, 2017
lastupdated: "2017-04-10"

---
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# IP Table Rules

To allow the enforcement of iptable rules on your destination, you must have the `Restrict network access` option checked under the Network Security panel of your destination.  At that point you can add the rules you want enforced, such as: 192.0.0.1 9000 (single IP and port),  192.0.0.1-192.0.0.5 5000:5005 (range of IPs and range of ports), or any combination therein.

If you are creating your private destinations with cURL, you could use a command like:

```
curl "https://sgmanager.ng.bluemix.net/v1/sgconfig/<gateway_id>/destinations" -H "Authorization: Bearer <security_token>" -H "Content-type: application/json" -d '{"desc":"My Private Destination","ip":"1.1.1.1","port":8000,"private":true}'
```
{: pre}

Once your private destination is created, you can add IP table rules with commands like:

```
curl -X PUT "https://sgmanager.ng.bluemix.net/v1/sgconfig/<gateway_id>/destinations/<destination_id>/ipTableRule" -H "Authorization: Bearer <security_token>" -H "Content-type: application/json" -d '{"src":"192.0.0.1","spt":"9000"}' -k
```
{: pre}

and

```
curl -X PUT "https://sgmanager.ng.bluemix.net/v1/sgconfig/<gateway_id>/destinations/<destination_id>/ipTableRule" -H "Authorization: Bearer <security_token>" -H "Content-type: application/json" -d '{"src_range":"192.0.0.1-192.0.0.5","spt":"5000:5005"}' -k
```
{: pre}

Please note that the first command uses `src` to provide a single IP whereas the second uses `src_range` to provide a range of IPs.

## IP Table Rules for Dynamic IPs
What if I want to limit access to a {{site.data.keyword.Bluemix_notm}} application to make sure only my {{site.data.keyword.Bluemix_notm}} app XYZ should be able to connect to my on premise destination endpoint? I don't know the IP address of my {{site.data.keyword.Bluemix_notm}} app and even if I knew it today, it could change tomorrow if I restart it. How can I configure iptable rules for a {{site.data.keyword.Bluemix_notm}} application?

Your application can call the {{site.data.keyword.SecureGateway}} API whenever it starts up to dynamically add an iptable Rule for itself. If your IP will be changing often and you don't want to have logic in place to remove previous IP table rules (which could be difficult since you won't necessarily know your previous IP), you could provide an application ID in the body when adding a rule (app : <appID>). If you provide an app ID, it will replace any other rule that is already using that ID.  Adding or replacing a rule with this ID would look like:

```
curl -X PUT "https://sgmanager.ng.bluemix.net/v1/sgconfig/<gateway_id>/destinations/<destination_id>/ipTableRule" -H "Authorization: Bearer <security_token>" -H "Content-type: application/json" -d '{"src":"192.0.0.1","app":1234}' -k
```
{: pre}
