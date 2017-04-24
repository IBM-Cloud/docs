---

copyright:
  years: 2015, 2017

lastupdated: "2017-03-08"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando logs no Kibana por meio de um painel
{:#kibana_analize_logs_dashboard}

Use a página *Painel* no Kibana para exibir coleções de visualizações que são agrupadas em painéis. Use os painéis para analisar seus dados do log e comparar resultados.{:shortdesc}

No {{site.data.keyword.Bluemix}}, há diferentes tipos de painéis que podem ser definidos e customizados para visualizar e analisar os dados.  Por exemplo, a tabela a seguir lista alguns tipos comuns de painéis:

| Tipo de painel | Descrição |
|-------------------|-------------|
| Painel Single-cf-app | Esse é um painel que mostra informações para um único aplicativo Cloud Foundry. |
| Painel de contêiner único  | Esse é um painel que mostra informações para um único contêiner.  |
| Painel de grupo de contêiner  | Esse é um painel que mostra informações para um grupo de contêiner específico.  |
| Painel Multi-cf-app | Esse é um painel que mostra informações para todos os aplicativos Cloud Foundry implementados no mesmo espaço do {{site.data.keyword.Bluemix_notm}}.  | 
| Painel de múltiplos contêineres  | Esse é um painel que mostra informações para todos os contêineres que estiverem implementados no mesmo espaço do {{site.data.keyword.Bluemix_notm}}.  |
| Painel de espaço | Este é um painel que mostra dados de criação de log que estão disponíveis em um espaço do {{site.data.keyword.Bluemix_notm}}.  | 

Para visualizar os dados em um painel, configure telas. O Kibana inclui diferentes visualizações, como tabela, tendências e histograma, que podem ser usadas para analisar as informações. Uma visualização é incluída como uma tela para um painel. É possível incluir, remover e reorganizar os painéis no painel. O objetivo de cada painel varia. Alguns painéis são organizados em linhas que fornecem os resultados de uma ou mais consultas. Outros painéis exibem documentos ou informações customizadas. Cada tela é baseada em uma procura. A procura define o subconjunto de dados que a tela exibe. Por exemplo, é possível configurar um gráfico de barras, gráfico de pizza ou tabela para visualizar os dados e analisá-los.  

A tabela a seguir lista as diferentes tarefas que podem ser executadas na página Painel:

| Atividade | Informações Adicionais |
|------|------------------|
| [Criando um novo painel](logging_kibana_analize_logs_dashboard.html#K4_dashboard_new) | É possível criar múltiplos painéis. Cada painel pode ser projetado para incluir diversas procuras e visualizações e um subconjunto diferente de dados do log.  |
| [Salvar um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save) | É possível salvar um painel para reutilização posterior.
 |
| [Carregar um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_reload) | É possível fazer upload de um painel para atualizar, modificar ou analisar seus dados. |
| [Excluir um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_delete) | Exclua painéis que não forem necessários. |
| [Exportar um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_export) | É possível exportar um painel como um arquivo JSON. |
| [Importar um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_import) | É possível importar um painel como um arquivo JSON. |
| [Compartilhar um painel](logging_kibana_analize_logs_dashboard.html#k4_dashboard_share) | É possível compartilhar um painel por meio de sua origem HTML ou por meio do painel do Kibana. |
| [Incluir uma visualização](logging_kibana_analize_logs_dashboard.html#k4_dashboard_add_visualization) | É possível incluir uma visualização ou procura existente em um painel.|

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.



## Criando um novo painel do Kibana
{: #K4_dashboard_new}

Conclua as etapas a seguir para criar um novo painel:

1. Na barra de ferramentas da página Painel, clique no botão **Novo painel** ![Novo painel](images/k4_dash_new_icon.jpg "Novo painel").

2. Inclua uma ou mais procuras e visualizações. Para obter mais informações, consulte [Incluindo uma nova procura ou visualização](logging_kibana_analize_logs_dashboard.html#K4_dashboard_add_visualization).

    Ao incluir uma procura ou visualização, uma tela é incluída no painel.

3. Arraste a tela e solte-a na parte do painel em que deseja posicioná-la.
 
4. Salve o painel para reutilização futura. Para obter mais informações, veja [Salvando um painel do Kibana](logging_kibana_analize_logs_dashboard.html#k4_dashboard_save).


## Incluindo uma nova procura ou visualização
{: #k4_dashboard_add_visualization}

Conclua as etapas a seguir para incluir uma visualização ou procura existente:

1. Na barra de ferramentas da página Painel, clique no botão **Incluir visualização** ![Incluir visualização](images/k4_dash_add_visualization_icon.jpg "Incluir visualização").

    **Nota**: é possível incluir visualizações e procuras. 

2. Selecione a guia **Visualizações** para incluir uma visualização ou selecione a guia **Procura** para incluir uma procura.

3. Clique na procura ou na visualização que deseja incluir. 

    Uma tela para essa procura ou visualização é incluída no painel.



## Salvando um painel do Kibana
{: #k4_dashboard_save}

Conclua as etapas a seguir para salvar um painel do Kibana após sua customização:

1. Na barra de ferramentas, clique no botão **Salvar** ![Salvar painel](images/k4_dash_save_icon.jpg "Salvar painel").

2. Insira um nome para o painel.

    **Nota:** se você tentar salvar um painel com um nome contendo espaços em branco, ele não será salvo.

3. Próximo ao campo de nome, clique no ícone **Salvar**.


## Excluindo um painel do Kibana
{: #k4_dashboard_delete}

Para excluir uma visualização, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Visualizações**, selecione as visualizações que deseja excluir.

3. Clique em **Excluir**.


## Carregando um painel do Kibana
{: #k4_dashboard_reload}

Conclua as etapas a seguir para carregar um painel salvo:

1. Na barra de ferramentas da página Painel, clique em **Carregar painel salvo** ![Carregar painel salvo](images/k4_dash_load_icon.jpg "Carregar painel salvo").

2. Selecione o painel que deseja carregar. 


## Exportando um painel do Kibana
{: #k4_dashboard_export}

Para exportar um painel como um arquivo JSON, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Painel**, selecione o painel que deseja exportar.

3. Clique em **Exportar**. 

4. Salve o arquivo.


## Importando um painel do Kibana
{: #k4_dashboard_import}

Para importar um painel como um arquivo JSON, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Painel**, selecione **Importar**.

3. Selecione um arquivo e clique em **Abrir**.

O painel é incluído na lista de painéis.


## Compartilhando um painel do Kibana
{: #k4_dashboard_share}

Conclua as etapas a seguir para compartilhar um painel:

1. Na barra de ferramentas da página Painel, clique no botão **Compartilhar painel** ![Compartilhar painel](images/k4_dash_share_icon.jpg "Compartilhar painel").

2. Escolha uma das seguintes ações:

    * **Integrar esse painel**: selecione essa opção para compartilhar o painel por meio de sua origem HTML. 
    
        Clique no botão de cópia ![Copiar para a área de transferência](images/k4_copy_to_clipboard.jpg "Copiar para a área de transferência") para copiar o código HTML que pode ser usado para integrar o painel em sua origem HTML. 
        
        **Nota**: para ver o painel, os usuários devem ser capazes de acessar o Kibana.
	
    * **Compartilhar um link**: selecione essa opção para compartilhar o painel no Kibana com outros usuários.



