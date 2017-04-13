---

copyright:
  years: 2017 lastupdated: "2017-03-16"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# High Security Business Network (HSBN) vNext Beta
{: #etn_overview}

O **HSBN vNext Beta** fornece uma solução pronta para gerar uma rede de negócios blockchain. O serviço provisiona a rede rapidamente e oferece um monitor para fácil gerenciamento e manutenção de seus recursos. Esse processo direto de formação e controle de uma rede permite que mais tempo e atenção sejam direcionados ao desenvolvimento e à implementação de soluções de negócios.{:shortdesc}

Redes **HSBN vNext Beta** são executadas em um ambiente altamente seguro no LinuxONE, em que os recursos de rede (peers, ordenadores, CA, código-fonte, livro razão) estão contidos em um **IBM Secure Service Container** (SSC). Os recursos incluem:
* Otimização de desempenho para comunicação de ponto a ponto
* Alta disponibilidade e estrutura para escalabilidade 
* Criptografia de hardware, chaves criptográficas à prova de violação e máquinas virtuais criptografadas
* Inicialização segura com software resistente à violação
* Nenhum acesso raiz
* Conformidade FIPS, alta proteção EAL, auditabilidade e otimização de criptografia

Uma assinatura para o plano **HSNB vNext Beta** inclui suporte para os recursos de rede a seguir:

- Um serviço de ordenação tolerante a falhas e travamento
- 2 peers por membro
- Até 5 membros de rede adicionais
- 5 chaincodes instanciados por membro
- Uma Autoridade de Certificação específica do membro
- Até 100 canais
- Políticas de controle padrão (todos os membros são administradores e podem emitir convites para participar da rede)

Consulte a seção [IBM Secure Service Container](etn_ssc.html) para obter mais detalhes sobre os recursos de segurança do ambiente.

## Usando o plano HSBN vNext Beta
{: #use_hsbn}

### Acesso ao plano

O plano **HSBN vNext Beta** do IBM Blockchain on Bluemix é concedido por solicitação. Quando você seleciona HSBN vNext Beta no Catálogo do Bluemix e cria uma instância de serviço, sua solicitação para participar da liberação Beta mais recente é enviada para a equipe do IBM Blockchain. Depois de aprovada, você receberá um convite por e-mail para participar do plano; siga as instruções para ativar o painel do plano HSBN vNext Beta.

No painel HSBN vNext Beta, selecione dentre as três opções:
1. **Iniciação Rápida de Rede**: crie uma rede do HSBN vNext Beta e convide outros para participar do Bluemix Orgs.
2. **Participar de Rede**: visualize convites para você participar de outras redes do HSBN vNext Beta.
3. **Monitorar Rede**: gerencie seus recursos de rede - peers, canais e chaincode.

<!-- to do - the rest of this page final edit -->

### Cenário de Amostra

Vamos supor que você é um fabricante de mármore e deseja aproveitar a rede do IBM Blockchain para transacionar com diferentes fornecedores. Como isso pode funcionar? Você poderia criar um canal de consórcio contendo todos os membros de rede e o estado atual de seu repositório de mármore publicamente disponível. Todas as transações que ocorrerem nesse canal ficarão visíveis e disponíveis para consulta para todos os membros na rede. No entanto, você também poderia criar "subcanais" ou canais independentes para acomodar questões de privacidade e confidencialidade. Digamos, por exemplo, que você oferecerá a um determinado fornecedor um preço melhor se ele atender a um determinado conjunto de condições. Essa transação pode ser realizada no subcanal, com o impacto resultante em seu fornecimento geral de mármore atualizado no canal do consórcio. Ou talvez você deseje trocar uma classe específica de mármore que não está disponível no canal do consórcio. Você poderia simplesmente transacionar com a parte necessária em um canal independente e o livro razão do canal do consórcio não seria afetado. Os canais fornecem um mecanismo poderoso para privacidade porque todos eles têm livros razão exclusivos e somente membros que estão assinados e autenticados em um canal podem interagir com o livro razão.  

### Criando uma rede
{: create_a_network}
A rede consiste nos componentes a seguir:
* Um serviço de ordenação responsável por autenticar transações e ordená-las em blocos para livros razão dos canais.
* Uma Autoridade de Certificação (CA) específica do membro responsável pela emissão do material de identidade para componentes de rede de cada membro.
* Peers específicos do membro que executam e confirmam transações e mantêm um livro razão do canal.

No painel de serviço de blockchain, clique no botão **Iniciação Rápida de Rede** e siga o assistente:
1. Na página **Nomear sua Rede**, insira o nome da rede de blockchain e o nome da empresa que representará sua identidade de membro e, em seguida, clique em **Avançar**;
2. Na próxima página **Convidar Membros**, especifique as informações organizacionais relevantes para os participantes que deseja convidar. Cada um terá um peer e uma CA provisionados ao se juntar à rede e todos os membros de rede manterão um livro razão para qualquer canal ao qual eles se juntaram.<br>
   **Nota:** é possível convidar no máximo 5 membros em uma rede.
3. Na página **Definir Regras de Governança**, você verá as configurações de política de rede. Por padrão, qualquer pessoa na rede pode criar novos canais e convidar membros.  
4. Na página **Gerar Certificado**, use a opção **Gerado Automaticamente** para criar os certificados para os componentes de rede de sua Organização. Esses certificados x509 não são expostos ao usuário.  
5. Por fim, na página **Revisar resumo**, revise a configuração para sua rede e clique em **Concluído** para autoinicializar sua rede.

Esse processo conclui a configuração inicial de sua rede.

### Participando de uma rede
{: invite_members}

Após a rede ser inicializada, seus convidados receberão um e-mail indicando a rede da qual eles foram convidados a participar, além de instruções para associar-se. Os convidados verão o botão **Convites pendentes** ativado no painel do plano HSBN vNext. Clique no botão para se juntar à rede:

1. Selecione a rede na lista e clique em **Participar de Rede**.
2. Na próxima tela, revise as regras de governança e clique em **Avançar**.
3. Na página **Gerar Certificado**, insira seu Nome da Organização e, em seguida, selecione a opção **Gerado Automaticamente**.
4. Na página **Revisar Resumo da Rede**, revise as configurações da rede e clique em **Concluído**. As configurações também mostram os **Participantes Convidados** que receberam convites para participar da rede.

Consulte o [Monitor](v10_dashboard.html) para obter instruções sobre como criar canais e instalar/instanciar o chaincode.

<!-- I think all of this is adequately covered in the Monitor Section; and we already tell the story in the Sample Scenario topic above -->


<!-- From Jeff: Agreed. Commenting out all the rest sections on the page.


### Creating new channels
{: prepare_private_channels}

With the latest HSBN vNext plan, you can create a private channel, install a customized chaincode, complete the trade, and update the inventory number upon the other parties in the network make a query or propose a new transaction.

1. On the HSBN vNext plan dashboard, select **Enter Monitor**.
2. Select **Channels**, and click **New Channel**.
3. On the **Create a Channel** page, enter the channel name and choose the company that you want to make trade with by adding members. Then, click **Create** to create another private consortium channel.
4. Select **Chaincode** after you click the **Enter Monitor** button on the dashboard. You can view the chaincode that are already installed on your peer, or install a new chaincode to the peer.<br>
  **Note:** You can install at most 5 chaincode apps per peer.
5. Click **Install Chaincode** to install the smart contract to the peer. A smart contract, also known as chaincode, is the programmatic code installed and instantiated onto a channel’s peers by an appropriately authorized member. End users then invoke chaincode through a client-side application that interfaces with a network peer. Chaincode runs network transactions, which if validated, are appended to the shared ledger and modify world state. Chaincode can be developed for business contracts, asset definitions, and collectively-managed decentralized applications. You can download [this sample code](https://github.com/hyperledger/fabric/blob/master/examples/chaincode/go/marbles02/marbles_chaincode.go){: new_window} to your local environment for testing.

**Note:** After you install the chaincode onto the peer, you must instantiate the chaincode by providing the initial arguments. In the case of the Marbles sample chaincode, you can input `marble1, blue, 35` in a comma separated list to indicate that you have 35 blue marble1 for trade.


### Commencing transactions
{: commence_txs}

To make transactions within your network, the trading parties must:
* Join the same channel within the network.
* Install the same version of the chaincode onto the peer that represents each organization.


Each successful transaction results in a new block appended to the blockchain, and the ledger in the levelDB updated with the new state. Other members in the network can query the ledger or the transaction history to decide the next transaction.



### Monitoring your network
{: monitor_network}

You can perform the following tasks after you click the **Enter Monitor** button on the dashboard:
* Create new channels and invite other members to join your channels to trade privately.
* Install new chaincodes to your peer to initiate or participate into new trade.
* View the changes of blocks, transactions, chaincode invocations.
* View the log on your peer.
* View the information of resources that your organization owns.
* Export a JSON file containing the low-level networking information for each of your components (such as enrollID/enrollSecret for your CA).  

See the [HSBN vNext Beta dashboard](v10_dashboard.md) for more information about the usage of each panel on the dashboard. 


-->
