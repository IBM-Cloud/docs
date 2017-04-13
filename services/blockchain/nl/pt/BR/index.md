---

copyright:
  years: 2017
lastupdated: "2017-04-06"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Iniciar
{: #gettingstartedtemplate}

**ATENÇÃO:** antes de usar qualquer plano do IBM Blockchain on Bluemix, deve-se ler as informações técnicas e de suporte em [Renúncia de Responsabilidade](needtoknow.html).
{:shortdesc}

## IBM Blockchain on Bluemix

O serviço do {{site.data.keyword.blockchainfull}} on Bluemix&reg; consiste em três planos de rede de blockchain. O plano mais recente, **High Security Business Network (HSBN) vNext Beta**, foi desenvolvido com código base do Hyperledger Fabric v1.0 e alavanca uma arquitetura modular para entregar nova funcionalidade. Os planos do IBM Blockchain on Bluemix permitem que desenvolvedores gravem e testem aplicativos de chaincode imediatamente, sem a necessidade de projetar e configurar uma rede de blockchain privada. Chaincode é o mecanismo por trás da troca segura e eficiente de ativos em redes de blockchain do Fabric e a gravação permanente dessas transações no livro razão

## Planos de oferta

Novos assinantes do IBM Blockchain on Bluemix agora podem se inscrever no plano **HSBN vNext Beta**. Essa oferta mais recente é desenvolvida com o Hyperledger Fabric v1.0, que fornece segurança, integridade, escalabilidade e desempenho de última geração. A Tabela 1 descreve os planos do Bluemix:

Tabela 1: planos do IBM Blockchain on Bluemix  

| Plano do Bluemix      | Status       | Disponível para Novos Assinantes  | Versão do Hyperledger Fabric
| ------------------------- |:--------------------------:|:-----:|:-----:|
| **HSBN vNext Beta** (1)   | Beta     | Sim |  v1.0 |
| HSBN (2) |  disponibilidade geral |  Sim |  v0.6 |
| Starter Developer (3)    | Beta     | Sim | v0.6 |

(1) O plano **High Security Business Network (HSBN) vNext Beta** fornece um mecanismo fácil para entrar no Bluemix Orgs e construir uma rede de blockchain distribuída.  
(2) O plano **High Security Business Network (HSBN) GA** fornece um ambiente do LinuxONE on z Systems de locatário único altamente seguro, com isolamento de código usando o [IBM Secure Service Container](etn_ssc.html).  
(3) O plano Starter Developer Beta fornece um ambiente apenas para desenvolvimento com vários locatários.  

## Detalhes do plano da oferta

A Tabela 2 fornece uma comparação detalhada do IBM Blockchain nos planos de oferta do Bluemix. Novos assinantes do IBM Blockchain on Bluemix devem escolher o plano **HSBN vNext Beta**. Os planos HSBN e Starter Developer estão fechados para novos assinantes, mas permanecem suportados pela IBM:

Table 2: detalhes do plano do IBM Blockchain on Bluemix  

| Plano do Bluemix:      | Starter Developer Network       | High Security Business Network       | High Security Business Network (HSBN) vNext Beta
| ------------------------- |:--------------------------:|:-----:|:-----:|
| Status:    | Beta     | disponibilidade geral | Beta |
| Finalidade:  |  Desenvolvimento e níveis de teste de segurança, desempenho e disponibilidade |  Simular uma rede corporativa e níveis de teste de segurança, desempenho e disponibilidade |  Configure uma rede de negócios corporativos com segurança no nível de produção, desempenho e disponibilidade |
| Nós:    | 4 peers + Autoridade de Certificação     | 4 peers + Autoridade de Certificação | gerenciamento dinâmico de componentes de rede |
| Monitor de Painel: | [Sim](ibmblockchainmonitor.html) | [Sim](ibmblockchainmonitor.html) | [Sim](v10_dashboard.html) |
| Ambiente:     | Múltiplos locatários compartilhados | Locatário único isolado | múltiplos níveis de isolamento |

# Links Relacionados
{: #rellinks}
## Tutoriais e amostras
{: #samples}
* [IBM Marbles Demo (GitHub)](https://github.com/IBM-Blockchain/marbles) - v0.6 & v1.0
* [IBM Commercial Paper Demo (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme) - v0.6
* [IBM Car Lease Demo (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md) - v0.6
* [Art Auction Demo (Github)](https://github.com/ITPeople-Blockchain/auction) v0.6 - v1.0 (executado localmente)

## Referência de API
{: #api}
* [Hyperledger Fabric API (GitHub)](https://github.com/hyperledger/fabric/tree/v0.6/docs/API)
* [HFC SDK for Node.js](https://github.com/hyperledger/fabric/tree/v0.6/sdk/node)

## Links Relacionados
{: #general}
* [Código de malha](https://github.com/hyperledger/fabric)
* [Fabric Composer](https://fabric-composer.github.io/)
* [Docs do Fabric v1.0](http://hyperledger-fabric.readthedocs.io/en/latest/)
* [Docs do Fabric v0.6](https://github.com/hyperledger/fabric/tree/v0.6/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [O que há de novo em Serviços do Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
