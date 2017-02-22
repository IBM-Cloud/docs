---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Levels of access for gateway roles

The following tables show the level of access for each of the gateway roles.

The tables show levels of access for:
- [Device Operations](#gateway-device-ops)
- [Log Operations](#gateway-log-ops)
- [Cache Operations](#gateway-cache-ops)
<!-- [Historian Operations](#gateway-historian) -->
- [Organization Operations](#gateway-org-ops)
- [Access Control Operations](#gateway-access-ops)
- [Analytics Operations](#gateway-analytics-ops)
- [Third-Party Operations](#gateway-third-party)  
<!-- - [Risk Management Operations](#gateway-risk-mgt) -->

## Gateway Roles
{: #gateway-roles}

### Device Operations {: #gateway-device-ops}

Device Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
Create, update, or delete devices|-|X
View devices|X|X
Activate device|-|X
Publish an event|X|X
Subscribe to an event|-|-
Publish a command|-|-
Subscribe to a command|X|X
Initiate device management action|X|X
View device management actions|X|X
Clear device management actions|-|-
Manage device management action bundles|-|X
Create, update, or delete device types|-|-
View device types|X|X
Manage diagnostic logs|-|-
View diagnostic logs|-|-

### Log Operations {: #gateway-log-ops}

Log Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
View server logs|-|-

### Cache Operations {: #gateway-cache-ops}

Cache Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
View live data (event cache)|-|-
Manage live data (event cache)|-|-


### Organization Operations {: #gateway-org-ops}

Organization Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
Configure storage parameters|-|-
Configure authentication Provider|-|-
Create, view, update, or delete Mail configuration|-|-
View available mail providers|-|-
Create, view, update, or delete mail templates|-|-
Create, update, or delete users|-|-
View users|-|-
Create, update, delete user invitations|-|-
View user invitations|-|-
Complete invitation|-|-
Create, update, or delete API Keys|-|-
View API keys|-|-
View organization usage information|-|-

### Access Control Operations {: #gateway-access-ops}

Access Control Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
View users properties (incl. access rights)|-|-
View users' own properties (incl access rights)|-|-
Manage users (incl. access rights|-|-
View API key properties (incl. access rights)|-|-
View API key's own properties (incl. access rights)|-|-
Create, update, or delete API keys (incl. access rights)|-|-
View device properties (incl access rights)|X|X
View device's own properties (incl. access rights)|X|X
Create, update, delete device (incl access rights)|-|X
View Roles|-|-
Create, update, delete Custom Roles|-|-
View Operations|-|-

### Analytics Operations {: #gateway-analytics-ops}

Analytics Operations || Gateway Roles|
:--------: | ---------------------|------------------------|
           | **Standard Gateway** | **Privileged Gateway** |
View analytics rules|-|-
Manage analytics rules|-|-
View analytics actions|-|-
Manage analytics actions|-|-
View analytics alerts|-|-
View analytics message schemas|-|-
Manage analytics message schemas|-|-

### Third-party Service Operations {: #gateway-third-party}

Third-party Service Operations || Gateway Roles|
:--------: | ---------------------|------------------------
           | **Standard Gateway** | **Privileged Gateway**
Process batch notifications from external platform|-|-
Process batch notifications and send them to external platform|-|-
Publish an event for a device|-|-
Subscribe to events from a device|-|-
set a callback URL for the external platform|-|-
Set subscription level of the external platform|-|-
Get status health status from connector|-|-
Verify if an external system is up and validate credentials|-|-
