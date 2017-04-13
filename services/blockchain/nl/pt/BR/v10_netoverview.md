---

copyright:
  years: 2017 lastupdated: "2017-03-16"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Visão geral da rede do HSBN vNext Beta
{: #v10_netoverview}


O serviço do HSBN vNext Beta alavanca o Hyperledger Fabric v1.0 para fornecer uma rede de blockchain segura e com permissões na qual os membros autenticados podem definir ativos facilmente e criar as soluções de negócios para modificar e trocá-los.{:shortdesc}

Esse serviço **simplifica enormemente** o processo de outra forma arcaico e tedioso de autoinicialização de uma rede de blockchain corporativa. Fornecemos a estrutura e o conjunto de ferramentas para convidar membros, agregar vários materiais de entidade criptográficos, estabelecer regras de governança e assim por diante. Esses processos complicados se tornam intuitivos e fáceis. Em minutos é possível gerar uma rede de alta segurança totalmente funcional com canais, políticas e diferentes tipos de lógica de negócios.  

A **Alta Disponibilidade** para os componentes integrais da rede (peers, serviço de ordenação, Autoridade de Certificação, chaincode) elimina os efeitos paralisantes que podem surgir de pontos únicos de falha. Um monitor de painel integrado permite o fácil gerenciamento desses componentes e fornece um mecanismo poderoso para visualizar os ativos e contratos inteligentes.

A **modularidade** da arquitetura do Hyperledger Fabric v1.0 e a separação distinta de funções de rede fornecem uma infraestrutura que permite a escalabilidade e o cálculo de alto desempenho.  

As verificações e os saldos que ocorrem em todo o ciclo de vida de uma transação asseguram resultados consistentes e completamente avaliados; e os livros razão permanecem constantemente sincronizados por meio de uma implementação do protocolo gossip conhecido. A identidade e o controle de acesso são impingidos facilmente por meio das operações de **assinatura/verificação** que ocorrem permanentemente em toda a rede.  

O **Conjunto de Ferramentas de Governança** é fornecido, permitindo que os membros administrem e gerenciem as regras de negócios críticas para suas redes. Por exemplo, você pode desejar implementar uma política que defina quantos membros de uma rede devem concordar para que um novo membro participe. Ou, talvez haja um ativo que requeira aprovação de cada participante para que uma modificação ocorra. As regras de governança são uma necessidade fundamental para qualquer tipo de rede de negócios e, muitas vezes, elas podem ser extremamente elaboradas. O conjunto de ferramentas de governança (por exemplo, editores de política) simplifica bastante esse processo.

O serviço é executado em um ambiente **altamente seguro e isolado** sem acesso externo (incluindo acesso raiz) para componentes de rede. Os dados são criptografados em andamento e em repouso e o suporte disponível para módulos de segurança de hardware permite que chaves digitais sejam protegidas em conformidade com os regulamentos do segmento de mercado. O **cálculo dedicado** é fornecido para interações de rede, garantindo, assim, o alto desempenho e a proteção de dados. Hashing, operações de assinatura/verificação e comunicações entre componentes são acelerados graças às implementações avançadas de criptografia.

A **Figura 1** mostra um exemplo de uma rede de blockchain implementada que consiste em quatro membros (cada um possui dois peers), uma Autoridade de Certificação responsável por distribuir o material de identidade criptográfico e um Serviço de Ordenação que define políticas e participantes de rede. O canal azul contém todos os quatro membros de rede, enquanto que o canal amarelo está restrito aos Membros 2, 3 e 4:

![Rede de Blockchain](images/blockchain_network.png "Exemplo de rede de blockchain")

*Figura 2. Uma rede de blockchain de exemplo consiste em quatro membros que alavancam canais para isolar dados*

Para obter detalhes completos sobre todos os recursos e funcionalidade do Hyperledger Fabric v1.0,
consulte a documentação completa da liberação em: http://hyperledger-fabric.readthedocs.io/en/latest/
