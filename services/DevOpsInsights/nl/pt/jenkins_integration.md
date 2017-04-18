---

copyright:
  years: 2016
lastupdated: "2016-11-11"

---

{:new_window: target="_blank"}
{:shortdesc: .shortdesc}
{:screen: .screen}
{:codeblock: .codeblock}
{:pre: .pre}

# Integrando o {{site.data.keyword.DRA_short}} com o Jenkins
{: #toolchain_configure_jenkins}

Após definir as políticas para o {{site.data.keyword.DRA_full}} monitorar, a próxima etapa será incluir o {{site.data.keyword.DRA_short}} em uma cadeia de ferramentas e, em seguida, configurar um pipeline de entrega contínua.
{:shortdesc}

<!--##Configuring a Jenkins project-->

É possível integrar o {{site.data.keyword.DRA_short}} em um projeto Jenkins ou ao longo de diversos projetos Jenkins relacionados. Isso permite que você
configure portas de qualidade, bem como receba dados de qualidade de construção no painel do {{site.data.keyword.DRA_short}}.

## Pré-Requisitos    
{: #DI_jenkins_prereqs}

* Deve-se ter acesso a um projeto Jenkins local ou ao servidor que estiver executando um projeto Jenkins.

## Instalando o plug-in do {{site.data.keyword.DRA_short}}
{: #DI_jenkins_install}

Para instalar o plug-in do {{site.data.keyword.DRA_short}} em seu projeto Jenkins, siga estas etapas:

  1. [Faça download do arquivo de instalação do IBM DevOps Insight
Plugin (.hpi)](https://github.ibm.com/oneibmcloud/DRA-Jenkins/blob/hpi-release/target/dra.hpi) a partir do repositório GitHub do plug-in.
  2. Em sua instalação do Jenkins, clique em **Gerenciar Jenkins**, selecione **Gerenciar plug-ins** e clique na guia
**Avançado**.
  3. Clique em **Escolher arquivo** e selecione o arquivo de instalação de plug-in do DevOps Insight.
  4. Clique em **Carregar**.
  5. Reinicie o Jenkins e verifique se o plug-in foi instalado.

## Integrando o {{site.data.keyword.DRA_short}} com o Jenkins    
{: #DI_jenkins_integrate}

Após o plug-in ser instalado, mas antes de integrar o {{site.data.keyword.DRA_short}} em sua instalação do Jenkins, acesse o [centro de controle](https://control-center.stage1.ng.bluemix.net/)
e crie pelo menos uma política.

Para cada uma das tarefas que você já tem e naquela que você deseja usar o {{site.data.keyword.DRA_short}}:

1. Inclua uma ação de pós-construção com o tipo **Publicar informações de construção para o {{site.data.keyword.DRA_short}}**,
**Publicar informações
de implementação para o {{site.data.keyword.DRA_short}}** ou **Publicar resultado de teste para o
{{site.data.keyword.DRA_short}}**. O tipo específico deve corresponder ao tipo de tarefa (construir, implementar ou
testar). Preencha os campos requeridos.
  * No campo Credencial, escolha o seu ID e a senha do Bluemix. Se eles não estiverem salvos no Jenkins, clique no botão **Incluir**
para incluí-los e salvá-los.
  * No campo Nome da tarefa de construção, especifique o nome de sua tarefa de construção exatamente como ele está no Jenkins. Se a construção ocorrer
juntamente com a tarefa de teste, deixe esse campo vazio. Se a tarefa de construção ocorrer fora do Jenkins, verifique **Construções estão sendo feitas fora
do Jenkins** e especifique o número da construção e a URL da construção.
  * Para o campo Local do arquivo de resultado, especifique o local do arquivo de resultado. Se o teste não gerar um arquivo de resultado, deixe este campo vazio. O plug-in fará upload de um arquivo de resultado padrão com base no status de tarefa de teste atual.
3. *Opcional*: se você quiser que as portas de política do DRA na tarefa de teste controlem a tarefa de implementação de recebimento de
dados, inclua outra ação de pós-construção com o tipo
**Porta de analítica de risco do DevOps** e conclua os campos necessários. A porta evitará que a tarefa de recebimento de dados seja executada se a tarefa de teste falhar em atender às políticas associadas.
4. Clique em **Aplicar** e, em seguida, clique em **Salvar**.

É possível clicar em **Construir agora** a partir da página de projeto para executar o projeto.

Após a construção ser executada, acesse o [centro de controle](https://control-center.stage1.ng.bluemix.net/) para verificar o seu status de
construção no painel. Se você configurou portas de política, também será possível ver resultados do {{site.data.keyword.DRA_short}} na página de Status da
construção atual.
