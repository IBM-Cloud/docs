---

copyright:
  years: 2017
lastupdated: "2017-03-08"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Renúncia de Responsabilidade
{: #etn_overview}

**ATENÇÃO:** deve-se revisar as informações a seguir antes de usar qualquer plano do IBM Blockchain on Bluemix.

## Instrução de suporte IBM

A IBM tem uma longa história de liderança em inovação, que continua com os planos de oferta do IBM Blockchain on Bluemix. Blockchain é uma tecnologia em rápida progressão, projetada para revolucionar vários segmentos de mercado, desde finanças até logística, passando pela cadeia de suprimento. Por meio de vários programas de adoção antecipada, clientes e parceiros de negócios IBM têm conduzido o blockchain ativamente como uma solução industrial. O IBM Blockchain on Bluemix é um programa desses. **Assim como qualquer nova tecnologia, os usuários do IBM Blockchain on Bluemix devem estar preparados para mudanças rápidas e fundamentais**.  
{:shortdesc}

A arquitetura por trás do IBM Blockchain é o projeto Hyperledger Fabric da Linux Foundation. O Fabric está atualmente com status *Ativo* e passando por desenvolvimento contínuo. Cada contribuição da comunidade de software livre melhora o Hyperledger Fabric, mas pode apresentar desafios de adoção. Durante o ciclo do projeto *Ativo*, os clientes podem usar o Hyperledger Fabric v1.0 para teste e simulação de rede.**A IBM tem reservas com relação à definição ou troca de ativos financeiros ou de quaisquer ativos de valor, diretamente em qualquer rede de blockchain do Hyperledger Fabric**.  

## Instrução de software livre

O plano **High Security Business Network (HSBN) vNext Beta** foi desenvolvido com código de software livre do Hyperledger Fabric v1.0 da Linux Foundation. Os planos Starter Developer e High Security Business Network (HSBN) foram desenvolvidos com o código do Hyperledger Fabric v0.6. Os membros do Hyperledger Project, incluindo a IBM, continuam contribuindo com o código-fonte, o qual é revisado, examinado e testado posteriormente pela comunidade. Hyperledger Fabric v1.0 está atualmente *Ativo*; detalhes sobre o status *Ativo* e sobre o ciclo de vida do Hyperledger Project estão disponíveis em https://wiki.hyperledger.org/community/project-lifecycle.  

## Instrução de suporte de chaincode

As práticas de codificação a seguir NÃO são suportadas em redes do IBM Blockchain:

1. Usando matrizes associativas com iteração (a ordem é aleatória em Go).
2. Lendo uma lista de itens a partir de uma tabela de KVS (a ordem não é garantida).
3. Gravando chaincode inseguro para encadeamento (consulta e chamada podem ser chamadas em paralelo).
4. Substituindo memória global ou armazenamento em cache para variáveis de estado do livro razão em chaincode.
5. Acessando serviços externos, como bancos de dados, diretamente a partir de chaincode.
6. Usando bibliotecas ou variáveis globais que podem introduzir o não determinismo (como usar "aleatório" ou "tempo").
7. Iterando usando GetRows.  

Além disso, os planos HSBN e Starter (Hyperledger Fabric v0.6) não suportam chaincode não determinístico, o que apresenta risco para a consistência e a integridade de dados; para obter detalhes, consulte [chaincode não determinístico](nondeterministic.html).
