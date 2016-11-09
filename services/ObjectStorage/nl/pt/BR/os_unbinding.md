---

copyright:
  years: 2014, 2016

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Desvinculando e desprovisionando sua instância do {{site.data.keyword.objectstorageshort}}{: #deprovisioning-object-storage}

*Última atualização: 19 de outubro de 2016*
{: .last-updated}


### Desvinculando sua instância
Se você não tiver mais necessidade do
{{site.data.keyword.objectstorageshort}} em seu app Cloud Foundry, mas desejar
manter seus dados salvos, poderá desvincular sua instância do serviço de seu app.

**Atenção**: se você desvincular uma instância do
{{site.data.keyword.objectstorageshort}} de um aplicativo
{{site.data.keyword.Bluemix_notm}} ou excluir a chave de serviço, todas as suas
credenciais para essa instância serão excluídas e não poderão ser restauradas. 

1. Abra os detalhes do seu app no console do {{site.data.keyword.Bluemix_notm}}.
2. Selecione a instância do {{site.data.keyword.objectstorageshort}} e clique em **Desvincular serviço**.
3. Clique em **REMOVER**.
4. Clique em **REMONTAR**.



### Desprovisionando sua instância

Se você tiver uma instância desvinculada do {{site.data.keyword.objectstorageshort}} que não é mais necessária, poderá excluir a instância.

**Atenção**: quando você desprover uma instância do
{{site.data.keyword.objectstorageshort}}, o projeto em nuvem será excluído. Todos
os contêineres e objetos na instância desprovisionada serão excluídos e não
poderão ser restaurados.

1. Abra os detalhes do seu app no console do {{site.data.keyword.Bluemix_notm}}.
2. Selecione a instância do {{site.data.keyword.objectstorageshort}} e clique em **Excluir**.
3. Clique em **REMONTAR**.
