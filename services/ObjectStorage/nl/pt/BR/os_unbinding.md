---

copyright:
  years: 2014, 2016
lastupdated: "2016-12-06"

---
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Desvinculando e desprovisionando sua instância do {{site.data.keyword.objectstorageshort}} {: #deprovisioning-object-storage}

Se você tiver vinculado o {{site.data.keyword.objectstorageshort}} a um aplicativo Cloud Foundry e não tiver mais necessidade de armazenamento, será possível desvincular e desprover sua instância.
{: shortdesc}


## Desvinculando sua instância
Se você não tiver mais necessidade do {{site.data.keyword.objectstorageshort}} em seu app Cloud Foundry, mas desejar manter seus dados salvos, será possível desvincular a instância do serviço de seu app.

**Atenção**: se você desvincular uma instância do
{{site.data.keyword.objectstorageshort}} de um aplicativo
{{site.data.keyword.Bluemix_notm}} ou excluir a chave de serviço, todas as suas
credenciais para essa instância serão excluídas e não poderão ser restauradas. A conta do {{site.data.keyword.objectstorageshort}} não será excluída até que a instância do {{site.data.keyword.objectstorageshort}} seja desprovida. É possível gerar novas credenciais de nuvem religando ou criando uma nova chave de serviço.

1. Para ver os serviços que estão vinculados ao seu app, clique na guia Conexões no aplicativo Cloud Foundry.
2. Localize o serviço que deseja desvincular e clique no botão do menu no tile do serviço.
3. Selecione **Desvincular serviço**.
4. Limpe a caixa **Excluir instância de serviço** e clique em **OK**.
5. Clique em **Remontar** para que sua mudança entre em vigor.



## Desprovisionando sua instância

Se você tiver uma instância do {{site.data.keyword.objectstorageshort}} que não é mais necessária, será possível excluí-la.

**Atenção**: ao desprover uma instância do {{site.data.keyword.objectstorageshort}}, o projeto em nuvem e a conta Swift serão excluídos. Todos
os contêineres e objetos na instância desprovisionada serão excluídos e não
poderão ser restaurados.

1. Para ver os serviços que estão vinculados ao seu app, clique na guia Conexões no aplicativo Cloud Foundry.
2. Localize o serviço que deseja desvincular e clique no botão do menu no tile do serviço.
3. Selecione **Excluir serviço**.
4. Clique em **Excluir** para confirmar.
5. Clique em **Remontar** para que sua mudança entre em vigor.
