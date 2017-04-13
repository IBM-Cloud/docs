---

copyright:
  years: 2017
lastupdated: "2017-03-07"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}


# Problemas conhecidos do HSBN
{: #etn_overview}



Os problemas do plano HSBN a seguir foram relatados:

1. Ao usar o High Security Business Network, que utiliza o Hyperledger Fabric v0.6.1, reconfigurar a rede periodicamente durante uma fase de desenvolvimento será sugerido se houver mais do que aproximadamente cinquenta implementações de chaincode.  Redefinir a rede remove o chaincode implementado e os dados que foram coletados.  Isso fornece uma chance de remover o chaincode mais antigo que foi substituído por melhorias feitas durante uma fase de desenvolvimento iterativo.  Se você estiver em uma fase pós-desenvolvimento, o número de implementações de chaincode deverá ser monitorado para deixar capacidade para o chaincode mais importante.
2. Erros esporádicos "503 Serviço Indisponível" e "502 Gateway Inválido" recebidos ao executar uma consulta de status da rede e dos peers.
3. Potencial para mensagens "Server.Serve falhou ao concluir o handshake de segurança" nos logs para vp1. Esse é um erro não fatal e não relacionado à operação de rede.
4. As **Credenciais de Serviço** podem não se autopreencher; nesse caso, gere as credenciais da seguinte maneira:

 a) A partir do seu Painel de Serviço, clique na guia **Credenciais de Serviço**:

  ![Credenciais de Serviço HSBN](images/hsbn.png "Service Credentials HSBN")

 b) Na guia **Credenciais de Serviço**, clique no botão para **Nova Credencial**:

  ![Nova Credencial HSBN](images/hsbn1.png "New Credential HSBN")

c) Uma nova janela intitulada **Incluir Nova Credencial** é exibida; clique no botão **Incluir** na parte inferior desta janela:

  ![Incluir Nova Credencial HSBN](images/hsbn2.png "Add New Credential HSBN")

 d) Agora sua tela deve ser semelhante ao exemplo a seguir. Clicar em **Visualizar Credenciais** revelará uma carga útil JSON que contém as Credenciais de Serviço para sua instância HSBN.  

  ![Credenciais Geradas HSBN](images/hsbn3.png "Credentials Generated")


## Como Obter Ajuda

Para suporte e ajuda com a sua rede do IBM Blockchain on Bluemix, veja [Obtendo suporte](ibmblockchain_support.html).
