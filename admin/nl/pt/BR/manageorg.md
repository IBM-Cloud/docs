---

copyright:

  years: 2015, 2017
lastupdated: "2017-04-11"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:new_window: target="_blank"}

# Gerenciando Organizações
Como um proprietário da conta ou um gerenciador de organização, é possível executar tarefas de gerenciamento da organização, incluindo renomear sua organização, excluir uma organização ou um espaço, atualizar funções da organização ou do espaço e gerenciar cotas e domínios.
{:shortdesc}

Na barra de menus do console, clique em **Gerenciar > Conta > Organizações** para gerenciar suas organizações. 

**Nota:** é possível visualizar recursos de uma organização por vez somente. Se você for um membro de múltiplas organizações, poderá alternar organizações do link de preferências de conta do usuário na barra de menus do console.

## Renomeando organizações
{: #orgrename}

Conclua as etapas a seguir para renomear sua organização:
1. Clique em **Gerenciar** > **Conta** >
**Organizações**.
2. Identifique a organização que você deseja renomear e clique em **Visualizar detalhes**.
3. Clique em **Editar organização**.
4. Clique em **Editar** próximo ao nome da organização.
5. Digite o novo nome da organização e clique em **Salvar**.

## Excluindo organizações e espaços
{: #deleteorgs}

Como o proprietário da conta, entre em contato com o [Suporte do {{site.data.keyword.Bluemix_notm}} ![Ícone de link externo](../icons/launch-glyph.svg)](http://ibm.biz/bluemixsupport){: new_window} para excluir uma organização.

**Nota**: Não é possível inverter operações de exclusão. Você perderá todos os seus apps e serviços que estão associados à organização.

Conclua as etapas a seguir para excluir uma organização ou um espaço:
1. Clique em **Gerenciar** > **Conta** >
**Organizações**.
2. Identifique a organização que você deseja editar e clique em **Visualizar detalhes**.
3. Identifique o espaço que você deseja excluir e clique em **Editar espaço**.
4. Clique em **Excluir espaço**.

## Editando funções de usuário
{: #listmembers}

Conclua as etapas a seguir para editar as funções de usuário de uma organização específica:
1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Identifique a organização para a qual deseja visualizar os membros e clique em **Visualizar detalhes**.
3. Clique em **Editar organização**.
4. É possível ver os membros de sua organização e suas funções na guia **USUÁRIOS**.

Conclua as etapas a seguir para editar as funções de usuário de um espaço específico:
1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Identifique a organização para a qual deseja visualizar os membros e clique em **Visualizar detalhes**.
3. Identifique o espaço para a qual deseja visualizar os membros e clique em **Editar espaço**.
4. É possível ver os membros de seu espaço e suas funções na guia **USUÁRIOS**.

## Gerenciando cota
{: #managequota}

Como um proprietário da conta ou gerenciador de organização do {{site.data.keyword.Bluemix_notm}}, é possível visualizar a cota usada e alocada para uma
organização. A cota representa os limites de recurso para a organização, a qual é designada quando a organização é criada. Dependendo se você tem uma conta de avaliação
ou uma conta faturável, os recursos que estão disponíveis para uma organização variam. Qualquer aplicativo ou serviço em um espaço dentro da organização contribui
para o uso da cota alocada.

Para visualizar a cota usada e alocada de uma organização, conclua as etapas a seguir:
1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Identifique a organização para a qual deseja visualizar a cota e clique em **Visualizar detalhes**.
3. Clique em **Editar organização**.
4. Se você tiver espaços definidos em mais de uma região, selecione a região específica que deseja visualizar.
5. Clique em **COTA**. 
6. Por padrão, a página de cota do **Cloud Foundry** é aberta. É possível visualizar os detalhes da cota para os recursos a seguir:
 * MEMÓRIA
 * SERVIÇOS
 * PLANO
 * PREÇO
7. Clique em **Contêineres** para visualizar a alocação de cota de contêiner usada e disponível. A alocação de contêiner varia dependendo
de seu plano de precificação. É possível visualizar os detalhes da cota para os recursos a seguir:
 * MEMÓRIA
 * IP PÚBLICO
 * COMPARTILHAMENTOS DE ARQUIVO
8. Clique em **Servidores virtuais** para visualizar as máquinas virtuais.

**Nota:** Os contêineres não estão disponíveis na região de Sydney do {{site.data.keyword.Bluemix_notm}}. 

Para obter mais informações sobre contêineres, consulte [Cota](/docs/containers/container_planning.html#container_planning_quota) na
documentação de Contêineres.
Para mudar a cota que está alocada para uma organização, deve-se abrir um chamado de suporte. Para obter mais informações sobre como abrir um chamado de suporte,
consulte [Obtendo suporte ao cliente](/docs/support/index.html#contacting-support). 

## Gerenciando Domínios
{: #managedomains}

Como um proprietário da conta ou gerenciador de organização, é possível visualizar o domínio do sistema e incluir domínios customizados para aplicativos que são construídos dentro de uma organização e
de seus espaços. Como um gerenciador de espaço, a guia **Domínios** para um espaço é uma lista somente leitura dos domínios designados ao espaço.

1. Clique em **Gerenciar** &gt; **Conta** &gt;
**Organizações**.
2. Identifique a organização para a qual deseja visualizar ou editar domínios.
3. Selecione **Visualizar detalhes** para essa organização.
4. Clique em **Editar organização**.
5. Clique em **DOMÍNIOS**.

Se você incluir um domínio customizado, deverá
configurar seu servidor DNS para resolver seu domínio customizado para apontar para o
domínio do sistema {{site.data.keyword.Bluemix_notm}}. Dessa maneira, quando o {{site.data.keyword.Bluemix_notm}} receber uma solicitação para seu domínio customizado, ele poderá roteá-la adequadamente para seu app. O domínio do sistema está sempre disponível para um espaço e domínios customizados também podem ser alocados para um espaço. Os apps criados em um espaço podem usar qualquer um dos domínios listados para esse espaço. Para obter mais informações sobre como criar e usar domínios customizados, consulte [Usando um domínio customizado](/docs/manageapps/updapps.html#domain).
