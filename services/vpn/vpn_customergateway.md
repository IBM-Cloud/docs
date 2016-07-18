---

copyright:

  years: 2015, 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring the gateway at your data center or SoftLayer server
{: #vpn_yourdatacenter}
*Last updated: 08 June 2016*
{: .last-updated}

You need an IPsec VPN gateway at your data center or SoftLayer server to form a secure connection with the {{site.data.keyword.vpn_short}} service. The following VPN gateway configurations are required at your data center or SoftLayer server:

* Enable Network Address Translation (NAT) traversal at your VPN gateway only if your VPN gateway is behind NAT. 
* Use the same preshared key that you used while configuring the IBM VPN service.
* Add 172.31.0.0/16 as the remote subnet.
* Ensure that the encryption, authentication, and PFS group settings are the same at the IBM VPN gateway and your VPN gateway.
