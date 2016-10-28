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
Última atualização: 20 de setembro de 2016
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

Também é possível sempre saber o status de seu ambiente, verificando a página Status. À medida que ocorrem, incidentes e eventos de atualização de manutenção disruptiva planejada são relatados na página
Status. O {{site.data.keyword.Bluemix_notm}}
também envia notificações para a área Notificações na página de Administração para eventos como atualizações planejadas ou de manutenção pendentes.

### Notificações

É possível visualizar notificações para o seu ambiente local ou dedicado, a fim de monitorar o status de seu ambiente. Revise a tabela a seguir, para obter informações sobre os tipos diferentes de
notificações e onde cada tipo de notificação é postado.

*Tabela 2. Tipos de eventos e métodos de notificações*

| **Tipo de evento** | **Método de Notificação** |       
|-----------------|-------------------|
| Atualizações de Manutenção | Você é alertado sobre atualizações de manutenção futuras na área Notificações na página de Administração. Acesse a página **Administração** e, em seguida, selecione o ícone **Notificações** ![Notificações](images/icon_announcement.svg). Para
ver uma lista completa e o histórico de suas notificações pendentes e completas, clique em **ADMINISTRAÇÃO &gt; INFORMAÇÕES DO SISTEMA** &gt; *Número*
**pendente**.|
|  | Você também é alertado sobre eventos de atualização de manutenção disruptiva planejada na página Status. Clique no ícone
**{{site.data.keyword.avatar}}**
![Avatar](../support/images/account_support.svg) e selecione
**Status**.|
|  | É possível ampliar o recurso de notificação configurando uma assinatura que envia um e-mail a destinatários de sua opção. Ou é possível configurar uma assinatura que use
webhooks para integrar as notificações a partir da página Administração com um serviço da web de sua opção.|
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
**Status**.  |

### Configurando assinaturas de eventos

É possível estender a funcionalidade das notificações que são enviadas para a página de Administração e a página Status usando inscrições de evento. Use inscrições de evento para configurar um e-mail
customizado ou use webhooks para integrar com uma ferramenta de sua opção. 
 * Se você selecionar a opção de e-mail, as suas notificações serão enviadas aos endereços de e-mail que especificar. É possível selecionar notificações de incidentes ou atualizações de manutenção. Uma
notificação por e-mail inicial será enviada. Em seguida, se o incidente ou a atualização de manutenção tiver uma mudança feita nela, outra notificação com a mudança será enviada sempre que uma mudança
for feita.  
 * Se você selecionar a opção webhooks, as suas notificações serão roteadas diretamente para um destino de sua opção, como um número de telefone (por mensagem SMS). É possível customizar o tipo de notificação, especificamente atualizações de manutenção ou alertas de incidente crítico e as informações incluídas no corpo de cada notificação.

**Nota**: somente usuários com a permissão de super usuário (`ops.admin`) podem configurar inscrições de evento.

É possível acessar a página de **Inscrições de evento**, de uma das maneiras a seguir:

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
| Ativar | Selecione a opção para ativar as notificações por e-mail. Limpe a seleção para desativar a notificação por e-mail. As assinaturas são ativadas por padrão. |
| Tipo | Selecione **E-mail**. |
| Evento | Selecione para ser inscrito para notificações para um evento de **Manutenção** ou **Incidente**. |
| Combinar notificações | Selecione a opção para combinar as notificações de incidentes
para todas as regiões em uma única notificação. Essa opção está disponível somente para incidentes. |
| Assunto | Insira a linha de assunto para o e-mail. Este campo é requerido.  |
| Corpo | Insira o texto do corpo da mensagem a ser enviada no e-mail. É possível usar os valores de carga útil da IBM para preencher a notificação por e-mail com informações pertinentes. Consulte a tabela
de [Valores da seção de carga útil](index.html#payload) para identificar quais valores é possível utilizar. Use marcas HTML básicas para estruturar o seu e-mail. Este campo é requerido. |
| Para | Insira o endereço ou endereços de e-mail usando uma lista separada por vírgula para os destinatários da notificação por e-mail. Expanda as opções "cc" ou "bcc" para copiar outros no e-mail. Este campo é requerido. |
| Descrição | Inclua uma descrição exclusiva para a assinatura que você está criando. |


*Tabela 4. Campos de formulário de inscrição de evento para uma assinatura de webhook*

| **Campo** | **Descrição** |
|-----------------|-------------------|
| Ativar | Selecione a opção para ativar a notificação. Limpe a seleção para desativar a
notificação. As assinaturas são ativadas por padrão. |
| Tipo | Selecione **Webhook** |
| Método | Selecione **GET** ou **POST**. |
| Evento | Selecione para ser inscrito para notificações para um evento de **Manutenção** ou **Incidente**. |
| Combinar notificações | Selecione a opção para combinar as notificações de incidentes
para todas as regiões em uma única notificação. Essa opção está disponível somente para incidentes. |
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
| {{content.title}} | título Message |  Atualização de manutenção e incidente |
| {{content.message}} | Descrição da mensagem |   Atualização de manutenção e incidente |
| {{region}} | Região afetada | Atualização de manutenção e incidente |
| {{content.severity}} | Classificação de gravidade | Incidente |
| {{content.category}} | Serviços afetados | Incidente |
| {{content.subCategoryName}} | Componentes afetados | Incidente |
| {{status}} | Status da atualização | Atualização de manutenção |
| {{content.scheduleWindow.start}} | A data de início planejada para a atualização | Atualização de manutenção |
| {{content.disruption}} | Componentes afetados | Atualização de manutenção |
| {{type}} | Atualização ou incidente | Atualização de manutenção e incidente |
| {{content.scheduleWindow.end}} | O horário de encerramento planejado para a atualização | Atualização de Manutenção |

Quando a sua inscrição de evento for salva, você receberá notificações por meio do método que você configurar. Notificações ainda são postadas nos locais a seguir:  
 * Na página Status para incidentes 
 * Na página Status para os eventos de atualização de manutenção disruptiva planejada
 * Na área de Notificações da página de Administração para atualizações de manutenção

É possível selecionar qualquer inscrição de evento salva, visualizar a atividade recente ou editar conforme necessário. Clique para expandir qualquer entrada de atividade recente para visualizar os
detalhes de histórico.

## Atualizações de Manutenção
{: #oc_schedulemaintenance}

É possível visualizar atualizações de manutenção planejadas e pendentes, se você tiver a permissão de superusuário (`ops.admin`), clicando em **ADMINISTRAÇÃO &gt; INFORMAÇÕES
DO SISTEMA &gt; *Número* pendente** para acessar a página de **Atualizações do sistema**. Todos os usuários de seu ambiente podem visualizar os eventos de atualização de
manutenção disruptiva planejada clicando no ícone **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) e, em seguida, selecionando
**Status**.

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
- Uso de cota de memória da organização, memória de app alocada com base na cota de memória total usada e uma visualização de uso de GB/hora por app para uma organização específica. Também é possível
visualizar o uso de cota para todas as organizações na página de Administração da organização na seção **Monitoramento de cota**. Consulte [Administração da organização](../admin/index.html#orgusage).


### Uso do Recurso
{: #resourceusage}

Para visualizar informações de uso de recurso, clique em **ADMINISTRAÇÃO &gt; Uso de recurso**.

Na seção **Uso de recurso**, é possível visualizar as informações a seguir:

- Informações de uso de recurso, como a quantia de memória e de espaço em disco que pode ser reservado e quanto está fisicamente disponível e a quantia de memória e de espaço em disco que está realmente
reservado e quanto é usado fisicamente. Também é possível ver informações sobre o uso de CPU médio em todos os Droplet Execution Agents (DEAs). Para ver o uso de sua memória, disco ou CPU pelo DEA, clique em
**Detalhamento**.
É possível ver um resumo das quantias **Reservadas** e **Físicas** para a sua memória e disco.
	<dl>
	<dt><strong>Física</strong></dt>
	<dd>A quantia de memória ou espaço em disco que foi comprada para o seu ambiente. </dd>
	<dt><strong>Reservada</strong></dt>
	<dd>A quantia total de memória ou espaço em disco que está disponível para ser reservado por todos os aplicativos implementados e em execução em seu ambiente. Como os aplicativos raramente usam toda a
memória que está reservada por eles, o valor físico geralmente é inferior ao valor reservado.</dd>
	</dl>

	Além da representação gráfica, é possível ver a porcentagem de memória e espaço em disco que o seu ambiente está usando. Também é possível ver ambas as quantias, reservada e física, em GB, do uso real
comparado com a quantia que está disponível.
Para ver mais informações detalhadas sobre o seu uso de memória física e reservada, clique em **Histórico.** É possível especificar o prazo para visualizar como semanal ou mensal. A
visualização **Uso de memória histórico** mostra um gráfico de uso de memória durante o tempo que você escolher.  

	<dl>
	<dt><strong>Limite reservado</strong></dt>
	<dd>Mostrado como uma linha pontilhada horizontal, o Limite reservado é a quantia total de memória que pode ser coletivamente reservada por todos os aplicativos em execução em seu ambiente.</dd>
	<dt><strong>Reservada</strong></dt>
	<dd>A Área reservada mostra a memória que está atualmente reservada coletivamente por todos os aplicativos em execução em seu ambiente.
	<p>Para ver quais organizações reservaram mais memória em um determinado momento, passe o mouse sobre o ponto ao longo da Área reservada que está associado a esse momento. Em seguida, é possível clicar em uma
organização no gráfico de pizza que é exibido para ver mais informações sobre essa organização.</p></dd>
	<dt><strong>Limite físico</strong></dt>
	<dd>Exibido como uma linha pontilhada horizontal, o Limite físico mostra a quantia de memória física que foi comprada para o seu ambiente.</dd>
	<dt><strong>Física</strong></dt>
	<dd>A Área física mostra a quantia de memória que realmente está sendo usada.</dd>
	</dl>
- Informações de uso de rede para entrada de largura da banda e saída da largura da banda, nas últimas 6 horas ou no último dia. Os dados exibidos são baseados na soma do tráfego de entrada e de saída para as redes públicas e privadas.
- Tempo médio de resposta para o {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, 1 hora e 1 dia.
- Transações médias por segundo para {{site.data.keyword.Bluemix_notm}} nos últimos 10 minutos, hora e dia.

### Uso de conta
{: #accountusage}

É possível visualizar o uso mensal de sua conta para seu ambiente dedicado ou local. É possível usar esses dados para identificar quanto cobrar de organizações específicas com base no uso das mesmas. Todos
os usuários do console do administrador que são designados com a permissão de **Usuários** com acesso de **Leitura** podem visualizar os dados de uso de conta. Além
disso, os gerentes de faturamento da organização podem visualizar os dados de uso de conta para as suas organizações, mesmo se o gerenciador de faturamento não tiver a permissão **Usuários**
do console do administrador designada. Como um administrador do console do administrador (permissão de superusuário), é possível designar a função de gerenciador de faturamento para as organizações clicando
no ícone **{{site.data.keyword.avatar}}** ![Avatar](../support/images/account_support.svg) &gt; **Gerenciar organizações**.

Para visualizar dados de uso de conta, conclua estas etapas:

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

A tabela a seguir mostra a lista de relatórios de segurança gerados para o {{site.data.keyword.Bluemix_notm}} Local e o {{site.data.keyword.Bluemix_notm}} Dedicated. A maioria dos
relatórios é gerada em uma base diária. No entanto, a criptografia e os relatórios de eventos de gerenciamento de chave são gerados mensalmente. Todos os relatórios são retidos por 90 dias no console de
administração para a sua recuperação. Após esses 90 dias, os relatórios estarão disponíveis por solicitação a partir do {{site.data.keyword.Bluemix_notm}} por 9 meses. No total, os
relatórios estarão disponíveis para recuperação por até 1 ano.

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

É possível monitorar o status para a sua instância do {{site.data.keyword.Bluemix_notm}}, usando a página Status do {{site.data.keyword.Bluemix_notm}}. Clique no ícone
**{{site.data.keyword.avatar}}**
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

Se você tiver um serviço que deseja exibir em seu catálogo do {{site.data.keyword.Bluemix_notm}}, deve-se implementar e registrar um [broker de serviço](http://docs.cloudfoundry.org/services/api.html){: new_window}. Após registrar seu broker, será possível escolher quais organizações podem acessar o serviço em sua instância local ou dedicada.

Os métodos para trabalhar com o seu broker de serviço variam, dependendo de quantos serviços ele gerencia ou se ele já foi registrado com o {{site.data.keyword.Bluemix_notm}}.

- Se o seu broker de serviço gerenciar um serviço, será possível usar a interface com o usuário para registrá-lo após ter implementado a [API do broker de serviço](http://docs.cloudfoundry.org/services/api.html){: new_window}. Consulte [Registrando um broker de serviço que gerencia um serviço](index.html#registerbrokerui).
- Se o seu broker de serviço gerenciar múltiplos serviços, use a CLI cf com o plug-in da CLI do administrador do [{{site.data.keyword.Bluemix_notm}}
](../cli/plugins/bluemix_admin/index.html) (subcomando ba) ou use a [API de serviço customizado](index.html#servicebrokerapi).
- Se seu broker de serviço já estiver registrado e você desejar atualizar ou excluir o mesmo, use a CLI cf com o [plug-in de administrador do {{site.data.keyword.Bluemix_notm}}](../cli/plugins/bluemix_admin/index.html) (subcomando `ba`) ou use a [API de serviço customizada](index.html#servicebrokerapi).

#### Registrando um broker de serviço que gerencia um serviço
{: #registerbrokerui}

Revise as informações a seguir e conclua as etapas para registrar o seu broker de serviço:

**Antes de iniciar**: <a href="http://docs.cloudfoundry.org/services/api.html" target="_blank">Implemente a API do broker de serviço do Cloud Foundry</a> para ativar a comunicação
entre o seu serviço e o {{site.data.keyword.Bluemix_notm}}. A API do broker de serviço é um conjunto de terminais REST que são consumidos pelo {{site.data.keyword.Bluemix_notm}}.

Quando você estiver implementando o broker de serviço, na resposta JSON de <code>GET /v2/catalog</code>, deve-se fornecer as definições para seu serviço e planos de serviço, incluindo as informações de serviço que deseja exibir. Por exemplo, revise o JSON de amostra a seguir da resposta do Catálogo (GET):

```
{
"services": [
        {
      "bindable":true,
      "description":"Cool Service is an analytics and data warehousing solution.",
      "id":"cool-service-id",
      "name":"coolservice",
      "metadata":{
         "displayName":"Cool Service",
         "serviceMonitorApi":"https://myservicesstatus.mybluemix.net/healthcheck/",
         "providerDisplayName":"Empresa Cool",
         "longDescription":"Cool Service é uma solução de data warehousing e análise de dados. É possível mover rapidamente seus dados para um banco de dados colunar contido na memória de próxima geração e começar a executar consultas analíticas complexas.",
                "bullets": [
                    {
               "title": "Rápido e simples",
                        "description": "O Cool Service usa terminologia colunar dinâmica contida na memória e inovações, como processamento de vetor paralelo e compactação acionável para varrer e retornar rapidamente os dados relevantes."
            },
            {
               "title": "Conectividade",
                        "description": "O Cool Service é construído para permitir que você se conecte facilmente a todos os seus serviços e aplicativos. You can start analyzing your data immediately with familiar tools."
            }
         ],
                "featuredImageUrl": "http://path/to/icon_64x64.png",
                "imageUrl": "http://path/to/icon_50x50.png",
                "mediumImageUrl": "http://path/to/icon_32x32.png",
                "smallImageUrl": "http://path/to/icon_24x24.png",
                "documentationUrl": "http://path/to/documentation.html",
                "instructionsUrl": "http://path/to/servicesample.md",
                "termsUrl": "http://path/to/terms_of_agreement.pdf",
                "media": [{
               "type": "youtube",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/youtube/video",
			"caption": "Usando o Cool Service em 60 segundos"
            },
            {
               "type": "image",
			"thumbnailUrl": "http://path/to/thumbnail.png",
			"url": "http://path/to/image_file.png",
			"caption": "O Cool Service conecta aplicativos"
            },
            {
               "type": "video",
			"thumbnailUrl": "http://path/to/thumb.png",
			"caption": "O Cool Service trabalha com tabelas",
			"source": [{
                     "type": "video/mp4",
				"url": "http://path/to/video_file.mp4"
                  },
                  {
                     "type":"video/ogg",
                     "url":"http://path/to/video_file.ogg"
                  }
               ]
            }
         ]
      },
            "plans": [
                {
            "name": "smallplan",
                    "description": "Esquema e espaço de tabela dedicados por instância de serviço em um servidor compartilhado. 1 GB e 10 GB de armazenamento do banco de dados compactado pode conter até 5 GB e 50 GB de dados descompactados, respectivamente, com base nas proporções de compactação típica.",
                    "free": false,
                    "id": "cool-service-plan-id",
                    "metadata": {
               "bullets": [
                  "1 GB no mín. por instância. 10 GB no máximo por instância."
               ],
                        "costs": [
                            {
                     "unitId": "INSTANCES_PER_MONTH",
                                "unit": "MONTHLY",
                                "partNumber": "D15UTLL"
                            }
               ],
                        "displayName": "Pequeno"
                    }
         }
      ]
   }
]
}
```
{: codeblock}

As tabelas a seguir podem ajudá-lo a preencher o arquivo de JSON.

*Tabela. Campos de JSON*

| **Campos de JSON** | **Descrição** |
|-----------------|-----------------|
|ligáveis   | Um valor booleano que indica se as instâncias de serviço podem ser ligadas a aplicativos.  |
|Descrição | A descrição do serviço que é exibida quando você usa o comando cf marketplace ou passa o mouse sobre o ícone de serviço no catálogo da interface com o usuário do
{{site.data.keyword.Bluemix_notm}}. É possível incluir uma única sentença ou frase para a descrição. |
|Nome | O nome do serviço que é exibido na interface de linha de comandos cf. Esse nome deve ser exclusivo no {{site.data.keyword.Bluemix_notm}} e deve usar letras minúsculas e não deve conter espaços. Não
é possível mudar o nome do serviço após registrar o serviço com o {{site.data.keyword.Bluemix_notm}}. |
|ID  | O ID do serviço. Esse ID deve ser exclusivo no {{site.data.keyword.Bluemix_notm}} e deve ser um GUID (Identificador Exclusivo Global). Não é possível mudar o ID do serviço depois de registrar o
serviço com o {{site.data.keyword.Bluemix_notm}}. |
|meta-dados | Os metadados de plano de serviço que são exibidos no catálogo do {{site.data.keyword.Bluemix_notm}} e na folha de precificação. O campo de metadados é um campo opcional. É possível
especificar campos adicionais para os metadados. Consulte a tabela a seguir para [Campos de metadados](index.html#metadatafields) para obter mais informações. |
|planejamentos | Uma matriz de definições de plano de serviço. Consulte a tabela a seguir para [Campos de plano](index.html#planfields) para obter mais informações. |

*Tabela. Campos de metadados*
{: #metadatafields}

| **Valores de metadados** | **Descrição** |
|---------------------|-----------------|
|nome de exibição          | O nome do plano que é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Esse nome é exibido na página de detalhes do serviço no catálogo e na folha de precificação. Altere
para letras maiúsculas somente a primeira letra do nome do plano. Não use "Padrão" como o nome do plano padrão; use "Padrão" como alternativa. |
|providerDisplayName | O nome do provedor de serviços |
|longDescription | A descrição detalhada para o serviço. Considere usar pelo menos duas sentenças para uma descrição longa. |
|planejamentos                | Uma matriz de definições de plano de serviço. Cada entrada de matriz do campo de planos consiste nos campos a seguir: nome, descrição, grátis, ID e metadados. Consulte a tabela
a seguir para [Campos de plano](index.html#planfields) para obter mais informações. |
|projéteis | Uma matriz de sequências que são exibidas para um serviço. É possível usar marcadores para fornecer informações além da descrição longa. O campo de marcadores deve conter, pelo menos, dois elementos de marcador. Cada
marcador inclui o campo de título e descrição. |
|imageUrl | A URL de uma imagem de PNG grande (50 x 50 pixels). |
|smallImageUrl | A URL de uma imagem de PNG pequena (24 x 24 pixels). |
|mediumImageUrl | A URL de uma imagem de PNG média (32 x 32 pixels). |
|featuredImageUrl | A URL de uma imagem apresentada (64 x 64 pixels). |
|documentationUrl | A URL de documentação sobre o serviço. |
|termsUrl | A URL para arquivos PDF que contêm termos de acordo. |
|mídia (opcional) | Uma matriz de elementos para exibir os vídeos e as capturas de tela que introduzem o serviço na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Um elemento de mídia pode conter os campos a seguir: type (imagem, youtube, vídeo), thumbnailUrl (A URL da imagem de visualização para o elemento de mídia.), url (A URL da captura de tela ou o vídeo do YouTube.),
source (As origens de vídeos que não estão hospedadas no YouTube. O "tipo" da origem do vídeo deve ser suportado por HTML5. Inclua "tipo" e "url" para o vídeo.) e legenda (A legenda para o elemento de mídia. As
legendas ajudam na acessibilidade para pessoas com deficiências para entenderem os seus elementos de mídia.). |
|serviceKeysSupported | Um valor booleano que indica se a API de chaves de serviço é suportada. A API de chaves de serviço é usada para permitir que um serviço seja usado fora do {{site.data.keyword.Bluemix_notm}}. O valor padrão é false. |
|plan_updateable | Um valor booleano que indica se o serviço suporta mudanças de plano. O valor padrão é false. |
|embeddableDashboard (opcional) | Um campo que indica como o painel de serviço é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Se você não especificar esse campo, o painel será integrado, mas estará restrito a uma largura mínima de 960px e o painel terá preenchimento horizontal adicional ao redor do iframe. É
possível usar verdadeiro, falso, drill down ou ativação. É possível usar os campos a seguir para este valor: verdadeiro, falso, drill down e ativação.  |
|notCreatable (opcional) | Um valor booleano que indica se instâncias para o serviço podem ser criadas a partir da interface com o usuário do {{site.data.keyword.Bluemix_notm}} e a partir da interface da linha de comandos. Um
valor verdadeiro significa que as instâncias de serviço não podem ser criadas a partir da interface com o usuário do {{site.data.keyword.Bluemix_notm}} ou a partir da interface da linha de comandos cf. O valor padrão é false. |
|notCreatableMessage (opcional) | Uma mensagem que será exibida na interface com o usuário do {{site.data.keyword.Bluemix_notm}} se as instâncias de serviço não puderem ser criadas. Se você não
especificar esse campo, a mensagem padrão a seguir será exibida: A ser notificado quando estiver disponível, confirme o seu endereço de e-mail ou insira um endereço de e-mail diferente. |
|notCreatableRobotMessage (opcional) | Uma mensagem que é exibida na bolha de fala da página de detalhes do serviço na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. A mensagem é usada para indicar se um serviço pode ter um problema ou outro motivo que esteja causando sua indisponibilidade. É possível especificar uma mensagem para explicar o motivo. 
Se você não especificar esse campo, a mensagem padrão a seguir será exibida: Esse serviço está indisponível atualmente. |
|apiReferenceUrl (opcional) | A URL do iframe na área Referência da API na página de detalhes do serviço em Catálogo. Se não usado para a página de detalhes do serviço no Catálogo, será possível inserir o valor
numérico designado para o seu Doc da API REST para seu serviço ao registrá-lo no microsserviço do Doc da API REST do {{site.data.keyword.Bluemix_notm}}. Isso exibirá o seu Doc da API REST no painel de
serviço. |
|sdkDownloadUrl (opcional) | A URL da página da web que será aberta quando você clicar no botão Download SDK. O botão Download SDK está no ladrilho de serviço da página de visão geral do aplicativo no	Painel. A página da web é aberta em uma nova guia do navegador. |
|serviceMonitorApi    | A URL para uma API que retorna os dados de JSON, conforme mostrado no exemplo a seguir, que relata o funcionamento do serviço. Deve-se ter serviceMonitorApi ou
serviceMonitorApp em seus metadados de serviço. Consulte a amostra de código a seguir para obter um exemplo. |
|serviceMonitorApp    | A URL para um aplicativo que pode ser implementado no {{site.data.keyword.Bluemix_notm}} e ligado a um serviço para fornecer a saída específica de status de serviço. O
aplicativo deve retornar o mesmo formato de dados de JSON que a serviceMonitorApi. Deve-se ter serviceMonitorApi ou serviceMonitorApp em seus metadados de serviço. Consulte a amostra de código a seguir para
obter um exemplo. |

```
{
    "service": "servicename",
    "version": 1,
    "health": [
        {
            "plan": "starter",
            "status": 0,
            "serviceinput": "count(*) from healthcheck",
            "serviceoutput": "10…or error 1234 database not running",
            "responsetime": 4
        },
        {
            "plan": "enterprise",
            "status": 1,
            "serviceinput": "count(*)fromhealthcheck",
            "serviceoutput": "10…orerror1234databasenotrunning",
            "responsetime": 4
        }
    ]
}
```
{: pre}

O exemplo a seguir mostra como a resposta de JSON de GET /v2/catalog é mapeada para a página de detalhes do serviço no catálogo do {{site.data.keyword.Bluemix_notm}}:

![Detalhes do serviço no catálogo.](images/metadata.png "Visualização de detalhes do serviço do catálogo do Bluemix")

*Tabela. Campos de plano*
{: #planfields}

| **Valores de plano** | **Descrição** |
|---------------------|-----------------|
|Nome       | O nome do plano de serviço que é usado na interface de linha de comandos cf. Por exemplo, o nome do plano é exibido na saída do comando cf marketplace. O nome do plano deve estar em letras minúsculas e não deve conter espaços e deve ser exclusivo dentro do serviço.  |
|Descrição       | A descrição do plano de serviço. A descrição é exibida após você selecionar um plano na página de detalhes do serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. |
|grátis      | Um valor booleano que indica se o plano de serviço é grátis. O valor padrão é verdadeiro. |
|ID       | O ID do plano de serviço. O ID deve ser exclusivo dentro de {: new_window}e deve ser um GUID.  |
|metadados (opcional)    | Os metadados de plano de serviço que são exibidos no catálogo do {{site.data.keyword.Bluemix_notm}} e na folha de precificação. O campo de metadados é um campo opcional. É
possível especificar os campos a seguir no campo de metadados: displayName, tipo (assinatura, reservável, planDetails), custo, custos (unitId, unidade, partNumber) e paidOnly. Consulte a tabela
a seguir para [Campos de metadados de plano](index.html#planmetadata) para obter mais informações. |

*Tabela. Campos de metadados de plano*
{: #planmetadata}

| **Valores de metadados de plano** | **Descrição** |
|------------------------|-----------------|
|nome de exibição             | O nome do plano que é exibido na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Esse nome é exibido na página de detalhes do serviço no catálogo e na folha de precificação.   |
|type                    | O tipo do plano. É possível usar os valores a seguir para esse campo: assinatura (Um plano de assinatura. O valor-padrão é falso.), reservável (Um plano reservável. Esse valor é
usado quando o plano é um plano de assinatura, ou seja, o valor de plan.metadata.subscription é verdadeiro. O valor-padrão é falso.), planDetails (Uma quantidade e descrição detalhadas dos recursos que podem
ser usados com o plano. Esse valor é usado quando o plano é reservável, ou seja, o valor de plan.metadata.reserveable é verdadeiro.) |
|projéteis                 | Uma descrição dos recursos que podem ser usados com o plano. A descrição é exibida na coluna **Recursos** na página de detalhes do serviço do catálogo e na folha de precificação. |
|custos                   | As informações de custo sobre o serviço que é exibido na coluna Preço na página de detalhes do serviço do catálogo e na folha de precificação. Cada entrada de matriz contém os
campos a seguir: unitId (O ID da unidade. Use a forma plural e altere para letras maiúsculas todas as letras. Para planos grátis, esse campo é opcional), unidade (A métrica que é usada para calcular os
encargos do serviço. O valor desse campo é usado na interface com o usuário do {{site.data.keyword.Bluemix_notm}} para representar a métrica de encargo) e partNumber (O identificador
`part_number` que é usado pelo sistema de faturamento. Para planos grátis, esse campo é opcional).   |
|paidOnly (opcional)     | Um valor booleano que indica se esse plano de serviço está disponível apenas para o {{site.data.keyword.Bluemix_notm}} pagar contas. Um valor de **true** significa que o plano de serviço é somente para contas de pagamento e não pode ser incluído em contas para teste. Um valor de **false** significa que o plano de serviço pode ser incluído nas contas de pagamento e contas para teste. O valor padrão é **false**.	  |

O exemplo a seguir mostra como a resposta de JSON de GET /v2/catalog é mapeada para a página de detalhes do serviço no catálogo do {{site.data.keyword.Bluemix_notm}}. Especificamente, como
os campos de metadados do plano descritos na tabela anterior mapeiam para a interface com o usuário:

![Detalhes de metadados de plano no catálogo.](images/plan_metadata.png "Visualização de valores de metadados de plano de catálogo do Bluemix")


<ol>
<li>Após você ter implementado a API do broker de serviço, acesse <strong>ADMINISTRAÇÃO</strong> &gt; <strong>GERENCIAMENTO DE CATÁLOGO</strong>.</li>
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

É possível expandir a seção **Monitoramento de cota** para visualizar as informações a seguir:

- O uso de memória do ambiente detalha o uso de memória para o ambiente do sistema integral. O gráfico mostra as informações a seguir: 
<ul>
<li>A memória física que está em uso e o limite de memória física</li>
<li>a cota de memória reservada e o limite de memória reservada</li>
<li>a cota total de memória para as suas organizações</li>
</ul>
Os tipos de uso de memória a seguir são exibidos no gráfico.

	<dl>
	<dt><strong>Físico usado</strong></dt>
	<dd>A memória física que é usada por seu ambiente.</dd>
	<dt><strong>Limite físico</strong></dt>
	<dd>A memória física total disponível para seu ambiente.</dd>
	<dt><strong>Cota reservada</strong></dt>
	<dd>A soma de memória que é reservada para todos os aplicativos implementados, em todas as organizações. A soma da cota que é reservada pode exceder o limite de memória física para o seu ambiente. Por exemplo, se você tiver um limite de memória física de 16 GB, você poderia reservar 4 GB de memória cada para um total de cinco aplicativos diferentes. A cota que é reservada excede o limite de memória física. No entanto, em muitos casos, as organizações podem não usar a cota total que é reservada individualmente para cada aplicativo. Além disso, todos os aplicativos podem não usar a sua cota total de memória reservada ao mesmo tempo.</dd>
	<dt><strong>Limite reservado</strong></dt>
	<dd>A memória total que pode ser reservada em todos os aplicativos para o seu ambiente.</dd>
	<dt><strong>Cota total</strong></dt>
	<dd>A cota de memória total em todas as organizações.</dd>
	</dl>
	**Nota**: os dados são atualizados automaticamente a cada 4 horas. Clique em **Recalcular** se você deseja atualizar os dados na página antes que sejam atualizados automaticamente.

- Uso de memória da organização. Esta seção detalha o uso de memória em um nível de organização. É possível visualizar a cota de memória total, a cota que é reservada e a memória física usada por cada organização. O gráfico fornece informações que são listadas pela memória mais alta reservada por organização e a organização que reserva a maior quantia de memória, por padrão, é listada primeiro. É possível classificar por
**Mais alto uso de memória** e **Excesso de alocação de memória**.

	<dl>
	<dt><strong>Mais alto uso de memória</strong></dt>
	<dd>Use esta opção para identificar a organização que reservou a maior quantia de memória. Classifique pelo uso de memória mais alto para identificar as organizações que reservaram a maior quantia de memória. A lista é classificada por cota reservada. </dd>
	<dt><strong>Alocação de memória em excesso</strong></dt>
	<dd>Use esta opção para identificar as organizações que possuem uma cota de memória total que é maior do que o necessário. Classifique por uso de memória em excesso para identificar as organizações que estão usando a menor quantia de memória para a cota que foi alocada para a organização. </dd>
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

É possível incluir usuários individualmente ou em grupos. Geralmente, os usuários são incluídos em sua instância do {{site.data.keyword.Bluemix_notm}} a partir do registro de usuário de sua empresa por meio do
Lightweight Directory Access Protocol (LDAP). Também é possível visualizar permissões de usuário. Se você tiver recebido permissão de
**Super usuário**, será possível também configurar e gerenciar
permissões de outros usuários. Clique em **ADMINISTRAÇÃO &gt; ADMINISTRAÇÃO DE USUÁRIO**.

A página Administração de usuário exibe todos os usuários da
instância local ou dedicada. As permissões para cada usuário são exibidas usando ícones na tabela. Estas
podem ser as permissões: Nenhuma, **Super usuário**,
**Acesso básico**, **Catálogo**,
**Relatórios** e **Usuários**.
As permissões de **Superusuário** e **Acesso básico** podem ser configuradas como **Ativada** ou **Desativada**, enquanto as
permissões restantes são ativadas ou desativadas com tipos de acesso específicos, incluindo acesso de **Leitura** ou **Gravação** para essa permissão, conforme
representado por ícones. Consulte
[Permissões](#permissions) para obter descrições de cada tipo e explicação dos ícones.

### Trabalhando com Usuários

Dependendo de seu acesso de **Leitura** ou **Gravação** para as permissões de acesso dos usuários, é possível procurar usuários existentes, remover usuários e
incluir usuários individualmente ou por um grupo. Se você tiver a permissão de **Superusuário**, terá acesso total para concluir quaisquer tarefas para gerenciamento de usuários
no ambiente. Revise as tarefas de gerenciamento de
usuários a seguir e o nível de acesso necessário para concluir cada tarefa:

* Localizar usuários. Se tiver acesso de **Leitura** ou
**Gravação** e você souber todo ou parte do nome do usuário, poderá
localizar os usuários na tabela usando o campo **Procurar**. Também é possível filtrar a lista de usuários por sua organização e permissões. Para filtrar uma lista de usuários, conclua
estas etapas:
  <ol>
  <li>Clique em <strong>Filtrar</strong>. </li>
  <li> Clique em <strong>Organizações</strong> ou <strong>Permissões</strong>, dependendo de por qual delas você deseja filtrar.
  <dl>
	<dt><strong>Organização</strong></dt>
	<dd>Para filtrar os usuários por sua organização, inicie digitando o nome da organização no campo de <strong>Organização</strong> e selecione a organização a partir da lista. Em seguida, selecione a função
ou as funções designadas para os usuários dentro da organização.</dd>
	<dt><strong>Permissões</strong></dt>
	<dd>Para filtrar os usuários por suas permissões, primeiro selecione o tipo de usuário ou usuários. Por exemplo, talvez você queira ver todos os Superusuários. Para permissões diferentes de
<strong>Superusuário</strong> ou <strong>Acesso básico</strong>, também é possível selecionar o tipo de acesso, por exemplo, <strong>Leitura</strong> ou
<strong>Gravação</strong>.</dd>
	</dl></li>
  <li>Clique em <strong>Aplicar</strong>.</li>
   </ol>

   A janela Administração de usuário mostra os filtros que você configura e os usuários que resultaram a partir dos filtros especificados. É possível, então, procurar um usuário na tabela filtrada. Também
é possível modificar a lista de filtros especificados removendo uma opção de filtro da lista.

* Incluir um único usuário. Se você tiver a permissão de **Super usuário** ou a permissão de **Usuários** com acesso de **Gravação**, será possível incluir usuários.

  1. Para incluir um único usuário a partir de seu diretório LDAP, clique em **Incluir usuário**.
  2. No campo de **Procura**, digite o endereço de e-mail para o usuário e, em seguida, selecione o usuário a partir da lista preenchida.
  3. Em seguida, a partir do campo **Org**, escolha a organização na qual você deseja incluir o usuário inserindo o nome da organização e selecionando-o a partir da lista preenchida.
  4. Para incluir o usuário na organização selecionada, clique em **Incluir usuário**.

  **Nota**: quando a operação de inclusão é bem-sucedida, o usuário é incluído na tabela para você visualizar e procurar. Quando os usuários são
incluídos, eles não possuem permissões designadas.

* Incluir um grupo de usuário a partir do seu diretório LDAP. Se você tiver a permissão de **Super usuário** ou a permissão de **Usuários** com acesso de **Gravação**, será possível incluir usuários.

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

* Inclua um grupo de usuários, importando uma planilha que inclua IDs de usuário, endereços de e-mail do usuário e a organização à qual você planeja incluir o usuário. Se você tiver a permissão de **Super usuário** ou a permissão de
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

Os usuários podem ser designados com as permissões a seguir com níveis de acesso específicos (de leitura ou gravação) que permitem que o usuário conclua tarefas específicas dentro do console
do administrador.

*Tabela 7. Permissões*

| **Permissão do usuário** | **Descrição** |       
|-----------------|-------------------|
| Superusuário | Os usuários com permissão de **Super usuário** configurada como **Ligado** podem editar permissões para outros usuários. Se você tiver a permissão ativa,
ela ativa automaticamente o acesso total a todas as outras permissões. Além das tarefas esboçadas para cada permissão nessa tabela, eles também podem configurar inscrições de eventos para serem alertados
diretamente sobre manutenção ou incidentes, planejarem manutenção, executarem verificações em componentes do console e criarem organizações e espaços para o ambiente. Essa permissão é equivalente à função do
administrador (admin) para o console do administrador.  |
| Acesso básico | Os usuários com permissão de **Acesso básico** configurada
como **Ligado** têm permissão para ver a opção da página de
Administração na interface com o usuário do {{site.data.keyword.Bluemix_notm}}. Usuários com a permissão ativada podem acessar os quadros de [Informações do sistema](#oc_system) e de [Uso de
recursos](#oc_resource). Sem essa permissão, os usuários não podem ver ou acessar a opção de menu de Administração. Essa permissão é equivalente à função do administrador (admin) para o console do administrador. Essa
permissão é equivalente à permissão de login usada anteriormente para o console do administrador. |
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
