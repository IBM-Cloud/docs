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

# Levels of access for application roles

The following tables show the level of access for each of the application roles.

The tables show levels of access for:
- [Device Operations](#app-device-ops)
- [Log Operations](#app-log-ops)
- [Cache Operations](#app-cache-ops)
<!-- [Historian Operations](#app-historian) -->
- [Organization Operations](#app-org-ops)
- [Access Control Operations](#app-access-ops)
- [Analytics Operations](#app-analytics-ops)
- [Third-Party Operations](#app-third-party)  
<!-- - [Risk Management Operations](#app-risk-mgt) -->

## Application Roles
{: #app-roles}

### Device Operations {: #app-device-ops}

Device Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
Create, update, or delete devices|X|X|X|-|-|-
View devices|X|X|X|X|X|-
Activate device|X|X|X|-|-|-
Publish an event|X|-|X|-|-|X
Subscribe to an event|X|X|X|X|X|X
Publish a command|X|X|X|X|-|-
Subscribe to a command|X|-|X|-|-|X
Initiate device management action|X|X|-|-|-|-
View device management actions|X|X|-|-|-|X
Clear device management actions|X|X|-|-|-|-
Manage device management action bundles|X|X|-|-|-|-
Create, update, or delete device types|X|X|X|-|-|-
View device types|X|X|X|X|-|-
Manage diagnostic logs|X|X|-|-|-|X
View diagnostic logs|X|X|X|-|-|-

### Log Operations {: #app-log-ops}

Log Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
View server logs|X|X|X|-|-|-

### Cache Operations {: #app-cache-ops}

Cache Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
View live data (event cache)|X|X|X|X|X|X
Manage live data (event cache)|X|X|X|X|X|X

### Organization Operations {: #app-org-ops}

Organization Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
Configure storage parameters|-|-|-|-|-|-
Configure authentication provider|-|-|-|-|-|-
Create, view, update, or delete mail configuration|-|-|-|-|-|-
View available mail providers|X|X|-|-|-|-
Create, view, update, or delete mail templates|X|X|-|-|-|-
Create, update, or delete users|-|X|-|-|-|-
View users|X|X|-|-|-|-
Create, update, or delete user invitations|-|X|-|-|-|-
View user invitations|X|X|-|-|-|-
Complete invitation|X|X|-|-|-|-
Create, update, or delete API Keys|-|X|-|-|-|-
View API keys|X|X|-|-|-|-
View organization usage information|X|X|-|-|-|-

### Access Control Operations {: #app-access-ops}

Access Control Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
View users properties, including access rights|X|X|-|-|-|-
View users' own properties, including access rights|-|-|-|-|-|-
Manage users, including access rights|-|X|-|-|-|-
View API key properties, including access rights|X|X|-|-|-|-
View API key's own properties, including access rights|X|X|X|X|X|X
Create, update, delete API keys, including access rights|-|X|-|-|-|-
View device properties, including access rights|X|X|X|X|X|-
View device's own properties, including access rights|-|-|-|-|-|-
Create, update, delete device, including access rights|X|X|X|-|-|-
View Roles|X|X|-|-|-|-
Create, update, delete custom roles|-|X|-|-|-|-
View operations*|X|X|-|-|-|-

### Analytics Operations {: #app-analytics-ops}

Analytics Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
View analytics rules|X|X|-|X|X|-
Manage analytics rules|X|X|-|X|-|-
View analytics actions|X|X|-|X|X|-
Manage analytics actions|X|X|-|X|X|-
View analytics alerts|X|X|-|X|X|X
View analytics message schemas|X|X|-|X|X|-
Manage analytics message schemas|X|X|-|X|-|-

### Third-party Service Operations {: #app-third-party}

Third-party Service Operations ||| Application Roles||||
:--------: | -------------|-------------|---------------|-----|---
           | **Standard Application** | **Operations Application** | **Backend Trusted Application** | **Data Processor Application** | **Visualization Application** | **Device Application**
Process batch notifications from external platform|X|X|-|-|-|-
Process batch notifications and send them to external platform|X|X|-|-|-|-
Publish an event for a device|X|X|-|-|-|-
Subscribe to events from a device|X|X|-|-|-|-
Set a callback URL for the external platform|X|X|-|-|X|-
Set the subscription level of the external platform|X|X|-|-|X|-
Get status health status from connector|X|X|X|-|X|-
Verify if an external system is up and validate credentials|X|X|X|-|X|-
