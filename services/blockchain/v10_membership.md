---

copyright:
  years: 2017
lastupdated: "2017-03-13"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Network membership
{: #v10_membership}

As a platform for **permissioned** blockchain networks, Hyperledger Fabric includes
robust components for managing the network identities of all member organizations
and their users. The requirement for a permissioned identity for every user enables
ACL-based control over network activity, and guarantees that every transaction is
ultimately traceable to a registered user.
{:shortdesc}

To manage network identities, Hyperledger Fabric includes a modular **Certificate
Authority (CA)** component, which issues PKI-based certificates to member
organizations and their associated users. The CA (fabric-CA by default) issues a
root certificate (**rootCert**) to each **member** (organization or individual)
that is authorized to join the network. The CA also issues an enrollment
certificate (**eCert**) to each **user** that the member has authorized to join
the network. Each enrolled user is also granted a number of transaction certificates
(tCerts); each **tCert** authorizes one network transaction. This certificate-based
control over network membership and actions enables members to restrict access to
private and confidential channels, applications and data, by specific user identities.

In addition to the Certificate Authority, Hyperledger Fabric includes a
**Membership Service Provider (MSP)** component. The MSP is installed on each channel
peer, to ensure that transaction requests issued to the peer originate from an
authenticated and authorized user identity.

For more information on the Hyperledger Fabric Membership Services component, see the
complete [Fabric documentation](http://fabric-rtd.readthedocs.io/en/latest/index.html).
