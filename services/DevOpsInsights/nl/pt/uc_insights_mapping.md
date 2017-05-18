---

copyright:
  years: 2017
lastupdated: "2017-03-14"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Mapeando ambientes para relatórios
{: #uc_insights_mapping}

As informações que você vê no Delivery Insights são agrupadas por *ambientes lógicos*, que são coleções de ambientes do IBM UrbanCode Deploy (também denominados *ambientes físicos*). É possível agrupar seus ambientes em ambientes lógicos de qualquer maneira que faça sentido para sua organização.
{:shortdesc}

## Ambientes lógicos

O Delivery Insights agrupa os ambientes do IBM UrbanCode Deploy em um ou mais ambientes lógicos. Dessa forma, é possível coletar ambientes em grupos que façam sentido para você e sua organização. Por exemplo, se você tiver vários ambientes de produção para vários aplicativos, será possível agrupar todos esses ambientes em um único ambiente lógico e combinar métricas para todos esses ambientes em um único painel do ambiente de produção. O mapeamento acontece por sequência de procura, portanto, é possível agrupar ambientes de qualquer maneira que faça sentido para os servidores IBM UrbanCode Deploy.

## Ambientes lógicos padrão

Por padrão, seus relatórios incluem ambientes lógicos que correspondem a ambientes do IBM UrbanCode Deploy usando sequências. Por exemplo, todos os ambientes com "dev" no nome são mapeados para o ambiente lógico DEV e todos os ambientes com "prod" no nome são mapeados para o ambiente lógico PROD.

![Os ambientes lógicos padrão](images/uc_insights_mapping.gif)

## Mapeando ambientes para ambientes lógicos

É possível mapear manualmente os ambientes físicos para ambientes lógicos ou usar padrões para associar ambientes físicos a ambientes lógicos dinamicamente.

Para mapear ambientes físicos para ambientes lógicos usando um padrão, siga estas etapas:

1. No {{site.data.keyword.DRA_short}}, clique em **Delivery Insights > Mapear ambientes**.
1. Clique em um ambiente lógico existente ou clique em **Incluir ambiente lógico**.
1. Nas configurações para o ambiente lógico, em **Padrões**, clique em **Incluir padrão**.
1. Especifique um padrão para nomes de ambiente. É possível usar o asterisco (*) como um curinga. Por exemplo, o padrão `env` corresponde aos ambientes `env1`, `env2` e `env`.
1. Verifique se o ambiente lógico contém os ambientes que você deseja.

Para mapear ambientes para ambientes lógicos manualmente, clique em **Incluir manualmente** e selecione os ambientes a serem incluídos ou removidos.

![Configurando a integração no DevOps Connect](images/uc_insights_mapping_manually.gif)

Agora que você mapeou ambientes para ambientes lógicos, será possível ver informações de relatório agregadas por esses ambientes lógicos.
