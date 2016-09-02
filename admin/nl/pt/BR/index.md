---



copyright:

  years: 2015, 2016



---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando o {{site.data.keyword.Bluemix_notm}} Local e {{site.data.keyword.Bluemix_notm}} Dedicated
{: #mng}
Última atualização: 16 de agosto de 2016
{: .last-updated}

Se você tiver acesso de administrador para o {{site.data.keyword.Bluemix}}
Local ou o {{site.data.keyword.Bluemix_notm}} Dedicated, acesse a página
**Administração** para gerenciar recursos, monitorar o uso de cotas,
administrar permissões de usuário, planejar notificações de upgrade, visualizar
relatórios e logs de segurança e mais. É possível gerenciar suas organizações criando espaços e configurando [funções de usuário e permissões](index.html#oc_useradmin); veja [Gerenciando suas organizações](../admin/orgs_spaces.html).
{:shortdesc}

*Tabela 1. Tarefas administrativas para gerenciar a instância local ou dedicada do {{site.data.keyword.Bluemix_notm}}*

| O que fazer? | Detalhes |    
|----------------|---------|
|Monitorar o uso do sistema | Clique em **ADMINISTRAÇÃO &gt; USO**. Visualize as informações do sistema, monitore o uso da CPU e o uso do plano para tomar as melhores decisões para seus negócios. Consulte [Visualizando informações de uso](index.html#oc_resource).|
|Gerenciar seu catálogo | Clique em **ADMINISTRAÇÃO &gt; GERENCIAMENTO DO CATÁLOGO** para gerenciar quais serviços estão visíveis para seus usuários e organizações. Consulte [Gerenciando seu catálogo](index.html#oc_catalog).|
|Administrar organizações | Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DA ORGANIZAÇÃO** para criar organizações, monitorar cotas para organizações e tomar decisões baseadas em necessidades rapidamente. Consulte [Administrando organizações](index.html#oc_organizations).|
|Criar espaços e designar funções de usuário | Clique no ícone **{{site.data.keyword.avatar}}** ![ícone Avatar](../support/images/account_support.svg) e, em seguida, selecione **Gerenciar organizações** para criar espaços em suas organizações. Inclua usuários e designe funções de organização e espaço para os usuários. Consulte
[Gerenciando as suas organizações](../admin/orgs_spaces.html). |
|Gerenciar permissões de usuário administrativo | Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DE USUÁRIO** para incluir usuários, remover usuários e ajustar permissões de usuários. Veja [Gerenciando usuários e permissões](index.html#oc_useradmin). |
|Revisar relatórios e logs | Clique em **ADMINISTRAÇÃO &gt; RELATÓRIOS E LOGS** para visualizar relatórios de segurança e logs de auditoria para sua instância. Consulte [Visualizando relatórios](index.html#oc_report). |
|Visualizar Informações do Sistema | Clique em **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA** para visualizar informações do sistema, como atualizações de manutenção pendentes, nome e versão de sua instância, região, URL da API, URL da CLI, detalhes da configuração de LDAP, mapeamentos de grupos e de usuários, estatísticas e domínios compartilhados. Consulte [Visualizando informações do sistema](index.html#oc_system). |
|Estender notificações e configurar inscrições de eventos | Clique em **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente**. É possível usar webhooks para integração com um serviço da web de sua opção para configurar uma assinatura de notificação de eventos para uma atualização ou um incidente. Consulte [Notificações e inscrições de eventos](index.html#oc_eventsubscription). |



## Notificações e inscrições de eventos
{: #oc_eventsubscription}

Também é possível sempre saber o status de seu ambiente, verificando a página Status. Conforme ocorrerem, os incidentes são relatados na página Status. O {{site.data.keyword.Bluemix_notm}}
também envia notificações para a área Notificações na página de Administração para eventos como atualizações planejadas ou de manutenção pendentes.

### Notificações

É possível visualizar notificações para o seu ambiente local ou dedicado, a fim de monitorar o status de seu ambiente. Revise a tabela a seguir, para obter informações sobre os tipos diferentes de
notificações e onde cada tipo de notificação é postado.

*Tabela 2. Tipos de eventos e métodos de notificações*

| **Tipo de evento** | **Método de Notificação** |       
|-----------------|-------------------|
| Atualizações de Manutenção | Você é alertado sobre atualizações de manutenção futuras na área Notificações na página de Administração. Acesse a página **Administração** e, em seguida, selecione o ícone **Notificações** ![Notificações](images/icon_announcement.svg). Para
ver uma lista completa e o histórico de suas notificações pendentes e completas, clique em **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA** &gt; *Número*
**pendente**. É possível ampliar o recurso de notificação configurando uma assinatura que envia um e-mail a destinatários de sua opção. Ou é possível configurar uma assinatura que use
webhooks para integrar as notificações a partir da página Administração com um serviço da web de sua opção. |
| Incidentes críticos | Você é alertado sobre incidentes críticos na página Status. Clique
no ícone **{{site.data.keyword.avatar}}**
![Avatar](../support/images/account_support.svg) e selecione
**Status**. É
possível ampliar o recurso de notificação configurando uma inscrição de evento que envia um e-mail a um destinatário de sua opção. Ou é possível configurar uma assinatura que use
webhooks para integrar as notificações a partir da página Administração com um serviço da web de sua opção.  |  
| {{site.data.keyword.Bluemix_notm}} Status | É sempre possível visualizar o status mais recente para a plataforma, os serviços e a sua instância do {{site.data.keyword.Bluemix_notm}} na
página Status. Clique no ícone
**{{site.data.keyword.avatar}}**
![Avatar](../support/images/account_support.svg) e selecione
**Status**.   |

### Configurando assinaturas de eventos

É possível ampliar a funcionalidade das notificações que são enviadas para a página Administração e a página Status usando inscrições de evento para configurar um e-mail customizado ou usar webhooks
para integrar com uma ferramenta de sua opção. Se você selecionar a opção webhooks, as suas notificações serão roteadas diretamente para um destino de sua opção, como um número de telefone (por mensagem SMS). É possível customizar o tipo de notificação, especificamente atualizações de manutenção ou alertas de incidente crítico e as informações incluídas no corpo de cada notificação.

**Nota**: somente usuários com a permissão de super usuário (`ops.admin`) podem configurar inscrições de evento.

Para acessar a página de **Inscrições de Evento**, conclua as etapas a seguir:

* Para notificações de atualização de manutenção, acesse **INFORMAÇÕES DO SISTEMA &gt; *Número* pendente &gt; Assinaturas**.
* Para notificações de incidentes, clique no ícone
**{{site.data.keyword.avatar}}**
![Avatar](../support/images/account_support.svg) &gt;
**Status** e, em seguida, clique no ícone
**Assinar**
![Assinar](images/icon_subscribe.svg).

**Nota**: é possível acessar a página de inscrição de evento para ambos os tipos de notificações usando um dos dois métodos descritos.

Para criar uma assinatura de e-mail ou webhook a partir da página de **Inscrições de Evento**, conclua as etapas a seguir:

1. Clique em **Incluir assinatura**.
2. Preencha o formulário de inscrição de evento. Para obter informações sobre os campos no formulário, os valores a serem usados na seção de carga útil e o corpo da mensagem do modelo de e-mail,
revise as tabelas a seguir.
3. Após concluir o formulário, é possível escolher a partir das opções a seguir:

  * Clique em **Salvar** para salvar a assinatura em sua lista de inscrições de evento.
  * Clique em **Salvar e Testar** para salvar e testar a notificação.
  * Clique em **Salvar e Fechar** para salvar a assinatura em sua lista de inscrições de evento e retorne para a página anterior.

*Tabela 3. Campos de formulário de inscrição de evento para uma assinatura de e-mail*

| **Campo** | **Descrição** |
|-----------------|-------------------|
| Tipo | Selecione **E-mail**. |
| Evento | Selecione para ser inscrito para notificações para uma Atualização ou um Incidente. |
| Ativar | Selecione a opção para ativar as notificações por e-mail. Limpe a seleção para desativar a notificação por e-mail. As assinaturas são ativadas por padrão. |
| Combinar notificações | Selecione a opção para combinar as notificações de incidentes
para todas as regiões em uma única notificação. Essa opção está disponível somente para incidentes. |
| Assunto | Insira a linha de assunto para o e-mail. Este campo é requerido.  |
| Corpo | Insira o texto do corpo da mensagem a ser enviada no e-mail. É possível usar os valores de carga útil da IBM para preencher a notificação por e-mail com informações pertinentes. Consulte a tabela
de [Valores da seção de carga útil](index.html#payload) para identificar quais valores é possível utilizar. Use marcas HTML básicas para estruturar o seu e-mail. Se você não inserir informações nesta seção, receberá uma notificação sem quaisquer informações adicionais. Este campo é requerido. |
| Para | Insira o endereço ou endereços de e-mail usando uma lista separada por vírgula para os destinatários da notificação por e-mail. Expanda as opções "cc" ou "bcc" para copiar outros no e-mail. Este campo é requerido. |
| Descrição | Inclua uma descrição exclusiva para a assinatura que você está criando. |


*Tabela 4. Campos de formulário de inscrição de evento para uma assinatura de webhook*

| **Campo** | **Descrição** |
|-----------------|-------------------|
| Tipo | Selecione **Webhook** |
| Método | Selecione **GET** ou **POST**. |
| Evento | Selecione para ser inscrito para notificações para uma Atualização ou um Incidente. |
| Ativar | Selecione a opção para ativar a notificação. Limpe a seleção para desativar a
notificação. As assinaturas são ativadas por padrão. |
| Combinar notificações | Selecione a opção para combinar as notificações de incidentes
para todas as regiões em uma única notificação. Essa opção está disponível somente para
incidentes. |
| URL | Insira a URL para se conectar ao seu serviço da web. |
| Descrição | Inclua uma descrição exclusiva para a assinatura que você está criando. |
| Nome de Usuário | Insira seu nome de usuário para o seu serviço da web. Se não desejar usar suas credenciais pessoais, será possível configurar um ID funcional para usar especificamente com o {{site.data.keyword.Bluemix_notm}}. |
| Senha | Insira a senha para o seu serviço da web. |
| Carga Útil | Se tiver selecionado o método POST, insira as propriedades específicas para o serviço da web que você está usando,
pareadas com os valores de carga útil usados para a notificação da IBM. Consulte a tabela
de [Valores da seção de carga útil](index.html#payload) para identificar quais valores é possível utilizar. Se você não inserir informações nesta seção, receberá uma notificação sem quaisquer informações adicionais. |

*Tabela 5. Valores da seção de carga útil*
{: #payload}

| **Valor IBM** | **Descrição** | **Tipo do evento** |
|----------------|----------------|------------------------|
| {{content.title}} | título Message |  Atualização e incidente  |
| {{type}} | Atualização ou incidente | Atualização e incidente |
| {{region}} | Região afetada | Atualização e incidente |
| {{content.message}} | Descrição da mensagem |   Atualização e incidente  |
| {{content.severity}} | Classificação de gravidade | Incidente |
| {{content.category}} | Serviços afetados | Incidente |
| {{content.subCategoryName}} | Componentes afetados | Incidente |
| {{status}} | Status da atualização | Atualizar |
| {{content.scheduleWindow.start}} | A data de início planejada para a atualização | Atualizar |
| {{content.scheduleWindow.end}} | O horário de encerramento planejado para a atualização | Atualizar |
| {{content.disruption}} | Componentes afetados | Atualizar |

Quando a sua inscrição de evento for salva, você receberá notificações por meio do método que você configurar. Notificações ainda são postadas na página Status para incidentes e na área Notificações da página Administração para atualizações de manutenção.

É possível selecionar qualquer inscrição de evento salva, visualizar a atividade recente ou editar conforme necessário. Clique para expandir qualquer entrada de atividade recente para visualizar os
detalhes de histórico.

## Atualizações de Manutenção
{: #oc_schedulemaintenance}

É possível visualizar atualizações de manutenção planejadas e pendentes, acessando **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente** para acessar
a página **Atualizações do sistema**.

**Nota**: consulte a seção a seguir para [Configurar janelas de manutenção pré-aprovadas](index.html#preapprovedmaintenance) para iniciar. Essas janelas devem ser configuradas em ordem para a IBM planejar a manutenção
para o seu ambiente.

<dl>
<dt>Atualizações sem interrupção</dt>
<dd>Uma atualização sem interrupção não afeta o seu ambiente, os seus aplicativos em execução ou o acesso de seus usuários aos seus aplicativos. Esse tipo de atualização não requer aprovação caso a caso e
será aplicado durante as janelas de manutenção pré-aprovadas, disponíveis que você configurar a partir da página Atualizações do sistema.</dd>
<dt>Atualizações disruptivas</dt>
<dd>Uma atualização disruptiva pode afetar o seu ambiente, os aplicativos em execução ou o acesso de seus usuários aos aplicativos. Deve-se planejar e aprovar cada uma dessas atualizações de manutenção
dentro da janela de manutenção atribuída de 21 dias. É possível selecionar a data e hora sugeridas de implementação, a opção para qualquer uma de suas janelas pré-aprovadas ou é possível abrir o calendário
para selecionar três datas e horas específicas para a IBM escolher ao planejar a atualização.</dd>
</dl>


### Configurando janelas de manutenção pré-aprovadas
{: #preapprovedmaintenance}

Antes de iniciar o planejamento e aprovar atualizações, deve-se configurar as janelas de manutenção pré-aprovadas. Atualizações sem interrupção são planejadas durante os horários de janela pré-aprovados.

É necessário configurar no mínimo 12 horas disponíveis por semana para no mínimo
dois dias durante cada semana. Por exemplo, é possível configurar períodos de 6 horas ao
longo de dois dias separados ou períodos de 4 horas ao longo de três dias separados. Para assegurar que as janelas forneçam tempo suficiente para uma atualização ser aplicada, cada janela deve ter
um mínimo de quatro horas de duração.

**Nota**: somente usuários com a permissão de super usuário
(`ops.admin`) podem planejar e aprovar atualizações de manutenção.

1. Acesse **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente &gt; Gerenciar Disponibilidade**.
2. Expanda a seção **Gerenciar janelas de atualização disponíveis**.
3. Clique em **Incluir novo** ![Incluir novo](images/add-new.png).
4. Configure a sua primeira janela de disponibilidade, selecionando a frequência, a duração e o horário de início para a janela.
5. Opcional: Selecione **Marcar como preferencial**, se você
gostaria de definir seu período de disponibilidade recorrente como um tempo preferencial
para implementações a serem planejadas. Os períodos preferenciais têm prioridade,
quando possível.
6. Clique em
**Enviar**.
7. Repita esse processo até ter atendido aos requisitos mínimos para as janelas semanais.

### Configurando janelas de manutenção indisponíveis

Após configurar as suas janelas de manutenção pré-aprovadas, é possível optar por configurar datas e horas específicas em que o seu ambiente não está disponível para atualizações. Por exemplo, é possível
escolher um final de semana ou feriado de alto tráfego quando você não deseja que nenhuma manutenção seja aplicada, para assegurar que os seus aplicativos estejam disponíveis para os usuários.

1. Acesse **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente &gt; Gerenciar Disponibilidade**.
2. Expanda a seção **Gerenciar janelas de atualização indisponíveis**.
3. Clique em **Incluir novo** ![Incluir novo](images/add-new.png).
4. Configure a sua janela indisponível, selecionando a frequência, a duração e o horário de início para a janela.
5. Clique em
**Enviar**.

### Planejando e aprovando atualizações
{: #scheduleandapprove}

Após você configurar as suas janelas de manutenção pré-aprovadas, atualizações sem interrupção serão planejadas automaticamente durante esses horários. A sua aprovação explícita para esses tipos de
atualizações não é necessária. No entanto, é possível visualizar os detalhes de cada atualização de manutenção incluindo o que está sendo atualizado, quanto tempo a atualização levará e para quando a
atualização está planejada.

Para visualizar os detalhes para uma atualização sem interrupção, conclua as etapas a seguir:

1. Acesse **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente**.
2. Identifique quaisquer linhas que tenham **Planejamento de Cliente Necessário** configurado como **Não**.
3. Selecione a linha para essa atualização, para visualizar os detalhes.

Uma atualização disruptiva pode afetar o seu ambiente, os aplicativos em execução ou o acesso de seus usuários aos aplicativos. Deve-se planejar e aprovar cada uma dessas atualizações de manutenção
dentro da janela de manutenção atribuída de 21 dias. É possível selecionar a data e hora sugeridas de implementação, a opção para qualquer uma de suas janelas pré-aprovadas ou é possível abrir o calendário
para selecionar três datas e horas específicas para a IBM escolher ao planejar a atualização.

Para atualizações disruptivas que requerem a sua aprovação, conclua as etapas a seguir:

1. Acesse **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA &gt; *Número* pendente**.
2. Identifique quaisquer linhas que tenham **Planejamento de Cliente Necessário** configurado como **Sim**.
3. Selecione a linha para essa atualização para revisar os detalhes para a atualização, incluindo a descrição da atualização, a data e hora sugeridas para a atualização, os componentes afetados e a
duração para a atualização.
4. Selecione **Planejar e aprovar**.
5. Escolha entre as opções a seguir:
**Data sugerida**,
**Datas alternativas** ou **Qualquer janela pré-aprovada**. Se
você selecionar **Datas alternativas**, será possível abrir o
calendário para selecionar três opções para a IBM escolher.
6. Opcional: Na lista de datas alternativas selecionadas no calendário, selecione
aquelas que você deseja configurar como datas preferenciais para implementação. Cada data
selecionada é mencionada como preferencial para o implementador que está planejando a
implementação. A IBM tenta planejar a manutenção durante as janelas de atualização preferenciais.
7. Selecione **Enviar** quando tiver concluído.

Com base em sua seleção, a atualização será planejada para implementação durante a data sugerida que você aceitou, durante uma de suas janelas pré-aprovadas ou uma das datas e horas específicas que
você selecionou. Quando a atualização estiver planejada para implementação pela IBM, você verá a data planejada refletida nos detalhes para a atualização na página
**Atualizações do Sistema**. É possível replanejar uma implementação já
planejadas somente se um dia (24 horas) antes a data e hora de início planejada
permanecer. Uma vez replanejada uma implementação, não será possível replanejá-la
novamente.


## Visualizando as informações do sistema
{: #oc_system}

Para visualizar informações do sistema, clique em
**ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA**.

É possível expandir e visualizar várias seções sobre atualizações de manutenção pendentes, informações gerais do sistema e detalhes de configuração de LDAP.

### Atualizações do sistema pendentes

Na seção Atualizações, é possível ver o número de notificações de atualizações pendentes que requerem ação de sua parte. Há dois tipos de atualizações de manutenção que você pode ver:

<dl>
<dt>Atualizações sem interrupção</dt>
<dd>Uma atualização sem interrupção não afeta o seu ambiente, os seus aplicativos em execução ou o acesso de seus usuários aos seus aplicativos. Esse tipo de atualização não requer aprovação caso a caso. Essas atualizações são aplicadas nas janelas de manutenção pré-aprovadas e disponíveis que você configura na página Atualizações do sistema.</dd>
<dt>Atualizações disruptivas</dt>
<dd>Uma atualização disruptiva pode afetar o seu ambiente, os aplicativos em execução ou o acesso de seus usuários aos aplicativos. Você tem a capacidade de planejar e aprovar cada uma dessas atualizações de
manutenção dentro da janela de manutenção atribuída de 21 dias, para assegurar que a atualização não seja aplicada durante as horas críticas de negócios. É possível selecionar a data e hora sugeridas de
implementação, que são baseadas em suas janelas de manutenção pré-aprovadas ou é possível selecionar dois horários e datas adicionais para a IBM escolher ao aplicar a atualização.</dd>
</dl>

Para obter mais informações sobre a configuração de janelas de manutenção
pré-aprovadas e datas indisponíveis específicas para manutenção, consulte
[Atualizações de manutenção](admin/index.html#oc_schedulemaintenance).

### Informações gerais do sistema

Na seção Informações gerais, é possível visualizar as informações a seguir:

- Informações básicas sobre a construção do {{site.data.keyword.Bluemix_notm}}.
- Informações de API incluindo a versão, a URL, a região e um link para a documentação de CLI.
- Informações de domínio compartilhadas sobre seu sistema e serviço.
- Estatísticas sobre o número total de aplicativos, usuários e organizações.

### Detalhes de configuração do LDAP

Na seção Detalhes de configuração LDAP, é possível selecionar o servidor
LDAP e visualizar informações sobre os mapeamentos de usuários e de grupos. Se estiver usando o {{site.data.keyword.IBM}} WebID, ele será indicado nesta seção.

## Visualizando o uso e relatórios
{: #oc_resource}

É possível visualizar diferentes tipos de informações de uso para a sua instância local ou dedicada e a conta do {{site.data.keyword.Bluemix_notm}}. Também é possível fazer o download e
visualizar relatórios de segurança e logs para a sua instância do {{site.data.keyword.Bluemix_notm}}.

- Informações do recurso, incluindo espaço em disco, uso de CPU, uso de rede e tempos médios de resposta. Consulte [Uso de recursos](index.html#resourceusage).
- Uso da conta por organização, incluindo o número de apps do tempo de execução com uso, número total de GB/horas de tempo de execução e o número de instâncias de serviço com uso. Consulte [Uso da conta](index.html#accountusage).
- Uso de cota de memória da organização, memória de app alocada com base na cota de memória total usada e uma visualização de uso de GB/hora por app para uma organização específica. Também é possível visualizar o uso de cotas para todas as organizações na página Administração da organização na seção Monitoramento de cota. Consulte [Administração da organização](../admin/index.html#orgusage).


### Uso do Recurso
{: #resourceusage}

Para visualizar informações de uso de recursos, clique em **ADMINISTRAÇÃO &gt; USO**.

Na seção Monitoramento de recurso, é possível visualizar as
informações a seguir:

- Informações de uso do recurso, tais como quantos GB de memória e quantos GB de espaço em disco são
usados. É possível visualizar o uso de CPU médio em todos os Droplet Execution Agents (DEAs). Clique no quadrado de
**CPU** e poderá ver o uso de CPU para cada DEA. O DEA com o mais alto uso é listado primeiro e cada
um é identificado por suas tarefas e endereço IP. O uso de CPU é separado em três categorias que incluem a quantia de
CPU gasto em processos do sistema, quantia de CPU gasta em processos do usuário e quantia de
CPU gasta em processos em espera.
- As informações de uso da rede para entrada de largura da banda e saída da largura da banda, durante o último dia, durante a última semana ou
durante o último mês.
Os dados exibidos são baseados na soma do tráfego de entrada e de saída para as redes públicas e privadas.
- Tempo médio de resposta para {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, hora e dia.
- Transações médias por segundo para {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, hora e dia.

### Uso de conta
{: #accountusage}

É possível visualizar o uso mensal de sua conta para seu ambiente dedicado ou local. É possível usar esses dados para identificar quanto cobrar de organizações específicas com base no uso das mesmas.

<ol>
<li>Clique no ícone <strong>{{site.data.keyword.avatar}}</strong>
![Avatar](../support/images/account_support.svg) &gt;
<strong>Conta</strong> &gt; <strong>Detalhes do uso</strong>.</li>
<li>Selecione a organização para a qual deseja ver os dados.</li>
<li>É possível ver detalhes de uso para as categorias a seguir:
<ul>
<li>Apps de tempo de execução que têm uso</li>
<li>Uso total de apps de tempo de execução em GB/horas</li>
<li>Instâncias de serviço que têm uso</li>
</ul>
</li>
<li>Opcional: visualize os seus dados para um mês específico usando o menu <strong>Sua atividade na nuvem</strong> para selecionar um mês de sua opção.</li>
<li>Opcional: clique em <strong>EXPORTAR DADOS</strong> e selecione <strong>CSV</strong> ou <strong>JSON</strong> para exportar seus dados do mês selecionado para um arquivo <code>CSV</code> ou <code>JSON</code>.</li>
</ol>

Também é possível visualizar o uso mensal e os encargos associados no nível de conta para seus tempos de execução, apps e serviços organizados a partir do {{site.data.keyword.Bluemix_notm}} Public. É possível usar esses dados para identificar quanto cobrar de organizações específicas com base no uso das mesmas.

<ol>
<li>Clique no ícone <strong>{{site.data.keyword.avatar}}</strong>
![Avatar](../support/images/account_support.svg) &gt;
<strong>Conta</strong> &gt; <strong>Detalhes do uso</strong>.</li>
<li>Clique em <strong>Public</strong>.</li>
<li>Selecione a organização para a qual deseja ver dados ou selecione <strong>Todas as organizações</strong> para visualizar os dados para todas as organizações de uma vez.</li>
<li>É possível ver detalhes de uso para as categorias a seguir:
<ul>
<li>Apps de tempo de execução que têm uso</li>
<li>Uso total de apps de tempo de execução em GB/horas</li>
<li>Instâncias de serviço que têm uso</li>
<li>Um resumo de encargos para todos os tempos de execução, serviços e apps organizados</li>
</ul>
</li>
<li>Opcional: visualize os seus dados de um mês específico, selecionando um mês de sua opção a partir do gráfico de barras. Os dados do mês atual são exibidos por padrão.</li>
<li>Opcional: clique em <strong>EXPORTAR DADOS</strong> e selecione <strong>CSV</strong> ou <strong>JSON</strong> para exportar seus dados do mês selecionado para um arquivo <code>CSV</code> ou <code>JSON</code>.</li>
</ol>


### Uso da organização
{: #orgusage}

Para visualizar o uso por organização, clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DA ORGANIZAÇÃO** e, em seguida, selecione uma organização a partir da **Lista de organizações**. Na página **Gerenciar organizações** para a organização selecionada, é possível visualizar as informações de uso a seguir:

- Número de serviços que estão atualmente em uso.
- Número de rotas que estão atualmente em uso.
- Gráfico de cota de memória que mostra o quanto da cota está usado e quanto não está atualmente sendo usado.
- Gráfico de alocação de aplicativos que mostra quais aplicativos estão incluídos na cota de memória usada.
- Gráfico de uso de aplicativos medido que mostra um relatório trimestral de GB/horas usados por app implementado. É possível selecionar a **Visualização de lista** para ver dados de todos os apps, incluindo a alocação de memória por app e o uso de GB/hora medido para os últimos três meses.

Para obter mais informações sobre como visualizar o uso por organização, ajustar planos de cotas e gerenciar suas organizações, consulte [Administrando organizações](../admin/index.html#oc_organizations).

### Relatórios
{: #oc_report}

É possível visualizar os logs e relatórios de segurança, como
DataPower&trade;, firewall, e auditoria de login, para a instância
do {{site.data.keyword.Bluemix_notm}}. Para visualizar relatórios e logs, clique em
**ADMINISTRAÇÃO &gt; RELATÓRIOS E LOGS**.

Selecione a partir das opções a seguir:

- É possível selecionar as datas de início e de encerramento nos campos para filtrar quais relatórios e logs são
exibidos.
- É possível expandir e visualizar vários relatórios na área de janela de navegação.
- É possível procurar em sua coleção de relatórios e logs. A procura se aplica aos nomes de relatório
bem como ao conteúdo de texto contido nos logs e relatórios. Também é possível escolher filtrar sua procura por
**Eventos de administração**, **Relatórios do DataPower**,
**Firewall** e **Auditoria de login**.
- Ao exibir um relatório ou log, é possível clicar no ícone ![Download](images/icon_download.png)
para fazer download do relatório.

A tabela a seguir mostra a lista de relatórios de segurança gerados para o {{site.data.keyword.Bluemix_notm}} Local e o {{site.data.keyword.Bluemix_notm}} Dedicated.

*Tabela 6. Lista de relatórios de segurança*

| **Categoria** | **Relatório** | **Descrição** |      
|-----------------|-------------------|---------------------|
| Firewall | Logins de firewall | Eventos relacionados a login do administrador para os dispositivos de firewall Vyatta. |
| Firewall | Negações de firewall | Eventos gerados pelos dispositivos de firewall Vyatta quando uma solicitação para acessar é negada de acordo com as regras de firewall que estão em vigor. |
| Eventos de login do administrador do {{site.data.keyword.Bluemix_notm}} | Login de administradores do {{site.data.keyword.Bluemix_notm}} | Eventos gerados pelo sistema operacional quando um administrador inicia uma sessão SSH em cada sistema {{site.data.keyword.Bluemix_notm}}. |
| Eventos de login do desenvolvedor de aplicativos do {{site.data.keyword.Bluemix_notm}} | Login de desenvolvedores de aplicativos do {{site.data.keyword.Bluemix_notm}} | Eventos gerados pelo componente de login da plataforma {{site.data.keyword.Bluemix_notm}} quando um usuário da plataforma {{site.data.keyword.Bluemix_notm}} inicia uma sessão usando a linha de comandos, as APIs REST ou a interface com o usuário do {{site.data.keyword.Bluemix_notm}}. |
| Eventos administrativos do administrador do {{site.data.keyword.Bluemix_notm}} | Eventos administrativos do sistema operacional dos administradores do {{site.data.keyword.Bluemix_notm}} | Eventos gerados pelo sistema operacional quando um administrador executa ação em uma sessão de trabalho atual. |
| Eventos administrativos do desenvolvedor de aplicativos do {{site.data.keyword.Bluemix_notm}} | Eventos administrativos do {{site.data.keyword.Bluemix_notm}} (Cloud Foundry) | Eventos relacionados a operações executadas pelo usuário da plataforma {{site.data.keyword.Bluemix_notm}} usando a linha de comandos, as APIs REST ou a interface com o usuário do {{site.data.keyword.Bluemix_notm}}. |
| Eventos administrativos do banco de dados do administrador do {{site.data.keyword.Bluemix_notm}} | Eventos administrativos do banco de dados | Eventos relacionados a operações executadas por um administrador de banco de dados nos bancos de dados internos do {{site.data.keyword.Bluemix_notm}}. |
| Eventos de administração | Eventos de gerenciamento do usuário | Eventos relacionados a ações de gerenciamento do usuário executadas na página Administração. |
| Eventos de administração | Catálogo | Eventos relacionados a mudanças no Catálogo de serviços. |
| Eventos de administração | Eventos de gerenciamento de relatórios de segurança | Eventos relacionados a ações de gerenciamento de relatórios de segurança executadas na página Administração. |
| Revisões de acesso | Relatório de revisões de acesso | Revisões para acessos privilegiados. |
| Gerenciamento de mudanças | Gerenciamento de mudanças de software | Atividade de gerenciamento de mudanças. |
| Gerenciamento de chave | Gerenciamento de certificados SSL customizados | Certificações SSL customizadas que foram transferidos por upload e armazenadas. |
| Encryption | Criptografia de dados em trânsito | Criptografia de dados em trânsito que foi configurada. |
| Anti-virus | Relatório de varredura antivírus | Software antivírus que está em vigor. |
| Gerenciamento de correção de software | Relatório de aplicativo de correção | Correções de software que foram aplicadas. |
| Gerenciamento de incidentes de segurança | Relatório de correção de incidentes de segurança | Evidência de incidentes de segurança para gerenciamento de incidentes de segurança. |

## Visualizando o status
{: #oc_status}

É possível visualizar o status para o ambiente do {{site.data.keyword.Bluemix_notm}} e para o console de administração.

### Status do ambiente do {{site.data.keyword.Bluemix_notm}}

É possível monitorar o status para a sua instância do {{site.data.keyword.Bluemix_notm}}, usando a página Status do {{site.data.keyword.Bluemix_notm}}. 
Clique no ícone **{{site.data.keyword.avatar}}**
![Avatar](../support/images/account_support.svg) e selecione
**Status**. 

A página Status é o local central para localizar notificações e anúncios sobre os eventos principais que estão afetando a plataforma do {{site.data.keyword.Bluemix_notm}} e os serviços principais no {{site.data.keyword.Bluemix_notm}}. É possível assinar um feed RSS para notificações de modo que não seja necessário verificá-las. Para obter mais informações sobre a página Status e a configuração do feed RSS, veja [Visualizando o {{site.data.keyword.Bluemix_notm}}](../support/index.html#viewing-bluemix-status).

### Status do console de administração

Após a implementação inicial do seu ambiente do {{site.data.keyword.Bluemix_notm}}, uma verificação é concluída automaticamente nos componentes que são usados para administrar o seu ambiente. É possível acessar a página Verificação do console administrativo, para verificar o status dos componentes após a verificação ter sido executada. Para acessar a página, acesse
<code>https://console.&lt;subdomain&gt;.bluemix.net/check</code>, em que `<subdomain>` é o nome de sua instância local ou dedicada.

É possível executar uma verificação a qualquer momento. Deve-se ter efetuado login a fim de selecionar a opção para executar a verificação. Se você encontrar falhas enquanto estiver incluindo um
usuário, editando uma organização ou gerenciando os seus serviços, execute esta verificação para identificar se quaisquer componentes estão falhando ou estão desconectados. É possível abrir um chamado de
suporte com as informações da verificação, para ter o problema resolvido rapidamente.

## Gerenciando seu catálogo
{: #oc_catalog}

É possível gerenciar quais serviços e iniciadores do
{{site.data.keyword.Bluemix_notm}} ficarão visíveis
para usuários no catálogo do {{site.data.keyword.Bluemix_notm}}. Clique em **ADMINISTRAÇÃO &gt; GERENCIAMENTO DO CATÁLOGO**.

Selecione um título de iniciador ou serviço para editar a visibilidade do plano do iniciador ou serviço. Para
editar a visibilidade, selecione dentre as opções a seguir:

- Para mostrar o serviço ou o iniciador oculto para que
ele fique visível para seus usuários no catálogo, selecione
**ATIVAR TODOS OS PLANOS**.
- Para ocultar o serviço ou o iniciador de seus usuários no
catálogo do {{site.data.keyword.Bluemix_notm}}, selecione
**DESATIVAR TODOS OS PLANOS**.
- Para controlar a visibilidade de um plano individual, selecione o nome do plano e, em seguida, use o menu suspenso para selecionar **Ativar para todas as organizações**, **Desativar para todas as organizações** ou **Ativar plano para organizações específicas**.

<!-- staging only start -->

Também é possível gerenciar a ordem de prioridade dos buildpacks disponíveis para serem escolhidos com base na compatibilidade para os seus desenvolvedores quando eles estiverem criando aplicativos.

1. Acesse **ADMINISTRAÇÃO &gt; GERENCIAMENTO DE CATÁLOGO**
2. Acesse a seção **Calcular**.
3. Selecione **Prioridade do buildpack**.
4. Selecione a opção de buildpack que você deseja priorizar como mais alta ou mais baixa na lista.
5. Com a opção selecionada, use as setas para mover a opção na lista.

<!-- staging only end -->

### Registrando um broker de serviço
{: #servicebrokerui}

Se você tiver um serviço que deseja exibir em seu catálogo do {{site.data.keyword.Bluemix_notm}}, deve-se implementar e registrar um broker de serviço. Após registrar seu broker, será possível escolher quais organizações podem acessar o serviço em sua instância local ou dedicada.

Os métodos para trabalhar com seu broker de serviço variam, dependendo de quantos serviços ele gerencia ou se ele já foi registrado com o {{site.data.keyword.Bluemix_notm}}.

- Se o seu broker de serviço gerenciar um serviço, será possível usar a interface com o usuário para registrá-lo após ter implementado a [API do broker de serviço](http://docs.cloudfoundry.org/services/api.html){: new_window}. Consulte [Registrando um broker de serviço que gerencia um serviço](index.html#registerbrokerui).
- Se o seu broker de serviço gerencia vários serviços, neste momento, não será possível registrá-lo após ter implementado a API do broker de serviço. Em vez disso, use a CLI cf com o [plug-in de administrador do {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (subcomando `ba`) ou use a [API de serviço customizada](index.html#servicebrokerapi).
- Se seu broker de serviço já estiver registrado e você desejar atualizar ou excluir o mesmo, use a CLI cf com o [plug-in de administrador do {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (subcomando `ba`) ou use a [API de serviço customizada](index.html#servicebrokerapi).

#### Registrando um broker de serviço que gerencia um serviço
{: #registerbrokerui}

Conclua as etapas a seguir para registrar seu broker de serviço:

<ol>
<li><a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implemente a API do broker de serviço Cloud Foundry</a> para ativar a comunicação entre seu serviço e o {{site.data.keyword.Bluemix_notm}}. A API do broker de serviço é um conjunto de terminais REST que são consumidos pelo {{site.data.keyword.Bluemix_notm}}.<br />
<br />
<p>Quando você estiver implementando o broker de serviço, na resposta JSON de <code>GET /v2/catalog</code>, deve-se fornecer as definições para seu serviço e planos de serviço, incluindo as informações de serviço que deseja exibir. Por exemplo, revise o JSON de amostra a seguir da resposta do Catálogo (GET)</p>
<p><pre>
"services": [
   {
      "bindable":true,
      "description":"O Cool Service é uma solução de data warehousing e analítica.",
      "id":"cool-service-id",
      "name":"coolservice",
      "tags": [
         "customer_dedicated"
      ],
      "metadata": {
         "displayName": "Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Empresa do Cool",
         "longDescription":"O Cool Service é uma solução de data warehousing e analítica. É possível mover rapidamente os seus dados para um banco de dados colunar contido na memória e começar a executar
consultas analíticas complexas.",
         "bullets": [
            {
               "title": "Fast and Simple",
               "description": "Cool Service uses dynamic in-memory columnar technology and innovations, such as parallel vector processing and actionable compression to rapidly scan and return relevant data."
            },
            {
               "title": "Connectivity",
               "description":"O Cool Service é construído para permitir que você se conecte facilmente e a todos os seus serviços e aplicativos. É possível começar a analisar os seus dados imediatamente com
ferramentas familiares."
            }
         ],
         "featuredImageUrl": "http://path/to/icon_64x64.png",
         "imageUrl": "http://path/to/icon_50x50.png",
         "mediumImageUrl": "http://path/to/icon_32x32.png",
         "smallImageUrl": "http://path/to/icon_24x24.png",
         "documentationUrl": "http://path/to/documentation.html",
         "instructionsUrl": "http://path/to/servicesample.md",
         "termsUrl": "http://path/to/terms_of_agreement.pdf",
         "media":[
            {
               "type": "youtube",
               "thumbnailUrl": "http://path/to/thumbnail.png",
               "url": "http://path/to/youtube/video",
               "caption": "Using Cool Service in 60 Seconds"
            },
            {
               "type": "image",
               "thumbnailUrl": "http://path/to/thumbnail.png",
               "url": "http://path/to/image_file.png",
               "caption": "Cool Service connects applications"
            },
            {
               "type": "video",
               "thumbnailUrl": "http://path/to/thumb.png",
               "caption": "Cool Service works with tables",
               "source": [
                  {
                     "type": "video/mp4",
                     "url": "http://path/to/video_file.mp4"
                  },
                  {
                     "type": "video/ogg",
                     "url": "http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
      "plans":[
         {
            "name":"smallplan",
            "description":"Esquema e espaço de tabela dedicados por instância de serviço em um servidor compartilhado. 1 GB e 10 GB de armazenamento do banco de dados compactados podem conter até 5 GB e 50 GB
de dados descompactados, respectivamente, com base nas proporções de compactação típicas.",
            "free":false,
            "id":"cool-service-plan-id",
            "metadata": {
               "bullets": [
                  "Mín. de 1 GB por instância. Máx. de 10 GB por instância."
               ],
               "costs":[
                  {
                     "unitId":"INSTANCES_PER_MONTH",
                     "unit":"MONTHLY",
                     "partNumber":"D15UTLL"
                  }
               ],
               "displayName":"Small"
            }
         }
      ]
   }
]
}
</pre></p>
<p><strong>Nota</strong>: ao criar um broker de serviço para um ambiente local ou dedicado, deve-se especificar `customer_dedicated` no campo "tags" de seu arquivo JSON de definição de serviço.</p>
</li>
<li>Após implementar a API do broker de serviço, acesse <strong>ADMINISTRAÇÃO </strong> &gt; <strong>GERENCIAMENTO DE CATÁLOGO</strong>.</li>
<li>Clique em <strong>REGISTRAR UM BROKER DE SERVIÇO</strong>.</li>
<li>Preencha o formulário inserindo valores nos campos a seguir:
<ul>
<li>Nome do broker de serviço</li>
<li>URL do broker de serviço</li>
<li>Nome do usuário do broker de serviço</li>
<li>Senha do broker de serviço</li>
</ul>
</li>
<li>Click <strong>CONNECT</strong>.</li>
<li>Revise as informações de seu serviço, incluindo os planos disponíveis, o ícone e a descrição do serviço.<br />
<p><strong>Nota</strong>: se precisar mudar as informações do catálogo para o serviço, atualize seu broker de serviço e inicie o processo de registro novamente preenchendo o formulário.</p>
</li>
<li>Clique em <strong>REGISTRAR</strong>.</li>
<li>Escolha ativar todos os planos ou apenas planos específicos para o serviço. Todos os planos são desativados por padrão.</li>
<li>Ative a instância de serviço para todas as organizações ou organizações específicas.</li>
</ol>

Agora é possível ver seu serviço na categoria Serviços customizados em seu Catálogo do {{site.data.keyword.Bluemix_notm}}. Acesse **ADMINISTRAÇÃO &gt; GERENCIAMENTO DO CATÁLOGO** e selecione o quadro no catálogo. É possível ativar diferentes planos e editar a visibilidade do plano de suas organizações a qualquer momento.

## Administrando as organizações
{: #oc_organizations}

É possível gerenciar suas organizações criando e excluindo organizações, incluindo ou removendo gerenciadores para organizações e monitorando o uso de cota para tomar as melhores decisões para seus negócios.

Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DA ORGANIZAÇÃO**.

É possível expandir e visualizar várias seções. Também é possível revisar e gerenciar os planos de cota para suas organizações.

### Criando organizações

Para criar uma nova organização e incluir gerenciadores, conclua as etapas a seguir:

1. Clique em <strong>CRIAR ORGANIZAÇÃO</strong>.
2. Insira um nome para a organização
3. Insira o nome ou o e-mail da pessoa que deseja incluir como um gerente. É possível incluir mais de um gerenciador inserindo e selecionando múltiplos nomes.
4. Clique em <strong>CRIAR ORGANIZAÇÃO</strong> para salvar suas mudanças e criar a organização.

### Criando Espaços

É possível criar espaços em
sua organização, por exemplo, um espaço *dev* como
um ambiente de desenvolvimento, um espaço *test* como um ambiente
de teste e um espaço *production* como um ambiente de
produção. Em seguida, é possível associar os apps aos espaços. Conclua as etapas a seguir para criar um espaço:

1. Acesse o ícone **{{site.data.keyword.avatar}}** ![ícone Avatar](../admin/images/account_support.svg) &gt; página **Gerenciar organizações**.
2. Selecione a organização na qual deseja incluir um espaço.
3. Clique em **Criar um espaço**.
4. Insira um nome de espaço.
5. Clique **Criar**.


### Monitoramento de cota

Na seção Monitoramento de cota, é possível expandir a seção e visualizar as informações a seguir:

- Uso de memória do ambiente. Esta seção detalha o uso de memória para o ambiente do sistema integral.
	O gráfico fornece informações que incluem a memória do sistema usado, a memória do sistema total,
 a cota que é usada e a cota total alocada. A lista de termos a seguir define os tipos de uso de memória
 que são exibidos no gráfico.

	<dl>
	<dt><strong>Memória do sistema usado</strong></dt>
	<dd>A memória física que é usada por seu ambiente.</dd>
	<dt><strong>Memória total do sistema</strong></dt>
	<dd>A memória física total disponível para seu ambiente.</dd>
	<dt><strong>Cota implementada</strong></dt>
	<dd>A soma de memória que é alocada para todos os apps implementados, em todas as organizações. A soma da cota
 implementada pode exceder a memória total do sistema físico para seu ambiente. Por exemplo,
 se você tiver uma memória total do sistema de 16 GB e alocar 4 GB de memória cada num
 total de cinco organizações diferentes, a cota total excede a memória total do sistema
 que foi alocada para todas as organizações. No entanto, em muitos casos, as organizações podem não
 usar a cota total que é alocada individualmente para cada organização. Além disso,
 todas as organizações podem não usar sua alocação de memória de cota total ao mesmo tempo. </dd>
	<dt><strong>Cota total</strong></dt>
	<dd>A memória total que é alocada em todas as organizações.</dd>
	</dl>

- Uso de memória da organização. Esta seção detalha o uso de memória em um nível de organização. É possível
visualizar o abono da cota total e a cota que é implementada para cada organização. O gráfico fornece informações que
são listadas pelo mais alto uso de memória por organização e a organização que usa a maior quantia de memória, por
padrão, é listada primeiro. É possível classificar por
**Mais alto uso de memória** e **Excesso de alocação de memória**.

	<dl>
	<dt><strong>Mais alto uso de memória</strong></dt>
	<dd>Use esta opção para identificar a organização que usa a maior quantidade de memória. Classifique pelo mais alto uso de
memória para identificar as organizações que estão usando a maior quantia de memória. A lista é classificada pela cota
implementada. </dd>
	<dt><strong>Alocação de memória em excesso</strong></dt>
	<dd>Use esta opção para identificar as organizações que possuem um plano de cota que é maior do que o necessário.
	Classifique
por uso de memória em excesso para identificar as organizações que estão usando a menor quantia de memória para a cota
que foi alocada para a organização. </dd>
	</dl>

### Ajustando planos de cota

Para mudar o plano de cota para uma organização, conclua as etapas a seguir:

<ol>
<li>Clique na barra no gráfico para a organização que deseja editar na seção de uso de memória da Organização ou selecione o nome da organização a partir da seção Lista de organizações.</li>
<li>Na página Gerenciar organização, é possível mudar o plano de cota, mude o nome da organização e inclua ou remova os gerenciadores.<br />
<p><strong>Nota</strong>: se você selecionar um plano de cota que não seja suficiente para o uso atual para a organização, receberá uma mensagem.</p>
</li>
<li>Para salvar qualquer mudança feita na página Gerenciar organização, clique em <strong>SALVAR</strong>.</li>
</ol>

### Gerenciando suas organizações na lista de organizações

Na seção Lista de organizações, é possível visualizar todas as organizações no ambiente do {{site.data.keyword.Bluemix_notm}} e é possível tomar ações para organizações individuais clicando no nome da organização.

- Para excluir a organização, clique no ícone **Excluir** ![Excluir](images/icon_trash.svg) na coluna Ações.
- Para visualizar o plano de cota e uso para uma organização, clique no nome da organização na lista. Na página **Gerenciar organizações** para a organização selecionada, é possível visualizar as informações de uso a seguir:

  - Número de serviços que estão atualmente em uso.
  - Número de rotas que estão atualmente em uso.
  - Gráfico de cota de memória que mostra o quanto da cota está usado e quanto não está atualmente sendo usado.
  - Gráfico de alocação de aplicativos que mostra quais aplicativos estão incluídos na cota de memória usada.
  - Gráfico de uso de aplicativos medido que mostra um relatório trimestral de GB/horas usados por app implementado. É possível selecionar a **Visualização de lista** para ver dados de todos os apps, incluindo a alocação de memória por app e o uso de GB/hora medido para os últimos três meses.

- Para editar o nome da organização e incluir ou remover os gerenciadores, clique no nome da organização na lista e siga os prompts na tela.

## Gerenciando usuários e permissões
{: #oc_useradmin}

É possível incluir usuários individualmente
ou em grupos e visualizar permissões do usuário. Geralmente, os usuários são incluídos em sua instância do {{site.data.keyword.Bluemix_notm}} a partir do registro de usuário de sua empresa por meio do
Lightweight Directory Access Protocol (LDAP). Se você tiver recebido permissão de
**Super usuário**, será possível também configurar e gerenciar
permissões de outros usuários. Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DE USUÁRIO**.

A página Administração de usuário exibe todos os usuários da
instância local ou dedicada. As permissões para cada usuário são exibidas usando ícones na tabela. Estas
podem ser as permissões: Nenhuma, **Super usuário**,
**Acesso básico**, **Catálogo**,
**Relatórios** e **Usuários**.
As permissões **Super usuário** e **Acesso
básico** podem ser configuradas como **Ativado** ou
**Desativado**, enquanto as permissões restantes são ativadas ou
desativadas com tipos de acesso específicos, incluindo **Leitura** ou
**Gravação** para essa permissão, conforme representado por ícones. Consulte
[Permissões](#permissions) para obter descrições de cada tipo e explicação dos ícones.

### Trabalhando com Usuários

Dependendo de seu acesso de **Leitura** ou **Gravação** para as permissões de acesso dos usuários, é possível procurar usuários existentes, remover usuários e
incluir usuários individualmente ou por um grupo. Observe que se você tiver a permissão
de **Super usuário**, terá acesso total para concluir quaisquer
tarefas para gerenciamento de usuários no ambiente. Revise as tarefas de gerenciamento de
usuários a seguir e o nível de acesso necessário para concluir cada tarefa:

* Localizar usuários. Se tiver acesso de **Leitura** ou
**Gravação** e você souber todo ou parte do nome do usuário, poderá
localizar os usuários na tabela usando o campo **Procurar**.

* Incluir um único usuário. Se você tiver a permissão de **Super usuário** ou a permissão de **Usuários** com acesso de **Gravação**, será possível incluir usuários.

  1. Para incluir um único usuário a partir de seu diretório LDAP, clique em **Incluir usuário**.
  2. No campo de **Procura**, digite o endereço de e-mail para o usuário e, em seguida, selecione o usuário a partir da lista preenchida.
  3. Em seguida, a partir do campo **Org**, escolha a organização na qual você deseja incluir o usuário inserindo o nome da organização e selecionando-o a partir da lista preenchida.
  4. Para incluir o usuário na organização selecionada, clique em **Incluir usuário**.

  **Nota**: quando a operação de inclusão é bem-sucedida, o usuário é incluído na tabela para você visualizar e procurar. Quando os usuários são
incluídos, eles não possuem permissões designadas.

* Incluir um grupo de usuário a partir do seu diretório LDAP. Se você tiver a
permissão de **Super usuário** ou a permissão de
**Usuários** com acesso de **Gravação**, será
possível incluir usuários.

  1. Clique em **Incluir grupo de usuários**.
  2. No campo de **Procura**digite um nome do grupo para procurar e selecione o nome do grupo na lista preenchida.
  3. Em seguida, a partir do campo **Org**, escolha a organização na qual você deseja incluir o grupo de usuários inserindo o nome da organização e selecionando-o a partir da lista
preenchida.
  4. Para incluir o grupo de usuários na organização selecionada, clique em **Incluir usuários**.

  **Nota**:
grupos de mais de 50 usuários são incluídos por meio de
uma tarefa em lote de segundo plano. Quando a operação de inclusão
é bem-sucedida, o usuário ou o grupo é incluído na tabela para você visualizar e procurar. Quando os usuários são
incluídos, eles não possuem permissões designadas.

* Inclua um grupo de usuários, importando uma planilha que inclua IDs de usuário, endereços de e-mail do usuário e a organização à qual você planeja incluir o usuário. 
Se você tiver a permissão de **Super usuário** ou a permissão de
**Usuários** com acesso de **Gravação**, será
possível incluir usuários.

**Nota**: insira IDs de usuário que correspondem aos valores usados em seu registro do usuário.

  1. Clique em **Importar usuários**.
  2. Clique em **Fazer download do modelo (.CSV)** para fazer o download de uma planilha com as colunas necessárias que é possível preencher ou é possível criar a sua própria usando
uma planilha que inclui os cabeçalhos da coluna requeridos: **ID do usuário**, **E-mail** e **Organização**.  Duas colunas opcionais também estão
incluídas no modelo: **Nome** e **Sobrenome**.
  3. Preencha os valores de usuário para as colunas necessárias. Se você não estiver usando um diretório LDAP, use os cabeçalhos da coluna necessários e opcionais para os usuários que você estiver
importando.
  4. Salve o arquivo e clique em **Fazer upload de arquivo**.

  **Nota**: as colunas em sua planilha podem estar em qualquer ordem desde que você tenha todas as colunas necessárias. Se a importação foi bem-sucedida, você receberá uma mensagem de
confirmação que indica que todos os usuários foram incluídos. Se a importação foi bem-sucedida para alguns usuários, mas
não para outros, revise a mensagem de erro para tomar ação sobre os usuários que não puderam ser incluídos.

* Remover usuários. Se você tiver a permissão de
**Super usuário** ou a permissão de **Usuários**
com acesso de **Gravação**, será possível remover usuários do ambiente
permanentemente.

    1. Localize o usuário e clique no ícone ![Excluir](images/icon_trash.svg).
    2. Clique em **Remove**.

* A edição de permissões e organizações às quais os usuários pertencem requer que você
tenha permissão de **Super usuário**. Para editar permissões para usuários, localize o usuário e
clique no nome do usuário. A
partir da página **Editar usuário**, é possível ativar ou desativar permissões:

    * Selecione **Ligar** na lista para ativar a permissão
de **Super usuário** ou **Acesso básico**.
    * Selecione **Leitura** a partir da lista para permitir que o usuário tenha acesso de **Leitura** (somente leitura) para essa permissão ou selecione
**Gravação** para permitir acesso de **Gravação** (editar ou incluir e remover) para essa permissão.
    * Selecione **Desligar** para desativar
qualquer uma das permissões.

    **Nota**: configurar a permissão de
**Super usuário** como **Ligado** configura todas
as outras permissões com acesso de **Gravação**.

* Para incluir ou remover um usuário de uma organização específica, deve-se ter
permissão de **Super usuário** ou permissão de
**Usuários** com acesso de **Gravação**.

    1. Para incluir um usuário em uma organização, selecione o nome do usuário a partir da tabela para acessar a página **Editar usuário**. Em seguida, use o campo de procura para
localizar uma organização, selecione a organização a partir da lista e clique em **Salvar**.
    2. Para remover um usuário de uma organização, selecione o nome do usuário a partir da tabela, para acessar a página **Editar usuário**. Em seguida, clique em
![Remover](images/icon_remove.svg) para a organização a partir da qual você deseja remover o usuário e clique em **Salvar**.

### Permissões
{: #permissions}

Os usuários podem ser designados com as permissões a seguir com níveis de acesso específicos que permitem que o usuário conclua tarefas específicas:

*Tabela 7. Permissões*

| **Permissão do usuário** | **Descrição** |       
|-----------------|-------------------|
| Superusuário | Os usuários com permissão de **Super usuário** configurada como **Ligado** podem editar permissões para outros usuários. Se você tiver a permissão ativa,
ela ativa automaticamente o acesso total a todas as outras permissões. Além das tarefas
esboçadas para cada permissão nesta tabela, também pode configurar
inscrições de eventos para ser alertado diretamente sobre manutenção ou incidentes,
planejar manutenção, executar verificações em componentes do console e criar organizações
e espaços para o ambiente. |
| Acesso básico | Os usuários com permissão de **Acesso básico** configurada
como **Ligado** têm permissão para ver a opção da página de
Administração na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Usuários com a permissão ativada podem acessar os quadros de [Informações do sistema](#oc_system) e de [Uso de
recursos](#oc_resource). Sem essa permissão, os usuários não podem ver ou acessar a opção de menu de Administração. |
| Catálogo | Usuários com permissão de **Catálogo** podem ter o acesso designado para **Leitura** ou **Gravação** (modificar) cujos serviços
estão disponíveis na instância local ou dedicada. O acesso de leitura permite que o usuário acesse o quadro de Gerenciamento de catálogo para visualizar serviços disponíveis. O acesso de gravação permite que o
usuário acesse o quadro de [Gerenciamento de catálogo](#oc_catalog) para visualizar serviços, editar a visibilidade de serviços, registrar serviços customizados e controlar a lista de
prioridades do buildpack. |  
| Relatórios | Usuários com permissão de **Relatórios** podem ter o acesso designado para **Leitura** ou **Gravação** (modificar) relatórios de segurança. O
acesso de leitura permite que o usuário acesse o quadro Relatórios e Logs para fazer
download de relatórios. O acesso de gravação permite que o usuário visualize o quadro [Relatórios e
logs](#oc_report), bem como use a CLI para fazer upload de novos relatórios e criar novas categorias para os usuários acessarem. |
| Usuários | Os usuários com permissão de **Usuários** podem ter designado o acesso para **Leitura** (visualizar) a lista de usuários ou **Gravação**
(incluir ou remover) usuários. Essa permissão não permite configurar permissões para outros usuários. O acesso de gravação permite que o usuário inclua novos usuários no ambiente, exclua usuários do ambiente
e inclua usuários existentes em organizações que já existem no ambiente. Além disso, o acesso de **Gravação** permite que o usuário inclua novas organizações, exclua organizações e
edite os usuários dentro das organizações. |


As permissões podem ser ativadas para o usuário com o acesso de **Leitura** ou **Gravação** para essa permissão, conforme representado pelos ícones a seguir:

* O ícone ![Ativado, representado por uma marca de seleção](images/icon_enabled.svg) associada com uma permissão significa que ela está ativada.
* O ícone ![Leitura, representado por um olho](images/icon_read.svg) significa que o usuário tem acesso de **Leitura** (somente leitura) para essa permissão.
* O ícone ![Gravação, representado por um lápis](images/icon_write.svg) significa que o usuário tem acesso de **Gravação** (editar, incluir ou remover) para essa
permissão.


## Gerenciando usuários com a API REST Admin
{: #usingadminapi}

É possível usar a API REST `Admin` para
incluir e remover usuários de sua instância do {{site.data.keyword.Bluemix_notm}}.
Os terminais da API REST `Admin` e respostas JSON são fornecidos numa base experimental para ativar as operações básicas a partir de uma linha de comandos. Os terminais e URLs nos exemplos nessas informações podem mudar ou podem ser descontinuados em breve.

As ferramentas a seguir são pré-requisitos para usar os exemplos abaixo. É possível optar por
            usar outras ferramentas também.
* cURL, para inserir solicitações API REST como comandos. cURL é um utilitário grátis que pode
                    ser usado para enviar solicitações de HTTP para um servidor e receber as respostas
                    do servidor por meio de uma interface de linha de comandos. É
possível fazer o download de cURL a partir do
[site de download de cURL](http://curl.haxx.se/download.html){: new_window}.
* Python, para usar a ferramenta JSON de pretty-print do Python. Essa ferramenta opcional considera o texto JSON como entrada e fornece saída fácil de ler. Você
pode fazer o download do Phython no
[site de downloads de
Python](https://www.python.org/downloads){: new_window}.

### Efetuando login no Console administrativo

Antes que quaisquer solicitações de API `Admin` possam ser executadas, deve-se efetuar login no Console administrativo. Se
você tiver a permissão de **Super usuário** ou a permissão de
**Usuários** com acesso de **Gravação**, será
possível incluir ou remover usuários. Deve-se ter permissão de
**Super usuário** para editar permissões de outros usuários.

Para efetuar login no Console administrativo, é possível usar a
autenticação de acesso básico no terminal `https://<your_host>.ibm.com/login`. O servidor retorna um cookie com a sua sessão. Use esse cookie para todas as operações com o Console administrativo.

**Nota:** A sessão se torna inválida se não usada por algumas horas.

Para efetuar login no Console administrativo, execute o comando a seguir:

`curl --user <user_id>:<password> -c ./cookies.txt --header "Accept: application/json" https://<your_host>.ibm.com/login | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">--user <em>user_id</em>:<em>password</em></dt>
<dd class="pd">Aceita o ID de usuário e a senha e envia um cabeçalho de Autorização básica.</dd>


<dt class="pt dlterm">-c <em>filename</em></dt>
<dd class="pd">Armazena o ID de usuário e a senha especificados como um cookie no arquivo especificado.</dd>


<dt class="pt dlterm">--header</dt>
<dd class="pd">Envia um cabeçalho Aceitar.</dd>

</dl>

O exemplo a seguir mostra a saída a partir deste
                comando:
```
{
    "message": "Logged in",
    "name": {
        "familyName": "*last_name*",
        "givenName": "*first_name*"
    }
}
```
{: screen}

### Listando organizações
{: #listingorg}

Ao incluir um usuário, você deve especificar uma organização. É possível usar a API REST `Admin` para listar todas as organizações. Deve-se
ter a permissão de **Usuários** com o acesso de
**Leitura** para listar organizações. Para listar todas as
organizações, execute o comando a seguir: 

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/organizations | python -m json.tool`
{: codeblock}

<dl class="parml">

<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>

</dl>

Para cada organização, os resultados incluem as informações a seguir
* `"guid"`, GUID da organização
* `"name"`, nome da organização

O exemplo a seguir mostra a saída a partir deste
                comando:
```
{
     "resources": [
         {
             "guid": "05af098d-d476-4fb0-8b87-a84350e72af3",
             "name": "org-1"
         },
         {
             "guid": "5129a5a8-37c2-4ee4-a9b2-bebae3531db5",
             "name": "org-2"
         },

		 		 ....

		 ],
		 "total_results": 284
}
```
{: screen}

### Listando usuários
{: #listingusr}

É possível determinar se um usuário já foi incluído no
ambiente do {{site.data.keyword.Bluemix_notm}} usando
a API REST `Admin` para listar usuários registrados. Deve-se ter
permissão de **Usuários** com o acesso de **Leitura** para
listar usuários registrados. Para listar todos os usuários, execute o comando a seguir:

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>
</dl>

Para cada usuário registrado, os resultados incluem as informações a seguir
* `"first_name"` (nome) e `"last_name"` (sobrenome)
* `"user_id"`, ID de usuário e endereço de e-mail
* `"guid"`, GUID da organização.
* `"permissions"` que são designadas ao usuário para o Console administrativo.

O exemplo a seguir mostra a saída a partir deste
                comando:

```
{
    "next_url": "/codi/v1/users?results_per_page=100&amp;page=2",
    "prev_url": "",
    "resources": [
        {
            "active": true,
            "created_at": "2015-04-08T17:38:51.788Z",
            "created_by": "",
            "first_name": "some first name",
            "guid": "5d5268cf-39c0-48d3-96ae-7afe928e5dd7",
            "last_name": "some last name",
            "permissions": [
                {
                    "display": "ops.admin"
                },
                {
                    "display": "ops.catalog.write"
                },
                {
                    "display": "ops.reports.write"
                },
                {
                    "display": "ops.catalog.read"
                },
                {
                    "display": "ops.users.write"
                },
                {
                    "display": "ops.reports.read"
                },
                {
                    "display": "ops.login"
                },
                {
                    "display": "ops.users.read"
                }
            ],
            "user_id": "someid@us.ibm.com"
        },
		 		 ...


     }
    ],
    "total_pages": 395,
    "total_results": 39421
}

```
{: screen}

### Incluindo um usuário

É possível usar a API REST `Admin` para
incluir usuários na instância do {{site.data.keyword.Bluemix_notm}}. Deve-se ter
permissão de **Usuários** com acesso de
**Gravação** para incluir usuários ou a permissão de **Super
usuário** (ops.admin) para o console administrativo. Além disso, como
Administrador, você pode permitir que os membros da organização que não têm a
permissão de `usuário` ou `super usuário` do console
administrativo geral tenham a capacidade de incluir novos usuários somente na organização
deles. Use o comando de API a seguir para essa capacidade específica para gerenciadores
de organização:

```
PUT console.<subdomain>.bluemix.net/codi/env_config/allow_managers?flag=<TRUE or FALSE>
```
{: screen}

Você pode incluir um usuário ou uma lista de usuários. É possível incluir usuários em uma única organização ou em diversas organizações. Para incluir um usuário, deve-se fornecer as informações a seguir:

* Primeiro nome (nome) e último nome (sobrenome) do usuário. Forneça
`"first_name"` e `"last_name"` em
[Listando usuários](index.html#listingusr).
* Endereço de e-mail e ID de usuário: forneça
`"user_id"` em
[Listando usuários](index.html#listingusr) para o
endereço de e-mail e o ID de usuário.
* `"guid"`. Forneça o GUID da organização em
[Listando organizações](index.html#listingorg).

Forneça as informações em um arquivo JSON.

`curl -b ./cookies.txt https://<your_host>.ibm.com/codi/v1/users | python -m json.tool`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-b <em>filename</em></dt>
<dd class="pd">Passa o ID de usuário e a senha que foram armazenados previamente com a opção <samp class="ph codeph">-c</samp> no arquivo para o servidor HTTP como um cookie.</dd>
</dl>

<ol>
<li>Crie um arquivo JSON que contenha as informações em um formato JSON apropriado.
<p>Por exemplo, crie um arquivo nomeado `user.json` que possua o conteúdo a seguir:</p>
<pre>
{
    "members": [
        {
            "emails": [
                "some_user_id@domain.com"
            ],
            "first_name": "Some_first_name",
            "last_name": "Some_last_name",
            "user_id": "some_user_id@domain.com"
        }
    ],
    "organization_roles": [
        {
            "id": "7a891f9c-e4e7-46c7-8b4e-dffaa7eb3bcd"
        }
    ]
}
</pre>
</li>
<li>Poste o conteúdo do arquivo JSON para o terminal do usuário
executando o seguinte comando:<br/><br/>
<code>
curl -v -b ./cookies.txt -X POST -H "Content-Type: application/json" -d @./user.json https://<your_host>.ibm.com/codi/v1/users
</code>
</li>
</ol>

<dl class="parml">

<dt class="pt dlterm">-v </dt>
<dd class="pd">Especifica a saída detalhada.</dd>


<dt class="pt dlterm">-X POST</dt>
<dd class="pd">Especifica uma solicitação POST, substituindo a solicitação GET padrão.</dd>


<dt class="pt dlterm">-H "Content-Type: application/json"</dt>
<dd class="pd">Especifica o cabeçalho do tipo de conteúdo que, nesse caso, é JSON.</dd>


<dt class="pt dlterm">-d *data*</dt>
<dd class="pd">Especifica os dados, nesse caso, o arquivo `user.json`, a ser enviado na solicitação POST para o servidor HTTP.</dd>

</dl>



O exemplo a seguir mostra a saída a partir deste
                comando:

```
* Conectado ao host local (127.0.0.1) porta 3000 (#0)
 > POST /codi/v1/users HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 > Content-Type: application/json
 > Content-Length: 333
 >
 * upload completamente enviado: 333 de 333 bytes
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < vary: X-HTTP-Method-Override
 < content-type: application/json
 < date: Wed, 22 Apr 2015 19:32:54 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 5612 msec
 ```
{: screen}

### Removendo um usuário

É possível usar a API REST `Admin` para
remover usuários da instância do {{site.data.keyword.Bluemix_notm}}. Deve-se ter
permissão de **Usuários** com acesso de
**Gravação** para remover usuários.


Para remover um usuário, deve-se fornecer o ID de usuário do usuário. Execute o comando a seguir:

`curl -v -b ./cookies.txt -X DELETE https://<your_host>.ibm.com/codi/v1/users?user_id=<some_user_id@domain.com>`
{: codeblock}

<dl class="parml">
<dt class="pt dlterm">-X DELETE</dt>
<dd class="pd">Especifica uma solicitação DELETE.</dd>
</dl>

O exemplo a seguir mostra a saída a partir deste
                comando:

```
 * connect to ::1 port 3000 failed: Connection refused
 *   Trying 127.0.0.1...
 * Conectado ao host local (127.0.0.1) porta 3000 (#0)
 > DELETE /codi/v1/users?user_id=exampleuser@domain.com HTTP/1.1
 > User-Agent: curl/7.37.1
 > Host: localhost:3000
 > Accept: */*
 > Cookie: opsConsole.sid=s%3AHLcwKGumyEb3IxREmikDOG3ATKD5xYMe.jfjWAa1tJC0rGghpeV8RPHqE2JaFVL4ZFIJbQpSC%2FAI
 >
 < HTTP/1.1 201 Created
 < x-powered-by: Express
 < content-type: application/json
 < date: Wed, 22 Apr 2015 21:01:09 GMT
 < connection: close
 < transfer-encoding: chunked
 < X-Time_Check: Proxy Time: 1922 msec
 <
 ```
{: screen}

## API de serviço customizado
{: #servicebrokerapi}

Há três APIs que podem ser usadas para registrar ou criar um novo serviço, atualizar um serviço e excluir um serviço.

Todas as APIs são relativas a <code>https://console.&lt;subdomain&gt;.bluemix.net/</code>.

<dl>
<dt><strong>&lt;subdomain&gt;</strong></dt>
<dd>Este valor é o nome da sua instância local ou dedicada. O nome de
subdomínio de sua instância do {{site.data.keyword.Bluemix}}
foi designado durante o onboarding.</dd>
</dl>

## Registrando um novo serviço

Use a API a seguir e os exemplos de código para registrar um novo serviço.

### Rotear
{: #registerroute}

```
POST /codi/v1/serviceBrokers
```
{: screen}

### Pedido
{: #registerrequest}

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. |
| auth_username | Nome do usuário usado para conectar ao broker de serviço. |
| auth_password | Senha usada para conectar ao broker de serviço. |
| broker_url | URL usada para conectar ao broker de serviço. |
| owningOrganization | Organização inicial para incluir o serviço na lista de desbloqueio. |

*Tabela 8. Campos*

#### Corpo
{: #registerbody}

```
{
  "name" : "Service broker's name",
  "auth_username" : "username",
  "auth_password" : "password",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Cabeçalhos
{: #registerheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Resposta
{: #registerresponse}

#### Barra de Status
{: #registerstatus}

```
201 Criado
```
{: screen}

#### Corpo
{: #registerbody2}

```
{
  "entity": {
    "name": "Service broker's name",
    "broker_url": "https://provision-broker.comp.bluemix.net/bmx/provisioning/brokers/2063580064-8f23230c-7f36-4ce5-a298-2ab4108f1120",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "49f3adcc-ecc2-46fa-83c1-03322f04b3b1",
    "created_at": "2015-12-07T19:51:50Z",
    "updated_at": null,
    "url": "/v2/service_brokers/49f3adcc-ecc2-46fa-83c1-03322f04b3b1"
  }
}
```
{: screen}

## Atualizando um serviço

Use a API a seguir e os exemplos de código para atualizar um serviço.

### Rotear
{: #updateroute}

`PUT /codi/v1/serviceBrokers`
{: screen}

### Pedido
{: #updaterequest}

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. O nome com que esse serviço foi criado não pode ser mudado. |
| auth_username | Nome do usuário usado para conectar ao broker de serviço. |
| auth_password | Senha usada para conectar ao broker de serviço. |
| broker_url | URL usada para conectar ao broker de serviço. |
| owningOrganization | Organização inicial para incluir o serviço na lista de desbloqueio. |

*Tabela 9. Campos*

#### Corpo
{: #updatebody}

```
{
  "name" : "Service Broker's name",
  "auth_username" : "username",
  "auth_password" : "newPassword",
  "broker_url" : "https://broker.comp.com",
  "owningOrganization" : "ORG"
}
```
{: screen}

#### Cabeçalhos
{: #updateheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Resposta
{: #updateresponse}

#### Barra de Status
{: #updatestatus}

```
201 Criado
```
{: screen}

#### Corpo
{: #updatebody2}

```
{
  "entity": {
    "name": "Service Broker's name",
    "broker_url": "https://provision-broker.dys0.bluemix.net/bmx/provisioning/brokers/2063580064-d11bdd84-7556-469f-858d-2098b531f7f2",
    "auth_username": "username",
    "space_guid": null
  },
  "warnings": [],
  "metadata": {
    "guid": "2cbdb812-d37f-443b-894a-a96de31e5c38",
    "created_at": "2015-12-07T20:11:08Z",
    "updated_at": "2015-12-07T20:11:19Z",
    "url": "/v2/service_brokers/2cbdb812-d37f-443b-894a-a96de31e5c38"
  }
}
```
{: screen}

## Excluindo um serviço

Use a API a seguir e os exemplos de código para excluir um serviço.

| **Nome** | **Descrição** |
|-----------------|-------------------|
| Nome | Nome do broker de serviço. O nome com que esse serviço foi criado não pode ser mudado. |

*Tabela 10. Parâmetro*

### Rotear

```
DELETE /codi/v1/serviceBrokers?name=name of service broker
```
{: screen}

### Pedido
{: #deleterequest}

#### Cabeçalhos
{: #deleteheaders}

```
Authorization: bearer eyJ0eXAiOiJKV1QiLCJhbG ... ciOiJIUzI1
Host: console.comp.bluemix.net
Content-Type: application/json
```
{: screen}

### Resposta
{: #deleteresponse}

#### Barra de Status
{: #deletestatus}

```
204 Sem conteúdo
```
{: screen}

## Gerenciando usuários com a CLI cf
{: #usingadmincli}

É possível gerenciar usuários para o ambiente do
{{site.data.keyword.Bluemix_notm}} usando a
interface da linha de comandos do Cloud Foundry com o plug-in
CLI admin do {{site.data.keyword.Bluemix_notm}}. Por
exemplo, é possível incluir usuários a partir de um registro LDAP.

Antes de iniciar, instale a interface de linha de comandos do cf. O plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}
requer o cf versão 6.11.2 ou posterior. [Download
da interface de linha de comandos do Cloud Foundry](https://github.com/cloudfoundry/cli/releases){: new_window}

**Restrição:** A interface de linha de
comandos do Cloud Foundry não é suportada por
Cygwin. Use a interface de linha de comandos do Cloud Foundry
em uma janela de linha de comandos diferente da janela de linha de comandos do Cygwin.

### Incluindo o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}

Após a interface de linha de comandos do cf ser instalada, é possível
incluir o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}.

**Nota**: se você tiver instalado
anteriormente o plug-in Administrador do
{{site.data.keyword.Bluemix_notm}}, poderá ser necessário desinstalar o plug-in, excluir o repositório e reinstalar para obter as atualizações mais recentes.

Conclua as etapas a seguir para incluir o repositório e instalar
o plug-in:

<ol>
<li>Para incluir o repositório do plug-in Administrador do {{site.data.keyword.Bluemix_notm}}, execute o comando a seguir:<br/><br/> <code> cf add-plugin-repo BluemixAdmin https://console.&lt;subdomain&gt;.bluemix.net/cli </code><br/><br/>
<dl class="parml">
<dt class="pt dlterm">&lt;subdomain&gt;</dt>
<dd class="pd">Subdomínio da URL da sua instância do
{{site.data.keyword.Bluemix_notm}}.</dd>
</dl>
</li>
<li>Para instalar o plug-in CLI admin do
{{site.data.keyword.Bluemix_notm}}, execute o seguinte
comando:<br/><br/> <code>
cf install-plugin bluemix-admin-cli -r BluemixAdmin
</code>
</li>
</ol>

Para ver uma lista de comandos, execute o comando
a seguir:

`cf plugins`
{: codeblock}

Para obter ajuda adicional para um comando, use a opção `-help`.

Para obter mais informações sobre como trabalhar com o plug-in da CLI Admin do {{site.data.keyword.Bluemix_notm}}, veja  [Admin do {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html).
