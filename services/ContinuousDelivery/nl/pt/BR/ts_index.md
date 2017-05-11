---

copyright:
  years: 2015, 2017
lastupdated: "2017-2-9"

---
<!-- Common attributes used in the template are defined as follows: -->
{:tsSymptoms: .tsSymptoms}
{:tsCauses: .tsCauses}
{:tsResolve: .tsResolve}
{:new_window: target="_blank"}
{:shortdesc: .shortdesc}

# Resolução de problemas do {{site.data.keyword.contdelivery_short}}
{: #ts_cd}

Obtenha respostas para perguntas comuns de resolução de problemas sobre como usar {{site.data.keyword.contdelivery_full}}.
{:shortdesc}


## Não é possível autorizar com o GitHub
{: #cannot_authorize_github}

Você não tem autorização com o GitHub.
{:shortdesc}

Se você não tiver autorizado o {{site.data.keyword.Bluemix_notm}} a acessar a conta do GitHub, qualquer um destes problemas poderá ocorrer:
{: tsSymptoms}

 * Quando você tentar incluir a integração de ferramenta GitHub em sua cadeia de ferramentas, a integração de ferramenta não será incluída.
 * O pipeline não é executado automaticamente quando você envia mudanças por push para seu repositório GitHub ou GitHub Enterprise.

O {{site.data.keyword.Bluemix_notm}} não está autorizado a acessar o GitHub.  
{: tsCauses}
 
Se você estiver configurando a integração de ferramenta GitHub enquanto estiver criando sua cadeia de ferramentas, siga estas etapas:
{: tsResolve}
 
  1. Na seção Integrações configuráveis, clique em **GitHub**. 
  1. Se você estiver criando a cadeia de ferramentas no {{site.data.keyword.Bluemix_notm}} Public e não for autorizado {{site.data.keyword.Bluemix_notm}} a acessar o GitHub, clique em **Autorizar** para acessar o website GitHub. 
  1. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix_notm}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.
  
Se você já tiver uma cadeia de ferramentas, atualize a configuração da integração de ferramenta GitHub:

 1. No painel do DevOps, na página **Cadeias de ferramentas**, clique na cadeia de ferramentas para abrir sua página Visão geral. Como alternativa, na página Visão geral do app, no cartão do Continuous Delivery, clique em **Visualizar cadeia de ferramentas** e, em seguida, clique em **Visão geral**.
 1. No cartão GitHub, clique no menu e, em seguida, em **Configurar**.
 1. Atualize as definições de configuração para autorizar o {{site.data.keyword.Bluemix_notm}} a acessar o GitHub. Clique em **Autorizar** para acessar o website do GitHub. Se você não
tiver uma sessão GitHub ativa, será solicitado que efetue login. Clique em **Autorizar aplicativo** para permitir que o {{site.data.keyword.Bluemix_notm}} acesse sua conta GitHub. Se
você tiver uma sessão GitHub ativa, mas não tiver inserido sua senha recentemente, poderá ser solicitado que insira sua senha GitHub para
confirmar.
 1. Quando tiver finalizado a atualização das configurações, clique em **Salvar integração**.


## A integração de ferramenta não está configurada
{: #tool_integration_error}

Depois de configurar uma integração de ferramenta para sua cadeia de ferramentas, o erro `Falha na configuração` é exibido em seu cartão de ferramenta.
{:shortdesc}

Depois de configurar uma integração de ferramenta, você visualiza seu cartão de ferramenta na página Visão geral da cadeia de ferramentas e observa que a configuração falhou.
{: tsSymptoms}

 ![Erro de falha na configuração](images/tool_setup_failed.png)
 
Quando você inclui uma integração de ferramenta, a cadeia de ferramentas se comunica com a ferramenta que é representada pela integração de ferramenta para provisionar quaisquer recursos necessários e associá-los à cadeia de ferramentas. Se ocorrer um erro durante o processo de configuração ou se a comunicação entre a cadeia de ferramentas e a ferramenta não for concluída corretamente, a integração de ferramenta será colocada em um estado de erro.
{: tsCauses}

Configure a integração de ferramenta novamente:
{: tsResolve}

1. Em seu cartão de ferramenta, passe o mouse sobre a mensagem `Falha na configuração` e clique em **Reconfigurar**.

 ![Botão Reconfigurar](images/tool_reconfigure.png)
 
1. Certifique-se de que esteja usando parâmetros de configuração válidos. Se o erro tiver sido causado por uma configuração inválida, uma mensagem de erro será exibida; por exemplo, `A integração não pôde ser configurada. Verifique as configurações e tente novamente. Motivo: api_key:fakeKey inválida`. Atualize as configurações da integração de ferramenta e clique em **Salvar integração**.
1. Se o erro tiver sido causado por um problema de comunicação, clique em **Salvar integração** para tentar novamente.
