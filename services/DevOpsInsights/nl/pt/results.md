---

copyright:
  years: 2016, 2017

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Exibição de resultados

## Avaliações do Deployment Risk

Após um pipeline ser executado, o {{site.data.keyword.DRA_short}} começa a coletar e analisar os resultados de teste a partir dele, para estabelecer uma referência. Dados de cada execução subsequente são coletados e comparados com resultados anteriores. Portas de decisão usam esses dados para determinarem quando
parar uma implementação. 

É possível ver seus dados de avaliação de implementação e de porta no painel Deployment Risk. Para abrir o painel, abra o {{site.data.keyword.DRA_short}} e, no menu lateral, clique em **Deployment Risk**.

Se você estiver usando um pipeline do {{site.data.keyword.contdelivery_short}}, será possível visualizar os relatórios de execução de porta individuais do próprio pipeline. Para visualizar o relatório de decisão de uma porta no pipeline:

1. No estágio que contém a porta a ser verificada, clique em **Visualizar logs e histórico**.

2. Na tarefa que contém a porta, clique no nome da porta.

3. Na visualização de log, localize a mensagem `Verifique o relatório do {{site.data.keyword.DRA_short}} aqui` e clique no link para abrir o relatório.

## Relatórios do Developer Insights e do Team Dynamics

É possível visualizar painéis sobre sua equipe e codificar após um período de mineração de dados inicial. No menu de navegação de serviço, clique em **Developer Insights** ou **Team Dynamics** e, em seguida, selecione uma categoria de dados para visualizar essas informações.
