---

copyright:
  years: 2015, 2016, 2017
lastupdated: "2017-03-17"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# IBM Cloud Identity and Access Management (IAM)
{: #iam_overview}

IBM Cloud IAM provides a secure way to manage user and service identities and the access to resources for those identities. You can view and manage users across the account or organization, depending on the access options that you are authorized to manage. You can perform all operations for users including inviting and managing users and their assigned roles, and the accounts or organizations, or both, that they can access. As an account owner, you can manage the access options of which you and the users are both members, regardless of role, in the current account.

Identity management includes the following:
 * User management 
   * create, delete, update user information
   * API Key management
   * token creation, refresh and exchange
   * user identity authentication
 * Service id management
   * create, delete, update user information
   * API Key management
   * token creation, refresh and exchange
   * service identity authentication
   
   
Access Management includes the following:
 * Policy Management
   * create, delete and update policies
 * Decisions on access to resources
 
## Identity Overview
{: #identity}

The Cloud IAM Token Service is the authentication service for IBM Cloud and builds on the open standards specified by [OAuth 2.0]( https://tools.ietf.org/html/rfc6749), [JWT](https://tools.ietf.org/html/rfc7519), [JWT Profile](https://tools.ietf.org/html/rfc7523), and [JWKS](https://tools.ietf.org/html/rfc7517).

One focus of the Token Service is the authentication of developers, operators and administrators for the IBM Cloud Platform. For this authentication, the Token Service is connected to the IBMid system to authenticate users and in dedicated and local environments, it can be connected to a customer chosen authentication system like LDAP. 

To retrieve an IAM token, you can use the standard OAuth 2.0 grant types like `password`, for example:
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=password&username=<IBMid>&password=<IBMid password>
       [&ims_account=<ims account>][&bss_account=<bss account>]
       [&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

As an extension to OAuth 2.0, you need to provide account information to make the token account specific. Also you can list different response types to get `UAA` or `IMS` tokens for interactions with CloudFoundry APIs or IMS APIs.

The Cloud IAM Token Service allows you to create, update, delete and use API keys for users. Those API keys can be created either with API calls or the Bluemix Console. To leverage an API key, an adopter can use the following extended grant type:
```
curl 
    -u "<clientid>:<clientsecret>" 
    –H "Content-Type: application/x-www-form-urlencoded" 
    –d "grant_type=urn:ibm:params:oauth:grant-type:apikey&
       apikey=<apikeyvalue>[&response_type=cloud_iam,uaa,ims_portal]"
    "https://iam.ng.bluemix.net/oidc/token[?pretty=true]"
```
{: codeblock}

The resulting token can be used like one retrieved with a password grant or UI login.

As further variation, the Cloud IAM Token Service allows you to log in interactively with the UI. This is implemented by using the OAuth 2.0 grant type `authorization_code` and is also known as `OAuth Dance`, because it causes multiple web browser redirects during the authentication phase.

The other focus of the Token Service is the ability to create Service Ids and API keys for Service Ids. A Service Id is similar to a "functional id" or an "application id" and is used to authenticate against services, and not to represent a user.

Users can create Service Ids and bind them to scopes like a Bluemix account, CloudFoundry organization or a CloudFoundry space. This binding is done to give the Service Id a container to live in. This container also defines who can update and delete the Service Id and who can create, update, read and delete API Keys that are associated to that Service Id. A Service Id is NOT related to a user.

To get a better understanding of how to use Service Ids, you can try out our [Demo Application](https://iam.ng.bluemix.net/demo) that demonstrates the APIs.

## Access Management Overview
{: #access_management}

IAM is an Attribute Based Access Control system (ABAC) with conditions inspired by the
[NIST](http://nvlpubs.nist.gov/nistpubs/specialpublications/NIST.sp.800-162.pdf) publication.  

IAM uses a combination of attributes to determine access to resources. IAM policies have rules that are applied to the roles, users/service ids attributes, resource attributes, and conditions. This allows a flexible and powerful approach to defining access for users and service ids.

For example, take a virtual machine, VM123 can have the following attributes: 
```
    resource: {
      'serviceName': 'virtual-machine',
      'region': 'us-south',
      'resourceType': 'vm',
      'resource': 'vm123'
    }
```
{: codeblock}
  
Any combination of those resource attributes can be used to create a policy.

For more detailed examples, see [IAM Policy examples](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/policy_examples.html#iam_policy_examples).

ABAC is different than Role Based Access Control (RBAC), where pre-defined roles are assigned to users. These pre-defined roles have specific privileges and users with that role have all of the privileges that are defined by that role. 
 
For example, a Virtual Machine `Administrator` Role. This role implies all Administrator type privileges on any virtual machine resource. 

A simple way to think about ABAC is:

1. There are Users, Resources, Contexts, and Actions.
1. Each instance of a User, Resource, Context, and Action has a unique identifier.
1. Each instance is given attributes.
   Basically this means: "What is true about the instance from an authorization standpoint".
   Examples:
   1. The User is a Pisces and was born in the 1960's.
   1. The Resource is a Baseball team roster.
   1. The Context is 9:00 AM to 5:00 PM Eastern Time.
   1. The Action is "can update".
1. Policies are created to determine what set of attributes have permission for the User to perform the Action on the Resource.
1. When a request is made by a User to perform an Action on a Resource, the policies are consulted to see whether the request is allowed.

The following image shows a detailed view of the authorization sequence.

![Authorization Sequence](auth_sequence.png)

## Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To set up access control for your service you must use the following steps as part of your onboarding process:

### Step 1: Create a service id by making this http request:
```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
```
{: codeblock}

Curl command:
```  
curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
```
{: codeblock}

The following describes the `Service id` and `Service crn` values used in the `curl` command in more detail:
  
#### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value that is specified has no effect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization. When you onboard with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources that are owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/) for more information on this api and related apis.

#### Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help completing these fields.

From the response, save metadata->uuid and metadata->crn, which are your service id and service id crn.


### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id is given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```
{: codeblock}

### Step 3: You must create an api-key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
{: codeblock}

Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
{: codeblock}

`boundTo` needs to be the crn of your service id (field metadata->crn saved from step 1’s response). The name and description can be anything.

From the response, save entity->apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

### Step 4: Get an access token for your service IDs API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, which is your API key value (apikey_value).

  * Then get the token with the API key value (make sure that you use escape characters):

    Curl Command: 
```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
```
{: codeblock}

Use the **access_token** field in the result, which is your api-key token (for your service id). The **access_token** needs to be URL-encoded when used in the curl command that's previously shown.


### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
  
Curl command:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```
{: codeblock}

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
{: codeblock}
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, when using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  

### Step 6: Verify the service registered according to the details in step 5.

```
curl -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Step 7 (Optional): Delete the service that you registered in step 5.

```
curl -X DELETE -H "Authorization: <api key token>" "https://iampap.ng.bluemix.net/acms/v1/services/<service_name>"
```

### Step 8: Configure the service to use the PEP SDK in order to check permissions with the PDP. Choose the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)
 

## Terminology
{: #terminology}

### Identity Terminology

* IBMid - An identity provided and hosted by IBM to access the IBM Cloud, IBM applications, communities, and support.
* User Id - Identification that represents a real person.
* Service Id - Identification that represents a technical user, machine, application or services. Similar to "Functional Ids" or "Application Ids" that also represent a technical user, but uses the "User Id" entity type.
* OAuth 2.0 - Open standard to authorize access to applications and APIs without providing credentials to the target service. OAuth is also used to contain authentication information.
* OpenID Connect - Open standard built on top of OAuth 2.0 which focuses on providing information about the authenticated user.
* Client Id - Applications that interact with OAuth 2.0 compliant endpoints require a secret client id / secret pair to authenticate. An application needs to register with a Token Service to get a client id.
* Token endpoint - Used by the client to obtain one ore more tokens by presenting identity information like a username or password, authorization grant or refresh token.
* Authorization endpoint - Used by the client to authenticate a user through the UI to the token service.
* Token - An opaque or transparent string that enables an application to retrieve the authentication and/or authorization of an identity.
* Access token - This token is used to be sent around as identity information to APIs. It contains identity information and is only valid for a short time.
* Refresh token - This token is stored on the client that requested authentication only. It is used to get a new access token, (i.e. refresh the access token), if the access token expires. As the refresh token is long living, it must not leave the client system except for the purpose of refreshing the access token itself.
* Identity cookie - Upon login to the IBM Cloud Token Service, a cookie containing your identity is issued to your browser. You will not be re-challanged to login as long as this cookie exists and is valid. It expires after 24 hours, if you logout from the IBM Cloud Token Service or if you close your browser.
* JSON Web Token - A JSON-based standard (RFC 7519) to represent access tokens. The content of the access token is transparent, (i.e. can easily be read). A JWT-based token is typically signed to be able to verify the proof of origin of that token.
* Public Key - Can be used to validate a signature of a JSON Web Token. If using asymmetric encryption, the public key can safely be published for consumption by clients.
* Private Key - Can be used to create a signature for a JSON Web Token. This key must be kept secret, otherwise valid access tokens can be created by others.
* realmid - Identifier to distinguish users from different user registries. Currently used values are "IBMid" for users authenticated by the IBMid system and "iam" for Service Ids authenticated by the Token Service.
* identifier - Identifier which never changes and uniquely identifies a user inside one user registry (denoted by the `realmid` parameter). The combination <realmid>-<identifier> must always result in a uniquely identifiable user. In the case of IBMid, the IBM unique identifier 'IUI' is used.             
* subject - The user name of the identity. Often in the same form like an email address. In the case of IBMid, this is the IBMid of the identity.
* Custom claims - Additional non-standard information inside a JSON Web Token.

### Access Management Terminology

* (PAP) Policy Administration Point - Point that manages access authorization policies.
* (PDP) Policy Decision Point - Point that evaluates access requests against authorization policies before issuing access decisions.
* (PEP) Policy Enforcement Point - Point which intercepts user's access request to a resource, and makes a decision request to the PDP to obtain the access decision (i.e. access to the resource is approved or rejected), and acts on the received decision.
* (PIP) Policy Information Point - The system entity that acts as a source of attribute values (i.e. a resource, subject, environment).
* (PRP) Policy Retrieval Point - Point where the XACML access authorization policies are stored, typically a database or the file system.
* subject - The "who" in a resource and subject authorization pair, such as a user or group. The resource is which resource the subject can access.
* role - A collection of permissions that can be assigned to a user, group of users, system, service, or application that enable it to perform certain tasks.
* resource - A physical or logical object that actions can be performed on, such as an organization, a space, a database, or a table.
* conditions - A function that evaluates to "True", "False" or “Indeterminate”.
* actions - A defined task that an application performs on an object or resource as a result of an event.
* policy - A set of rules, an identifier for the rule-combining algorithm and (optionally) a set of obligations or advice. Can be a component of a policy set.

## System Defined Roles
{: #system_defined_roles}

IBM Cloud Roles represent a collection of actions and these actions are provided by IAM enabled services.

Grouping actions as roles provides flexibility to support actions for any 
services or resources by using a minimal set of System defined 
roles. For example, if you need an `Administrator` for VMs, Storage and 
Networking, you can use the `Administrator` role for all three but just change 
the target of the policy. `Administrator` on VMs, `Administrator` on Storage 
and `Administrator` on Networking.

*What IBM Cloud IAM does not do*: An alternative that is used by other access management 
systems are to build resources into the role. This approach inadvertently causes 
a new role name for every type of resource that is introduced in the system. For 
example, with this approach you would need a `VMAdministrator` role, a 
`StorageAdministrator` role and a `NetworkAdministrator` role to cover 
administration for resources of VMs, Storage, and Network.


The following table shows IAM System Defined Roles and examples of actions that map to them.

|IBM Cloud Role Name| Description | Example Actions|
|:-----------------|:-----------------|:-----------------|
|Viewer|actions that do not change state (i.e. read only)| <ul><li>list devices</li><li>read storage object</li><li>run query</li><li>execute search</li></ul>|
|Editor|actions that can modify the state and create/delete subresources|<ul><li>create vm</li><li>delete vm</li><li>attach storage</li><li>reboot</li><li>start/stop</li><li>rename</li></ul>|
|Operator|actions required to configure and operate resources|<ul><li>update configuration</li><li>start/stop vm</li><li>view logs</li><li>backup/restore</li></ul>|
|Administrator|all actions including the ability to manage access control|<ul><li>invite user</li><li>create vm</li>update user access policies</li><li>list devices</li><li>create vm</li><li>delete vm</li><li>attach storage</li><li>reboot</li><li>start/stop</li><li>rename</li><li>backup/restore</li></ul>|
|Billing Administrator|actions related to the administration of billing|<ul><li>update credit card</li><li>list invoices</li><li>download invoices</li></ul>|

The most current list of System Defined Roles can be queried from the PAP 
micro-service at:

Curl command: 

`curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'`
    
    
## Service action format
{: #action_format}

Actions must be defined in 1 of 2 formats:
  
* Standard:

    `<service-name>.<component>.<verb>`
* Access Control Intercept Point: 

    `<METHOD> /<api_route>`
  
### Standard
Most services call the IAM PDP directly and can modify source code to support the standard action formatting.  
 
 This format must include all three parts and is alphanumeric, no spaces or special characters other than '-'.

`<service-name>.<component>.<verb>`

Where 
* service-name - The service name that is defined in the CRN service-name field.
* component - resource or subresource of the service.
* verb - Verb that defines supported action for the service name component. 
  
For example: `key-protect.keys.decode` 
* service-name = key-protect
* component = keys
* verb = decode

### REST API Access Control Intercept Point
{: intercept_point}

In some cases REST API requests are directed through a gateway that acts as an Access Control Intercept Point. The IAM PDP is called directly from the intercept point before calling the actual REST API service. The service that processes the REST API request never calls the IAM PDP.

The intercept point only knows about the REST API route and the endpoint to send the request to. See, [Considerations for Access Control Intercept Points](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/intercept_point.html#intercept_point_overview) for more details.


 This format must include all of both parts and supports safe characters for URLs as specified by [RFC 1738](https://www.ietf.org/rfc/rfc1738.txt).
 
 
`<METHOD> /<api_route>`
  
Where
* METHOD - The REST API method. 
* api_route - The URI for the REST API.

For Example: `GET /v1/things/thing123`
* METHOD = GET
* api_url = /v1/things/thing123

<!---
# Setting up access control for your service
{: #setup_access_mgmt}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding.

To setup access control for your service you must use the following steps.

#### Step 1: Create a service id by making this http request:
  ```
  POST https://iam.ng.bluemix.net/serviceids
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "name": "<service id name>",
    "description": "<service id description>",
    "boundTo": "<crn>"
  }
  ```
Curl command:
  ```  
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"name": "<service id name>", "description": "<service id description>", "boundTo": "<crn>"}' 'https://iam.ng.bluemix.net/serviceids'
  ```
  
### Service id 
  
The service id name can be the same as the service name that appears in the crns for your service.
  
Your service id must be bound to an account, organization, or space. This binding determines who can manage your service id. For example, the administrator where your service id is bound are able to update or delete. Your {{site.data.keyword.Bluemix_notm}} token needs to have access to the account, organization, and space you are binding the id to. To bind to an account, the `boundTo` crn must look like the following: 

`crn:v1:::<service name>::a/<account id>:::` 
  
For an organization it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:o/<organization id>:::` 
  
For a space it must look like the following:
`crn:v1:<cname>:<ctype>:<service name>:<region>:s/<space id>:::`  
  
The `boundTo` value specified has no affect on which resources your service id can access. 
  
IAM access policies control which resources your service id can access. Even though your service id is bound to an IBM organization, IAM policies can be created that allow your service id to access resources outside of that organization.  When on boarding with IAM the first access policy that is created by the IAM team allows the service id to create policies for any resources owned by your service.

See [createServiceid](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createServiceid) for more information on this api and related apis.

###Service crn

The service-name in the `boundTo` crn must match the service name that appears in the crn for your service.
  
See the [CRN spec](https://github.ibm.com/ibmcloud/builders-guide/blob/master/specifications/crn/CRN.md) for help filling in these fields.

From the response, save metadata->uuid and metadata->crn, which are your service id and service id crn.


#### Step 2: Contact the AccessControl Squad at [#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 
Your service id will be given the role of Administrator of policies for your service's resources.

Use this format:
```
IAM adopter service info

service id: uuid from step #1
service name: your service name as it will appear in the crns for your service
```

#### Step 3: You must create an api key from your service id. Use the following http request:
```
  POST https://iam.ng.bluemix.net/apikeys
  Authorization: <bluemix token>
  Content-Type: application/json

  {
    "boundTo": "<service id crn>",
    "name": "<api key name>",
    "description": "<api key description>"
  }
```
Curl command: 
```
  curl -X POST -H 'Authorization: <bluemix token>' -H 'Content-Type: application/json' -d '{"boundTo": "<service id crn>", "name": "<api key name>", "description": "<api key description>"}' https://iam.ng.bluemix.net/apikeys
```
`boundTo` needs to be the crn of your service id (field metadata->crn saved from step 1’s response). The name and description can be anything.

From the response, save entity->apiKey.

See [createAPIKey](https://iam.stage1.ng.bluemix.net/ibm/api/explorer/#!/Cloud_IAM_Service_Id_and_Api_Key_MVP/createAPIKey) for more information on this api and related apis.

#### Step 4: Get an access token for your service id's API key. 

When the permission is established, your service can make PAP and PDP requests for your service's resources.

Use the entity **apiKey** field from step #3, this is your API key value (apikey_value).

  * Then get the token with the API key value (make sure you use escape characters):

    Curl Command: 
    ```
    curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H "Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-type%3Aapikey&apikey=<apikey_value>" "https://iam.ng.bluemix.net/oidc/token"
    ```

Use the **access_token** field in the result, this is your api key token(for your service id).


#### Step 5: Register the list of possible service actions for the service name.

  a. Map service actions to IAM System Defined Roles. This mapping is used later during the service registration.

  * A list of IAM System Defined Roles can be found by performing the following request:
Curl command:
```
curl -X GET --header 'Accept: application/json' --header 'Authorization: <api key token>' 'https://iampap.ng.bluemix.net/acms/v1/roles'
```

**Note:** Use the _crn version_ of the IAM System Defined Roles in your service registration payload.

The following is an example of mapping service actions to roles.

  <table>
    <tr>
      <th>API Endpoint</th>
      <th>Service Action</th>
      <th>IAM System Defined Roles</th>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}</td>
      <td>key-protect.keys.create</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>GET /api/keys/{key_id}</td>
      <td>key-protect.keys.read</td>
      <td>Viewer, Editor, Administrator</td>
    </tr>
    <tr>
      <td>PUT /api/keys/{key_id}</td>
      <td>key-protect.keys.update</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>DELETE /api/keys/{key_id}</td>
      <td>key-protect.keys.delete</td>
      <td>Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/encode</td>
      <td>key-protect.keys.encode</td>
      <td>Editor, Administrator</td>
    </tr>
    <tr>
      <td>POST /api/keys/{key_id}/decode</td>
      <td>key-protect.keys.decode</td>
      <td>Editor, Administrator</td>
    </tr>
  </table>

  b. Use the following command line to register your service with the `PAP`:
```
  curl -X PUT -H 'Content-Type: application/json' -H 'Accept: application/json' -H 'Authorization: <api key token>' -d '{
    "displayName": {
      "default": <service display name>
    },
    "actions": [{
      "id": <service_action>,
      "displayName": {
        "default": <service action display name>
      },
      "roles": [<system_defined_role_crn>]
    }]
  }' 'https://iampap.ng.bluemix.net/acms/v1/services/<service_name>'
  ```
  
Actions must be defined as specified in the 
[Service Action Format](https://console.stage1.ng.bluemix.net/docs/developing/Access-Management/index.html#action_format).
  
For example, using the standard format:

  `<service-name>.<component>.<verb>`
  
  Using action `key-protect.keys.decode` from the previous example 
  * service-name = key-protect
  * component = keys
  * verb = decode
  
  [TODO: Also support REST like action format, yet to be approved]: <>

#### Step 6: Configure the service to use the PEP SDK in order to check permissions with the PDP. Pick the corresponding SDK language.

  * [PEP SDK for Java](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Java)
  * [PEP SDK for Nodejs](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Node)
  * [PEP SDK for Python](https://github.ibm.com/IAM/access-management/wiki/PEP-SDK-for-Python)


<!---
# Identity and Access Management Adopter Guidelines
{: #iam_guidelines}

Onboarding a service to {{site.data.keyword.Bluemix_notm}} is a different set of operations than onboarding a service with Cloud IAM. Technically you can onboard with {{site.data.keyword.Bluemix_notm}} and Cloud IAM independently and in any order. The Cloud IAM team is working with the {{site.data.keyword.Bluemix_notm}} service onboarding team so that the {{site.data.keyword.Bluemix_notm}} service on boarding process will also include Cloud IAM onboarding. Until that work is complete please use the following onboarding steps.

- Users are identified with their IBMid.
  - Users authenticate with their IBMid and password.
  - Authentication returns a UAA/OAuth token which is used to access services within the IBM Cloud.
  
- Services are identified by their ServiceIDs.
  - Services authenticate with their ServiceID and APIkey.
  - Authentication returns an OAuth token which is used to access other services within the IBM Cloud.
  
- Services grant access to their resources by creating *Access Policies*.
  - *Roles* can be viewed and *Access Policies* can be managed through the 
  *Policy Administration Point (PAP)*.
  - Actions are permitted or denied through the *Policy Enforcement Point (PEP)* and *Policy Decision Point (PDP)*. 
  

## Creating a ServiceID
{: #create_serviceid}

To create a ServiceID you must use one of the following steps:

Make a one-time request for your ServiceID/APIkey.

 * Create a ServiceID with [swagger](https://iam.ng.bluemix.net/docs).
```
POST /serviceids
```
 * Create a ServiceID using `curl`.
```
curl -X POST -H "Authorization: $CF_TOKEN" -H 'Content-Type: application/json' -d '{"name": "IAMdemo", "description": "IAM demo of adopting service", "boundTo": "crn:v1:staging:public:docker-registry:us-south:o/57666a74-e136-4eb0-a085-220345fac266:::"}' 'https://iam.ng.bluemix.net/serviceids’
```
**Note**
The `boundTo` is the {{site.data.keyword.Bluemix_notm}} Org that is owned by you or your admin.

## Creating a ServiceID metadata response
{: #create_serviceid_metadata}

The following is a ServiceID metadata response using `curl`. Your service ID is expressed with a UUID and CRN format.

```
{"metadata":{\
"uuid":"ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"crn":"crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::\
serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07",\
"version":"1-4d9b1b10ce893f750a2d7e0d6ee34fd7"},"entity":{"boundTo":"crn:v1:staging:public:docker-registry:\
us-south:o/57666a74-e136-4eb0-a085-220345fac266:::","name":"IAMdemo","descripti\
on":"IAM demo of adopting service"}}
```

## Creating an APIkey for your ServiceID
{: #create_apikey_serviceid}

Create an APIkey
```
POST /apikeys
```

The following is a `curl` example of creating an APIkey
```
curl -X POST -H 'Authorization: $CF_TOKEN' -H 'Content-Type: application/json' -d '{"boundTo": "crn:v1:staging:public:iam:us-south:o/57666a74-e136-4eb0-a085-220345fac266::serviceid:ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07", "name": "IAMdemo", "description": "IAM deom of adopting service"}' https://iam.ng.bluemix.net/apikeys
```

## Authenticating with an APIkey
{: #auth_apikey}

The following is a `curl` example of authenticating with an APIkey
```
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -H \
"Accept: application/json" -d "grant_type=urn%3Aibm%3Aparams%3Aoauth%3Agrant-ty\
pe%3Aapikey&apikey=DuE2s….bfRKc=" "https://iam.s\tage1.ng.bluemix.net/oidc/token”
{"access_token":"eyJraWQiOiIyMDE2MTAyNC0wMDowMDowMCIsImFsZyI6IlJTMjU2In0.eyJpZG\
VudGlmaWVyIjoiU2VydmljZUlkLTNlYzBkZDAyLTdhMTAtNDBiZi05MmU3LWI5YTMyOTU0N2MwNyIsI\
nN1YiI6IlNlcnZpY2VJZC0zZWMwZGQwMi03YTEwLTQwYmYtOTJlNy1iOWEzMjk1NDdjMDciLCJzdWJf\
dHlwZSI6IlNlcnZpY2VJZCIsImFjY291bnQiOnsiYnNzIjoiMDY0Zjg3NTZlMzZlODk5MDAyYjliM2M\
wNzZiZTM3OGIifSwibWZhIjp7fSwiaWF0IjoxNDc5Mzk3MTYwLCJleHAiOjE0Nzk0MDA3NjAsImlzcy\
I6Imh0dHBzOi8vaWFtLnN0YWdlMS5uZy5ibHVlbWl4Lm5ldC9vaWRjL3Rva2VuIiwiZ3JhbnRfdHlwZ\
SI6InVybjppYm06cGFyYW1zOm9hdXRoOmdyYW50LXR5cGU6YXBpa2V5Iiwic2NvcGUiOiJvcGVuaWQi\
LCJjbGllbnRfaWQiOiJkZWZhdWx0In0.APRVqQmfUwn6K4Kg2sicT_kGpqSGQXr4Vua8Q5p4B0_dfGE\
tbbe10JqHeE4ovud6u8xjclAIcqCcbjIH4RijnUNGReVse49gS6JlXxmiNGA8OVlNGjiL68ygIpYsj-\
crx8kVuTrXAFqx9lhLEBhAzDneldu-gjSz7wrQKqISikcMXPXQkmLDuoT-OGNq8rG4fCiENBiweUrGf\
_Yw9W5NSiWyQGdWmczS70Krc_hx1iXskmt8pz5_0_vPXY6_tG5rY6KPw-bHO1wux91Q7aTZwCmaL0zI\
F2d3cIuFe1XywJ_926MfwWy65MxC3xv7-_rsZMFoprrLtBsuEnshNWUDhg",
"token_type":"Bearer","expires_in":3600,"expiration":1479400760}
```

## Registering your ServiceID with IAM
{: #register_serviceid}

To complete the on boarding process, contact the AccessControl Squad at
[#iam-adopters](https://ibm-cloudplatform.slack.com/messages/iam-adopters). 

Your service id will be given the role of Administrator of policies for your 
service's resources.

Call the `PAP` and `GET` the existing policies
```
curl -X GET -H 'Authorization:<APIkeyToken>' \
'https://iampap.ng.bluemix.net/acms/v1/scopes/global/service_ids/\
ServiceId-3ec0dd02-7a10-40bf-92e7-b9a329547c07/policies'

Response:
{"policies":[]}  <-- no policies yet
```

## Creating access policies
{: #creating_policies}

Now that you are fully on boarded, you can begin creating access policies 
for resources owned by your service.
-->

# Lab Service Ids and API keys

interconnect-service1:
  * ServiceId-2bc4561c-615f-4ba3-ab50-eba3b70a69d3
  * 7DRDYlbFM8Mpt7cOKS7clQisOItOfFcvItkd4MQsd20M

interconnect-service2:
  * ServiceId-089f58e9-f0a0-4b47-b3db-a2d9036080aa
  * rOB0ZqGR1pbiWxNMbn_OfFDmuJcULhqnYW_G0hNnJj0w

interconnect-service3:
  * ServiceId-9a57c3ed-2a8d-45ff-8b34-a7feb80e81bd
  * 6qZoPsd_V47hQQHHVFR1Z8PeGwTZKmNxHgGlURH7OIPf

interconnect-service4;
  * ServiceId-df633c5f-dee3-4e7b-87c3-7a3ed57d6509
  * 3yICAhsR55nlXJLjPA2nLBcAM1SX7LrXpOabjivVeteQ

interconnect-service5:
  * ServiceId-e3703b76-4f91-4323-9b6d-db3122952a72
  * 1ZD8qf_jqHC7JVOzrrvbuI3Dcr153hkGsr4Ll7EvsXKW

interconnect-service6:
  * ServiceId-2a31b14e-6cad-4597-82cf-04f2cb16c26d
  * XFROeDFVyBnJfecSjNhZngPDOniX-5qXl9QWZrsuNjYY

interconnect-service7:
  * ServiceId-56b98026-bb1c-4166-8128-c4841d10373c
  * cBponeC40MEgPy4mW55kb26XbMFAVmF0y2T3T1fYXJuL

interconnect-service8:
  * ServiceId-7a9cf953-044e-474a-9ffb-e66a1b68f437
  * OEGprDQNk7TLxFNrCbKfvLGxQRrbGS-PvhKSCUYJYn1a

interconnect-service9:
  * ServiceId-147203b6-0156-41c6-a28c-7306f047eebb
  * 2OiRisDKDXYA0_0BtlA7OyBk-7II9NUa709HgbF-D_kY

interconnect-service10:
  * ServiceId-87909073-acb8-403c-ab32-91d632e6c5a6
  * 93eWV_Ns2UrjNGENaaau1yOQmGDvTO2FxEivThGIZUOV

interconnect-service11:
  * ServiceId-0e2ec208-926e-4db7-aab4-c0d3bf44865f
  * gEa6bECSMAVF68cS5AbckIKp47_OX3_q63JNWI6-Q5Y0

interconnect-service12:
  * ServiceId-c793ae24-5f43-4c55-815a-830b8c79d1ee
  * WRSnr-FJZ_mI2DbG-8MNqPdAZHq3IkVZU-WbWL7l7uNC

interconnect-service13:
  * ServiceId-b426e816-6975-47df-ac69-01c08560ef3e
  * MkFJJ_zJDg5MiIRUo78dzCC-Mmw3r9DSzZVMvHZ7A63Z

interconnect-service14:
  * ServiceId-d97a9df4-6dbe-43ab-8b10-a70bb3ff9085
  * N63GX1wfo6UDc5kNrEWYHcPT27bD9V0JLmoB-iKsPfEb

interconnect-service15:
  * ServiceId-c6090a5b-569d-40cc-84f5-12480a9ede60
  * xLuJdPmW5npQMuHs4hyJOWZMaYY7i_DwZOSjWlZjnjjK

interconnect-service16:
  * ServiceId-c1d34878-cac3-43a3-bad6-a5b4992d9ed9
  * UZjSMGF8Aw42lzbHtkgDH14FyJxe0s0aN0O4Qk9uBe8T

interconnect-service17:
  * ServiceId-9ccaba36-6b07-4e9b-8b97-fbe1111f4908
  * CJb3qUI3cQWUiMMSt2RuL3ti9yE-F2-i2-1yIfowOM30

interconnect-service18:
  * ServiceId-84a01c41-8330-49e3-842f-b45eaa368d3d
  * 8-qw4_k5Sbjd1sxAiKksHubfPIlkjK2C9S0DnK-WpPDo

interconnect-service19:
  * ServiceId-2ef5d7ea-7ce0-453d-aa70-fbc5f4b781ef
  * Cz4QHZR_qd_WUZsScF-dVcu31J08dPuF_gszMd4oCLJj

interconnect-service20:
  * ServiceId-9e85525e-fe29-45e1-81b5-0681cd0b7f22
  * -OeamgjtKqnGUmdKFAVOWjKhYJMYP8HstCcPrRKfy4V9

interconnect-service21:
  * ServiceId-62c49423-3205-446e-a4aa-e24deb9b158e
  * N2XQ6MpKTvRJX_2IuDQoOiMK5AIhICUFj2wMVyg8O6Pn

interconnect-service22:
  * ServiceId-2de4c08b-f2cc-4e93-bb8b-eebf2222f93e
  * lEOzJvJJV0EgDjQQa8g5kr_D-PawYqIN-QE1QTNpoD5S

interconnect-service23:
  * ServiceId-49e6dc57-70f2-4a69-aac9-311394454475
  * G7epLqdbohZ8tVs8Jcx4qSjlMzlzrw2piNEnPiP4RZ7A

interconnect-service24:
  * ServiceId-7a4ac3ec-bd69-4dbf-8439-f8f5a2ffb88a
  * I7d2KnqbyeQG1rk1AcKeVXgNT1iqCwhSAhan9g-pWucx

interconnect-service25:
  * ServiceId-542a018b-9248-4bb3-bfc1-e0c9d1e70b46
  * WUl0OMnGkLP1BF3bdkqOJeT3niuwD2p1kWd8In05jpho

interconnect-service26:
  * ServiceId-c94f5b5e-0d43-4843-8153-d402fae7e1b5
  * dBtmioisFz_7gTYBPL1IArA_E9F4HYnYYAKVZJfxIcv3

interconnect-service27:
  * ServiceId-37986f6b-325c-42c3-8973-c88c7d365c0c
  * SY1kOsSpSPSLOocmBMwuPWO7u-60aglBliO2Qa4tu4dv

interconnect-service28:
  * ServiceId-08a48402-a02c-4fe6-9260-635188202aad
  * QFaQPoJaYAcVsVlmnVIlkO1haVY_xg8ZZEt-AkmAzAIn

interconnect-service29:
  * ServiceId-e9414ce2-c8d5-44d6-be68-f6c5176f4482
  * FKiafH2hr8eooB0nS6N-3vDrYkIbltzBZb688U8JxpvD

interconnect-service30:
  * ServiceId-e5caa06b-4087-4f55-b51c-bbbad4d78d84
  * 2hcjXXt2G7hmyqAhWlqhXHL9OwFlNdr2_3NZ3tVkBMF2

interconnect-service31:
  * ServiceId-e71b84e8-fe53-4e40-af46-af26f9e59db3
  * 0vwL6DjNl8ATJJ_mvHrEfuzYt9dyeZulA1nKj_q3zUjf

interconnect-service32:
  * ServiceId-fc200643-5788-4af9-a1a5-847d373331b3
  * gM919kowr90lDhuRNbvc-kt3WOKW0YQLRGYNqLVbwC-B

interconnect-service33:
  * ServiceId-df0898a2-8b19-49fc-a88b-f4868c6d2b18
  * KjDoJ5z2WGv2hIG9PRJuylkh0SPLnvAYLY7mVRkmCGGf

interconnect-service34:
  * ServiceId-1eaa9835-fb15-49a6-b19c-74970795a33f
  * wUXkKrKqJmZO8S4io1QoryPlZml9_G6A4L-6WHftl7Ny

interconnect-service35:
  * ServiceId-14f7e5fc-5be8-49b5-9843-4b338cc0c34e
  * Fi7nwbNHJVU7CXAba-MJR2jiCSG524zQVb5CIFWwAM1D

interconnect-service36:
  * ServiceId-fdfe7ec7-1ec7-4798-bb1d-1815b0d31b57
  * wEj7KGnheNnadxzLTOjOe1TlSqgOB75pEzEV5tz6xxl9

interconnect-service37:
  * ServiceId-4488b45e-992f-4479-8cc1-c7160dafb067
  * weXbJ6CkIgcY0K6Aly3yNmjVb6a7cFWhlphaiD27XMdY

interconnect-service38:
  * ServiceId-5830536e-b38e-47a4-9b2b-d3c996a545dd
  * ElMOFJEGKh6qbq1CLoImqK8gvSP0KQLyxmPlY8bZecbw

interconnect-service39:
  * ServiceId-a03d5d46-d064-41c3-b330-35dfc149333b
  * qR0PIg9jT-cPWbj8ShWmha42qXP5Qijoin8l0TfxBH8w

interconnect-service40:
  * ServiceId-8b7e2cdc-b1c6-4707-8554-7c42c7ff1276
  * VZofAdNllinmi7jQMfQlmvbbJcbpAguunzKKeanweF8c

interconnect-service41:
  * ServiceId-cda9707c-8fee-497d-a514-e593b4e01002
  * Eoj46Od3qp381LaEc5nhYj-CIGZmrJKt4Gc9oRfB1naD

interconnect-service42:
  * ServiceId-c743b5f8-5ba6-464e-86ed-83e8dd3ee1b5
  * nespdN1a1I_TQ7pwgBD2gCgtjWpHJrUigUk_69GJTCDC

interconnect-service43:
  * ServiceId-40513e4d-53e6-4dde-8baf-f3a5c82ba234
  * lYCUBuwNSyW9DNOXcBXfof4znnrZihALfdbTRvytni48

interconnect-service44:
  * ServiceId-afee12ac-c58a-433c-be98-416acbb670e2
  * 2SBqJdVgwwuBBV8k3eDg6_4NVeDBaLynQgImqct4DfFv

interconnect-service45:
  * ServiceId-65a3733a-eb0a-402b-ae91-5a412dc9725f
  * to5dKzNvpNLearwdg0KeJc-zftazx-xlu0yt1uk1Q0VP

interconnect-service46:
  * ServiceId-10413fbe-10aa-4bb5-b641-65a9bbeb9d53
  * kKyrLaYCqbhNxH-Axcv7ABcX0aGdPw-MR2nYjkVORVhY

interconnect-service47:
  * ServiceId-82ead5c9-195a-4780-bbec-b3655a475896
  * -uTIzbpCJSIn45vYZP86YtrKzpgwyQZThibltlL2rRgu

interconnect-service48:
  * ServiceId-c06741b5-0ec8-4131-8b2b-276a4f72c0a1
  * 6FpfmxrQpdD00X4_m8Jhk-r4Bwg4x47BZRnLfA-qVe67

interconnect-service49:
  * ServiceId-ee93887b-11d1-49b9-be63-2764a42beb57
  * 46ZqlkPk_n3QjTbweHa3X4HLQc4N-_O0ODYSfDHu_vui

interconnect-service50:
  * ServiceId-71dd52eb-7bbc-4ff0-aaf3-70816830660e
  * vDhkWd9DzUf7V_5cWaMhmz8IPmyshCJlZcu_tf39EyNm


