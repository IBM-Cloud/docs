---

copyright:
  years: 2016

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Monitor de painel
{: #blockchain_dashboard_monitor}
Última atualização: 13 de outubro de 2016
{: .last-updated}

O monitor de painel fornece uma visão geral de seu ambiente de blockchain, incluindo dados de desempenho e chaincode implementado. Use o monitor para visualizar
informações de rede sobre peers, logs, estado de livro razão, APIs e chaincode.  
{:shortdesc}

<br>
## Guias do monitor
{: #blockchain_dashboard_monitor_tabs}

As guias a seguir são exibidas no painel:
  - Rede
  - Cadeia de blocos
  - Chaincode de demo
  - APIs
  - Registros
  - Barra de Status
  - Versão

**Guia Rede**: monitore o status de seus peers e qualquer contêiner de chaincode que estiver em execução, conforme mostrado na Figura 1. Visualize as rotas de Descoberta e de
API para os seus peers de validação e Autoridade de certificação, que são os valores de host de nó e porta combinados. Por exemplo, o fragmento de código de JSON para as suas **Credenciais de
serviço** do Bluemix no **Painel de serviço** mostra que `"discovery_host"` e `"discovery_port"` equivalem à rota exibida na guia
**Rede**. Esses valores são úteis para se conectar manualmente ao Bluemix.

![](images/IBC_BMX_Monitor_Network.png "Guia Rede")
*Figura 1. Guia Rede*


**Guia Blockchain**: visualize o estado atual de seu blockchain. Conforme mostrado na Figura 2, é possível visualizar todas as transações, o estado atual do livro razão e os dados de
desempenho para a rede:

![](images/IBC_BMX_Monitor_Blockchain.png "Guia Blockchain")
*Figura 2. Guia Blockchain*


**Guia Chaincode de demo**: aprenda e experimente três modelos chaincode de amostra, que é possível implementar e chamar em sua rede. As instruções são fornecidas para guiá-lo através
do processo, conforme mostrado na Figura 3. Todas as implementações e chamadas de chaincode são gravadas no log e também podem ser visualizadas nas guia Logs em tempo real, Blockchain e API.  

![](images/IBC_BMX_Monitor_Demo.png "Guia Chaincode de demo")
*Figura 3. Guia Chaincode de demo*


**Guia APIs**: use a UI do Swagger para interagir com sua rede de blockchain através da API REST, conforme mostrado na Figura 4:  

![](images/IBC_BMX_Monitor_API.png "Guia APIs")
*Figura 4. Guia APIs*


**Guia Logs**: visualize logs para peers de validação e Serviços de associação, que incluem os resultados de todas as transações na rede. É possível usar informação de log para
inspecionar transações e solucionar problemas de chaincode.  

![](images/IBC_BMX_Monitor_Logs.png "Guia Logs")
*Figura 5. Guia Logs*


**Guia Status**: visualize métricas de desempenho para serviço, teste de rede e automatizado, conforme mostrado na Figura 6. Exiba dados para o mês anterior. Essa guia também contém
anúncios de código, fóruns gerais, problemas conhecidos e notas sobre a liberação para o IBM Blockchain.  

![](images/IBC_BMX_Monitor_Status.png "Guia Status")
*Figura 6. Guia Status*


**Guia Suporte**: relate um problema e visualize o seu Status de serviço, conforme mostrado na Figura 7:

![](images/IBC_BMX_Monitor_Support.png "Guia Suporte")
*Figura 7. Guia Suporte*
