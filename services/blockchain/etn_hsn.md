---
 
copyright:
years: 2016
 
---
 
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}
 
 
# High Security Business Network
{: #etn_overview}
 
*Last updated: 14 July 2016*
{: .last-updated}

The High Security Business Network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in a secure services container (SSC), providing your enterprise with the security and impregnability that customers have come to expect from z Systems technology.  The SSC also delivers performance optimization for  peer-to-peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  
{:shortdesc}

The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, is tamper-resistant.  Root users of the platform and system administrators cannot access or see z secure container contents.  In addition, the LinuxONE on z provides you with FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization.

See the [Secure Services Container](etn_ssc.html) section for more details on the security features provided through the SSC.
