---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# o quê há de novo
{: #whatsnew}

O plano **HSBN vNext Beta** é desenvolvido com uma confirmação estável do código base de software livre do [Hyperledger Fabric v1.0](https://www.hyperledger.org/){:new_window}. O Hyperledger Fabric v1.0 implementa uma arquitetura modular que fornece uma plataforma resiliente, segura e customizável para construir redes de blockchain corporativas.  
{: shortdesc}

O serviço do **HSBN vNext Beta** move além de um único ambiente de simulação para entregar uma rede de blockchain distribuída com grupos de recursos que abrangem várias organizações do Bluemix. Consulte o tópico [Visão Geral](v10_netoverview.html) para obter informações adicionais sobre a arquitetura de rede.

## Nova arquitetura no v1.0
{:why}

A arquitetura do Hyperledger Fabric evoluiu significativamente na v1.0 para empoderar
redes corporativas focadas em segurança, escalabilidade, confidencialidade e desempenho. Os peers são divididos em
dois tempos de execução distintos - **endossar** e **confirmar** - e a responsabilidade pela ordenação da
transação é considerada em um componente separado. Questões de privacidade e confidencialidade são tratadas por meio dos canais, que
fornecem segregação de dados. Existem livros razão em uma base por canal, portanto, as redes podem ser customizadas para
suportar diferentes combinações de transações bilaterais, multilaterais ou até mesmo públicas.

Visualize a seção [Detalhamento da Arquitetura do Hyperledger](http://hyperledgerdocs.readthedocs.io/en/latest/arch-deep-dive.html){: new_window} para obter informações adicionais sobre topologia de rede e a interação.

## Mudanças Adicionais

O plano HSBN vNext Beta também inclui as mudanças a seguir:
* O [novo painel](v10_dashboard.html) permite que os assinantes criem uma rede de
blockchain, convidem membros, participem de outra rede e gerenciem recursos e ativos.
* O [novo aplicativo de chaincode de amostra Marbles para v1.0](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} permite a experimentação com o código base mais recente.
* O novo [fluxo de transação](http://hyperledger-fabric.readthedocs.io/en/latest/txflow.html) no Hyperledger Fabric v1.0 assegura
a consistência e a integridade de dados implementando diversos pontos de verificação em todo o processo de transação.
