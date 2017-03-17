---

copyright:
  years: 2016, 2017
lastupdated: "2016-10-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network
{: #etn_overview}


The IBM Blockchain High Security Business Network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in an IBM Secure Service Container, providing  the levels of security and impregnability that enterprise customers have come to expect from z Systems technology.  The IBM Secure Service Container also delivers performance optimization for  peer-to-peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  
{:shortdesc}

The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, it is tamper-resistant.  Root users of the platform and system administrators cannot access or see secure container contents.  LinuxONE on z provides FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization.

See the [IBM Secure Service Container](etn_ssc.html) section for more details on the security features.
