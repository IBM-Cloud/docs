---



copyright:

  years: 2015, 2017
lastupdated: "2017-01-09"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando a sua conta do {{site.data.keyword.Bluemix_notm}}
{: #mngacct}

Acesse o link **Conta** para configurar notificações, visualizar o uso da conta ou visualizar sua fatura.
{:shortdesc}

## Inscrevendo-se para o {{site.data.keyword.Bluemix_notm}}
{: #signup}

É possível se inscrever para uma conta {{site.data.keyword.Bluemix_notm}} usando um ID IBM existente, criando um novo ou usando um ID federado. Um ID federado é um ID dentro do domínio de uma empresa que foi registrado na IBM para que as credenciais do domínio e do usuário possam ser usadas para acessar aplicativos da web IBM.  

Um ID federado poderá ser usado para se inscrever para o
{{site.data.keyword.Bluemix_notm}} somente se sua empresa já tiver trabalhado
com a IBM para se registrar.  O registro do domínio de uma empresa na IBM permite que
os usuários efetuem log-in nos produtos e serviços IBM usando suas credenciais de usuário
da empresa existentes. A autenticação então é manipulada pelo provedor de identidade da
sua empresa. Quando você efetuar log-in no {{site.data.keyword.Bluemix_notm}} com
um ID federado, será solicitado a efetuar log-in por meio da página de log-in de sua
empresa. Para obter informações sobre como solicitar o registro do domínio da sua empresa ou organização na IBM ou para obter mais informações sobre o processo, veja o [IBMid Enterprise Federation Adoption Guide ![Ícone de link externo](../icons/launch-glyph.svg)](https://ibm.box.com/v/IBMid-Federation-Guide){: new_window}. Um patrocinador IBM, como um defensor da oferta
ou do cliente, é necessário quando você solicita o registro de IDs federados.

| Métodos de inscrição | Detalhes |    
|-----------------|---------|
|ID IBM existente | Se você já tiver um ID IBM, inscreva-se para o {{site.data.keyword.Bluemix_notm}} com suas credenciais existentes que você usa para outros produtos e serviços IBM. É necessário inserir um número de telefone ao se inscrever. |
|Novo ID IBM | Se você ainda não tiver um ID IBM, poderá selecionar para criar um. O ID IBM permite que você use um nome de usuário de login para todos os produtos e serviços IBM utilizados, incluindo o {{site.data.keyword.Bluemix_notm}}. É necessário inserir suas informações pessoais, incluindo nome e sobrenome, número de telefone e a senha para as novas credenciais. É possível usar esse ID IBM para efetuar login ao usar outros produtos e serviços IBM.  |
|ID federado | Se sua empresa solicitou o registro das credenciais do usuário a partir
do domínio de sua empresa na IBM, será possível se inscrever para o
{{site.data.keyword.Bluemix_notm}} usando as credenciais que você já usa para
login de sua empresa. É necessário inserir um número de telefone ao se inscrever. |
{:caption="Tabela 1. Métodos de inscrição" caption-side="top"}

## Configurando Notificações
{: #notifications}

Clique em **Conta** &gt; **Notificações** para configurar a conta geral e as notificações de gastos. As notificações de
gastos estão disponíveis apenas para proprietários da conta do {{site.data.keyword.Bluemix_notm}} de Assinatura e Pagamento por uso.

É possível configurar notificações por e-mail para incidentes e manutenção planejada do {{site.data.keyword.Bluemix_notm}} e é possível configurar notificações de gastos que o alertam quando a
sua conta estiver próxima do limite de gastos que você especificou. Conclua as tarefas a seguir para configurar tipos diferentes de notificação para a sua conta.

### Configurando notificações de plataforma

Clique em **Conta** &gt; **Notificações** &gt; **Plataforma** para configurar notificações por e-mail para incidentes e manutenção planejada do {{site.data.keyword.Bluemix_notm}}. É possível selecionar ou limpar cada opção para
ativar ou desativar a notificação por e-mail.

<!-- staging only

**Note**: You are always alerted by email about emergencies and pricing changes.

On the **Platform** tab you can also customize notifications for your orgs, spaces, or applications. Complete the following steps to add a customized notification:

<ol>
<li>Select **Add a Notification**.</li>
<li>Use the search field to find the org, application, service, or resource that you want to set a notification for, or expand the item in the pre-populated list.</li>
<li>Select *Email* to set the notification type.</li>
</ol>

staging only end -->

### Configurando notificações de gastos
{: #spendingnotifications}

Se você for um proprietário da conta do {{site.data.keyword.Bluemix_notm}} de Assinatura ou de Pagamento por uso, será possível configurar notificações de gastos por e-mail. Configure as notificações para a conta
total, o tempo de execução, o contêiner e gastos de serviço, bem como os gastos para serviços individuais, excluindo serviços de terceiro. Você recebe notificações ao atingir 80%, 90% e 100% dos limites de
gastos especificados. É possível editar cada notificação de gastos a qualquer momento, conforme as suas necessidades mudarem.

Conclua as etapas a seguir, para configurar as notificações de e-mail para limites de gastos:

<ol>
<li>Clique em **Conta** &gt; **Notificações** &gt; **Gastos**.</li>
<li>Insira um valor numérico para configurar o limite de gastos para acionar uma notificação para cada tipo de notificação:<br />
<ul>
<li>Total da conta</li>
<li>Tempo de Execução Total</li>
<li>Total de serviços</li>
<li>Total do contêiner</li>
<li>Gastos para um serviço específico</li>
</ul>
</li>
<li>Quando terminar, clique em **Save**.</li>
</ol>

**Nota**: se você tiver uma conta de
avaliação, será possível fazer upgrade para uma conta de Assinatura ou de Pagamento por uso, para configurar limites de gastos. Para obter mais
informações sobre contas de Pagamento por uso e de Assinatura, consulte [Como você é faturado](/docs/pricing/index.html#pay-accounts).

## Visualizando o uso
{: #acctusage}

Como um proprietário da conta ou um gerente de faturamento de uma organização, é possível usar a página Painel de uso para ver os encargos em tempo real para os tempos de execução, contêineres, serviços e suporte que são usados por mês em suas organizações. É possível ver o consumo de serviço e de GB/horas do tempo de execução em todas as regiões ou é possível selecionar para ver uma região
específica.

Para abrir a página Painel de uso, clique em **Conta** &gt; *your_account_name* &gt; **Painel de uso**. Os gerentes de faturamento podem ver os detalhes somente das organizações nas quais eles são gerentes de faturamento.

O proprietário da conta é cobrado pelo uso total que é incorrido entre todas as organizações no término de cada ciclo de faturamento. Como um proprietário da conta, é possível filtrar o resumo de uso
por região e organização. Também é possível clicar em um determinado mês, para ver o uso para aquele mês. Selecione **Todas as organizações** na lista **Organização** para ver o uso de todas as organizações na conta.

## Atualizando informações de faturamento
{: #account_billing}

Como o proprietário da conta, você pode editar, incluir ou remover informações de cartão de crédito salvas que estão associadas com a sua conta do {{site.data.keyword.Bluemix_notm}}. Clique em **Conta** &gt; *your_account_name* &gt; **Faturamento**.

Se você tiver uma conta do SoftLayer vinculada à sua conta do {{site.data.keyword.Bluemix_notm}}, consulte [Faturamento para uso do {{site.data.keyword.Bluemix_notm}} quando as contas estão vinculadas](/docs/admin/softlayerlink.html#bill_usage) para obter mais informações sobre como você é faturado.
