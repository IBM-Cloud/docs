---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Introdução ao IBM {{site.data.keyword.blockchain}}
{: #gettingstartedtemplate}
Última atualização: 13 de outubro de 2016
{: .last-updated}

**ATENÇÃO:** antes de usar o plano do Starter Developer (Beta) ou o plano High Security Business Network (disponibilidade geral), deve-se ler as informações
técnicas e de suporte em [O que você precisa saber](needtoknow.html).
<br><br>

## Status do planejamento de oferta

O plano do Starter Developer é uma liberação Beta e fornece um ambiente de desenvolvimento com diversos locatários. O plano do High Security Business Network
tornou-se disponível geralmente (liberação de disponibilidade geral) em 20 de outubro de 2016. O plano do High Security Business Network fornece um ambiente de LinuxONE on z altamente
seguro, de locatário único, com isolamento de código usando o [IBM Secure Service Container](etn_ssc.html).
<br><br>

## IBM Blockchain on Bluemix

O serviço {{site.data.keyword.blockchainfull}} on Bluemix&reg; entrega uma rede de blockchain de desenvolvimento e teste de quatro nós para você, no clique de um botão. Em vez de criar uma rede de blockchain a partir do zero, os desenvolvedores podem começar imediatamente a compor aplicativos e implementar chaincode. O
serviço do IBM Blockchain on Bluemix é uma rede de ponto a ponto com permissão, construída sobre o código do
[Hyperledger Fabric v0.5](https://github.com/hyperledger-archives/fabric/tree/v0.5-developer-preview) a partir do Hyperledger Project do Linux
Foundation.
{:shortdesc}

As redes do Blockchain são usadas para trocarem e controlarem ativos digitais seguramente e de maneira eficiente e para registrarem permanentemente todas as transações no livro razão compartilhado. Para
obter detalhes sobre o blockchain, consulte o tópico [Sobre o blockchain](ibmblockchain_overview.html).
<br><br>

## Escolha o seu plano de rede

Você tem uma escolha entre dois planos do IBM Blockchain on Bluemix: o **Starter Developer Network** ou o **High Security Business Network**. Use o gráfico de
comparação abaixo para escolher o ambiente correto para você.

<!-- Commenting our for move to GA status jh 10/07/16
![](images/red_alert.png)  **The High Security Business Network** plan is a limited Beta offering; to select this plan, you must first request preapproval at [IBM Blockchain on IBM Bluemix](http://www-stage.watson.ibm.com/files/blockchain/bluemix.html). -->

| Plano do Bluemix:      | Starter Developer Network       | High Security Business Network
| ------------------------- |:--------------------------:|:-----:|
| Status:    | Beta     | disponibilidade geral |
| Finalidade:  |  Desenvolvimento e níveis de teste de segurança, desempenho e disponibilidade |  Simular uma rede corporativa e níveis de teste de segurança, desempenho e disponibilidade |
| Nós:    | 4 nós + Autoridade de certificação     | 4 nós + Autoridade de certificação |
| [Monitor de painel:](ibmblockchainmonitor.html) | Sim | Sim |
| Transações confidenciais: | Sim | Sim |
| [Consenso:](etn_pbft.html) | PBFT | PBFT |
| Ambiente:     | Múltiplos locatários compartilhados | Locatário único isolado |
| [IBM Secure Service Container:](etn_ssc.html) | NÃO | Sim |

<br>
## Ative o seu plano de rede

Use as etapas a seguir para criar e implementar uma instância de serviço desvinculada de sua rede de blockchain.  A sua rede inclui um ambiente de desenvolvimento com os nós de validação e um serviço
de segurança e permite que você implemente o chaincode, visualize logs e construa aplicativos:

1. A partir da página [ Serviço do {{site.data.keyword.blockchain}}](https://console.ng.bluemix.net/catalog/services/blockchain/), complete o formulário **Incluir
serviço** na área de janela direita:
  - **Espaço:** selecione **dev**.
  - **App:** selecione **Deixar desvinculado** ou, para ligar o seu serviço a um de seus aplicativos Bluemix.org,
**Selecionar um aplicativo**.
  - **Nome do serviço:** insira um nome ou valor exclusivo, como **Teste do Blockchain Net123**.
  - **Nome da credencial:** deixe o valor padrão.
  - **Plano selecionado:** escolha **Starter Developer** ou **High Security**.
  - Clique no botão **CREATE**.
2.  Você está agora na tela **Painel de serviço** para o seu novo serviço. A partir daqui, é possível **Gerenciar** a sua instância da rede; clique em
**LAUNCH** para usar o seu monitor de blockchain.
3.  O monitor de blockchain exibe detalhes de rede, logs em tempo real, estado atual do livro razão, APIs e modelos de chaincode. Use o painel para qualquer uma das funções a seguir:
  - Acessar rotas de Descoberta e de API para peers de rede.
  - Visualizar qualquer contêiner de chaincode em execução.
  - Visualizar logs em tempo real e solucionar problemas de chaincode.
  - Visualizar o estado do mundo para o livro razão.
  - Acessar a UI do Swagger e interagir com a sua rede através da API REST.
  - Implementar um dos três exemplos de chaincode.


# Links Relacionados
{: #rellinks}
## Tutoriais e amostras
{: #samples}
* [Demo do IBM Marbles (GitHub)](https://github.com/IBM-Blockchain/marbles)
* [Demo do IBM Commercial Paper (GitHub)](https://github.com/IBM-Blockchain/cp-web#readme)
* [Demo do IBM Car Lease (Github)](https://github.com/IBM-Blockchain/car-lease-demo/blob/master/README.md)
* [Demo do Leilão de arte (Github)](https://github.com/ITPeople-Blockchain/auction)

## Referência de API
{: #api}
* [UI do Swagger](https://obc-service-broker-staging.stage1.mybluemix.net/swagger)
* [API de malha do Hyperledger (GitHub)](https://github.com/hyperledger/fabric/tree/master/docs/API)
* [SDK do HFC for Node.js](https://github.com/hyperledger/fabric/tree/master/sdk/node)

## Links Relacionados
{: #general}
* [Código de malha](https://github.com/hyperledger/fabric)
* [Whitepaper](https://github.com/hyperledger/hyperledger/wiki/Whitepaper-WG)
* [Especificação e documentos relacionados do protocolo](https://github.com/hyperledger/fabric/tree/master/docs)
* [StackOverflow](http://stackoverflow.com/questions/tagged/hyperledger)
* [Linux Foundation](https://www.hyperledger.org/)
* [O que há de novo em Serviços do Bluemix](http://www.ng.bluemix.net/docs/whatsnew/index.html#services_category){:new_window}


<!--
[Bluemix Pricing Sheet](https://console.ng.bluemix.net/pricing/)
[IBM Bluemix Prerequisites](https://developer.ibm.com/bluemix/support/#prereqs) -->
