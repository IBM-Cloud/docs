---

copyright:
  years: 2015, 2017

lastupdated: "2017-04-06"

---


{:shortdesc: .shortdesc}
{:new_window: target="_blank"}
{:codeblock: .codeblock}
{:screen: .screen}

# Analisando logs no Kibana usando visualizações 
{:#logging_kibana_visualizations}

Use a página *Visualizar* no Kibana para criar visualizações, como gráficos e tabelas, que podem ser usadas para analisar seus dados do log e comparar resultados. 
{:shortdesc}

É possível usar uma visualização individualmente para analisar seus logs. 

* É possível criar visualizações em uma procura que você define e salvar na página *Descobrir* ou em uma nova consulta que você define na página *Visualizar*. A procura define o subconjunto de dados que uma visualização exibe.

* O tipo de visualização que for escolhido determina como os dados são exibidos para análise.

A tabela a seguir lista os diferentes tipos de visualizações:

| Tipo de visualização | Descrição |
|-----------------------|-------------|
| gráfico de Áreas | Exibe dados quantitativos graficamente. Use para comparar dois ou mais conjuntos de dados agregados. |
| Tabela de Dados | Exibe dados brutos em formato tabular para uma agregação composta. |
| Gráfico de Linhas | Exibe dados baseados em tempo. Use para comparar dois ou mais conjuntos de dados agregados baseados em tempo. |
| Widget de redução de preço | Use para exibir informações de texto. |
| de Métrica | Use para mostrar uma contagem de ocorrências ou a média exata de um campo numérico. |
| Gráficos de pizza | Use para exibir diferentes valores de um campo. | 
| Gráfico de barras verticais | Exibe dados que são baseados em tempo e dados que não são baseados em tempo. Use para agrupar dados. |
{: caption="Tabela 1. Tipos de visualização" caption-side="top"}

Na página Visualizar, é possível executar qualquer uma das tarefas a seguir:

| Atividade | Informações Adicionais |
|------|------------------|
| [Criar uma nova visualização](logging_kibana_visualizations.html#logging_k4_visualizations_create) | É possível criar visualizações em uma procura que você define e salvar na página *Descobrir* ou em uma nova consulta que você define na página *Visualizar*. |
| [Salvar uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_save) | É possível salvar visualizações para reutilização posterior. |
| [Carregar uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_reload) | É possível fazer upload de uma visualização para atualizar, modificar ou analisar seus dados. |
| [Excluir uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_delete) | Exclua visualizações que não forem necessárias. |
| [Exportar uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_export) | É possível exportar uma visualização como um arquivo JSON.  |
| [Importar uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_import) | É possível importar uma visualização como um arquivo JSON.  |
| [Compartilhar uma visualização](logging_kibana_visualizations.html#logging_kibana_visualizations_share) | É possível compartilhar uma visualização por meio de sua origem HTML ou por meio do painel do Kibana.  |
{: caption="Tabela 2. Tarefas para trabalhar com visualizações" caption-side="top"}


## Criando visualizações por meio das consultas no Kibana
{:#logging_k4_visualizations_create}

Conclua as etapas a seguir para criar uma visualização na página Visualizar:

1. Ative o Kibana e, em seguida, selecione a página **Visualizar**.

2. Criar uma nova visualização. Na barra de ferramentas, clique no botão **Nova visualização** ![Nova visualização](images/k4_visualization_new_icon.jpg "Nova visualização").

3. Selecione uma visualização.
    
4. Selecione uma origem de procura. Selecione uma das opções a seguir:

    * Clique em **Em uma nova procura**.
    * Clique em **Em uma procura salva**. 
  
5. Configure a consulta.

    * Se você selecionar **Em uma procura salva**, escolha uma consulta de procura. A consulta é usada para recuperar os dados que são usados para a visualização. 

        Depois de selecionar uma procura, o construtor de visualização se abre e carrega os dados para a consulta selecionada. A seguinte mensagem é exibida: *Esta visualização é vinculada a uma procura salva: your_search_name*. 
	
	**Nota**: quaisquer mudanças feitas em uma procura salva são refletidas automaticamente na visualização. Para desativar atualizações automáticas que você faz na consulta que é vinculada a essa visualização, dê um clique duplo na mensagem: *Esta visualização é vinculada a uma procura salva: your_search_name*. 

    * Se você selecionar **Em uma nova procura**, defina uma nova consulta. A consulta é usada para definir o subconjunto de dados que é recuperado e usado pela visualização.

        Para obter mais informações, consulte
[Filtrando logs definindo consultas customizadas](k4_filter_queries.html#k4_filter_queries).

6. No construtor de visualização, selecione uma agregação da métrica para o eixo Y.

7. No construtor de visualização, selecione um tipo de depósito. Em seguida, selecione uma agregação de depósito.
  
8. Inclua subdepósitos para dividir os dados.

Para obter mais informações sobre o Kibana, consulte o [Guia do Usuário do Kibana ![Ícone de Link externo](../../../icons/launch-glyph.svg "External link icon")](https://www.elastic.co/guide/en/kibana/4.1/index.html){: new_window}.

## Excluindo uma visualização
{:#logging_kibana_visualizations_delete}

Para excluir uma visualização, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Visualizações**, selecione as visualizações que deseja excluir.

3. Clique em **Excluir**.


## Exportando uma visualização
{:#logging_kibana_visualizations_export}

Para exportar uma visualização como um arquivo JSON, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Visualizações**, selecione a visualização que deseja exportar.

3. Clique em **Exportar**.

4. Salve o arquivo.

## Importando uma visualização
{:#logging_kibana_visualizations_import}

Para importar uma visualização como um arquivo JSON, conclua as etapas a seguir na página Configurações:

1. Na página Configurações, selecione a guia **Objetos**.

2. Na guia **Visualizações**, selecione **Importar**.

3. Selecione um arquivo e clique em **Abrir**.

A visualização é incluída na lista de visualizações.


 
## Carregando uma visualização
{:#logging_kibana_visualizations_reload}

Conclua as etapas a seguir para carregar uma visualização salva:

1. Na barra de ferramentas da página Visualizar, clique no botão **Carregar visualização salva** ![Carregar visualização salva](images/k4_visualization_open_icon.jpg "Carregar visualização salva ").

2. Selecione a visualização que deseja carregar. 


## Salvando uma visualização
{:#logging_kibana_visualizations_save}

Conclua as etapas a seguir para salvar uma visualização na página Visualizar:

1. Na barra de ferramentas da página Visualizar, clique no botão **Salvar visualização** ![Salvar visualização](images/k4_visualization_save_icon.jpg "Salvar visualização").

2. Insira um nome para a visualização.

3. Clique em salvar. 



## Compartilhando uma visualização
{:#logging_kibana_visualizations_share}

Conclua as seguintes etapas para compartilhar uma visualização na página Visualizar:

1. Na barra de ferramentas da página Visualizar, clique no botão **Compartilhar visualização** ![Compartilhar visualização](images/k4_visualization_share_icon.jpg "Compartilhar visualização").

2. Escolha uma das seguintes ações:

    * **Integrar essa visualização**: selecione essa opção para compartilhar a visualização em sua origem HTML. 
    
        Clique no botão de copiar ![Copiar para a área de transferência](images/k4_copy_to_clipboard.jpg "Copiar para a área de transferência") para copiar o código HTML que pode ser usado para integrar a visualização em sua origem HTML. 
	
	**Nota**: para ver a visualização, os usuários devem ser capazes de acessar o Kibana.
	
    * **Compartilhar um link**: selecione essa opção para compartilhar a visualização no Kibana com outros usuários.



