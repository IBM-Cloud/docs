---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# O Que Você Precisa Saber
{: #etn_overview}
Última atualização: 13 de outubro de 2016
{: .last-updated}

**ATENÇÃO:** deve-se revisar as informações a seguir antes de usar o plano do IBM Blockchain on Bluemix: Starter Developer (Beta) ou High
Security Business Network (disponibilidade geral).
<br><br>

## Instrução de suporte IBM

A IBM tem uma longa história de liderança em inovação, que continua com as ofertas do IBM Blockchain mais recentes. O Blockchain é uma tecnologia em rápida
progressão que é projetada para desmembrar uma série de segmentos de mercado, desde finanças até logística. Através de vários programas de adoção antecipada, os
clientes da IBM e os parceiros de negócios já estão influenciando a direção futura de blockchain. O IBM Blockchain on Bluemix é um programa desses. **Como
com qualquer nova tecnologia, os usuários do IBM Blockchain on Bluemix devem estar preparados para mudanças rápidas e fundamentais**.  
{:shortdesc}

A arquitetura por trás do IBM Blockchain é o Hyperledger Project do Linux Foundation. O Hyperledger Fabric é um projeto de software livre sob desenvolvimento
ativo, atualmente em status de *Incubação*. Cada contribuição da comunidade de software livre torna o Hyperledger Fabric mais robusto, mas pode
apresentar desafios de adoção. Durante o ciclo de *Incubação*, os clientes podem usar o Hyperledger Fabric v0.5 para teste e simulação de rede, mas a
**IBM tem reservas com relação à execução de ativos financeiros de valor diretamente em uma rede de blockchain do Hyperledger Fabric v0.5**.  
<br>

## Instrução de software livre

O IBM Blockchain on Bluemix &mdash; tanto o plano do Starter Developer quanto o plano do High Security Business Network &mdash; usa o software livre do Hyperledger Fabric v0.5 da Linux Foundation. Os membros do Hyperledger
Project, incluindo a IBM, contribuem com código para a malha, após a qual ele é revisado, examinado e testado pela comunidade. O Hyperledger Fabric v0.5 está
atualmente no estado de *Incubação*; detalhes sobre o estado de *Incubação* e sobre o ciclo de vida inteiro para o Hyperledger Project
estão disponíveis em https://github.com/hyperledger/hyperledger/wiki/Project-Lifecycle.
<br><br>

## Instrução de suporte de chaincode

O IBM Blockchain não suporta [chaincode não determinístico](ibmblockchain_tutorials.html#ndcc), que apresenta risco para consistência e
integridade de dados em qualquer rede de blockchain. Antes de implementar um novo chaincode em sua rede do IBM Blockchain on Bluemix, revise os detalhes sobre
[chaincode não determinístico](ibmblockchain_tutorials.html#ndcc).

Além do [chaincode não determinístico](ibmblockchain_tutorials.html#ndcc), as práticas de codificação a seguir NÃO são suportadas em redes do
IBM Blockchain:

1. Usando matrizes associativas com iteração (a ordem é aleatória em Go).
2. Lendo uma lista de itens a partir de uma tabela de KVS (a ordem não é garantida).
3. Gravando chaincode inseguro para encadeamento (consulta e chamada podem ser chamadas em paralelo).
4. Substituindo memória global ou armazenamento em cache para variáveis de estado do livro razão em chaincode.
5. Acessando serviços externos, como bancos de dados, diretamente a partir de chaincode.
6. Usando bibliotecas ou variáveis globais que podem introduzir não determinismo (como usar “random” ou "time").
<br><br>

## Como Obter Ajuda

Para suporte e ajuda com a sua rede do IBM Blockchain on Bluemix, veja [Obtendo suporte](ibmblockchain_support.html).
