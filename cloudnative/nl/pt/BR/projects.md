---

copyright:
  years: 2016, 2017
lastupdated: "2017-03-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen:.screen}
{:codeblock:.codeblock}

# Projects
{: #projects}

O {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}} combina a interface com o usuário do app, dados e serviços em um *projeto* completo. Ao criar um
projeto, todas as partes necessárias de seu app e os recursos incluídos são mantidos no
servidor {{site.data.keyword.Bluemix_notm}}. Será possível fazer download do código de app e das credenciais e inicializadores necessários, se os serviços estiverem configurados em seu projeto. É possível visualizar todos os seus projetos selecionando **Projetos**.  

É possível visualizar informações adicionais sobre um único projeto, selecionando-o na página **Projetos**. Isso exibe a página **Visão geral do projeto**, que inclui os serviços que estão configurados e disponíveis para o projeto. Serviços são recursos
separados que estendem seu app incluindo uma função. Como são incluídos individualmente, é possível incluir os serviços necessários, como serviços de push, autenticação, dados e armazenamento ou outros serviços. Ao incluir um serviço em seu projeto na página **Visão geral do projeto** e seguir as instruções para configurá-lo, ele será associado automaticamente ao app. Para obter mais informações sobre a página Visão geral do projeto, veja [Página Visão geral do projeto](project_overview_page.html).

Para criar seu projeto, deve-se selecionar um [padrão](patterns.html), seguido por um [iniciador](starters.html).


## Página Visão geral do projeto
{: #project_overview}

É possível visualizar e trabalhar com um único projeto do {{site.data.keyword.Bluemix}} {{site.data.keyword.dev_console}}, selecionando o projeto na página **Projetos**, que abre a página Visão geral do projeto.
{: shortdesc}

A página **Visão geral do projeto** exibe um quadro para cada recurso que está configurado ou disponível para configuração com o projeto selecionado. O quadro exibe o tipo do recurso e um botão *ações* com três pontos alinhados verticalmente. Exemplos de recursos que podem estar disponíveis ou configurados incluem {{site.data.keyword.mobilepushshort}}, Analítica ou Dados e armazenamento. Os recursos compatíveis dependem do tipo de projeto e dos recursos que estão disponíveis nessa região, portanto, nem todos eles estarão disponíveis para serem associados a todos os projetos. 

Quando um tipo de recurso ainda não está associado ao projeto, um botão **Criar** é exibido no quadro. As opções do botão de ações são para criar uma instância do serviço ou para incluir uma instância de serviço existente quando o recurso ainda não estiver associado. Selecionar **Incluir existente** fornece uma lista das instâncias de serviço desse tipo em seu espaço.

Se o recurso já estiver associado a esse projeto, o nome da instância de serviço associada será exibido no quadro depois do tipo de recurso. Isso facilita localizar qual instância de serviço está relacionada a esse projeto no {{site.data.keyword.dev_console}}. As ações que estão disponíveis no botão de ações são **Visualizar** e **Remover** quando o recurso já está associado ao projeto. A remoção de uma instância de serviço remove apenas a associação a esse projeto e não exclui a instância de serviço do {{site.data.keyword.dev_console}}. Para excluir uma instância de serviço, clique na página **Web e Dispositivo móvel > Serviços** para visualizar e excluir as instâncias de serviço.

Selecione **Obter o código** no quadro **Código** para fazer download do código para seu projeto. Para obter mais informações sobre como fazer download do código, veja [Obter código](get_code.html).


## Atualizando seu projeto para usar um novo Iniciador
{: #update-starter}

1. Na página **Projetos** ou **Visão geral do projeto**, clique no ícone do **Menu overflow** e selecione **Atualizar Iniciador**.

2. Escolha um novo Iniciador e clique em **Atualizar**.

3. Clique em **Obter o código** na página **Visão geral do projeto** para selecionar sua linguagem.

   Como alternativa, é possível clicar na página **Código**.


## Atualizando seu projeto para gerar uma nova linguagem
{: #update-language}

1. Nas páginas **Projetos** ou **Visão geral do projeto**, clique no ícone do **Menu overflow** e selecione **Atualizar Iniciador**.

2. Selecione uma nova linguagem e clique em **Atualizar**.

3. Clique em **Obter o código** na página **Visão geral do projeto** para selecionar sua linguagem.
