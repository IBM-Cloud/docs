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

# Levels of access for user roles

The following tables show the level of access for each of the default user roles.

The tables show levels of access for:
- [Device Operations](#user-device-ops)
- [Log Operations](#user-log-ops)
- [Cache Operations](#user-cache-ops)
<!-- [Historian Operations](#user-historian) -->
- [Organization Operations](#user-org-ops)
- [Access Control Operations](#user-access-ops)
- [Analytics Operations](#user-analytics-ops)
- [Third-Party Operations](#user-third-party)  
<!-- - [Risk Management Operations](#user-risk-mgt) -->

## User role permissions {: #user-roles}

### Device Operations {: #user-device-ops}

Device Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
Create, update, or delete devices | X | X | X | - | -
View devices | X | X | X | X | X
Activate device | X | X | X | - | -
Publish an event | - | - | - | - | -
Subscribe to an event | X | X | X | X | X
Publish a command | X | X | X | - | -
Subscribe to a command | - | - | - | - | -
Initiate device management action | X | X | X | - | -
View device management actions | X | X | X | X | X
Clear device management actions | X | X | X | - | -
Manage device management action bundles | X | X | X | - | -
Create, update, or delete device types | X | X | X | - | -
View device types | X | X | X | X | X
Manage diagnostic logs | X | X | X | - | -
View diagnostic logs | X | X | X | - | -

### Log Operations {: #user-log-ops}

Log Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
View server logs | X | X | X | X | X

### Cache Operations {: #user-cache-ops}

Cache Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
View live data (event cache) | X | X | X | X | X
Manage live data (event cache) | X	| X | X |	X	| -

### Organization Operations {: #user-org-ops}

Organization Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
Configure storage parameters|	X| - |-|-|-				
Configure authentication provider|	X|-|-|-|-				
Create, view, update, delete mail configuration	|X|-|-|-|-				
View available IoTP mail providers	|X|	X|-|-|-			
Create, view, update, delete mail templates	|X	|X	|-|-|-		
Create, update, delete users	|X|	X|-|-|-			
View users	|X|	X|	X|	X|-
Create, update, delete user invitations|	X	|X	| -|-|-		
View user invitations	|X	|X	|- |- |-		
Complete invitation	|X|	X|	X|	X|	X
Create, update, delete API keys	|X	|X	| -|-|-		
View API keys	|X	|X	|- |- |-		
View ORG usage information	|X	|X	| -|-|-		

### Access Control Operations {: #user-access-ops}

Access Control Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
View users properties, including access rights	|X|	X|	X|	X| -
View users' own properties, including access rights	|X|	X|	X|	X|	X
Manage users, including access rights	|X	|X	|-|-|-		
View API key properties, including access rights|	X|	X|	X|	X|-
View API key's own properties, including access rights	|-|	-|	-| -| -		
Create, update, delete API key, including access rights	|X	|X	|-|-|-		
View device properties, including access rights	|X|	X|	X|	X|	X
View device's own properties, including access rights	|-	|- |- |- |-
Create, update, delete device, including access rights	|X|	X|	X|	-| -
View roles	|X	|X	|X	|X	|X
Create, update, delete custom roles	|X	|X |- |- |-
View operations*	|X	|X	|X	|X	|X

### Analytics Operations {: #user-analytics-ops}

Analytics Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
View analytics rules|	X|	X|	X|	X|	X
Manage analytics rules|	X|	X|	X|	X| -
View analytics actions|	X|	X|	X|	X|	X
Manage analytics actions|	X|	X|	X|	X| -
View analytics alerts|	X|	X|	X|	X|	X
View analytics message schemas|	X|	X|	X|	X|	X
Manage analytics message schemas|	X|	X|	X|	X| -

### Third-Party Service Operations {: #user-third-party}

Third-Party Service Operations ||| User Roles|||
:--------: | -------------|-------------|---------------|-----|---
           | **Administrator** | **Operator** | **Developer** | **Analyst** | **Reader**
Process batch notifications from external platform	|X|	X	|X |-|-
Process batch notifications and send them to external platform	|X|	X	|X| -| -		
Publish an event for a device	|X|	X	|X|	- |-
Subscribe to events from a device	|X	|X	|X |-| -		
Set a callback URL for the external platform	|X	|X	|X|	-| -
Set the subscription level of the external platform|	X|	X|	X |- |-		
Get status health status from connector	|X|	X	|X	|- |-
Verify if an external system is up and validate credentials	|X	|X|	X	|- |-
