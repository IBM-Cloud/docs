{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Configuring Gateway at Your Data Center or SoftLayer Server
{: #vpn_yourdatacenter}
*Last updated: 23 February 2016*

You need an IPSec VPN gateway at your data center or SoftLayer server to form a secure connection with IBM VPN service. The following VPN gateway configurations are required at your data center or SoftLayer server:

* Enable NAT traversal at your VPN gateway only if your VPN gateway is behind NAT. 
* Use the same preshared key that you had used while configuring the {{site.data.keyword.vpn_short}} service.
* Configure the subnets for all the containers (172.31.0.0/16) or container groups (172.30.0.0/16) for which you have enabled the IBM VPN service.
* Ensure that the encryption, authentication, and PFS group settings are same at the IBM VPN gateway and your VPN gateway.
