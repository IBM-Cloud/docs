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


O IBM Blockchain High Security Business Network é executado em um ambiente isolado e altamente seguro, que o distingue de outras ofertas hospedadas em nuvem. O
sistema operacional, a malha e os nós, todos, existem em um IBM Secure Service Container, fornecendo os níveis de segurança e impregnabilidade que os clientes
corporativos têm esperado da tecnologia z Systems.  O IBM Secure Service Container também entrega otimização de desempenho
para comunicação de ponto a ponto, disponibilidade, escalabilidade, criptografia de hardware, chaves de criptografia à prova de violação e VMs (máquinas virtuais) criptografadas com segurança.  
{:shortdesc}

O ambiente (LinuxONE on z) consiste em uma rede de quatro peers que implementa PBFT com Serviços de associação ativados, em execução em um contêiner de aplicativo.  O contêiner de aplicativo protege o
software blockchain, chaincode e dados em execução no sistema. O software blockchain dentro da inicialização segura pode ser assinado, atestado e criptografado; e,
uma vez instalado no contêiner de aplicativo, ele é resistente à violação.  Usuários raiz dos administradores de plataforma e de sistema não podem acessar nem ver
os conteúdos de contêiner seguro.  O LinuxONE on z fornece conformidade de FIPS, alta proteção do Evaluation Assurance Level, um ambiente operacional altamente auditável e otimização de criptografia.

Veja a seção [IBM Secure Service Container](etn_ssc.html) para obter mais detalhes sobre os recursos de segurança.
