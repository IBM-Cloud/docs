---



copyright:

  years: 2016, 2017
lastupdated: "2017-02-02"


---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Conta IBM {{site.data.keyword.Bluemix_notm}} Standard Beta 
{: #betaintro}

A conta {{site.data.keyword.Bluemix}} Standard Beta introduz uma nova conta grátis, que oferece uma nova maneira de trabalhar na Nuvem Pública {{site.data.keyword.Bluemix_notm}}. A conta Standard nunca expira, ao contrário da Avaliação de 30 dias do {{site.data.keyword.Bluemix_notm}}. É possível continuar a trabalhar em seus aplicativos {{site.data.keyword.Bluemix_notm}} sem quaisquer preocupações sobre restrições de tempo.{:shortdesc}

A participação na conta Standard Beta é possível apenas por meio de um convite. Depois de
aceitar o convite e criar sua conta Standard, será possível convidar amigos e colegas para participar
na conta Beta.  

## Introdução à conta {{site.data.keyword.Bluemix_notm}} Standard
{: #standardaccount}

Você pode estar se perguntando o que é diferente na conta Standard em comparação com
a conta para teste. As tabelas a seguir resumem os principais detalhes sobre a conta
{{site.data.keyword.Bluemix_notm}} Standard. 

|O que há de novo em uma conta Standard? |    
|-----------------|
| A conta nunca expira. |
| Os aplicativos Cloud Foundry podem acessar até 256 MB de memória de tempo execução instantânea
grátis. |
| É possível acessar planos Lite para Cloudant NoSQL DB e para a Plataforma Internet of Things com
mais serviços em breve. |
| Seus aplicativos serão suspensos se não houver atividade de desenvolvimento por 10 dias. |
| Suas instâncias de serviço serão excluídas após 30 dias de inatividade. |
{:caption="Table 1. What's new in a Standard Account" caption-side="top"}

|O que não mudará quando uma conta para teste for convertida? | 
|-----------------|
|A conta é grátis -- você não precisa de um cartão de crédito. |
|Quaisquer instâncias Lite do Cloudant NoSQL DB e da Plataforma Internet of Things. Uma instância
Lite para cada um desses serviços pode ser transferida para sua nova conta. |
|Sua organização, os espaços e as configurações de acesso de membro da equipe associada permanecem
os mesmos. Uma organização pode ser transferida para a sua nova conta. |
|O nível do Suporte {{site.data.keyword.Bluemix_notm}} permanece o mesmo. |
{:caption="Table 2. What's not changing" caption-side="top"}

**Nota** Se a sua conta para teste não for convertida, você verá uma mensagem explicando o motivo. Você pode ter mais de uma organização em sua conta para teste existente ou apps que não podem ser transferidos. É possível tomar a ação apropriada e, então, tentar
converter a conta novamente.

Quando você se inscrever para uma conta Standard, poderá convidar membros da equipe para colaborar na sua organização e espaços, visualizar seu uso, criar espaços, atualizar seu perfil
de conta e gerenciar sua organização. Para obter mais informações, veja [Configurando sua conta](/docs/admin/adminpublic.html#account).

### Planos Lite
{: #liteplans}
   
Os planos Lite, que também estão disponíveis em uma conta Pay-As-You-Go, são estruturados
como uma cota grátis. É possível trabalhar em seus projetos sem preocupações, sem o risco de gerar
uma conta acidental. A cota pode operar por um período de tempo específico, por exemplo, por um mês
ou em uma base de uso único. Aqui estão alguns exemplos de cotas do plano Lite:

<ul>
<li>Número máximo de dispositivos registrados.</li>
<li>Número máximo de ligações de aplicativos.</li>
<li>Limite de armazenamento de dados criptografados, por exemplo, 1 GB.</li>
<li>Capacidade de rendimento provisionada.</li>
</ul> 

Em uma conta Standard, é possível usar qualquer coisa no Catálogo
{{site.data.keyword.Bluemix_notm}} que tem um plano Lite. Os planos Lite são fáceis
de localizar. Por padrão, quando você abre o Catálogo, todos os serviços com um plano Lite
são exibidos e identificados com uma tag Lite ![tag Lite](../icons/Lite.svg). 
Selecione um serviço para visualizar os detalhes da cota para o plano Lite associado.

### O que está disponível na conta Standard?
{: #whatsavailable}

Em uma conta Standard, os aplicativos Cloud Foundry podem acessar um máximo de até 256 MB
de memória de tempo de execução instantânea. Se você exceder sua cota alocada, poderá parar alguns
dos seus apps para liberar memória de tempo de execução. 

Durante a conta Standard Beta, os serviços a seguir oferecem um plano Lite:

<ul>
<li>Cloudant NoSQL DB</li>
<li>Internet of Things Platform</li>
</ul>

Mais serviços serão incluídos nesta lista, portanto, fique ligado!

Quando os limites de cota forem atingidos, seu aplicativo será interrompido ou seu serviço
será desativado. Se o plano Lite especificar que a cota será fornecida mensalmente, o uso do recurso será reconfigurado no primeiro dia de cada mês, quando você poderá voltar a trabalhar com o serviço. Quando
você estiver se aproximando de um limite de cota, receberá um e-mail de notificação. 

É possível provisionar uma instância por Plano Lite. 

**Nota**: essas limitações se aplicam somente à conta Standard. A qualquer
momento, é possível fazer upgrade para uma conta de cobrança Pay-As-You-Go ou de Assinatura. Você paga
somente pelo que usar, além dos abonos grátis. Para obter mais
informações sobre contas de Pagamento por uso e de Assinatura, consulte [Como você é faturado](/docs/pricing/index.html#pay-accounts).

### Atividade de desenvolvimento
{: #devactivity}

Para ajudar os usuários da conta Standard a gerenciar melhor seus recursos, construímos alguns
recursos de eficiência que são baseados na atividade de desenvolvimento e no uso:

 * Seus apps serão suspensos após de 10 dias de inatividade de desenvolvimento. Isso ajudará
quando você desejar trabalhar em um novo app, porque não atingirá o limite de cota de memória
de 256 MB. Para acordar seus apps, comece a trabalhar neles novamente na linha de comandos do
Cloud Foundry ou no console do {{site.data.keyword.Bluemix_notm}}. 
 
 Aqui está uma lista de todos os comandos que acordarão seu app:
  * cf push
  * cf restate
  * cf restart
  * cf ssh
  * cf scale
  * cf stop
  * cf start
  * cf create-route
  * cf map-route
  * cf unmap-route
  * cf delete-route
  * cf enable-ssh
  * cf disable-ssh

 **Nota** Se o seu app já estiver ativado para ssh, os comandos
`cf enable-ssh` e `cf disable-sh` não o acordarão. 

 * Seus serviços do plano Lite serão excluídos se não houver nenhuma atividade neles por
30 dias. Então, você não precisará excluir instâncias inativas quando desejar criar uma nova
instância. Neste momento, somente o serviço da Plataforma Internet of Things está usando esse
recurso. 
 
 Mantenha sua instância Lite da Plataforma Internet of Things ativa ao efetuar login no
painel da instância de serviço da Plataforma Internet of Things.
 
### Participando da conta Standard Beta
{: #betainvitation}

Se você for selecionado para participar na conta Beta, um convite será enviado para o
endereço de e-mail associado à sua conta para teste do {{site.data.keyword.Bluemix_notm}}. Ao
receber o convite, conclua as instruções no e-mail para registrar-se para a conta Standard. 

Você está interessado em participar da oferta de conta Standard Beta? Pergunte a seus
amigos e colegas. Se eles foram convidados para participar na conta Beta e criaram sua conta
Standard, eles poderão convidá-lo também. 
