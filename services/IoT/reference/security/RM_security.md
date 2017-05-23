---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-12"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Risk and security management
{: #RM_security}

You can enhance security to enable creating, enforcing, and reporting on device connection security. With this enhanced security, certificates and transport layer security (TLS) authentication are used in addition to the user IDs and tokens that are used by {{site.data.keyword.iot_short_notm}} to determine how and where devices connect with the platform.

## Certificates
{: #certificates}

When certificates are enabled, during communication between devices and the server, any devices that do not have valid certificates  configured in the security settings are denied access, even if they use valid user IDs and passwords

To configure certificates and server access for devices, the system operator registers the associated certificate authority (CA) certiﬁcates and optionally registers message server certificates into the Watson IoT Platform platform.
To configure client certificates and server access for devices, the system operator imports the associated certificate authority (CA) certiﬁcates and messaging server certificates into {{site.data.keyword.iot_short_notm}}. The security analyst then conﬁgures the connection security policies so that the default connections between devices and the platform. The analyst can add different policies for different device types.

For information about how to configure certificates, see [Configuring certificates](set_up_certificates.html).

## Security settings
{: #connect_policy}

The security settings, including the use of connection policy settings, CA certificates, and messaging server certificates, enforce how devices connect to the platform. You can set up default connection policies for all device types and create custom settings for specific device types. The policy can be set to allow unencrypted connections, to enforce only transport layer security (TLS) connections, and to enable devices to authenticate with client-side certificates.

For information about how to configure connection security policies, see [Configuring security policies](set_up_policies.html).

Blacklist and whitelist policies provide the ability to control the locations from which devices are allowed to connect to the organization’s account. A blacklist identifies all of the IP addresses, CIDRs, or countries that are denied server access. A whitelist gives explicit access to specific IP addresses.

For information about how to configure blacklist and whitelist policies, see [Configuring blacklists and whitelists](set_up_policies.html#config_black_white).

## Organization plans and security policies
The enhanced security policies enable organizations to determine how they want devices to connect and be authenticated to the platform, by using connection policies and blacklist and whitelist policies. The security policy options that are available to an organization depend on the organization's plan type:

**Standard Plan:**
- System operators can configure connection policies with the following options:
    - TLS Optional
    - TLS with Token Authentication
    - TLS with Token and Client Certificate Authentication

**Advanced Security Plan (ASP) or Lite Plan:**
- System operators can configure connection policies with the following options:
    - TLS Optional
    - TLS with Token Authentication
    - TLS with Client Certificate Authentication
    - TLS with Token and Client Certificate Authentication
    - TLS with Client Certificate or Token
- System operators can configure blacklists or whitelists

## Risk and Security Management dashboard and reporting
{: #dashboard}

The system operator and the security analyst can use the Risk and Security Management dashboard to view the overall security status. Cards on the dashboard can provide a comprehensive compliance overview and the connection status of devices.

The following dashboard cards are available for analyzing risk and compliance:
 - **Connection Security Compliance**- Shows the level of compliance of devices that are connected to the server.
 - **Blacklist/Whitlelist Compliance** - Shows the level of compliance of devices based on the active blacklist or whitelist policy.
 - **Overall Policy Compliance** (Beta) - Shows the overall level of compliance based on all policies that are in place.
 - **Policy Violations** (Beta) - Shows the overall violations for each policy.

**Important**: The **Overall Policy Compliance** and **Policy Violations** cards are available only as part of a limited Beta program. To enable these dashboard cards, turn on the **Experimental Features** on the **Settings** page.

### Drill-down policy reporting (Beta)
{: #drill_down}

**Important**: The drill-down reporting feature for Risk Management policies is available only as part of a limited Beta program. To enable drill-down reporting, turn on the **Experimental Features** on the **Settings** page.

As part of the Beta feature, the system operator can drill down in each report to view the specific details of the devices that are compliant or in violation of policies.

You can access drill-down reports from the dashboard cards, from the **Policies** page where all of the security policies are listed, and from the details page for each policy. You can drill down to three levels of details in the reports:
1. The first level lists all of the policies that are contained in the selected policy type, for example, the default connection policy and any custom connection policies.
2. The second level shows the devices that are in violation of the policy and the cause of the violation.
3. The third level shows the specific details of an individual device that is in violation of the policy.
