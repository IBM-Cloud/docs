---

copyright:
  years: 2016, 2017
lastupdated: "2017-05-11"

---

{:new_window: target="\_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}
{:pre: .pre}

# Configuring security policies
{: #set_up_policies.md}

When an advanced security plan (ASP) is used for an organization, a security analyst can configure connection security policies and blacklists or whitelists. When a standard plan is used, the analyst can configure settings that have fewer options and cannot configure blacklists or whitelists.

For information about using APIs to manage policies, see [IBM Watson IoT Platform Risk Management APIs ![External link icon](../../../../icons/launch-glyph.svg)](https://docs.internetofthings.ibmcloud.com/apis/swagger/v0002/riskmgmt.html){: new_window}.

## Configuring connection security policies for advanced security
{: #config_connect}

You can set the default security level that is applied to all devices. You can then add custom security settings for specific devices.

1. On the Security **Policies** page, click **Configure** beside **Connection Security**.
2. Under **Default Connection Security**, select the default connection security level from the drop-down list. The value that you select here is applied to all devices, except for devices that have custom connection settings. These policies affect how the devices connect to the server, but they do not change any settings on the actual device or send any messages to the device. You can select one of the following security levels as the default:
    - TLS Optional
    - TLS with Token Authentication
    - TLS with Client Certificate Authentication
    - TLS with Token and Client Certificate Authentication
    - TLS with Client Certificate or Token
3. If necessary, click **Add Custom Connection** and select the device types and custom security levels.
3. Click **Refresh Compliance**. Based on the security level you select, the refreshed table shows the number of devices that are affected, and the predicted level of compliance at the set security level.
4. Click **Save**.

**Note:**
You also can access the connection security settings from the **General** page under **Settings**. Click **Open Connection Security Policy**.

## Configuring connection policies for standard security
{: #config_connect_standard}

For organizations that use standard security, you change the security settings in the **General** page under **Settings**. You can set the default security level that is applied to all devices.

1. Under **Settings**, select **General**.
2. Under **Connection Security**, select the default connection security level from the drop-down list. The value that you select here is applied to all devices. These policies affect how the devices connect to the server, but they do not change any settings on the actual device or send any messages to the device. You can select one of the following security levels as the default:
    - TLS Optional
    - TLS with Token Authentication
    - TLS with Token and Client Certificate Authentication
4. Click **Save**.

## Configuring blacklists and whitelists
{: #config_black_white}

Organizations that use advanced security can restrict access to the server from certain devices by using a blacklist or can use a whitelist to grant server access to specific devices. You can use either a blacklist or a whitelist, but you cannot use both.

### Configure a blacklist
{: #config_blacklist}

1. On the Security **Policies** page, in the **Blacklist** section, click **Configure**.
2. On the **Blacklist** page, click **Add to Blacklist**.
3. In the **Add to Blacklist** window, do one of the following:
    - On the **IP Address/Range** tab, enter the IP addresses devices that you want to block or the ranges of IP addresses for multiple consecutive devices.
    - On the **CIDR** tab, enter a Classless Inter-Domain Routing (CIDR) notated block.
    - On the **Country** tab, enter or select countries from which you want to block all devices.
4. In the **Add to Blacklist** window, click **Save**.
5. Review the list of blocked devices. Any devices that are a part of the list, which is based on IP address, CIDR, or country, are not able to connect to the {{site.data.keyword.iot_short_notm}} server.
6. Click **Save**.
7. Enable the blacklist. If you had a whitelist enabled, it becomes disabled.

### Configure a whitelist
{: #config_whitelist}

1. On the Security **Policies** page, click **Configure** beside **Whitelist**.
2. On the **Whitelist** page, click **Add to Whitelist**.
3. In the **Add to Whitelist** window, do one of the following:
    - On the **IP Address/Range** tab, enter the IP addresses devices that you want to allow access to or the ranges of IP addresses for multiple consecutive devices.
    - On the **CIDR** tab, enter a Classless Inter-Domain Routing (CIDR) notated block.
    - On the **Country** tab, enter or select countries from which you want to allow access for all devices.
4. In the **Add to Whitelist** window, click **Save**.
5. Review the list of allowed devices. Any devices that are a part of the list, which is based on IP address, CIDR, or country, are  able to connect to the {{site.data.keyword.iot_short_notm}} server.
6. Click **Save**.
7. Enable the whitelist. If you had a blacklist enabled, it becomes disabled.
