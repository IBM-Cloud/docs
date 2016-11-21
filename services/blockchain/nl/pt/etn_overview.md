---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Paisagem de rede
{: #etn_overview}
Última atualização: 13 de outubro de 2016
{: .last-updated}

O plano do Starter Developer e o plano do High Security Business Network do IBM Blockchain on Bluemix exploram as iterações mais recentes do Hyperledger Fabric v0.5, o protocolo de consenso do Practical
Byzantine Fault Tolerance (PBFT) e o Hyperledger Fabric Client (HFC) SDK para Node.js. Ambos os planos consistem em quatro nós de rede e uma Autoridade de certificação. A
Autoridade de certificação controla os "Serviços de associação", que gerenciam identidades, permissões de rede e transações confidenciais, por meio da emissão de certificados digitais.
{:shortdesc}

Os recursos de blockchain a seguir estão disponíveis em ambos os planos:

* O protocolo de consenso do PBFT gerencia a ordenação de todas as transações gravadas no livro razão compartilhado. Uma rede de blockchain do PBFT de quatro nós é capaz de chegar a um consenso, apesar
de um nó bizantino (com falha). Para obter detalhes de teste de consenso do PBFT, consulte [Testando o consenso e a disponibilidade](etn_pbft.html).
* O HFC SDK for Node.js permite que aplicativos do lado do cliente Node.js interajam com a rede de blockchain. Aplicativos do lado do cliente podem seguramente inscrever usuários por meio dos Serviços
de associação, emitir transações e criptograficamente trocar ativos por meio do uso de tCerts. Para obter mais informações sobre Serviços de associação e privacidade do usuário, consulte a seção
[HFC SDK for Node.js](etn_sdk.html) e as [Especificações de Protocolo](https://github.com/hyperledger/fabric/blob/master/docs/protocol-spec.md) do Hyperledger Fabric.
* É possível acessar detalhes sobre o seu ambiente de rede de blockchain por meio do [Painel do monitor do Bluemix](ibmblockchainmonitor.html).  

<br>
## Terminologia

A terminologia a seguir, juntamente com o diagrama subsequente, contextualiza os componentes de uma rede do IBM Blockchain:

* Membro - uma identidade para participar na rede de blockchain. Há diferentes classes de membros, incluindo usuários, peers, validadores e auditores.
* Serviços de associação - serviços relacionados à obtenção e ao gerenciamento de identidades de membro. Os serviços de associação são governados pelas Autoridades de certificação.  
* Registro - o ato de incluir a identidade de um novo membro na rede. Um membro pode ser incluído dinamicamente na rede por um usuário com privilégio de 'escrivão'. Os membros também têm
atribuições e atributos designados, que controlam o seu acesso e autoridade na rede. Nem funções e nem atributos podem ser designados dinamicamente; deve-se, como alternativa, editar o arquivo membersrvc.yaml.
* Inscrição - conclui o processo de registro permitindo que o novo membro acesse a rede de blockchain. A inscrição pode ser feita pelo novo membro após obter um segredo a partir de um escrivão
(fora da banda) ou por um intermediário com autoridade delegada para agir em nome do novo membro.  

<br>
## Arquitetura da Rede

A Figura 1 e a sua descrição subsequente descrevem a arquitetura de rede do IBM Blockchain e o fluxo de dados para serviços de membro, transações, consenso e
anexação ao livro razão:

![Rede dedicada](images/Architecture_BMX_dedicated.png "Arquitetura de rede do IBM Blockchain")
Figura 1.

As etapas a seguir descrevem o fluxo de rede da Figura 1 em detalhes:

1. Um usuário registrado se inscreve com a rede por meio do PKI (Serviços de associação) e recebe um certificado de inscrição de longo prazo (eCert) e um lote de certificados de transação
(tCerts).
2. O usuário implementa o chaincode na rede. O chaincode (contrato inteligente) codifica a lógica de negócios, ou regras, que regem um tipo específico de transação. Cada transação (implementar, chamar
ou consultar) requer um tCert exclusivo e deve ser assinada com a chave privada do usuário. O usuário deriva a sua chave privada a partir dos tCerts designados.
3. O usuário chama o contrato inteligente, que aciona o contrato para autoexecutar a sua lógica codificada.
4. Uma transação é enviada para um peer de rede. Assim que o peer receber a solicitação de transação, ele enviará a solicitação para o peer primário da rede (VP1 na Figura 1). O peer primário irá
solicitar um bloco de transações e transmitir essa ordem para os seus peers associados.
5. Peers usam o protocolo de consenso de rede (PBFT) para concordar com a ordem das transações enviadas. Esse processo de coletivamente solicitar transações é conhecido como consenso.  
6. Assim que os peers chegarem a um consenso, as solicitações de transação serão executadas e o bloco será anexado ao livro razão compartilhado.  

<!---Both the developer and high-security networks unlock several features in the Hyperledger fabric which robustly enhance security, confidentiality and privacy.  The only fundamental difference between the two is their operating/hosting environment.  The developer network runs in a shared multi-tenant environment on Softlayer, whereas the high-security network exists as an isolated single-tenant running in a secure services container.  Each network leverages the same capabilities from the fabric, including a PBFT consensus protocol and the enhanced Node.js SDK.~~

~~The High-Security business network runs in an isolated and highly secured environment, distinguishing it from other cloud-hosted offerings. The operating system, fabric, and nodes all exist in a secure services container (SSC), providing your enterprise with the security and impregnability that customers have come to expect from system Z technology.  The SSC delivers performance optimization in - peer to peer communication, availability, scalability, hardware encryption, tamper-proof crypto keys, and securely encrypted VMs.  See the [Secure Services Container](etn_ssc.html) section for more details on the security features provided through the SSC.  Additionally, the high security network unlocks numerous features of the Hyperledger fabric (unavailable in the developer service), which robustly enhance security, confidentiality and privacy.  The configuration is such that you are able to test and affirm these features.~~  
{:shortdesc}

~~The high security plan augments the developer plan by delivering several enhancements that help meet the security requirements and concerns of an enterprise-level participant:~~--->

<!---The environment (LinuxONE on z) consists of a four-peer network implementing PBFT with Membership Services enabled, running in an application container.  The application container protects blockchain software, chaincode, and data running within the system. The blockchain software within the secure boot can be signed, attested, and encrypted; and once installed in the application container, is tamper-resistant.  Root users of the platform and system administrators cannot access or see z secure container contents.  In addition, the LinuxOne on z provides you with FIPS compliance, high Evaluation Assurance Level protection, a highly auditable operating environment, and crypto optimization--->
