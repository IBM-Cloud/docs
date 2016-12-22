---

 

copyright:

  years: 2016
lastupdated: "2016-12-01"
 

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Fazendo upgrade e unificando as contas de cobrança do {{site.data.keyword.Bluemix_notm}} e do SoftLayer
{: #softlayerlink}

Se você tem uma conta para teste do {{site.data.keyword.Bluemix_notm}} e deseja acessar o painel Infraestrutura, deve-se fazer upgrade para uma conta pay-as-you-go do {{site.data.keyword.Bluemix_notm}}. Você também deverá fazer upgrade se usar outros recursos debitáveis que não estão disponíveis em uma conta para teste, ou sua conta para teste será concluída. 

É possível unificar suas contas de cobrança {{site.data.keyword.Bluemix_notm}} e SoftLayer existentes, vinculando as contas. Ao vincular as suas contas, você será faturado pelo {{site.data.keyword.Bluemix_notm}} pelos recursos do {{site.data.keyword.Bluemix_notm}} e do SoftLayer.

**Atenção:** Uma conta da assinatura do {{site.data.keyword.Bluemix_notm}} não pode ser vinculada com uma conta do SoftLayer. Para
acessar o painel Infraestrutura deve-se criar uma conta Pay-As-You-Go, uma segunda conta, que é automaticamente vinculada com uma conta do SoftLayer. Você, então,
receberá duas faturas, uma para cada conta do {{site.data.keyword.Bluemix_notm}}. Embora os seus recursos de infraestrutura irão ser faturados em uma conta
Pay-As-You-Go separada, os recursos poderão ser usados com apps e serviços em sua conta da assinatura. Por exemplo, se você ativar um serviço do Watson em sua conta
da assinatura, poderá copiar as credenciais de serviço e, em seguida, incluir as credenciais em seu aplicativo bare metal que for originado de sua conta
Pay-As-You-Go.
{:shortdesc}

## Fazendo upgrade para uma conta pay-as-you-go do {{site.data.keyword.Bluemix_notm}}
{: #upgradetopayg}

Ao efetuar login no {{site.data.keyword.Bluemix_notm}} usando uma conta para teste, não é possível acessar o painel Infraestrutura do {{site.data.keyword.Bluemix_notm}}. Se você deseja que seus apps usem os recursos de infraestrutura, deve-se fazer upgrade para uma conta pay-as-you-go.

Para fazer upgrade de sua conta para teste para uma conta pay-as-you-go do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

 1. Clique em **Conta** &gt; **Faturamento**.
 2. Em seguida, clique em **Incluir cartão de crédito**.
 3. Insira os detalhes de faturamento necessários. 
 4. Leia e aceite os termos e condições para a conta pay-as-you-go. 
 5. Ao concluir, clique em **Fazer upgrade**. 
 
Após fazer upgrade para uma conta pay-as-you-go, as opções de **Infraestrutura** são listadas no **Catálogo** {{site.data.keyword.Bluemix_notm}}. Se você usar mais do que o abono grátis, receberá uma fatura mensal do {{site.data.keyword.Bluemix_notm}}. A fatura será em dólares dos Estados Unidos (USD) e detalhará os encargos do recurso. 

## Unificando as contas do {{site.data.keyword.Bluemix_notm}} e do SoftLayer
{: #unifyingaccounts}

É possível unificar suas contas do {{site.data.keyword.Bluemix_notm}} e do SoftLayer para usar os recursos combinados. Ao vincular suas contas do {{site.data.keyword.Bluemix_notm}} e do Softlayer, você receberá uma única fatura do {{site.data.keyword.Bluemix_notm}}. Se você tiver uma conta existente do {{site.data.keyword.Bluemix_notm}}, o faturamento por meio do {{site.data.keyword.Bluemix_notm}} para recursos do SoftLayer
entrará em vigor para o novo ciclo de faturamento que se inicia após as contas serem vinculadas.

**Importante:** todas as contas vinculadas no {{site.data.keyword.Bluemix_notm}} devem ser contas de Pagamento por uso. É possível criar uma nova conta de Pagamento por uso ou
vincular uma conta de Pagamento por uso existente. Ou, é possível vincular uma conta para teste existente, mas ela terá upgrade feito para uma conta de Pagamento por uso. As contas de assinatura do {{site.data.keyword.Bluemix_notm}} não podem ser vinculadas.  

Após as suas contas serem vinculadas:

* Deve-se usar as credenciais IBMid para acessar as contas do SoftLayer e do {{site.data.keyword.Bluemix_notm}}.
* Quaisquer descontos existentes do SoftLayer são aplicados em encargos do {{site.data.keyword.Bluemix_notm}}. 
* Você receberá uma única fatura em dólares dos Estados Unidos (USD).
* É possível monitorar o uso de seus recursos do {{site.data.keyword.BluSoftlayer}} na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. 

**Atenção:** Após as contas serem vinculadas, elas não poderão ser desvinculadas. 

Se você tiver uma conta do SoftLayer e desejar vincular contas do SoftLayer e do {{site.data.keyword.Bluemix_notm}}, conclua estas etapas:

 1. A partir do {{site.data.keyword.slportal}}, clique em **Vincular uma Conta do {{site.data.keyword.Bluemix_notm}}**.
 2. Leia e aceite os termos para vincular contas do SoftLayer e do {{site.data.keyword.Bluemix_notm}}.
 3. Quando solicitado, forneça o endereço de e-mail que está associado à sua conta do {{site.data.keyword.Bluemix_notm}}. Se você não tiver uma conta do
{{site.data.keyword.Bluemix_notm}}, forneça o endereço de e-mail que deseja usar e, em seguida, siga as instruções para ser convidado para o {{site.data.keyword.Bluemix_notm}} e criar uma
conta.

Deve-se ser um Usuário Principal na conta do SoftLayer para vincular contas.

Após ter vinculado as suas contas, o link **Acesse o {{site.data.keyword.Bluemix_notm}}** estará disponível no cabeçalho global do SoftLayer. Clicar nesse link conduz você para a
página de login do {{site.data.keyword.Bluemix_notm}}. Além disso, o link **SoftLayer** agora está disponível no cabeçalho do {{site.data.keyword.Bluemix_notm}}. Clicar no link
conduz você para a página inicial do {{site.data.keyword.slportal}} em uma nova janela.

As ofertas de infraestrutura do {{site.data.keyword.Bluemix_notm}} estão conectadas a uma rede de três camadas, segmentando o tráfego público, privado e de gerenciamento. As ofertas de infraestrutura em uma conta do {{site.data.keyword.Bluemix_notm}} do cliente podem transferir dados entre si através da rede privada, sem nenhum custo. As ofertas de infraestrutura, como servidores bare metal, servidores virtuais e armazenamento em nuvem, conectam-se a outros aplicativos e serviços no catálogo do {{site.data.keyword.Bluemix_notm}}, como serviços, contêineres ou tempos de execução do Watson, através
da rede pública. A transferência de dados entre esses dois tipos de ofertas é medida e cobrada em taxas padrão de largura da banda da rede pública.

## Convidando membros da equipe do SoftLayer para o {{site.data.keyword.Bluemix_notm}}
{: #invite_users}

É possível convidar membros da equipe do SoftLayer para se juntarem ao {{site.data.keyword.Bluemix_notm}} quando você vincula suas contas do {{site.data.keyword.Bluemix_notm}} e do SoftLayer. Ou, é possível convidar membros da equipe do SoftLayer posteriormente, a partir da interface com o usuário do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

A partir da interface com o usuário do {{site.data.keyword.Bluemix_notm}}, é possível selecionar para convidar todos os membros de sua conta do SoftLayer ou é possível selecionar membros
individuais. Ao convidar membros da equipe, deve-se configurar a função de conta do {{site.data.keyword.Bluemix_notm}} para os convidados. Para obter mais informações sobre as diferentes funções no
{{site.data.keyword.Bluemix_notm}}, consulte [Funções de Usuário](https://console.ng.bluemix.net/docs/admin/users_roles.html#userrolesinfo).

Deve-se ser um Usuário Principal na conta do SoftLayer para convidar membros da equipe para a conta do {{site.data.keyword.Bluemix_notm}}.

Para convidar membros da equipe por meio do {{site.data.keyword.Bluemix_notm}}, conclua as etapas a seguir:

 1. Clique em **Conta** &gt; **Convidar membros da equipe**.
 2. Clique em **Incluir** para autenticar em sua conta do SoftLayer e visualizar uma lista de membros da equipe a partir de sua conta do {{site.data.keyword.BluSoftlayer}}
 3. Selecione os membros da equipe para convidar e clique em **Enviar**.
 
O membro da equipe recebe um e-mail que inclui um link **Associar-se à organização**. Se o membro da equipe não tiver um IBMid, ele será redirecionado para uma página de registro. Em seguida, ele poderá inserir algumas informações básicas e criar a sua conta do {{site.data.keyword.Bluemix_notm}}.

Para obter mais informações sobre convidar membros da equipe por meio da interface com o usuário do {{site.data.keyword.Bluemix_notm}}, consulte
[Convidando membros da equipe](https://console.ng.bluemix.net/docs/admin/users_roles.html#inviteteammembers).

## Alternando para o IBMid
{: #ibmid_switch}

A autenticação no SoftLayer agora usa o IBMid para fornecer um login único para o {{site.data.keyword.Bluemix_notm}}. Se você tiver uma conta existente do SoftLayer, será possível alternar para um IBMid. Um assistente de migração o guiará através desse comutador. 
{:shortdesc}

Após iniciar a alternância para o IBMid, contanto que você não conclua o processo, será possível cancelá-lo. Mas, você ainda será solicitado a alternar para o IBMid da próxima vez que efetuar login.

Para iniciar a alternância do seu nome de usuário existente do SoftLayer para um IBMid, conclua as etapas a seguir:

 1. No {{site.data.keyword.slportal}}, acesse a página Editar perfil do usuário e clique em **Alternar para IBMid**.
 2. Siga os prompts do assistente de migração para criar seu IBMid. Após criar seu IBMid, não será possível mudar o ID, que é um endereço de e-mail. É possível atualizar o e-mail associado a seu perfil, mas, por padrão, esse valor é configurado como o valor que você definiu para o seu IBMid. Após concluir o assistente, um e-mail é enviado para você.
 3. Ao receber o e-mail, siga o link ou copie e cole a URL em um navegador e insira o seu código de registro. O código é válido por 7 dias e pode ser usado apenas uma vez.  Após usá-lo, ele não poderá ser usado novamente.
 Após configurar o IBMid para o link de usuário do SoftLayer, é possível efetuar login em sua conta apenas com o IBMid.  No diálogo de login, deve-se usar o botão **Efetuar login com IBMid** em vez de inserir seu nome de usuário e senha do SoftLayer.
 
Se você for um novo cliente, ao efetuar check-out de sua ordem, você será solicitado a fornecer um endereço de e-mail para a sua conta do IBMid existente ou a criar uma nova conta de IBMid. 

### Mapeando várias contas do SoftLayer para um IBMid
{: #map_multiple_accounts}

Ao configurar a conta, será possível associar um único IBMid a várias contas do SoftLayer usando um endereço de e-mail existente. Somente um usuário do SoftLayer para cada conta pode ser mapeado para o IBMid único. O IBMid deve ser exclusivo dentro de cada conta do SoftLayer. No entanto, um usuário com acesso a várias contas do SoftLayer pode usar um único IBMid para acessar diversas contas do SoftLayer.

Por exemplo, um IBMid pode ser mapeado como o usuário principal nas contas A e B e como um usuário adicional nas contas C e D. Uma das contas mapeadas para esse IBMid é a conta padrão.  Normalmente, a conta padrão é a conta que foi mapeada primeiro para o IBMid. No entanto, é possível alternar qual conta é a conta padrão por meio do recurso de alternância de contas no Portal do Cliente.

Para um usuário com acesso IBMid a várias contas com a autenticação de dois fatores ativada, será necessário um código de verificação de autenticação de dois fatores apropriado por conta durante o login e a alternância da conta.

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

### Serviços do {{site.data.keyword.Bluemix_notm}} baseados em API
Nem todos os serviços do {{site.data.keyword.Bluemix_notm}} podem ser usados com o SoftLayer. Os serviços a seguir podem ser configurados para execução com o seu código do aplicativo:
* {{site.data.keyword.alchemyapishort}}
* {{site.data.keyword.alertnotificationshort}}
* {{site.data.keyword.sparks}}
* {{site.data.keyword.appseccloudshort}}
* {{site.data.keyword.blockchain}}
* {{site.data.keyword.cloudant}}
* {{site.data.keyword.conceptinsightsshort}}
* {{site.data.keyword.iotmapinsights_short}}
* {{site.data.keyword.dashdbshort}}
* {{site.data.keyword.dialogshort}}
* {{site.data.keyword.documentconversionshort}}
* {{site.data.keyword.twittershort}}
* {{site.data.keyword.weather_short}}
* {{site.data.keyword.iotdriverinsights_short}}
* {{site.data.keyword.geospatialshort_Geospatial}}
* {{site.data.keyword.graphshort}}
* {{site.data.keyword.iotelectronics}}
* {{site.data.keyword.languagetranslationshort}}
* {{site.data.keyword.messagehub}}
* {{site.data.keyword.mqa}}
* {{site.data.keyword.mobileappbuilder_short}}
* {{site.data.keyword.mql}}
* {{site.data.keyword.nlclassifierlshort}}
* {{site.data.keyword.objectstorageshort}}
* {{site.data.keyword.personalityinsightsshort}}
* {{site.data.keyword.presenceinsightsshort}}
* {{site.data.keyword.relationshipextractionshort}}
* {{site.data.keyword.retrieveandrankshort}}
* {{site.data.keyword.servicediscoveryshort}}
* {{site.data.keyword.speechtotextshort}}
* {{site.data.keyword.sqldb}}
* {{site.data.keyword.streaminganalyticsshort}}
* {{site.data.keyword.texttospeechshort}}
* {{site.data.keyword.toneanalyzershort}}
* {{site.data.keyword.tradeoffanalyticsshort}}
* {{site.data.keyword.visualinsightsshort}}
* {{site.data.keyword.visualrecognitionshort}}
* {{site.data.keyword.workflow}}
* {{site.data.keyword.workloadscheduler}}

**Nota:** nem todos os planos para esses serviços estão disponíveis. Somente os planos ativados para contas de Pagamento por uso estão disponíveis para uso com contas vinculadas. No
entanto, será possível usar qualquer plano para qualquer um desses serviços se você tiver uma conta do {{site.data.keyword.Bluemix_notm}} separada que for cobrada separadamente.

## Faturamento para uso do {{site.data.keyword.Bluemix_notm}} quando as contas estão vinculadas
{: #bill_usage}

Após ter vinculado suas contas de cobrança do {{site.data.keyword.Bluemix_notm}} e do SoftLayer, o próximo ciclo de faturamento será cobrado em uma única fatura do {{site.data.keyword.Bluemix_notm}}.
{:shortdesc}

O seu ciclo de uso do {{site.data.keyword.Bluemix_notm}} está em uma base por mês de calendário; portanto, a sua conta será faturada todo mês no dia de faturamento que foi estabelecido para
a sua concordância com os encargos. Com o SoftLayer, o seu ciclo de uso
começa a partir de quando você começou com o SoftLayer; portanto, você é faturado todo mês no mesmo dia do mês em que você se inscreveu para a sua conta do SoftLayer. 

Quando as suas contas estão vinculadas, o seu uso do {{site.data.keyword.Bluemix_notm}} continuará a ser medido para o ciclo do mês atual e você será faturado por esse uso em uma conta do {{site.data.keyword.Bluemix_notm}}. Iniciando no primeiro dia do próximo mês, seus encargos do {{site.data.keyword.Bluemix_notm}} e do SoftLayer serão combinados em sua fatura do {{site.data.keyword.Bluemix_notm}}.

Por exemplo, se você vinculou as suas contas em 16 de abril, obterá uma fatura do Bluemix para o seu uso de abril. Dependendo de quando você vinculou as suas contas, você poderá ter uma conta separada para o uso do SoftLayer. O uso de maio tanto para o SoftLayer como para o {{site.data.keyword.Bluemix_notm}} será faturado por meio de sua conta do {{site.data.keyword.Bluemix_notm}}.

![Vinculando o resumo de contas do Bluemix e do SoftLayer](images/BluemixSoftLayerBill.svg)

Após as contas serem vinculadas, a sua fatura do {{site.data.keyword.Bluemix_notm}} listará os encargos diferentes para cada recurso que você utilizou sob os títulos a seguir:

* **Servidores bare metal e serviços anexados**
* **Servidores virtuais e serviços anexados**
* **Serviços não anexados**

Para obter informações sobre como visualizar o uso do {{site.data.keyword.Bluemix_notm}}, consulte [Visualizando detalhes
de uso](https://console.ng.bluemix.net/docs/pricing/index.html#usage).

