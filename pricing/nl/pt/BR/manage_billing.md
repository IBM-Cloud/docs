---



copyright:

  years: 2017
lastupdated: "2017-04-12"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando o uso de contas vinculadas do {{site.data.keyword.Bluemix_notm}} 
{: #linked_usage}

Se você tiver uma conta vinculada do {{site.data.keyword.Bluemix_notm}} e do SoftLayer, será possível usar o Portal de controle para fazer um pagamento único, mudar os detalhes de seu cartão de pagamento, visualizar os itens de faturamento e visualizar suas faturas.

**Nota:** as opções de faturamento e uso exibidas no console do {{site.data.keyword.Bluemix}} poderão ser diferentes se você tiver uma conta grátis ou não tiver uma conta vinculada do {{site.data.keyword.Bluemix_notm}} e do SoftLayer.

## Fazendo um pagamento
{: #managemakeapayment}

É possível fazer um pagamento único a qualquer momento. O pagamento pode ser pelo saldo total ou por uma quantia parcial e os detalhes inseridos para o pagamento não serão registrados. No console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para fazer um pagamento único.

1. Selecione uma das opções a seguir, dependendo do painel que estiver sendo usado:   
 * No painel Apps ou Serviços, clique em **Gerenciar** &gt; **Faturamento e uso** &gt; **Fazer um pagamento**.  
 * No painel Infraestrutura, clique em **Conta** &gt; **Fazer um pagamento**.
3. No campo **Quantia de pagamento**, insira a quantia que deseja pagar.
4. Selecione seu método de pagamento:
 * Pagar com um cartão de crédito. Insira os detalhes de seu cartão e o endereço para cobrança do cartão. Em seguida, clique em **Fazer pagamento com cartão de crédito**. 
 * Pagar com PayPal. Digite seus detalhes quando solicitado para concluir o pagamento. 

Resolva os problemas relatados com o pagamento. O Saldo da conta é atualizado depois de o pagamento ser aceito. É possível entrar em contato com a
equipe de suporte clicando em **Suporte** &gt; **Incluir chamado**.

## Mudando o método de pagamento
{: #managepaymentmethod}

Cada conta faturável deve ter um cartão de crédito registrado que seja válido. Todo mês, o cartão de crédito é cobrado com a quantia de uso acumulada durante esse mês. No console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para incluir ou mudar os detalhes de seu pagamento. 

1. Selecione uma das opções a seguir, dependendo do painel que estiver sendo usado:  
 * No painel Apps ou Serviços, clique em **Gerenciar** &gt; **Faturamento e uso** &gt; **Modificar método de pagamento**.  
 * No painel Infraestrutura, clique em **Conta** &gt; **Faturamento** &gt; **Método de pagamento**.
2. Na seção Incluir método de pagamento, insira os detalhes do cartão de crédito e o endereço para cobrança do cartão. Em seguida, clique em **Incluir cartão de crédito**. 

Os detalhes de seu cartão são validados e, em seguida, o cartão ficará disponível para uso em sua conta dentro de 24 horas. Um e-mail de confirmação é
enviado para o contato inserido na seção de endereço para cobrança do cartão.

## Visualizando os itens de faturamento
{: #managebillingitems}

É possível associar itens de faturamento a dispositivos específicos e também desassociá-los. Por padrão, a
página Itens de faturamento exibe itens de faturamento associados. É possível mudar a visualização selecionando uma opção no
menu de exibição. A associação e desassociação podem ocorrer para um item ou para mais de um item de cada vez usando a operação Ações em massa. Os itens de faturamento individuais podem ser cancelados a qualquer momento na página Itens de faturamento. No console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para associar ou desassociar os itens de faturamento.

1. Selecione uma das opções a seguir, dependendo do painel que estiver sendo usado:   
 * No painel Apps ou Serviços, clique em **Gerenciar** &gt; **Faturamento e uso** &gt; **Itens de faturamento**.  
 * No painel Infraestrutura, clique em **Conta** &gt; **Faturamento** &gt; **Itens de faturamento**.
2. Selecione a opção de item de faturamento desejada e conclua os campos relevantes. 

## Visualizando suas faturas
{: #manageinvoices}

As faturas podem ser visualizados ou pagas a qualquer momento. Cada fatura é resumida pelo Número da fatura, Data, Tipo de fatura e vários
saldos monetários. Os tipos de fatura podem se enquadrar nas categorias a seguir:

 *  Nova -- a primeira fatura em uma série de faturas recorrentes.
 *  Recorrente -- uma fatura para encargos contínuos que estão ativos na conta há mais de um mês.
 *  Tarifa única -- uma tarifa única para despesas diversas, que podem incluir excedentes.
 *  Crédito -- um crédito do {{site.data.keyword.Bluemix_notm}} para o saldo da conta.
 *  Reembolso -- um reembolso ou uma reversão, para um encargo único ou contínuo.

A página Faturas também exibe um resumo de faturamento da conta, que inclui o próximo saldo atual e estimado,
o método de pagamento e a última e a próxima datas da fatura recorrente. É possível visualizar uma fatura no Portal de controle ou fazer download da fatura. 

No console do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir para visualizar uma fatura:

1. Selecione uma das opções a seguir, dependendo do painel que estiver sendo usado:  
 * No painel Apps ou Serviços, clique em **Gerenciar** &gt; **Faturamento e uso** &gt; **Faturas**.  
 * No painel Infraestrutura, clique em **Conta** &gt; **Faturamento** &gt; **Faturas**.
2. É possível visualizar uma fatura no Portal de controle ou fazer download da fatura. 

## Usando os serviços do {{site.data.keyword.Bluemix_notm}} com ativos do SoftLayer
{: #bluemix_services}

É possível usar facilmente serviços públicos do {{site.data.keyword.Bluemix_notm}} baseados em API com os seus ativos do SoftLayer. Todas as APIs são seguras e criptografadas para que os seus
dados estejam protegidos.
{:shortdesc}

Por exemplo, você já quis incluir recursos cognitivos do Watson em seus aplicativos em execução em servidores bare metal a partir do SoftLayer? É possível incluir um serviço como o
{{site.data.keyword.personalityinsightsshort}} para ajudar a entender o usuário do seu aplicativo em quatro etapas fáceis:

1. Localize o serviço no catálogo do {{site.data.keyword.Bluemix_notm}}.
2. Provisione uma instância do serviço com apenas alguns cliques.
3. Configure o serviço para executar com o seu código existente, copiando as credenciais de serviço e incluindo-as em seu aplicativo.
4. Após a atualização para o aplicativo, implemente a nova versão em sua infraestrutura do SoftLayer.

É possível ganhar conhecimento de *Insights e Cognitivo* chamando APIs do Watson a partir de seus aplicativos no SoftLayer, para torná-los mais personalizados. Ou, use serviços de
*Dados e de Analítica* para explorar a análise de alto desempenho para os seus aplicativos. Ou,
escolha banco de dados como serviço no qual você pode deixar o
gerenciamento para o
{{site.data.keyword.Bluemix_notm}}.

Modernize o seu desenvolvimento de aplicativo usando contêineres com serviços como {{site.data.keyword.activedeployshort}} e
{{site.data.keyword.deliverypipeline}}. É possível, então, usar o serviço do {{site.data.keyword.vpn_short}} para se comunicar com o SoftLayer
para conectar o seu contêiner em uma rede privada com a rede privada do SoftLayer. Todos os encargos de uso dos recursos de cálculo e serviços são refletidos em sua conta do {{site.data.keyword.Bluemix_notm}}.
