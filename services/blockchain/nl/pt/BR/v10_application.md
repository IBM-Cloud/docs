---

copyright:
  years: 2017
lastupdated: "2017-03-17"
---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Desenvolvimento de aplicativos
{: #v10_dashboard}


Use o exemplo de chaincode marbles02 e o app javascript correspondente como um modelo para criar sua própria solução de negócios.
{:shortdesc}


O app utiliza as APIs de SDK do Node.js para interagir com seus componentes de rede provisionados e, por fim, atingir seu peer com solicitações de transação. Localize os terminais de API para seu peer, a Autoridade de Certificação e o Serviço de Ordenação de rede dentro da guia **Credenciais de Serviço** na tela **Recursos** do Monitor e conecte essas sequências a um arquivo de configuração que acompanha seu app. No entanto, observe que, se você desejar atingir peers adicionais na rede (este é o caso quando você requer aprovação de um peer não pertencente à sua Organização), será necessário obter os terminais de API corretos para esses peers. Também é necessário armazenar o certificado de CA para a outra Organização para verificar respostas retornadas para seu aplicativo. Essas informações não são expostas em sua visualização **Recursos**, portanto, deve-se contatar o administrador apropriado para o Bluemix Org e adquirir esses dados em uma operação fora da banda. A URL de serviço de ordenação é comum na rede; não é necessária nenhuma informação específica do membro para esse componente.  

Visite o repositório do [Marbles](https://github.com/IBM-Blockchain/marbles/tree/v3.0) GitHub para obter o código-fonte e os pré-requisitos; siga o LEIA-ME e ative seu app.  

Explore o [repositório do SDK](https://github.com/hyperledger/fabric-sdk-node) para experimentar os testes de ponta a ponta e ganhar um entendimento melhor das APIs.
