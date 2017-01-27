---

copyright:
  years: 2014, 2017
lastupdated: "2017-01-17"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Desvinculando e desprovisionando sua instância do {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

Se o serviço {{site.data.keyword.objectstorageshort}} está ligado ao seu app Cloud Foundry, mas você não precisa mais de armazenamento, é possível desvincular e desprovisionar a sua instância.
{: shortdesc}


## Desvinculando sua instância

É possível manter seus dados salvos e desvincular o serviço do seu app Cloud Foundry. A conta {{site.data.keyword.objectstorageshort}} não é excluída até que o serviço seja desprovisionado.

**Atenção**: se você desvincular uma instância do {{site.data.keyword.objectstorageshort}} de um aplicativo {{site.data.keyword.Bluemix_notm}} ou excluir a
chave de serviço, todas as suas credenciais para essa instância serão excluídas e não poderão ser armazenadas. É possível gerar novas credenciais de nuvem religando sua instância ou criando uma nova chave de serviço.

1. Para ver os serviços que estão vinculados ao seu app, clique na guia Conexões no aplicativo Cloud Foundry.
2. Localize o serviço que você deseja desvincular e clique no botão do menu no quadrado de serviço.
3. Selecione **Desvincular serviço**.
4. Limpe a caixa **Excluir instância de serviço** e clique em **OK**.
5. Clique em **Remontar** para que sua mudança entre em vigor.



## Desprovisionando sua instância

Se você tiver uma instância do {{site.data.keyword.objectstorageshort}} que não é mais necessária, será possível excluí-la.

**Atenção**: ao desprover uma instância do {{site.data.keyword.objectstorageshort}}, o projeto em nuvem e a conta Swift serão excluídos. Todos
os contêineres e objetos na instância desprovisionada serão excluídos e não
poderão ser restaurados.

1. Para ver os serviços que estão vinculados ao seu app, clique na guia Conexões no aplicativo Cloud Foundry.
2. Localize o serviço que você deseja desprovisionar e clique no botão do menu no quadrado do serviço.
3. Selecione **Excluir serviço**.
4. Clique em **Excluir** para confirmar.
5. Clique em **Remontar** para que sua mudança entre em vigor.
