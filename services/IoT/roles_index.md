---

copyright:
  years: 2016, 2017
lastupdated: "2016-09-16"

---

{:new_window: target="blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# User, application, and gateway roles

Roles are sets of permissions that you can use to grant or restrict access to specific operations. You can use roles to manage permissions for groups of users, applications, and gateways.
{:shortdesc}

## User roles
{: #user_roles}

You can assign user roles when you add, invite, or register a user to your {{site.data.keyword.iot_full}}. You can also assign or change user roles at any time by using the {{site.data.keyword.iot_short_notm}} dashboard. For more information about assigning a role to a user, see [Managing user roles](managing_user_roles.html).

The following standard user roles are available:

User role | Description
------------- | -------------
Administrator | A 'super-user' role that grants access to all user-related APIs. Administrators cannot access operations that are restricted to devices and applications.
Operator | Intended for front-end organization users. Grants access to most organization operations, access control operations, analytics operations, third-party operations, and risk management operations.
Developer | Grants unrestricted access to device operations, log operations, cache operations, historian operations, analytics operations, and third-party service operations. The role provides limited access to organization, access control, and risk management operations.
Analyst | Grants access to analytics operations, including creating, updating, and deleting rules, actions, and schemas.
Reader | The default user role. Grants limited access to operations that are available to all users.

For more information about the user roles, see [User roles](reference/roles_access.html).

## Application roles
{: #application_roles}
You can assign application roles to grant or deny your applications access to specific operations. All application roles deny access to the following operations:

- All risk management operations
- Configure storage parameters
- Configure authentication providers
- Create, update, or delete email configuration

The following standard application roles are available:

Application role | Description
------------- | -------------
Standard | The default application role. Grants access to most application operations but no user or role operations.   
Operations | Grants access to the broadest range of operations, but denies access to subscribe or publish operations.
Backend Trusted | Intended for applications that do not require interaction from the systems operator. Denies access to device management, organization, role, or extension operations.
Data Processor | Intended for applications that perform analytics and data processing. Data processor applications are granted limited access to organization operations and user operations, but have full access to analytics operations, including creating and managing rules, actions, and schemas.
Visualization | Intended for applications that are responsible for generating visualizations of data. Visualization applications have access to live and stored data operations and dashboard operations.
Device | Intended for applications that take the role of devices; that is, they provide a source of data that is sent to the {{site.data.keyword.iot_short_notm}} as though it is a device. Device applications are granted only limited access to operations.

For more information about the operations access of application roles, see [Application roles](reference/app_roles_access.html).

## Gateway roles
{: #gateway_roles}
Gateways have a limited number of roles that govern the definition of the gateway and the ability to register devices to the {{site.data.keyword.iot_short_notm}}.

The following standard gateway roles are available:

Gateway role | Description
------------- | -------------
Standard | The default gateway role. It grants restricted access to operations.
Privileged | Intended for trusted gateways and allows privileged gateways to add devices to the {{site.data.keyword.iot_short_notm}}. It grants access to the relevant operations to add, update, and manage devices and device properties, but has no access to other operations.  

For more information about the operations access of gateway roles, see [Gateway roles](reference/gateway_roles_access.html).
