---

copyright:
  years: 2016
lastupdated: "2016-08-02"

---

{:shortdesc: .shortdesc}
{:codeblock: .codeblock}
{:screen: .screen}
{:pre: .pre}

# Monitorando a atividade de seu {{site.data.keyword.openwhisk_short}} de atividade com o Painel do {{site.data.keyword.openwhisk_short}}

O [Painel do {{site.data.keyword.openwhisk}}](https://{DomainName}/whisk/dashboard/) fornece um resumo gráfico de sua atividade. Utilize o painel para determinar o desempenho e o funcionamento de suas ações do {{site.data.keyword.openwhisk_short}}.
{:shortdesc}

Clique em **Recarregar** a qualquer momento para atualizar o painel com os dados do log de ativação mais recentes.

## Resumo da Atividade
{: #summary}

Essa visualização fornece um resumo de alto nível de seu ambiente do {{site.data.keyword.openwhisk_short}}. Use a visualização **Resumo de atividade** para monitorar o funcionamento e o desempenho gerais de seu serviço ativado pelo {{site.data.keyword.openwhisk_short}}. A partir das métricas nessa visualização, é possível executar o seguinte:
* Determine a taxa de uso das ações ativadas pelo {{site.data.keyword.openwhisk_short}} de seu serviço visualizando o número de vezes que eles foram chamadas.
* Determine a taxa geral de falha entre todas as ações. Se você identificar um erro, será possível isolar quais serviços ou ações tiveram erros exibindo a visualização **Histograma de atividade**. Isole os próprios erros visualizando o **Log de atividades**.
* Determine o nível de desempenho de suas ações visualizando o tempo médio de conclusão associado a cada ação.

<!-- For tips on improving performance, see troubleshooting? -->

## Linha do tempo da atividade
{: #timeline}

A visualização **Linha de tempo de atividades** exibe um gráfico de barras verticais para visualizar a atividade de ações passadas e presentes. Vermelho indica erros em ações específicas. Correlacione essa visualização com o **Log de atividades** para localizar mais detalhes sobre os erros.

## Histograma de atividade
{: #histogram}

A visualização **Histograma de atividade** exibe um gráfico de barras horizontais para visualizar a atividade de ações passadas e presentes. Vermelho indica erros em ações específicas. Correlacione essa visualização com o **Log de atividades** para localizar mais detalhes sobre os erros.

## Log de atividades
{: #log}

Essa visualização exibe uma versão formatada do log de ativação. Ela mostra os detalhes de cada ativação, mas pesquisa uma vez por minuto para ver se há novas ativações. Clique em uma ação para exibir um log detalhado.
**Nota:** Para obter a saída exibida no Log de atividades usando a
CLI, use o comando a seguir:

  ```
  wsk activation poll
  ```
  {: pre}

## Opções de Filtragem
{: #filtering}

Selecione qual log de ação deseja visualizar e selecione o prazo da atividade registrada.

**Nota:** Esses filtros são aplicados a todas as visualizações no painel.
